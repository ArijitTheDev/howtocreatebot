# How to Create A Discord Bot

In this tutorial I'm gonna explain, how can you create your own discord bot!

### Code Editor
You can use any code editors you want. I'm not gonna give tutorials on code editors, that's a basic knowledge you can get from anywhere. I'm just going to give tutorial to you on how to create a Discord Bot!

### Packages Required
I'm mainly going to use a framework known as WOKCommands which is based on Discord.js, for making the bot.

To install Packages, follow these steps:
- Open your terminal in your project
- Type this command:
```
npm i wokcommands discord.js path mongoose

```
### Creating `index.js` file
```js
// Importing Packages
const Discord = require('discord.js')
const WOK = require('wokcommands')
const path = require('path')

// Creating Client
const { Client, Intents } = Discord
const client = new Client({
    intents: [
    Intents.FLAGS.GUILDS,
    Intents.FLAGS.GUILD_MESSAGES,
    Intents.FLAGS.GUILD_MESSAGE_REACTION
  ],
})

// Importing Config
client.config = require('./config.js')

//Creating Wokcommands instance
client.on('ready', () => {
const dbOptions = {
  keepAlive: true,
}
new WOK(client,{
  commandsDir: path.join(__dirname, 'commands')
  testServers: client.config.TESTSERVERS,
  botOwners: client.config.BOTOWNERS,
  mongoUri: client.config.DB_URI,
})

//Logging in the bot
client.login(client.config.BOT_TOKEN)
})
```
