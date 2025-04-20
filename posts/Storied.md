---
title: The power of ChatGPT deep research and why I built an email-journaling app
slug: storied
date: 2025-04-20
image: https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/storied/storied.png
subtitle: "In this post I cover the power of ChatGPT deep research and why I built a journaling app called Storied. I also cover the future of AI and how it will impact our lives, particularly in the realm of software engineering and SaaS."
---
This is going to be a bit of a scramble of a post, but here goes...

Over the past few months, I've been working on a new project called Storied. Storied is an email-journalling app that is designed to motivate users to write more. Essentailly, we send you an email every day with a prompt, and you can reply to it with your thoughts. This is a great way to get started with journaling.
## Deep Research
The idea behind Storied was not actually from my own experience with journaling. Recently, I've been looking into building a Micro-SaaS side-project both as a way to learn and as a way to make some extra money, but my largest
problem was that I didn't know what to build. I had a few ideas, but nothing that really stood out to me. I wanted to build something that would be useful to people, but I didn't know what that was.

I decided to turn to ChatGPT for help. OpenAI recently released a new feature called [Deep Research](https://openai.com/index/introducing-deep-research/)—a tool that allows ChatGPT to analyse huge amounts of data available on the internet
and produce a detailed report on a specific topic. While I had trialed idea brainstorming with ChatGPT before, it never really produced anything that I thought was useful. I decided to give it another go, and I was blown away by the results.

### The Prompt
Part of my initial prompt was asking the model to rate each idea on a few different factors:
- Problem clarity - How clear is the problem that the idea is trying to solve?
- Market size - How big is the potential market for this idea?
- Feasibility - Can I actually build this as a side-project?
- Monetization - How easy is it to monetize this idea?
- My personal excitement - using [ChatGPT memories](https://openai.com/index/memory-and-new-controls-for-chatgpt/), how excited does it think I would be to work on this idea?
- Market saturation - How saturated is the market for this idea?

Each of these factors was rated on a scale of 1-10, and I asked ChatGPT to provide a brief explanation for each rating. I also asked it to provide a summary of the idea and how it could be implemented. It the
was tasked to produce an overall rating out of 10.

### The Results
The results from this prompt were absolutely excellent—unlike anything I had seen before. In 11 minutes, using 20 sources, it produced a variety of ideas (some that I'll also be working on next!)
with detailed explanations of each idea, the ratings, and a summary of how it could be implemented. I was blown away by the results.

For some technical details: This was GPT 4o-mini, a fairly small model. Recent benchmarks have shown that o3, the large new flagship model, just only outperforms 4o with deep research. So it's not a suprise that these results
were pretty shockingly great. o3 wasn't released at the time, but I think trialing this again could be very very interesting. I encourage you to give it a go if you're interested in SaaS and have ChatGPT Plus.

Anyway...

I knew that I had to build something based on one of these ideas. The early concept behind Storied was one of 5 ideas that I was given. I built upon the idea and started to flesh it out, but here's the reasons ChatGPT gave for the idea:
- Many people want to keep a personal journal but struggle with consistency
- Journaling is popular for wellness and memory-keeping. Millions try journaling.
- Technically straightforward. (this turned out to not be true... more on this later lol)
- Freemium model fits well. Core logging via email is free to attract users. Premium features (full text search of entries, attaching photos, custom prompts, data backups) can justify a subscription.
- Few direct competitors use the email journaling approach.

## The Build
I started working on Storied on and off for a few weeks, and I was really excited about the idea. I decided to use some new techniques this time, but still sticking to the basics of SvelteKit and Firebase. Here's what I went with:
### shadcn & Tailwind
I decided to use [shadcn-svelte](https://www.shadcn-svelte.com/), a port of shadcn/ui to Svelte for the UI. I really love the style of shadcn and it's nice to move away from Material Design for a change, as I've used it for a lot of my projects. 
The library uses Tailwind CSS which I'm completely new to, but I really like it so far. I do have some complaints... mostly readability and the learning curve, but I'm definitely going to continue using it in the future and I'm glad I tried it out.
(I used to hate the idea!)
### Firebase
Although I'm still working with Firebase, I decided to go all-in on this project instead of building my own backend in between (slightly defeats the point haha). That meant using security rules, Cloud Functions, and extensions. Again, a few complaints about 
readability/cleanness of the code, but not a bad idea for building a side-project quickly. Definitely will use it again in the future, likely in the same way. Saves a lot of time and effort.
### Stripe
Believe it or not, I don't think I've ever built a web-app with payment logic before. Working with Stripe was nice and easy, especially using the [Firebase extension](https://extensions.dev/extensions/invertase/firestore-stripe-payments). It's quite
an old and buggy extension so I did have to use some hacky workarounds, but not something that was too difficult to deal with. I imagine I'll end up using Stripe again, but I'm also looking towards other provides/wrappers
for Stripe such as [Polar](https://polar.sh). I think they provide a really excellent developer experience.
### Email
Now this is where things get a bit tricky. I was determined to find a good price for email sending, so SendGrid and similar providers were immediately out of the question. This is going to get technical, so bear with me.
I decided to use AWS' SES (Simple Email Service) for receiving emails. It's a great service for a good price, but does cause some complications when running on Firebase. The final architecture looks like this:
- AWS SES receives the email
- SES saves the email to an S3 bucket
- SES triggers a Lambda function to retrieve the email and run some basic logic
- Lambda function forwards the email to a Firebase cloud function
- Firebase cloud function runs some more processing, cleans up the email, finds the relevant user, and saves it to Firestore where it's encrypted

It's a messy architecture. It does get the job done, and was unfortunately the best solution I could find for the price. Sending emails is slightly easier as SES has a JS SDK which a Cloud Function can easily call.
In future, I'd probably lean away from building email-based apps for this reason. It's a lot of work to get it all set up, and I think there are better solutions out there, just not at the price I was looking for. (maybe this is an API idea? 👀)
### The Future
I'm really excited about the future of Storied. I think it has a lot of potential to grow and become a popular journaling app. It'll take some work, but I'm excited to see where it goes. I've got lots of ideas!!

## The Future of AI
I think the future of AI is going to be really interesting. I think we're going to see a lot more tools like ChatGPT that are able to analyse large amounts of data and produce useful insights. 
While this will undoubtdely have wide impacts for the entire world, I think it's particularly prevalent in the software engineering and SaaS space. Idea generation might be an easy task for you, but that's not the only thing that AI can do.
If you struggle with anything from writing code to debugging to market research, tools like Deep Research really are the future. We'll see where it goes.

For now, please check out [Storied](https://storied.email) and let me know what you think! If you want a free discount for Storied Pro, drop me an email at [george@slz.lol](mailto:george@slz.lol) or send me a DM on Discord (seailz) and I'll get you a code.
I really appreciate any feedback you have so do feel free to [contact me](https://slz.lol/contact). I'm always happy to chat!