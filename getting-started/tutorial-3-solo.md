# Getting started

This document will show you, through the simple game "Fishy Adventures" how to create your own **Solo** game and test it.

The source code is available on GitHub: [https://github.com/CodinGame/game-fishy-adventures](https://github.com/CodinGame/game-fishy-adventures)

## Requirements

All you need is a Java IDE such as [Eclipse](https://www.eclipse.org/) or [IntelliJ](https://www.jetbrains.com/idea/) and a git client to clone the example.

⚠ To use the game viewer locally, your browser must support ES6 JavaScript modules. For Chrome, that's version 61 or more. For Firefox, from version 54 this feature is behind the dom.moduleScripts.enabled preference. To change preferences in Firefox, visit about:config.

## Import project

First of all, you need to download the source code of the game:
```
git clone https://github.com/CodinGame/game-fishy-adventures.git
```

Then, import this project as an existing maven project into your IDE:
- Eclipse: File > Import > Existing Maven Projects
- IntelliJ IDEA: Import Project > Select game-tictactoe > Import project from external model > Maven

## Project Hierarchy

Here's the file hierarchy for the project Fishy Adventures:
```
.
├── config
│   ├── config.ini
│   ├── statement_en.html
│   ├── statement_fr.html
│   ├── stub.txt
│   ├── test1.json
│   ├── test2.json
│   ├── test3.json
│   ├── test4.json
│   └── test5.json
├── pom.xml
├── README.md
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── codingame
│   │   │           └── game
│   │   │               ├── Action.java
│   │   │               ├── Constants.java
│   │   │               ├── Coord.java
│   │   │               ├── Player.java
│   │   │               └── Referee.java
│   │   └── resources
│   │       └── view
│   │           ├── assets
│   │           │   ├── background.png
│   │           │   ├── eggs.png
│   │           │   └── fish.png
│   │           ├── config.js
│   │           └── demo.js
│   └── test
│       ├── java
│       │   ├── Main.java
│       │   └── Player1.java
│       └── resources
│           └── log4j2.properties
```

- **./config:** contains the settings such as the game title, statement, test cases, number of players, etc.
- **./src/main/java:** source code of the game itself
- **./src/main/resources:** graphical assets and configuration of the view
- **./src/test/java:** classes used for local development (AI codes to test your game)

## Launch the game

The class to run is test/java/Main.java. This will launch a [web server](http://localhost:8888/) to serve a page with the viewer of the game.

![Game Preview](resources/testhtml.png)

Use this page to see the rendering of your game. It also allows you to export a zip archive of the game.

## Deploy on codingame

Go to [www.codingame.com](https://www.codingame.com), then click on **Contribute** > **Create a new puzzle** > **Solo Game** (This section is not available to anyone yet, please contact us if you want the access).

Then, import on CodinGame the game you have exported during the previous step. The game will be compiled on our servers and a preview link will appear if the compilation succeeded and if the configuration is correct.

## Create Your Own Game

Now that you are able to start a game on your computer and export it to CodinGame, you can start creating your own game. For that, it is suggested you start with the Skeleton: [https://github.com/CodinGame/game-skeleton](https://github.com/CodinGame/game-skeleton)

You can also read the code of others games (see [Examples](misc/misc-2-examples.md)). More advanced documentation is available in the [Core concepts](core-concepts/core-1-introduction.md) section.

If you do not have an artistic mind, we provide a [Github asset repository](https://github.com/CodinGame/codingame-sdk-assets) with a lot of free graphical resources to bootstrap your game.
