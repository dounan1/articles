WeChat “Jump and Jump” Game Popularize Mini-games, how can developers jump into it?
Author | Ling Huabin, Wang Zhe Editor in charge | Xu Weilong
![1]

When opening the new WeChat version 6.6.1, a starting page pops up: “playing a mini-game is what matters”. Suddenly, your entire circle of friends is playing the latest viral game - in wechat. Many game developers could not wait to dive into these popular mini-games. Today Wang Zhe and I will introduce WeChat mini-games development from the technical perspective. This series of articles summarize the collaboration between the Cocos Creator game engine team and the WeChat team. Cocos Creator v1.8 editor supports one-click release of WeChat game mini-games.

The article today is the first one of the mini-game development series.

1. Characteristics of the WeChat mini-game ecosystem
  WeChat game has released the first batch of 17 games, including six chess games, as well as happy match-three game, love matching-three, tank battle, guard your radish and other casual games.
  In terms of sources of traffic (entrance to the games), WeChat mini-games players mainly enter the games through the following channels: 
* WeChat group or sharing from friends* Scanning the QR code of the game* Recently played games displayed after pulling down the chatting page* Discover - Mini-program* Discover - Games - My mini-games
  ![2]
  From the technical point of view, WeChat mini-game is based on mini-program, with game library API added upon it. Mini-games can only run in the mini-program environment, so they are neither native games nor completely equivalent to HTML5 games. Despite that, mini-games are more friendly to HTML5 game developers. To minimize the cost of transferring HTML5 games to the mini-game platform, mini-games adopt WebGL, JavaScript, and other HTML5 technologies as much as possible. 
  Mini-games can be understood as games that are built with HTML5 technologies, provide a native game gaming experience and run within the WeChat environment. 
  ![3]
  There are many advantages of WeChat mini-games to use this model. The two biggest advantages are stability and control. Compared to native games, WeChat can enclose the whole game ecosystem within itself. Compared to HTML5 games, mini-games won’t be disturbed by injected advertisements and in-game payments.
  The runtime environment for WeChat mini-games has a major advantage compared to other Runtime environments that it is "compatible with HTML5 game ecosystem.” In other words, no matter which game engine you used to develop the HTML5 games, it will be very easy to transfer them to the mini-game environment. This enables WeChat mini-games to leverage the tremendous power of HTML5 ecosystem.
  Apart from technology, the strongest point of WeChat mini-games is social spreading. A crucial part of mini-game design is to utilize the social aspect of WeChat to acquire new users. We can see that in the first batch of mini-games, the entrances of the games are hidden deep in the WeChat app, except for “Jump and jump” which has a pop-up starting page. So the traffic sources are not mainly from recommendation list, but from social communication and sharing. This is very different from the popular game design philosophy in the market, which actively guide and filter the players by combining and opening servers.
  WeChat mini-games have premium traffic source, huge potential user base and the characteristics of quick-start and highly shareable. All these features point to a bright future of mini-games, now it’s up to you the game developers to catch this opportunity and find the types of games most suitable for WeChat users.
2. API Part I: The basic knowledge of developing mini-game
  As mentioned above, the development of mini-game mostly reuses the HTML5 technology stack, so developers of HTML5 games will get started much faster. They can even transfer HTML5 games to mini-game platform very quickly. Specifically, WeChat mini-game development technologies can be divided into three parts.
  ![4]
3. Low-level Technologies
  First is the programming language. WeChat mini-games only support JavaScript, but languages like TypeScript and CoffeeScript, which can be combined into JavaScript, can also be used as a development language.
  Second is what game libraries API do WeChat mini-games support. The supported APIs mainly include the Canvas 2D API of HTML5 and WebGL 1.0 API. The most important rendering effect can be done using any of these APIs, but they should not be mixed in game development. In addition to that, the rendering mode of WebGL also supports 3D rendering.
4. Middleware: Game Engine
  Directly using Canvas 2D or WebGL to make the game can be a very demanding, but also very time-consuming work, you certainly don’t want to spend over a year on a mini-game project, right? Therefore, the use of HTML5 game engine is a very wise choice. The high-level port that the engine encapsulates can greatly reduce the skill threshold for developers and shorten the project cycle. 
  At present, all the three major domestic game engine maker Cocos Creator, Egret, Laya have supported the release of mini-games. Phaser.js, Three.js and other foreign HTML5 engine don’t support direct release, but you can also successfully run in a small game environment after some customizations.
