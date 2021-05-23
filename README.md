<h1 align="center">
    Discord Downloader <i>Go</i>
</h1>
<p align="center">
    <a href="https://travis-ci.com/get-got/discord-downloader-go" alt="Travis Build">
        <img src="https://travis-ci.com/get-got/discord-downloader-go.svg?branch=master" />
    </a>
    <a href="https://hub.docker.com/r/getgot/discord-downloader-go" alt="Docker Build">
        <img src="https://img.shields.io/docker/cloud/build/getgot/discord-downloader-go" />
    </a>
    <a href="https://goreportcard.com/report/github.com/get-got/discord-downloader-go" alt="Go Report Card">
        <img src="https://goreportcard.com/badge/github.com/get-got/discord-downloader-go" />
    </a>
    <br>
    <a href="https://github.com/get-got/discord-downloader-go/releases" alt="All Releases">
        <img src="https://img.shields.io/github/downloads/get-got/discord-downloader-go/total?label=all-releases&logo=GitHub" />
    </a>
    <a href="https://github.com/get-got/discord-downloader-go/releases/latest" alt="Latest Release">
        <img src="https://img.shields.io/github/downloads/get-got/discord-downloader-go/latest/total?label=latest-release&logo=GitHub" />
    </a>
    <br>
    <a href="https://discord.gg/6Z6FJZVaDV">
        <img src="https://img.shields.io/discord/780985109608005703?logo=discord"alt="Join the Discord">
    </a>
</p>
<h2 align="center">
    <a href="https://github.com/get-got/discord-downloader-go/releases/latest">
        <b>DOWNLOAD LATEST RELEASE</b>
    </a>
</h2>

