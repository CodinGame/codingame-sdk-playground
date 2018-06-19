# Game Runner

The Game Runner lets you run your game locally during developement. It comes with a handy HTML package to watch each game's replay.

You can create your own AI for your game and use the Game Runner to connect it to your game's implementation.

You can also fiddle with your game's initialization input, such as the seed for random values (for **Multiplayer** games) or a [test case file](core-4-configuration.md#test-case-file) (for **Solo** games).

# Usage

Include the dependency below in the pom.xml of your project.
```xml
<dependency>
  <groupId>com.codingame.gameengine</groupId>
  <artifactId>runner</artifactId>
  <version>2.3.1</version>
</dependency>
```
Or a more recent version.

Instantiate a `MultiplayerGameRunner` or a `SoloGameRunner` to launch a game with the `start()` method. This will create a temporary directory and start a server to serve the files of that directory. You need not stop the previous server to launch a new game.

By default, you can access the game viewer for testing at [http://localhost:8888/test.html](http://localhost:8888/test.html). You may change the configuration of the game viewer by editing the `config.js` file. See the [Viewer configuration](core-4-configuration.md#viewer-configuration) for more details.

Warning ⚠ To use the game viewer locally, your browser must support ES6 JavaScript **modules**. For Chrome, that's version 61 or more. For Firefox, from version 54 this feature is behind the `dom.moduleScripts.enabled` preference. To change preferences in Firefox, visit `about:config`.


# Examples

In order to run a game, you must have prepared a `Referee` and a `Player`. The game will surely fail to finish if they are not properly implemented. See [Game Manager](core-3-game-manager.md) for details.

## Running a **Multiplayer** game

### Using the same java class for each player:
```java
MultiplayerGameRunner gameRunner = new MultiplayerGameRunner();
gameRunner.addAgent(Player.class);
gameRunner.addAgent(Player.class);
gameRunner.start();
    
```
⚠ _This method will prevent the agent from printing to stdout from any other class than Player. It has been deprecated for this reason._

### Using external python programs as players:
```java
MultiplayerGameRunner gameRunner = new MultiplayerGameRunner();

gameRunner.addAgent("python3 /home/user/player1.py");
gameRunner.addAgent("python3 /home/user/player2.py");
gameRunner.addAgent("python3 /home/user/player3.py");

gameRunner.start();
```

### Using a custom seed:
```java
// I want to debug the strange case of this particuliar seed: 53295539

Properties refereeInput = new Properties();
refereeInput.put("seed", "53295539");

MultiplayerGameRunner gameRunner = new MultiplayerGameRunner();
gameRunner.setGameParameters(refereeInput);
gameRunner.addAgent(Player1.class);
gameRunner.addAgent(Player2.class);
gameRunner.start();
```

## Running a **Solo** game

### Using a java class and a test case with its filename:
```java
SoloGameRunner gameRunner = new SoloGameRunner();
gameRunner.setTestCase("test1.json"); // You must set a test case to run your game.
gameRunner.setAgent(Player.class);
gameRunner.start();
```

# Viewing a replay

Once a game is run, files are copied into a temporary folder. A server is started to serve those files on `localhost:8888`.

The test page `/test.html` let's you watch the replay as it would appear on CodinGame.

Many of the viewers game-specific parameters may be changed by the default `config.js` file located in `src/main/resources/view` of your game's project. These parameters include: 
* The list of modules needed by the game.
* The colours for the different players (affects the IDE).

See the [Viewer configuration](core-4-configuration.md#viewer-configuration) for more details.