5. WeChat SDK 
  WeChat mini-games also provide a wealth of WeChat internal SDK for developers to build the user login, forwarding, ranking and other conventional social functions. 
  ![5]
  Furthermore, in addition to the conventional social functions, players can complete the team-building in the game by forwarding the game to friends, plus its click-and-play characteristic, together making the gaming experience greater than ever.
  ![6]Invite friends to join the game in mini-game Happy Tank Battle.![7]
  Friends can click the link to directly enter the game and complete the team
  This “group forwarding + click-to-play” mechanism can potentially lead to interesting social gaming phenomena.
6. API Part II: Understanding the Low-level Development Structure of Mini-game
  As we said at the beginning of this article, mini-games are neither native games nor equivalent to HTML5 games. However, its development environment is actually closely related to both types of games. The relationship between mini-games and HTML5 games is that the mini-games use the rendering interface of HTML5, but how is mini-game related to native games? Let us explain with an infographic:
  ![8]
  The environment in which the mini-games run is actually the native environment of WeChat. The JavaScript codes of the games are not executed by the browser, but by the independent JavaScript engine on the JS VM layer. On the Android platform, it uses Google's V8 engine and on iOS it uses Apple's JavaScript Core engine. 
  Of course, JS engine is only responsible for the interpretation and implementation of JS logic but does not support the rendering interface. Then how do mini-game developers connect their games to the rendering interface and many other WeChat programming interfaces? 
  Here we have to mention the “script binding technology“. This technology can bridge certain kind of native language interface to the script interface when called in the script layer interface, it will automatically forward the request to the native layer, thus calling the native interface. WeChat mini-game environment uses such technology to bind the iOS / Android native platform rendering, user, network, audio and video interfaces to a JavaScript interface. This is the mechanism of connecting WeChat native layer module to the mini-game layer module, as shown in the diagram above. Due to the limited space of this article, script binding technology can not be explored in more details. If you are interested, you can learn more about Cocos Creator's JSB binding implementation, which is the only fully open-source binding technology in game engines.
  Although mini-game has developed a technical structure, there are still numerous API compatibility issues when developers try to transfer HTML5 games to the mini-game platform. The simplest examples are “document object not found(does not exist)” and “image object does not exist”. In order to reduce the cost of transferring, WeChat team provided an Adapter script to improve the compatibility with some browsers.
  ![9]
  As shown above, the Adapter script provides most browser interfaces that HTML5 games rely on. This diagram also shows the interface modules that developers can use in WeChat games: 
* Browser rendering interface* Browser Adapter* WeChat service SDK
  It is worth mentioning that the Adapter script is no longer maintained, so the additional interface adapter needs to be completed by the developer and most of the features that rely on the DOM interface cannot fit into the mini-game environment. 
  We also mentioned just now that we recommend using the game engine to develop mini-games. The game engine not only encapsulates the high-level interface but also tries to eliminate the differences between the browser and the mini-game environment. 
  ![10]
  As we can see in the diagram, without the help of the game engine, developers need to face the low-level APIs of the mini-game. When developers use the game engine, the engine is dealing with the APIs.
  Here, let’s summarize the work that game engine can do for developers: 

Framework: High-level API encapsulation, more convenient for game development; Resource loading adapter; Event processing adapter; Audio playing adaptation; Window adaptation; Input box adaption; Adding other missing interfaces, such as adding DOM Parser to parse TileMap. 
Editor: Optimize the synergy of the programmer, designer, and planner.A good game editor can significantly shorten the development cycle. 
GENERAL: Excellent game engines can provide high device compatibility and stable performance; Cross-platform game engine can empower developers to publish HTML5 game, mini-game, native game seamlessly
High-efficiency game editors bring down development costs; the resulting low entry barriers reduce labor costs; high compatibility and stable performance reduce maintenance costs; cross-platform / channel feature brings a huge amount of traffic. For developers, these factors are the key to profitability.
4. Starting fine-tuning and debugging mini-games
  By the time this article is written, WeChat public platform has not opened to developers to release their games, so you can only try it on a technical level using the "experience mini-games" feature in mini-game development tools. But do not worry, WeChat team should soon open the application of the mini-game category. 
