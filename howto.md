### Add Streaming Extensions to a TypeScript/Node.js Bot

Starting with a JS sample bot:

- In order to use the preview version of the botbuilder-streaming-extensions library required to use Direct Line Speech, run the following terminal commands from the root dir of the bot:

	 ```
   npm config set registry https://botbuilder.myget.org/F/botbuilder-v4-js-daily/npm/		
    npm install		
    npm config set registry https://registry.npmjs.org/
    ```
    
- In your bot’s index.ts file update the line creating the restify server to read:

	`let server = restify.createServer({ handleUpgrades: true });`
	
- Still in index.ts define the BotFrameworkStreamingAdapter and add a GET endpoint to index.ts with the following code: 

```
const { BotFrameworkStreamingAdapter } = require('botbuilder-streaming-extensions');
server.get('/api/messages', function upgradeRoute(req, res) {
    const streamingAdapter = new BotFrameworkStreamingAdapter(bot);
    streamingAdapter.connectWebSocket(req, res, { 
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword,
        channelService: process.env.ChannelService,
    });
});
```
 
	
