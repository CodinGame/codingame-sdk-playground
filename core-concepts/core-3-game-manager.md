# The Game Manager

This document introduces the core code of the CodinGame's toolkit which includes the Game Manager and the viewer's replay engine.

# Usage

Include the dependency below in the pom.xml of your project.
```xml
<dependency>
  <groupId>com.codingame.gameengine</groupId>
  <artifactId>core</artifactId>
  <version>2.3.1</version>
</dependency>
```
Or a more recent version.


## Basic Implementation

Your project should include the class `Player` and the class `Referee`.
Your `Referee` class may then inject (using Guice) a singleton of `SoloGameManager` or `MultiplayerGameManager` (corresponding to the type of game you want to create) parameterized by your `Player` class.
Your `Player` class should extend from `AbstractSoloPlayer` or `AbstractMultiplayerPlayer`.

Example for a **Multiplayer** game:
```java
class Player extends AbstractMultiplayerPlayer {
    @Override
    public int getExpectedOutputLines() {
        return 1;
    }
}

public class Referee extends AbstractReferee {
    @Inject private MultiplayerGameManager<Player> gameManager;
    @Override
    public void init() {
    }

    @Override
    public void gameTurn(int turn) {
    }

    @Override
    public void onEnd() {
    }
}
```

Example for a **Solo** game:
```java
class Player extends AbstractSoloPlayer {
    @Override
    public int getExpectedOutputLines() {
        return 1;
    }
}

public class Referee extends AbstractReferee {
    @Inject private SoloGameManager<Player> gameManager;
    @Override
    public void init() {
    }

    @Override
    public void gameTurn(int turn) {
    }

    @Override
    public void onEnd() {
    }
}
```

The Game Manager's API will thus work with your `Player` class, which you may modify at leisure.

# Features

## General Features
This section introduces the different features of the Game Manager for any type of game.

For type-specific features, see:
- [Multiplayer Game Features](#multiplayer-game-features)
- [Solo Game Features](#solo-game-features)
- [Optimization Game Features](#optimization-game-features)
>Note that an Optimization game *is* a Solo game with more settings

### Players

You can get your `Player` instances from the Game Manager. They allow you to interact with the players' AIs.

You can use the `getNicknameToken()` and `getAvatarToken()` that will be converted into the real corresponding information by the viewer.

To allow the AIs to play:
- You must send input data to your players with `sendInputLine()`. 
- Execute one turn of their code with `execute()`
- Finally, get their output with `getOutputs()` and use them in your game.

**Timeout**
If a player times out (send an invalid value, takes too long to execute ...) you will be sent a `TimeoutException`. You can use this to end the game or deactivate the player, for example.

### Maximum number of turns

You can set the maximum number of turns before the game ends (even if there are still active players). If you don't set this paramter, the game will end within **400** turns.

```java
gameManager.setMaxTurns(200);
```

>This parameter is an important performance setting. See the [Guidelines](guidelines/guidelines-1-general.md) for more details.

### Turn maximum time

You can set the maximum time allowed to a Player to execute their code for a turn. If you don't set this paramter, the players will have **50**ms to execute.

```java
gameManager.setTurnMaxTime(45);
```

>This parameter is an important performance setting. See the [Guidelines](guidelines/guidelines-1-general.md) for more details.

### Tooltips

Tooltips will appear on the replay of the current game. They are usually short and describe when a player loses or timeout.

```java
gameManager.addTooltip(player, player.getNicknameToken() + " timeout!");
```

### Game Summary

You can add texts that will be displayed to all players in the game summary, under the viewer.

```java
gameManager.addToGameSummary(String.format("%s pushed %s!", player1.getNicknameToken(), player2.getNicknameToken()));
```

## Multiplayer Game Features <a name="multiplayer-game-features"></a>

`TODO`

## Solo Game Features <a name="solo-game-features"></a>

`TODO`

### Optimization Game Features <a name="optimization-game-features"></a>

`TODO`