5. Introduction of WeChat Developer Tools
  The following picture is the basic layout of WeChat Developer Tools when doing game development: 
  ![11]WeChat developer tools basic layout
  At the top of the page is the toolbar, which contains the most important functions including compilation, preview and configuration details; on the left is the simulator window to show the effect of game; on the upper right corner is the code editor, where you can view the list of files in the project, edit the text file; on the lower right corner is the debugger window, which you can use just like the Chrome development tool.
6. WeChat game configuration and file importing
  In a WeChat mini-game project, the configuration files such as project.config.json and game.json are the first files that we need to add. The file project.config.json can define your game appid, game name, configuration and so on. Game.json is mainly used to specify the game orientation and network timeout. 
  Noted that mini-game doesn’t support any HTML files, the entrance file is game.js. You need to start the game engine and game scripts in the game.js file using require function. The usage of require function follows the specification in node.js. 
7. Compile and preview 
  WeChat developers tools will monitor the changes in scripts and configurations and update automatically. You can also click the compile button at the top of the page to recompile. When you need to preview the effect of the game on your smartphone, you can click the preview button to generate a QR code and scan to enter the game. The process of generating a QR code is actually compressing and uploading a mini-package to the WeChat CDN, so it will take some time. 
8. Details Configuration 
  Details configuration includes some important configuration options, such as: 
* Debugging basic library: for mini-game you should choose game;* ES6 to ES5: whether or not ES6 script should be converted to ES5;* Automatic compression when uploading the code: whether to compress the script;* Do not check domain name security, TLS versions, and HTTPS certificates: This option needs to be turned on to properly access your server when you are testing locally or through an informal domain name.
5. Market Outlook
  Finally, in terms of market, the HTML5 technology stack, which is favored by WeChat mini-games, has great potential. Currently, there are many game engines that use JavaScript to support cross-platform games. Take Cocos Creator for an example, you can write a set of game codes in the editor and seamlessly publish it as an HTML5 mobile web game, PC web game, mobile phone native game, and mini-game. According to the industry report published by CNG (gama shuju) in early December, the market size for mobile phone native games in China is 116.2 billion RMB by 2017, and 64.8 billion for PC games and 15.6 billion for PC web games. Therefore, if we do a simple calculation using the proportion, the market size for mobile web game is  1162 ÷ 648 x 156 = RMB 28 billion RMB each year. (4.5 billion USD)
  If you think further, you will find that since Flash will stop official maintenance starting from 2020, a large number of PC web games are switching to HTML5 technology, and many mobile native games also reappear in the form of micro-client-side games. So if we leave out the constraints of internal competition, HTML5 technology stack can support a game market with the size of 28 billion (mobile web game) + 15.6 billion (PC web game) + some of the mobile native games ≈ 50 billion RMB each year. (8 billion USD)
  50 billion RMB is only the estimated size of the domestic market. According to the foreign market research firm Newzoo, in 2017, China's gaming industry accounts for 25% of the world’s gaming industry. So, HTML5 technology can theoretically support the global mobile web game, mobile native game and PC web game industry, the market size can go up to 200 billion RMB each year. (32 billion USD)
  Therefore, it is high time for game developers who want to enter this field to master the HTML5 technology stack and social game development techniques (such as WeChat mini-games, QQ limixiu, Facebook Instant Games, games on the new platform of mobile web games), understand the characteristics of users on these social platforms, and put forward targeted game design.
  And the general opinion is that under the influence of capital investments, the time window for mobile web game development would be only 1 to 1.5 years. There will be successful rollouts of the traditional native game makers as well as the emergence of new developers and publishers. It usually takes about 5 years for such a golden opportunity to appear in the gaming industry.



About the authors: 
Ling Hua Bin, Cocos Creator main programmer, Game Jamer, player. He was responsible for Cocos2d-JS, heat update framework, JSB framework. Now he is mainly responsible for the mini-game publishing process, Cocos Creator engine renderer architecture. 
Wang Zhe, Cocos Engine founder, chief customer service.
