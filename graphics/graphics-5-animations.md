# Animations

Once you have a set of images, you can animated them with a `SpriteAnimation`.

### Example

```java
graphicEntityModule.createSpriteAnimation()
    .setImages(heroSprites)
    .setX(hero.getX())
    .setY(hero.getY())
    .setDuration(2000)
    .setLoop(true)
    .setStarted(true);
```
- `setImages(heroSprites)`: set a `String` array containing the filenames of the sprites.
- `setX(hero.getX())`, `setY(hero.getY())`: set the position.
- `setDuration(2000)`: set how long the whole animation takes to be played (in milliseconds).
- `setLoop(true)`: if true, the animation will repeat. Otherwise, it will be played only once and the last sprite will remain displayed.
- `setStarted(true)`: if true, the animation plays. Otherwise, none of the sprites are displayed.
