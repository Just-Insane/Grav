---
title: 'Hass-Cog: Home Assistant + Discord'
date: '25-09-2017 00:43'
taxonomy:
    category:
        - blog
    tag:
        - Home Assistant
        - Discord
hide_git_sync_repo_link: false
visible: true
---

Hass-Cog: A plugin for the [Red-DiscordBot](https://github.com/Cog-Creators/Red-DiscordBot) bot which integrates [Home Assistant](https://home-assistant.io) and [Discord](https://discordapp.com).

===

## What is it

[Hass-Cog](https://github.com/Just-Insane/HASS-Cog) is a plugin (cog) written for the [Red-DiscordBot](https://github.com/Cog-Creators/Red-DiscordBot) bot which allows you to control your Home Assistant setup and it's configured devices from within Discord.

## How does it work

Hass-Cog uses the Home Assistant Python API, specifically the remote module. This allows the bot to communicate with a remote installation of Home Assistant over the network.

## What can I do with it

Currently it is quite limited, having only been started a couple of days ago.

As of this writing, you are able turn lights on and off, view the status of a light, or all lights, as well as view the climate (if you have a group named "climate").

!! Note: Due to the fact that Home Assistant can have a very varied configuration, please view the code in hass.py to ensure that your configuration is compatible. Currently only effects the `[p]hass climate` command.

More features are on their way! Stay tuned for updates.

## Issues/Questions/Concerns

What to do if you have Issues, Requests, and Questions

### Hass-Cog Issues

If you have issues with Hass-Cog, please open an issue on GitHub.

### Feature Requests

Please open an issue on GitHub.

### Questions

Feel free to open an issue on GitHub, or find me in the Red - Cog Support channel under #support_othercogs (please mention me `@just_insane#8594`, or the Home Assistant Discord server)