---
title: Making visual effects in Minecraft without mods
slug: flaps
date: 2026-01-11
image: https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/flaps/pig.png
subtitle: "
When trying to recreate a specific effect, I discovered a way to control visual shader effects on Minecraft clients from the server side using only resource packs and packets. 
It unlocked dynamic visuals in fully vanilla Minecraft. From camera shake to weather-driven effects, the possibilities are huge.
"
---

It's been a good few years since I've worked with Minecraft.

For a long time, I've wanted to create one specific effect found in the Legacy console editions of Minecraft: the [roll effect when gliding with an Elytra](https://www.youtube.com/watch?v=4TVhD3RRQrc). It's a small detail, but it adds a lot to the immersion and feel of flying.

I remember a few years ago asking about this in a technical Discord. The advice I was given was that there was a small chance it might be possible with complex shaders, but the general consensus was that it couldn’t be done without mods. That changes today.

# Discovery

Despite the pessimism, I decided to give it another go. After a ton of research with very undocumented features, I discovered that [Minecraft resource packs](https://minecraft.wiki/w/Resource_pack) can embed custom shaders that modify the game's rendering. This is notable because vanilla servers can force clients to use resource packs, meaning every connecting player automatically gets those shaders without installing anything.

While this sounds promising, it’s mostly unhelpful in practice because shaders are static files. We can't dynamically control them from the server - so you can only really have two states: the effect is on for the entire game, or it's off for the entire game. Not very useful.

However...

# Using the sun
Shaders do have *some* properties that they can access. And because they use GLSL, an actual programming language, we can do some interesting things with them. There's a very specific property; the `GameTime` property. 
This property is accessible in shaders and represents the in-game time and counts up in ticks. The key thing here is that the server can control this property by sending packets to clients.

We can now embed data and communicate it to shaders by sending packets to modify the `GameTime` property. This is huge.

# Implementation

With this discovery, the biggest problem was picking which shaders to override. There are two types of shaders in Minecraft:
<ul>
    <li><b>Core shaders</b>, which handle the majority of Minecraft's rendering (blocks, entities, the sky, etc)</li>
    <li><b>Post-process shaders</b>, which handle a few specific scenarios (spectating a creeper or spider, or when using the *Fabulous!* graphics setting)</li>
</ul>

Post-process shaders are easier to modify, actually supported by Mojang, and won't break with updates, but they are very limited in scope due to the conditions required for them to be active. 
Core shaders, on the other hand, are always active, but modifying them is highly experimental and unsupported by Mojang. Unfortunately, that makes modifying core shaders the only viable option to work for all players.

After a lot of trial and error, I managed to create a centralised file which multiple core shaders can implement, allowing for easy modification of effects to the entire game. 

![First time achieving custom shaders](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/flaps/firstshader.png)

And because we can control the `GameTime` property from the server, we can now create dynamic visual effects in vanilla Minecraft. I went straight back to my original goal of recreating the Elytra roll effect, and managed to achieve camera roll that accounts for entities, the terrain,
the hand, and everything else that shaders manage.

![Camera roll](https://raw.githubusercontent.com/seailz/blog/refs/heads/main/images/flaps/rotation.png)

## Entities
One of the biggest challenges was handling entities. The player's hand is considered an entity and will have effects applied to it. Blocks inside of inventories are also entities.
Filtering these out is tricky. The inventory items can be filtered by checking their render layer, but the hand is more difficult. The only way of detecting the hand is to check the proximity to the camera, which can lead to false positives with real mobs/entities and cause strange effects. For most servers,
this isn't worth the hassle, and having the hand be affected by the shader is recommended to prevent issues with entities.

# Possibilities
This shouldn't be possible. It seems completely weird that you can even do this, but here we are. And this effect isn't just limited to camera roll either, we can create all sorts of dynamic visual effects including:
- Dynamic weather effects (e.g., heat distortion during a heatwave)
- Visual effects tied to in-game events (e.g., screen distortion during earthquakes or explosions)
- Camera shake during horror scenes, boss fights, etc
- Dynamic day/night cycle effects (e.g., color grading during sunrise/sunset)
- Special effects for abilities or power-ups (e.g., motion blur when sprinting or speed boosts)
- And much more. Literally unlimited control over visual effects.

All managed by the server, without any mods. For example, here's a camera shake effect:
<video controls>
  <source src="https://github.com/user-attachments/assets/a44e6dd3-57b6-4b8c-827c-51507e512070" type="video/mp4">
</video>

# Conclusion

As a Minecraft developer who's been working with the game for upwards of 6 years now, this discovery really blew my mind. It's not even something you'd consider to be possible, but full, dynamic, visual effects are now an option for server owners in fully vanilla Minecraft.

If you want to check out the project, have a look at the [GitHub repository here](https://github.com/seailz/Flaps). I'm currently working on turning it into a library so that other developers can implement their own effects easily. Feel free to reach out if you have any questions or ideas!
