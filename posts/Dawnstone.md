---
title: Working with Candor Studios to revolutionize the way we order services
slug: candorstudios-dawnstone
date: 2025-02-20
image: https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/dawnstone/dawnstone.png
subtitle: "Over the last year, I've been working with Candor Studios to revolutionize the way we order services. This is a brief overview of the project and the impact it's projected to have on the industry."
---
For the past year, I've been collaborating with Candor Studios on a groundbreaking initiative—Project Dawnstone. Our goal? To revolutionize how services are ordered, making the process more accessible and seamless. With this platform, we're getting rid of Discord's UI limitations
and replacing it with a user-friendly system that provides a new medium for service teams to connect with clients. This is a brief overview of the project and the impact it's projected to have on the industry.


## The Problem
Despite rapid technological development across almost all industries, the service industry has remained relatively stagnant. Freelancers and service teams still rely on outdated methods to connect with clients,
with most service teams using Discord, a platform that was never designed for this purpose. While Discord functions well enough for this, it's not ideal. It's clunky
and not user-friendly, limiting the potential for growth in the industry and for service teams to expand their reach.

## The Solution
Project Dawnstone, also known as Candor Hub, aims to solve this problem by creating a platform that allows users to order services straight from the web. This platform is designed to be user-friendly and intuitive,
while still providing full support for the Discord servers at the backend. This means that service teams can continue to use Discord as they always have, while also expanding their reach
to new customers who might not know, or care, what Discord is.

This brings service teams into the traditional e-commerce and freelancing space, opening up new opportunities for growth and expansion. A whole new untapped market of users
now becomes available to them, and they can take advantage of this to grow their businesses and reach new heights.

## How It Works
Over the last year, I've been working with Candor Studios to develop this exact platform. We've been able to create a system where freelancers can use their
familiar Discord server to communicate with clients, while also providing a seamless experience for clients on a platform that they understand.

This system is designed to be user-friendly and intuitive, with a focus on providing a seamless experience for both service teams and clients. It's a win-win for everyone involved,
and I'm excited to see the impact it has on the industry as a whole.

The journey starts on the Candor Studios website, where clients can order a specific service. They enter their details, including their budget and description, in a way very
similar to how it's worked on Discord. This information is then used to create a Discord channel representing the order, and simultaneously, an order is created on the 
Candor Hub platform.

[![Candor Hub](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/dawnstone/order-page.png)](https://candorstudios.net)

From there, it's sent off to freelancers as normal who can send in their quotes. The client can then choose the freelancer they want to work with, and the process continues as normal.
Messages are fully synced between the Candor Hub platform and Discord, so there's no need to worry about missing anything. We use Discord Webhooks to make the messages
from the platform appear as familiar as possible, and the experience is seamless.

[![Candor Hub Webhook Message](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/dawnstone/webhook-message.png)](https://candorstudios.net)

### Freelancer Area
Freelancers have their own area on the Candor Hub platform where they can manage their orders, send quotes, and communicate with clients. This area is designed to be user-friendly
while, as always, remaining fully synced with Discord.

[![Candor Hub Freelancer Area](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/dawnstone/freealncerarea.png)](https://candorstudios.net)

## Testing & Feedback
We've been testing Project Dawnstone since December 2024, and the feedback has been overwhelmingly positive. Users have praised the platform for its ease of use and intuitive design,
and we've been able to make some significant improvements based on the feedback we've received. It's been a great process overall.

## Technologies Used
Project Dawnstone is built using a combination of technologies, including:
- **SvelteKit**: powers the frontend of the platform, providing a fast and responsive experience for users.
- **Java**: was used for the backend of the platform, handling the syncing between the Candor Hub platform and Discord.
- **Google Cloud**: was used for hosting and managing the backend instances, as well as for the Pub/Sub system that allows instances to communicate with each other.
- **Instcom**: a custom system built by me to allow the backend instances and Discord bots to communicate with each other in real-time.
- **Discord**: is still used as the main hub for the service team, with messages fully synced between the Candor Hub platform and Discord.

Candor's Discord bots, also built by me, needed to be connected together using one central channel where all instances can keep each other updated.
This was a challenge to implement, but we were able to overcome it by creating a system called Instcom which allows Dawnstone backend instances and
Discord bot instances to communicate with each other in real-time. This was based off Google Cloud's Pub/Sub system, and it's been working great so far
with hundreds of thousands of messages sent between instances over the last year.

More details on the vast amount of technologies to implement this project will be available in a future blog post, stay tuned!

## The Impact
The impact of Project Dawnstone is projected to be huge—we're setting a new industry standard. By bringing service teams into the traditional e-commerce and freelancing space, we're opening up new opportunities for growth
and expansion. Candor Studios, by creating this platform, is opening themselves up to a whole new market of users who might not have known about them before.
Combined with a comprehensive marketing strategy, this could lead to a significant increase in business for them and for the service teams they work with.

## Preview
The Candor Hub platform is currently in private beta, with a public release planned within the next month. If you're interested in learning more about the platform or would like to
use it for your own freelancing needs, it'll be available soon at [Candor Studios's website](https://candorstudios.net) (it is the website!). For updates, join [Candor's Discord server](https://discord.gg/fpKQS4dq7u) where an announcement will be made when it goes live. I'm excited to see the impact this has on the industry as a whole,
and I'm proud to have been a part of it!

If you'd like to contact me about this project or any other work, feel free to reach out to me on [my contact page](https://slz.lol/contact).

[![Candor Hub](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/dawnstone/welcome.png)](https://candorstudios.net)