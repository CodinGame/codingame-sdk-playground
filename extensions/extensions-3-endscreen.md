# EndScreenModule

Requires game engine version 1.35 or higher.

Can be used to display the ranking of a multiplayer game with any additional info you choose. The ranking will appear at the very end of the replay.

To guarantee the correct ranking, you must set this module's score property in your Referee's `onEnd()` method.

### Example
`Referee.java`
```java
  @Override
  public void onEnd() {
      endScreenModule.setScores(gameManager.getPlayers().stream().mapToInt(p -> p.getScore()).toArray());
  }
```
