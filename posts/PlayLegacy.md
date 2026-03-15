---
title: PlayLegacy and Minecraft’s UI Problem
slug: playlegacy
date: 2026-03-15
image: todo
subtitle: "
This is the story of how I recreated Minecraft’s classic console minigames in the modern game, fully without mods. The hardest part was not just rebuilding the games themselves, but recreating the console-style interface in a version of Minecraft where the server was never meant to control the player’s screen.
"
---

An old edition of Minecraft, the so-called [Legacy Console Editions (LCE)](https://minecraft.wiki/w/Legacy_Console_Edition), had a feature that me and many others have a lot of nostalgia for: the old mini games. These were simple, fast paced multiplayer games, baked into Minecraft itself, that anyone could play and join instantly.

While they're still technically available, they're diffcult to access without a copy of the original game. That led me, as a developer who hasn't worked on Minecraft projects in years, to a very specific question: how possible would it be to recreate these games faithfully in modern, Java Edition Minecraft, all without modding the game? Turns out a lot harder than I imagined...

This is a story about trying to make the UI feel native again in an environment where the server does not own the screen.

# The old games

There were three old minigames included in LCE:

- **Glide**, a race to the finish using the Minecraft Elytra
- **Battle**, a classic PvP style minigame
- **Tumble**, a spleef-style minigame

Each of the minigames use UI features that were generally thought to be incredibly difficult to replicate in modern Minecraft, especially because my main constraint was wanting to avoid using mods *at all*. Here's a few screenshots of the UI I'm attempting to rebuild:

// TODO Glide, Battle, and Tumble screenshots along with loading screen

Since the games were built into Minecraft itself, they had full access to custom UI features. Java Edition Minecraft servers are not afforded that luxury: since we only control the server, rather than the client, there are far more limitations on what we can show on screen.

# What we can do, and what's new

Java edition servers *can* automatically provide a resource pack-a set of textures and other items-to a player when they join, though, which allows a vast amount of new possiblities than just basic text display, albeit some of them being quite difficult to achieve.

## Glyphs and X/Y control

For example, it's been a common feature of newer, complex servers to use "glpyhs" - essentially retexturing unused Unicode characters - to display some basic UI on the screen. For example, if we define that `\uE001` equals a score icon, whever we display text we can include that score icon, which allows for some custom UI.

// Include basic ui demonstration

This typically isn't scalable to full-screen UI though, and it does face some quite important limitations. Most notably, it's quite difficult to move glyphs on the vertical axis. For the horizontal axis, it's fairly easy, we can define "spacing" glyphs - empty unicode characters - and place them dynmaically to move our icon around the screen.

// Show gif/video of ui moving

But veritcally, we cannot. For custom glyphs, this can be overcome by providing an "ascent" value inside our custom font. For normal text, it's a little more difficult, though not insurmountable, as we can define a custom text font and adjust the ascent values in that too.

So great: we've got full (ish) control over both axes of movement for both glyphs and normal text. But what if we wanted to do something fancy like adding a full screen background to recreate the old loading screen? That's quite difficult for a few reasons.

// Add loading screen png again

## Larger than 256x256
Glyphs are unfortuantley limited to 256x256 pixels. This creates quite a large limitation when doing very complex UI

# Shaders

## Statefullness

# Other UI

// TODO talk about moving and scaling the hotbar, glyphs, using inventories & flaps


# Conclusion

UI work in Java Edition is really tough. Really difficult. And despite all the cool things you *are* able to achieve, they generally rely on inherently unreliable features, break regularly, and are rather buggy. But that's the price to pay for these things. One thing has stuck with me, though: if you're determined enough to achieve something, no matter how limiting the engine may be, there was always another way. Only on 1 or 2 occassions throughout this entire project have I been hit with a full roadblock. Almost always there was a way around, however hidden, hacky, experimental or unreliable it may be.

If you're interested in checking PlayLegacy out, I'd really appreciate it as it's a really fun project that I've been working on for a few months. https://playlegacy.xyz is the website, and the server IP is playlegacy.xyz. Discord can be found at https://discord.gg/minigames.
