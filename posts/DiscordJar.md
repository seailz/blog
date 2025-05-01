---
title: How I built discord.jar, a library for the Discord API
slug: djar
date: 2025-05-01
image: https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/discordjar/slz-discord.jar.png
subtitle: "
    This is the story of how I built discord.jar, a library for the Discord API. I wanted to create a library that was easy to use and had a great developer experience. In this post, I will share my process of building discord.jar and the lessons I learned along the way.
"
---

# Introduction
I've been working with the Discord API for many years now, starting out with [JDA](https://github.com/discord-jda/JDA), a popular library in the Java ecosystem.
While I think JDA is a great library, I don't think it has the same "magic" developer experience similar to something like Svelte. So in November 2022, I decided that
I'd build my own library for the Discord API—and if it didn't work out? I'd still have learned a lot along the way. Those were my two main goals.

# Starting Out
Since this was my first API library, I kept it simple originally by experimenting with basic endpoint calling and response handling. But, I soon realized that I wanted to build a library that was easy to use and had a great developer experience. I wanted to create a library that felt like it was built for developers, 
something that could actually be used in production.

# Challenges
Over the last 2 years building discord.jar, various things propped up that caused quite significant roadblocks or challenges. Some of these were:
## Gateway
[Gateway](https://discord.dev/topics/gateway) is Discord's name for their two-way WebSocket API. This is how the real-time aspect of Discord works. Gateway is a monster to implement
for a few reasons:
- The sheer amount of events that each need to be individually implemented
- The connection process (handling reconnects, regular disconnects, heartbeating, etc) is very complex (cause it needs to be)
- The fact that the API is constantly changing and evolving
- Compression! Implementing it in discord.jar was my first time working with compression directly

I originally began with Spring's WebSocket API. This did work for quite a while, but it was fairly buggy and didn't support the complexities of implementing Gateway,
so eventually the entire Gateway implementation was rewritten using OkHttp instead. This was a huge improvement and allowed for a much more stable and performant library. It
just wasn't production ready before OkHttp.

The [`WebSocket`](https://github.com/discord-jar/discord.jar/blob/main/src/main/java/com/seailz/discordjar/ws/WebSocket.java) class handles most of the low-level WebSocket stuff,
and the [`Gateway`](https://github.com/discord-jar/discord.jar/blob/main/src/main/java/com/seailz/discordjar/gateway/Gateway.java) class handles the high-level stuff. The two classes work together to provide a seamless experience for the dev.

I still haven't finished implementing all the Gateway events (or the HTTP endpoints for that matter!) but it's stable enough now, just missing features.

## Rate-limiting
Rate-limiting is also a fairly complex thing to handle in this sort of library. discord.jar supports both asynchronous and synchronous requests to the API which does make it fairly difficult
when you run into rate-limits. We handle them in various ways:

- Ideally, a rate-limit should never occur. Discord responds with a retry after header to indicate when the endpoint can be used again.
- In practice, especially with async requests, this isn't always possible. Each bucket maintains its own rate-limit state, so if a request is made to a bucket that is already rate-limited, all other requests in that bucket will be held until the rate-limit is lifted.
    - However, if we have a case where a request is sent asynchronously, and before we get the response from Discord, another is sent asynchronoly, the second is potentially going to be rate-limited.
- So, if we do encounter a rate-limit, the request is tried again when the rate-limit is lifted.

This logic is available in the [`Bucket`](https://github.com/discord-jar/discord.jar/blob/main/src/main/java/com/seailz/discordjar/utils/rest/ratelimit/Bucket.java) class.

## Voice
Most Discord bots don't need to implement voice, but I wanted to ensure that discord.jar could support it nontheless. This was quite a messy one...

Discord's protocol for connecting to their voice servers is roughly this:
1. First, request from the main Gateway to connect to a separate Voice-related WebSocket
2. Then, you connect to that WebSocket which gives you a UDP address to connect to 
3. Connect to that UDP address, and start sending your encrypted packets

This is a very simplified version of the process, but it does give you an idea of how complex it is. My favourite story to tell
is that when implementing voice, because of a missing `this.`, I ended up sending the UDP packets to the bot (the host computer) instead of Discord. That one took a few months... 😂

# Conclusion
Overall, building discord.jar has been a great experience. I've learned a lot about building libraries, working with APIs, and the complexities of real-time communication.
There are certainly things I would change if I was to create a new library, but I'm still very proud of what I've built as it's, as we speak, being used in production by many bots.
There's still more work to be done! More endpoints to implement, more events to handle, but I'm excited to see where discord.jar goes in the future.