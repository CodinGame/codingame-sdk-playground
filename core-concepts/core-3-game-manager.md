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

### Example for a **Multiplayer** game:
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

### Example for a **Solo** game:
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

`TODO`

## Multiplayer Game Features <a name="multiplayer-game-features"></a>

`TODO`

## Solo Game Features <a name="solo-game-features"></a>

`TODO`

### Optimization Game Features <a name="optimization-game-features"></a>

`TODO`