This is a program that connects to a Discord Bot or User to locally download files posted in Discord channels in real-time as well as old messages. It can download any directly linked files or Discord attachments, as well as the highest possible quality files from specific sources _(see list below)_. It also supports extensive channel-specific configuration and customization. _See [Features](#Features) below for full list!_

<h3 align="center">
    <b>This project is a fork of <a href="https://github.com/Seklfreak/discord-image-downloader-go">Seklfreak's <i>discord-image-downloader-go</i></a></b>
</h3>
<h4 align="center">
    For list of differences and why I made an independent project, <a href="#differences-from-seklfreaks-discord-image-downloader-go--why-i-made-this"><b>see below</b></a>
</h4>

### Sections
* [**List of Features**](#features)
* [**Getting Started**](#getting-started)
* [**Guide: Downloading History _(Old Messages)_**](#guide-downloading-history-old-messages)
* [**Guide: Settings / Configuration**](#guide-settings--configuration)
* [**List of Settings**](#list-of-settings)
* [**Development, Credits, Dependencies**](#development)
  
<h3 align="center">
    <a href="https://discord.com/invite/6Z6FJZVaDV">
        <b>Need help? Have suggestions? Join the Discord server!</b>
    </a>
</h3>

## Features

### Supported Download Sources
* Discord File Attachments
* Direct Links to Files
* Twitter _(requires API key, see config section)_
* Instagram
* Reddit
* Imgur _(Single Posts & Albums)_
* Flickr _(requires API key, see config section)_
* Google Drive _(requires API Credentials, see config section)_
* Mastodon
* Tistory
* Streamable
* Gfycat
  
### Commands
Commands are used as `ddg <command> <?arguments?>` _(unless you've changed the prefix)_
Command     | Arguments? | Description
---         | ---   | ---
`help`, `commands`  | No    | Lists all commands.
`ping`, `test`      | No    | Pings the bot.
`info`      | No    | Displays relevant Discord info.
`status`    | No    | Shows the status of the bot.
`stats`     | No    | Shows channel stats.
`history`   | [**SEE HISTORY SECTION**](#guide-downloading-history-old-messages) | **(BOT AND SERVER ADMINS ONLY)** Processes history for old messages in channel.
`exit`, `kill`, `reload`    | No    | **(BOT ADMINS ONLY)** Exits the bot _(or restarts if using a keep-alive process manager)_.
`emojis`    | Optionally specify server IDs to download emojis from; separate by commas | **(BOT ADMINS ONLY)** Saves all emojis for channel.

## **WARNING!** Discord does not allow Automated User Accounts (Self-Bots/User-Bots)
[Read more in Discord Trust & Safety Team's Official Statement...](https://support.discordapp.com/hc/en-us/articles/115002192352-Automated-user-accounts-self-bots-)

While this project works for user logins, I do not reccomend it as you risk account termination. If you can, [use a proper Discord Bot user for this program.](https://discord.com/developers/applications)

> _NOTE: This only applies to real User Accounts, not Bot users. This program currently works for either._

## Getting Started
_Confused? Try looking at [the step-by-step list.](#getting-started-step-by-step)_

Depending on your purpose for this program, there are various ways you can run it.
- [Run the executable file for your platform. _(Process managers like **pm2** work well for this)_](https://github.com/get-got/discord-downloader-go/releases/latest)
- [Run automated image builds in Docker.](https://hub.docker.com/r/getgot/discord-downloader-go) _(Google it)._
  - Mount your settings.json to ``/root/settings.json``
  - Mount a folder named "database" to ``/root/database``
  - Mount your save folders or the parent of your save folders within ``/root/``
    - _i.e. ``X:\My Folder`` to ``/root/My Folder``_
- Install Golang and compile/run the source code yourself. _(Google it)_

You can either create a `settings.json` following the examples & variables listed below, or have the program create a default file (if it is missing when you run the program, it will make one, and ask you if you want to enter in basic info for the new file).
- [Ensure you follow proper JSON syntax to avoid any unexpected errors.](https://www.w3schools.com/js/js_json_syntax.asp)
- [Having issues? Try this JSON Validator to ensure it's correctly formatted.](https://jsonformatter.curiousconcept.com/)

### Getting Started Step-by-Step
1. Download & put executable within it's own folder.
2. Configure Main Settings (or run once to have settings generated). [_(SEE BELOW)_](#list-of-settings)
3. Enter your login credentials in the `"credentials"` section. [_(SEE BELOW)_](#list-of-settings)
4. Put your Discord User ID as in the `"admins"` list of the settings. [_(SEE BELOW)_](#list-of-settings)
5. Put a Discord Channel ID for a private channel you have access to into the `"adminChannels"`. [_(SEE BELOW)_](#list-of-settings)
6. Put your desired Discord Channel IDs into the `"channels"` section. [_(SEE BELOW)_](#list-of-settings)
- I know it can be confusing if you don't have experience with programming or JSON in general, but this was the ideal setup for extensive configuration like this. Just be careful with comma & quote placement and you should be fine. [See examples below for help.](#settings-examples)

### Bot Login Credentials...
* If using a **Bot Application,** enter the token into the `"token"` setting. Remove the lines for `"username"` and `"password"` or leave blank (`""`). **To create a Bot User,** go to [discord.com/developers/applications](https://discord.com/developers/applications) and create a `New Application`. Once created, go to `Bot` and create. The token can be found on the `Bot` page. To invite to your server(s), go to `OAuth2` and check `"bot"`, copy the url, paste into browser and follow prompts for adding to server(s).
* If using a **User Account (Self-Bot),** fill out the `"username"` and `"password"` settings. Remove the line for `"token"` or leave blank (`""`).
* If using a **User Account (Self-Bot) with 2FA (Two-Factor Authentication),** enter the token into the `"token"` setting. Remove the lines for `"username"` and `"password"` or leave blank (`""`). Token can be found from `Developer Tools` in browser under `localStorage.token` or in the Discord client `Ctrl+Shift+I (Windows)`/`Cmd+Option+I (Mac)` under `Application → Local Storage → https://discordapp.com → "token"`. **You must also set `userBot` within the `credentials` section of the settings.json to `true`.**

### Bot Permissions in Discord...
* In order to perform basic downloading functions, the bot will need `Read Message` permissions in the server(s) of your designated channel(s).
* In order to respond to commands, the bot will need `Send Message` permissions in the server(s) of your designated channel(s). If executing commands via an Admin Channel, the bot will only need `Send Message` permissions for that channel, and that permission will not be required for the source channel.
* In order to process history commands, the bot will need `Read Message History` permissions in the server(s) of your designated channel(s).

### How to Find Discord IDs...
* ***Use the info command!***
* **Discord Developer Mode:** Enable `Developer Mode` in Discord settings under `Appearance`.
* **Finding Channel ID:** _Enable Discord Developer Mode (see above),_ right click on the channel and `Copy ID`.
* **Finding User ID:** _Enable Discord Developer Mode (see above),_ right click on the user and `Copy ID`.
* **Finding Emoji ID:** _Enable Discord Developer Mode (see above),_ right click on the emoji and `Copy ID`.
* **Finding DM/PM ID:** Inspect Element on the DM icon for the desired user. Look for `href="/channels/@me/CHANNEL_ID_HERE"`. Using this ID in place of a normal channel ID should work perfectly fine.

### Differences from [Seklfreak's _discord-image-downloader-go_](https://github.com/Seklfreak/discord-image-downloader-go) & Why I made this
* _Better command formatting & support_
* Configuration is JSON-based rather than ini to allow more elaborate settings and better organization. With this came many features such as channel-specific settings.
* Channel-specific control of downloaded filetypes / content types (considers things like .mov as videos as well, rather than ignore them), Optional dividing of content types into separate folders.
* **Download Support for Reddit & Mastodon.**
* (Optional) Reactions upon download success.
* (Optional) Discord messages upon encountered errors.
* Extensive bot status/presence customization.
* Consistent Log Formatting, Color-Coded Logging
* Somewhat different organization than original project; initially created from scratch then components ported over.
* _Various fixes, improvements, and dependency updates that I also contributed to Seklfreak's original project._

> I've been a user of Seklfreak's project since ~2018 and it's been great for my uses, but there were certain aspects I wanted to expand upon, one of those being customization of channel configuration, and other features like message reactions upon success, differently formatted statuses, etc. If some aspects are rudimentary or messy, please make a pull request, as this is my first project using Go and I've learned everything from observation & Stack Overflow.

## Guide: Downloading History (Old Messages)
> This guide is to show you how to make the bot go through all old messages in a channel and catalog them as though they were being sent right now, in order to download them all.

### Command Arguments
If no channel IDs are specified, it will try and use the channel ID for the channel you're using the command in.

Argument / Flag         | Details
---                     | ---
**channel ID(s)**       | One or more channel IDs, separated by commas if multiple.
`all`                   | Use all available registered channels.
`cancel` or `stop`      | Stop downloading history for specified channel(s).
`--since=YYYY-MM-DD`    | Will process messages sent after this date.
`--since=message_id`    | Will process messages sent after this message.
`--before=YYYY-MM-DD`   | Will process messages sent before this date.
`--before=message_id`   | Will process messages sent before this message.

***Order of arguments does not matter.***

#### Examples
* `ddg history`
* `ddg history cancel`
* `ddg history all`
* `ddg history stop all`
* `ddg history 000111000111000`
* `ddg history 000111000111000, 000222000222000`
* `ddg history 000111000111000,000222000222000,000333000333000`
* `ddg history 000111000111000, 000333000333000 cancel`
* `ddg history 000111000111000 --before=000555000555000`
* `ddg history 000111000111000 --since=2020-01-02`
* `ddg history 000111000111000 --since=2020-10-12 --before=2021-05-06`
* `ddg history 000111000111000 --since=000555000555000 --before=2021-05-06`

## Guide: Settings / Configuration
> I tried to make the configuration as user friendly as possible, though you still need to follow proper JSON syntax (watch those commas). All settings specified below labeled `[DEFAULTS]` will use default values if missing from the settings file, and those labeled `[OPTIONAL]` will not be used if missing from the settings file.

When initially launching the bot it will create a default settings file if you do not create your own `settings.json` manually. All JSON settings follow camelCase format.

**If you have a ``config.ini`` from _Seklfreak's discord-image-downloader-go_, it will import settings if it's in the same folder as the program.**

### Settings Examples
The following example is for a Bot Application _(using a token)_, bound to 1 channel.

This setup exempts many options so they will use default values _(see below)_. It shows the bare minimum required settings for the bot to function.

`settings.json Example - Barebones:`
```javascript
{
    "credentials": {
        "token": "YOUR_TOKEN"
    },
    "channels": [
        {
            "channel": "DISCORD_CHANNEL_ID_TO_DOWNLOAD_FROM",
            "destination": "FOLDER_LOCATION_TO_DOWNLOAD_TO"
        }
    ]
}
```

`settings.json Example - Selfbot:`
```javascript
{
    "credentials": {
        "email": "REPLACE_WITH_YOUR_EMAIL",
        "password": "REPLACE_WITH_YOUR_PASSWORD"
    },
    "scanOwnMessages": true,
    "presenceEnabled": false,
    "channels": [
        {
            "channel": "DISCORD_CHANNEL_ID_TO_DOWNLOAD_FROM",
            "destination": "FOLDER_LOCATION_TO_DOWNLOAD_TO",
            "allowCommands": false,
            "errorMessages": false,
            "reactWhenDownloaded": false
        }
    ]
}
```

`settings.json Example - Advanced:`
```javascript
{
    "credentials": {
        "token": "YOUR_TOKEN",
        "twitterAccessToken": "aaa",
        "twitterAccessTokenSecret": "bbb",
        "twitterConsumerKey": "ccc",
        "twitterConsumerSecret": "ddd"
    },
    "admins": [ "YOUR_DISCORD_USER_ID", "YOUR_FRIENDS_DISCORD_USER_ID" ],
    "adminChannels": [
        {
            "channel": "CHANNEL_ID_FOR_ADMIN_CONTROL"
        }
    ],
    "debugOutput": true,
    "commandPrefix": "downloader_",
    "allowSkipping": true,
    "allowGlobalCommands": true,
    "asyncHistory": false,
    "downloadRetryMax": 5,
    "downloadTimeout": 120,
    "githubUpdateChecking": true,
    "discordLogLevel": 2,
    "filterDuplicateImages": true,
    "filterDuplicateImagesThreshold": 75,
    "presenceEnabled": true,
    "presenceStatus": "dnd",
    "presenceType": 3,
    "presenceOverwrite": "{{count}} files",
    "filenameDateFormat": "2006.01.02-15.04.05 ",
    "embedColor": "#EE22CC",
    "inflateCount": 12345,
    "channels": [
        {
            "channel": "THIS_CHANNEL_ONLY_DOWNLOADS_MEDIA",
            "destination": "media",
            "overwriteAllowSkipping": false,
            "saveImages": true,
            "saveVideos": true,
            "saveAudioFiles": true,
            "saveTextFiles": false,
            "saveOtherFiles": false
        },
        {
            "channel": "THIS_CHANNEL_IS_STEALTHY",
            "destination": "stealthy",
            "allowCommands": false,
            "errorMessages": false,
            "updatePresence": false,
            "reactWhenDownloaded": false
        },
        {
            "channels": [ "CHANNEL_1", "CHANNEL_2", "CHANNEL_3", "CHANNEL_4", "CHANNEL_5" ],
            "destination": "stuff",
            "allowCommands": false,
            "errorMessages": false,
            "updatePresence": false,
            "reactWhenDownloaded": false
        }
    ]
}
```

`settings.json Example - Pretty Much Everything:`
```javascript
{
    "_constants": {
        "DOWNLOAD_FOLDER":              "X:/Discord Downloads",
        "MY_TOKEN":                     "aaabbbccc111222333",
        "TWITTER_ACCESS_TOKEN_SECRET":  "aaabbbccc111222333",
        "TWITTER_ACCESS_TOKEN":         "aaabbbccc111222333",
        "TWITTER_CONSUMER_KEY":         "aaabbbccc111222333",
        "TWITTER_CONSUMER_SECRET":      "aaabbbccc111222333",
        "FLICKR_API_KEY":               "aaabbbccc111222333",
        "GOOGLE_DRIVE_CREDS":           "googleDriveCreds.json",

        "MY_USER_ID":       "000111222333444555",
        "BOBS_USER_ID":     "000111222333444555",

        "SERVER_MAIN":               "000111222333444555",
        "CHANNEL_MAIN_GENERAL":      "000111222333444555",
        "CHANNEL_MAIN_MEMES":        "000111222333444555",
        "CHANNEL_MAIN_SPAM":         "000111222333444555",
        "CHANNEL_MAIN_PHOTOS":       "000111222333444555",
        "CHANNEL_MAIN_ARCHIVE":      "000111222333444555",
        "CHANNEL_MAIN_BOT_ADMIN":    "000111222333444555",

        "SERVER_BOBS":              "000111222333444555",
        "CHANNEL_BOBS_GENERAL":     "000111222333444555",
        "CHANNEL_BOBS_MEMES":       "000111222333444555",
        "CHANNEL_BOBS_SPAM":        "000111222333444555",
        "CHANNEL_BOBS_BOT_ADMIN":   "000111222333444555",

        "SERVER_GAMERZ":                "000111222333444555",
        "CHANNEL_GAMERZ_GENERAL":       "000111222333444555",
        "CHANNEL_GAMERZ_MEMES":         "000111222333444555",
        "CHANNEL_GAMERZ_VIDEOS":        "000111222333444555",
        "CHANNEL_GAMERZ_SPAM":          "000111222333444555",
        "CHANNEL_GAMERZ_SCREENSHOTS":   "000111222333444555"
    },
    "credentials": {
        "token": "MY_TOKEN",
        "userBot": true,
        "twitterAccessToken": "TWITTER_ACCESS_TOKEN",
        "twitterAccessTokenSecret": "TWITTER_ACCESS_TOKEN_SECRET",
        "twitterConsumerKey": "TWITTER_CONSUMER_KEY",
        "twitterConsumerSecret": "TWITTER_CONSUMER_SECRET",
        "flickrApiKey": "FLICKR_API_KEY",
        "googleDriveCredentialsJSON": "GOOGLE_DRIVE_CREDS"
    },
    "admins": [ "MY_USER_ID", "BOBS_USER_ID" ],
    "adminChannels": [
        {
            "channel": "CHANNEL_MAIN_BOT_ADMIN"
        },
        {
            "channel": "CHANNEL_BOBS_BOT_ADMIN"
        }
    ],
    "debugOutput": true,
    "commandPrefix": "d_",
    "allowSkipping": true,
    "scanOwnMessages": true,
    "checkPermissions": false,
    "allowGlobalCommands": false,
    "autorunHistory": true,
    "asyncHistory": false,
    "downloadRetryMax": 5,
    "downloadTimeout": 120,
    "discordLogLevel": 3,
    "githubUpdateChecking": false,
    "filterDuplicateImages": true,
    "filterDuplicateImagesThreshold": 50,
    "presenceEnabled": true,
    "presenceStatus": "idle",
    "presenceType": 3,
    "presenceOverwrite": "{{count}} things",
    "presenceOverwriteDetails": "these are my details",
    "presenceOverwriteState": "this is my state",
    "filenameDateFormat": "2006.01.02_15.04.05_",
    "embedColor": "#FF0000",
    "inflateCount": 69,
    "numberFormatEuropean": true,
    "all": {
        "destination": "DOWNLOAD_FOLDER/Unregistered",
        "allowCommands": false,
        "errorMessages": false,
        "scanEdits": true,
        "ignoreBots": false,
        "overwriteAutorunHistory": false,
        "updatePresence": false,
        "reactWhenDownloaded": false,
        "typeWhileProcessing": false,
        "divideFoldersByServer": true,
        "divideFoldersByChannel": true,
        "divideFoldersByUser": false,
        "divideFoldersByType": false,
        "saveImages": true,
        "saveVideos": true,
        "saveAudioFiles": true,
        "saveTextFiles": false,
        "saveOtherFiles": true,
        "savePossibleDuplicates": true,
        "extensionBlacklist": [
            ".htm",
            ".html",
            ".php",
            ".bat",
            ".sh",
            ".jar",
            ".exe"
        ],
        "saveAllLinksToFile": "DOWNLOAD_FOLDER/Unregistered/Log.txt"
    },
    "allBlacklistChannels": [ "CHANNEL_I_DONT_LIKE", "OTHER_CHANNEL_I_DONT_LIKE" ],
    "allBlacklistServers": [ "SERVER_MAIN", "SERVER_BOBS" ],
    "servers": [
        {
            "server": "SERVER_MAIN",
            "destination": "DOWNLOAD_FOLDER/- My Server",
            "divideFoldersByChannel": true
        },
        {
            "servers": [ "SERVER_BOBS", "SERVER_GAMERZ" ],
            "destination": "DOWNLOAD_FOLDER/- Friends Servers",
            "divideFoldersByServer": true,
            "divideFoldersByChannel": true
        }
    ],
    "channels": [
        {
            "channel": "CHANNEL_MAIN_SPAM",
            "destination": "DOWNLOAD_FOLDER/Spam",
            "overwriteAllowSkipping": false,
            "saveImages": true,
            "saveVideos": true,
            "saveAudioFiles": true,
            "saveTextFiles": false,
            "saveOtherFiles": false
        },
        {
            "channel": "CHANNEL_BOBS_SPAM",
            "destination": "DOWNLOAD_FOLDER/Spam - Bob",
            "overwriteAllowSkipping": false,
            "saveImages": true,
            "saveVideos": true,
            "saveAudioFiles": true,
            "saveTextFiles": false,
            "saveOtherFiles": false
        },
        {
            "channels": [ "CHANNEL_MAIN_MEMES", "CHANNEL_BOBS_MEMES", "CHANNEL_GAMERZ_MEMES" ],
            "destination": "DOWNLOAD_FOLDER/Our Memes",
            "allowCommands": true,
            "errorMessages": true,
            "updatePresence": true,
            "reactWhenDownloaded": true,
            "saveImages": true,
            "saveVideos": true,
            "saveAudioFiles": false,
            "saveTextFiles": false,
            "saveOtherFiles": true
        }
    ]
}
```

## List of Settings
* **"_constants"** `[list of key/value strings]`
    * Use constants to replace values throughout the rest of the settings.
        * ***Note:*** _If a constants name is used within another longer constants name, make sure the longer one is higher in order than the shorter one, otherwise the longer one will not be used properly. (i.e. if you have MY\_CONSTANT and MY\_CONSTANT\_TWO, put MY\_CONSTANT\_TWO above MY\_CONSTANT)_
    * **Basic Example:**
    ```json
    {
        "_constants": {
            "MY_TOKEN": "my token here",
            "ADMIN_CHANNEL": "123456789"
        },
        "credentials": {
            "token": "MY_TOKEN"
        },
        "adminChannels": {
            "channel": "ADMIN_CHANNEL"
        }
    }
    ```
* **"credentials"** `[key/value object]`
    * **"token"** `[string]`
        * _Required for Bot Login or User Login with 2FA, don't include if using User Login without 2FA._
    * **"email"** `[string]`
        * _Required for User Login without 2FA, don't include if using Bot Login._
    * **"password"** `[string]`
        * _Required for User Login without 2FA, don't include if using Bot Login._
    * _`[DEFAULTS]`_ **"userBot"** `[bool]`
        * _Default:_ `false`
        * _Set to `true` for a User Login with 2FA, keep as `false` if using a normal Bot._
    * _`[OPTIONAL]`_ "twitterAccessToken" `[string]`
        * _Won't use Twitter API for fetching media from tweets if credentials are missing._
    * _`[OPTIONAL]`_ "twitterAccessTokenSecret" `[string]`
        * _Won't use Twitter API for fetching media from tweets if credentials are missing._
    * _`[OPTIONAL]`_ "twitterConsumerKey" `[string]`
        * _Won't use Twitter API for fetching media from tweets if credentials are missing._
    * _`[OPTIONAL]`_ "twitterConsumerSecret" `[string]`
        * _Won't use Twitter API for fetching media from tweets if credentials are missing._
    * _`[OPTIONAL]`_ "flickrApiKey" `[string]`
        * _Won't use Flickr API for fetching media from posts/albums if credentials are missing._
    * _`[OPTIONAL]`_ "googleDriveCredentialsJSON" `[string]`
        * _Path for Google Drive API credentials JSON file._
        * _Won't use Google Drive API for fetching files if credentials are missing._


* _`[OPTIONAL]`_ "admins" `[list of strings]`
    * List of User ID strings for users allowed to use admin commands
* _`[OPTIONAL]`_ "adminChannels" `[list of key/value objects]`
    * **"channel"** `[string]`
        * _Channel ID for admin commands & logging._
    * _`[DEFAULTS]`_ "logStatus" `[bool]`
        * _Default:_ `true`
        * _Send status messages to admin channel(s) upon launch._
    * _`[DEFAULTS]`_ "logErrors" `[bool]`
        * _Default:_ `true`
        * _Send status messages to admin channel(s) upon launch._
    * _`[DEFAULTS]`_ "unlockCommands" `[bool]`
        * _Default:_ `false`
        * _Unrestrict admin commands so anyone can use within this admin channel._


* _`[DEFAULTS]`_ "debugOutput" `[bool]`
    * _Default:_ `false`
    * Output debugging information.
* _`[DEFAULTS]`_ "commandPrefix" `[string]`
    * _Default:_ `"ddg "`
* _`[DEFAULTS]`_ "allowSkipping" `[bool]`
    * _Default:_ `true`
    * Allow scanning for keywords to skip content downloading.
    * `"skip", "ignore", "don't save", "no save"`
* _`[DEFAULTS]`_ "scanOwnMessages" `[bool]`
    * _Default:_ `false`
    * Scans the bots own messages for content to download, only useful if using as a selfbot.
* _`[DEFAULTS]`_ "checkPermissions" `[bool]`
    * _Default:_ `true`
    * Checks Discord permissions before attempting requests/actions.
* _`[DEFAULTS]`_ "allowGlobalCommands" `[bool]`
    * _Default:_ `true`
    * Allow certain commands to be used even if not registered in `channels` or `adminChannels`.
* _`[OPTIONAL]`_ "autorunHistory" `[bool]`
    * Autorun history for all registered channels in background upon launch.
    * _This can take anywhere between 2 minutes and 2 hours. It depends on how many channels your bot monitors and how many messages it has to go through. It can help to disable it by-channel for channels that don't require it (see `overwriteAutorunHistory` in channel options)._
* _`[OPTIONAL]`_ "asyncHistory" `[bool]`
    * _Default:_ `false`
    * Runs history commands simultaneously rather than one after the other.
      * **WARNING!!! May result in Discord API Rate Limiting with many channels**, difficulty troubleshooting, exploding CPUs, melted RAM.
* _`[DEFAULTS]`_ "downloadRetryMax" `[int]`
    * _Default:_ `3`
* _`[DEFAULTS]`_ "downloadTimeout" `[int]`
    * _Default:_ `60`
* _`[DEFAULTS]`_ "githubUpdateChecking" `[bool]`
    * _Default:_ `true`
    * Check for updates from this repo.
* _`[DEFAULTS]`_ "discordLogLevel" `[int]`
    * _Default:_ `0`
    * 0 = LogError
    * 1 = LogWarning
    * 2 = LogInformational
    * 3 = LogDebug _(everything)_
* _`[DEFAULTS]`_ "filterDuplicateImages" `[bool]`
    * _Default:_ `false`
    * **Experimental** feature to filter out images that are too similar to other cached images.
    * _Caching of image data is stored via a database file; it will not read all pre-existing images._
* _`[DEFAULTS]`_ "filterDuplicateImagesThreshold" `[float64]`
    * _Default:_ `0`
    * Threshold for what the bot considers too similar of an image comparison score. Lower = more similar (lowest is around -109.7), Higher = less similar (does not really have a maximum, would require your own testing).


* _`[DEFAULTS]`_ "presenceEnabled" `[bool]`
    * _Default:_ `true`
* _`[DEFAULTS]`_ "presenceStatus" `[string]`
    * _Default:_ `"idle"`
    * Presence status type.
    * `"online"`, `"idle"`, `"dnd"`, `"invisible"`, `"offline"`
* _`[DEFAULTS]`_ "presenceType" `[int]`
    * _Default:_ `0`
    * Presence label type. _("Playing \<activity\>", "Listening to \<activity\>", etc)_
    * `Game = 0, Streaming = 1, Listening = 2, Watching = 3, Custom = 4`
        * If Bot User, Streaming & Custom won't work properly.
* _`[OPTIONAL]`_ "presenceOverwrite" `[string]`
    * _Unused by Default_
    * Replace counter status with custom string.
    * [see Presence Placeholders for customization...](#presence-placeholders)
* _`[OPTIONAL]`_ "presenceOverwriteDetails" `[string]`
    * _Unused by Default_
    * Replace counter status details with custom string (only works for User, not Bot).
    * [see Presence Placeholders for customization...](#presence-placeholders)
* _`[OPTIONAL]`_ "presenceOverwriteState" `[string]`
    * _Unused by Default_
    * Replace counter status state with custom string (only works for User, not Bot).
    * [see Presence Placeholders for customization...](#presence-placeholders)


* _`[DEFAULTS]`_ "filenameDateFormat" `[string]`
    * _Default:_ `"2006-01-02_15-04-05 "`
    * [see this Stack Overflow post regarding Golang date formatting.](https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format)
* _`[OPTIONAL]`_ "embedColor" `[string]`
    * _Unused by Default_
    * Supports `random`/`rand`, `role`/`user`, or RGB in hex or int format (ex: #FF0000 or 16711680).
* _`[OPTIONAL]`_ "inflateCount" `[int]`
    * _Unused by Default_
    * Inflates the count of total files downloaded by the bot. I only added this for my own personal use to represent an accurate total amount of files downloaded by previous bots I used.
* _`[DEFAULTS]`_ "numberFormatEuropean" `[bool]`
    * _Default:_ false
    * Formats numbers as `123.456,78`/`123.46k` rather than `123,456.78`/`123,46k`.


* **"all"** `[key/value objects]`
    * **Follow `channels` below for variables, except channel & server ID(s) are not used.**
    * If a pre-existing config for the channel or server is not found, it will download from any and every channel it has access to using your specified settings.
* "allBlacklistServers" `[list of strings]`
    * _Unused by Default_
    * Blacklists servers (by ID) from `all`.
* "allBlacklistChannels" `[list of strings]`
    * _Unused by Default_
    * Blacklists channels (by ID) from `all`.


* _`[USE THIS OR CHANNELS]`_ **"servers"** `[list of key/value variables]`
    * _`[THIS OR BELOW]`_ **"server"** `[string]`
        * Server ID to monitor.
    * _`[THIS OR ABOVE]`_ **"servers"** `[list of strings]`
        * Server IDs to monitor, for if you want the same configuration for multiple servers.
    * **ALL OTHER VARIABLES ARE SAME AS BELOW**


* _`[USE THIS OR SERVERS]`_ **"channels"** `[list of key/value variables]`
    * _`[THIS OR BELOW]`_ **"channel"** `[string]`
        * Channel ID to monitor.
    * _`[THIS OR ABOVE]`_ **"channels"** `[list of strings]`
        * Channel IDs to monitor, for if you want the same configuration for multiple channels.
    * **"destination"** `[string]`
        * Folder path for saving files, can be full path or local subfolder.
    * _`[DEFAULTS]`_ "enabled" `[bool]`
        * _Default:_ `true`
        * Toggles bot functionality for channel.
    * _`[DEFAULTS]`_ "allowCommands" `[bool]`
        * _Default:_ `true`
        * Allow use of commands like ping, help, etc.
    * _`[DEFAULTS]`_ "errorMessages" `[bool]`
        * _Default:_ `true`
        * Send response messages when downloads fail or other download-related errors are encountered.
    * _`[DEFAULTS]`_ "scanEdits" `[bool]`
        * _Default:_ `true`
        * Check edits for un-downloaded media.
    * _`[DEFAULTS]`_ "ignoreBots" `[bool]`
        * _Default:_ `false`
        * Ignores messages from Bot users.
    * _`[OPTIONAL]`_ overwriteAutorunHistory `[bool]`
        * Overwrite global setting for autorunning history for all registered channels in background upon launch.
    * _`[DEFAULTS]`_ "updatePresence" `[bool]`
        * _Default:_ `true`
        * Update Discord Presence when download succeeds within this channel.
    * _`[DEFAULTS]`_ "reactWhenDownloaded" `[bool]`
        * _Default:_ `true`
        * Confirmation reaction that file(s) successfully downloaded.
    * _`[OPTIONAL]`_ "reactWhenDownloadedEmoji" `[string]`
        * _Unused by Default_
        * Uses specified emoji rather than random server emojis. Simply pasting a standard emoji will work, for custom Discord emojis use "name:ID" format.
    * _`[DEFAULTS]`_ "blacklistReactEmojis" `[list of strings]`
        * _Unused by Default_
        * Block specific emojis from being used for reacts. Simply pasting a standard emoji will work, for custom Discord emojis use "name:ID" format.
    * _`[DEFAULTS]`_ "typeWhileProcessing" `[bool]`
        * _Default:_ `false`
        * Shows _"<name> is typing..."_ while processing things that aren't processed instantly, like history cataloging.
    * _`[OPTIONAL]`_ "overwriteFilenameDateFormat" `[string]`
        * _Unused by Default_
        * Overwrites the global setting `filenameDateFormat` _(see above)_
        * [see this Stack Overflow post regarding Golang date formatting.](https://stackoverflow.com/questions/20234104/how-to-format-current-time-using-a-yyyymmddhhmmss-format)
    * _`[OPTIONAL]`_ "overwriteAllowSkipping" `[bool]`
        * _Unused by Default_
        * Allow scanning for keywords to skip content downloading.
        * `"skip", "ignore", "don't save", "no save"`
    * _`[OPTIONAL]`_ "overwriteEmbedColor" `[string]`
        * _Unused by Default_
        * Supports `random`/`rand`, `role`/`user`, or RGB in hex or int format (ex: #FF0000 or 16711680).
    * _`[DEFAULTS]`_ "usersAllWhitelisted" `[bool]`
        * _Default:_ `true`
        * Allow messages from all users to be handled. Set to `false` if you wish to use `userWhitelist` to only permit specific users messages to be handled.
    * _`[OPTIONAL]`_ "userWhitelist" `[list of strings]`
        * Use with `usersAllWhitelisted` as `false` to only permit specific users to have their messages handled by the bot. **Only accepts User ID's in the list.**
    * _`[OPTIONAL]`_ "userBlacklist" `[list of strings]`
        * Use with `usersAllWhitelisted` as the default `true` to block certain users messages from being handled by the bot. **Only accepts User ID's in the list.**
    * _`[DEFAULTS]`_ "divideFoldersByServer" `[bool]`
        * _Default:_ `false`
        * Separate files into subfolders by server of origin _(e.g. "My Server", "My Friends Server")_
    * _`[DEFAULTS]`_ "divideFoldersByChannel" `[bool]`
        * _Default:_ `false`
        * Separate files into subfolders by channel of origin _(e.g. "my-channel", "my-other-channel")_
    * _`[DEFAULTS]`_ "divideFoldersByUser" `[bool]`
        * _Default:_ `false`
        * Separate files into subfolders by user who sent _(e.g. "Me#1234", "My Friend#0000")_
    * _`[DEFAULTS]`_ "divideFoldersByType" `[bool]`
        * _Default:_ `true`
        * Separate files into subfolders by type _(e.g. "images", "video", "audio", "text", "other")_
    * _`[DEFAULTS]`_ "saveImages" `[bool]`
        * _Default:_ `true`
    * _`[DEFAULTS]`_ "saveVideos" `[bool]`
        * _Default:_ `true`
    * _`[DEFAULTS]`_ "saveAudioFiles" `[bool]`
        * _Default:_ `false`
    * _`[DEFAULTS]`_ "saveTextFiles" `[bool]`
        * _Default:_ `false`
    * _`[DEFAULTS]`_ "saveOtherFiles" `[bool]`
        * _Default:_ `false`
    * _`[DEFAULTS]`_ "savePossibleDuplicates" `[bool]`
        * _Default:_ `false`
        * Save file even if exact filename already exists or exact URL is already recorded in database.
    * _`[DEFAULTS]`_ "extensionBlacklist" `[list of strings]`
        * _Default:_ `[ ".htm", ".html", ".php", ".exe", ".dll", ".bin", ".cmd", ".sh", ".py", ".jar" ]`
        * Ignores files containing specified extensions. Ensure you use proper formatting.
    * _`[OPTIONAL]`_ "domainBlacklist" `[list of strings]`
        * Ignores files from specified domains. Ensure you use proper formatting.
    * _`[OPTIONAL]`_ "saveAllLinksToFile" `[string]`
        * Saves all sent links to file, does not account for any filetypes or duplicates, it just simply appends every raw link sent in the channel to the specified file.

### Presence Placeholders
_For `presenceOverwrite`, `presenceOverwriteDetails`, `presenceOverwriteState`_
Key | Description
--- | ---
`{{dgVersion}}`             | discord-go version
`{{ddgVersion}}`            | Project version
`{{apiVersion}}`            | Discord API version
`{{countNoCommas}}`         | Raw total count of downloads (without comma formatting)
`{{count}}`                 | Raw total count of downloads
`{{countShort}}`            | Shortened total count of downloads
`{{numServers}}`            | Number of servers bot is in
`{{numBoundServers}}`       | Number of bound servers
`{{numBoundChannels}}`      | Number of bound channels
`{{numAdminChannels}}`      | Number of admin channels
`{{numAdmins}}`             | Number of designated admins
`{{timeSavedShort}}`        | Last save time formatted as `3:04pm`
`{{timeSavedShortTZ}}`      | Last save time formatted as `3:04pm MST`
`{{timeSavedMid}}`          | Last save time formatted as `3:04pm MST 1/2/2006`
`{{timeSavedLong}}`         | Last save time formatted as `3:04:05pm MST - January 2, 2006`
`{{timeSavedShort24}}`      | Last save time formatted as `15:04`
`{{timeSavedShortTZ24}}`    | Last save time formatted as `15:04 MST`
`{{timeSavedMid24}}`        | Last save time formatted as `15:04 MST 2/1/2006`
`{{timeSavedLong24}}`       | Last save time formatted as `15:04:05 MST - 2 January, 2006`
`{{timeNowShort}}`          | Current time formatted as `3:04pm`
`{{timeNowShortTZ}}`        | Current time formatted as `3:04pm MST`
`{{timeNowMid}}`            | Current time formatted as `3:04pm MST 1/2/2006`
`{{timeNowLong}}`           | Current time formatted as `3:04:05pm MST - January 2, 2006`
`{{timeNowShort24}}`        | Current time formatted as `15:04`
`{{timeNowShortTZ24}}`      | Current time formatted as `15:04 MST`
`{{timeNowMid24}}`          | Current time formatted as `15:04 MST 2/1/2006`
`{{timeNowLong24}}`         | Current time formatted as `15:04:05 MST - 2 January, 2006`
`{{uptime}}`                | Shortened duration of bot uptime

## Development
* I'm a complete amateur with Golang. If anything's bad please make a pull request.
* Versioning is `[MAJOR].[MINOR].[PATCH]`

### Credits & Dependencies
* [github.com/Seklfreak/discord-image-downloader-go - the original project this originated from](https://github.com/Seklfreak/discord-image-downloader-go)

#### Core Dependencies
* [github.com/bwmarrin/discordgo](https://github.com/bwmarrin/discordgo)
* [github.com/Necroforger/dgrouter](https://github.com/Necroforger/dgrouter)
* [github.com/HouzuoGuo/tiedot/db](https://github.com/HouzuoGuo/tiedot)
* [github.com/fatih/color](https://github.com/fatih/color)

#### Other Dependencies
* [github.com/AvraamMavridis/randomcolor](https://github.com/AvraamMavridis/randomcolor)
* [github.com/ChimeraCoder/anaconda](https://github.com/ChimeraCoder/anaconda)
* [github.com/ChimeraCoder/tokenbucket](https://github.com/ChimeraCoder/tokenbucket)
* [github.com/Jeffail/gabs](https://github.com/Jeffail/gabs)
* [github.com/PuerkitoBio/goquery](https://github.com/PuerkitoBio/goquery)
* [github.com/azr/backoff](https://github.com/azr/backoff)
* [github.com/dustin/go-jsonpointer](https://github.com/dustin/go-jsonpointer)
* [github.com/dustin/gojson](https://github.com/dustin/gojson)
* [github.com/fsnotify/fsnotify](https://github.com/fsnotify/fsnotify)
* [github.com/garyburd/go-oauth](https://github.com/garyburd/go-oauth)
* [github.com/hako/durafmt](https://github.com/hako/durafmt)
* [github.com/hashicorp/go-version](https://github.com/hashicorp/go-version)
* [github.com/kennygrant/sanitize](https://github.com/kennygrant/sanitize)
* [github.com/nfnt/resize](https://github.com/nfnt/resize)
* [github.com/rivo/duplo](https://github.com/rivo/duplo)
* [golang.org/x/net](https://golang.org/x/net)
* [golang.org/x/oauth2](https://golang.org/x/oauth2)
* [google.golang.org/api](https://google.golang.org/api)
* [gopkg.in/ini.v1](https://gopkg.in/ini.v1)
* [mvdan.cc/xurls/v2](https://mvdan.cc/xurls/v2)