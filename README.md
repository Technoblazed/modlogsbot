# modlogsbot
Bot that copies mod logs from twitch into discord.

## Installation
1. Install node.js
2. run `npm install`
3. set up your config file
4. run `node index.js` or `node index.js path/to/config/file.json`
5. Go to `https://discordapp.com/oauth2/authorize?client_id=`discord client ID`&scope=bot&permissions=3072` and add it to your discord server.

# Config file
The config file is a JSON document that defines parameters for the bot and the channels it listens to. See settings.default.json for a template. By default, it has to be called `settings.json`

**DO NOT EDIT THE FILE WHILE THE BOT IS RUNNING, IT WILL GET OVERWRITTEN**

You will need:

1. A discord bot client ID and token
2. A twitch account that is moderator in the channels that you plan to use, with its ID and any oauth (can have no scope whatsoever)

### discord settings
`client_id`, `token`, `prefix` should be obvious. `admins` is a list of discord user IDs that can use commands.

### twitch settings
Unless using a load balancer for pubsub, `pubsub_server` should be "wss://pubsub-edge.twitch.tv/v1".
- `mod.id` and `mod.oauth` are the ID (not name!) and oauth of your twitch moderator account.
- `ignored.users` is a list of usernames, for which the `ignored.actions` commands should be ignored.
- `client_id` is any client_id to use (I could replace that with using the oauth, but I am planning to move to a multi-user system).

### listeners
Listeners can be added on the fly using the commands below and shouldnt be added manually, but for the sake of completeness:

- `listeners` is a list of listeners (duh), each containing a `twitch` and a `discord` object:
- `twitch` is an object containing `channel_id` and `channel_name` (these should be matching, else you will run into trouble, but if you know what you are doing and have a reason to do so, you can deviate from that)
- `discord` is an object containing just a `channel_id`, the place where the modlogs from the twitch channel are sent to.

# Commands
Commands are available to `admins` in discord only.
Available commands are:
- `!help` - lists the available commands
- `!invite` - gives a bot invite link
- `!listen <channel>` - listens to the twitch channel "`channel`" in the current channel
- `!unlisten [channel]` - unlistens from the channel "`channel`" in the current discord channel. If no channel is specified, it unlistens from all. If multiple are specified, it unlistens from all of them.
- `!list` - gives a list of chanels the bot is listening to.