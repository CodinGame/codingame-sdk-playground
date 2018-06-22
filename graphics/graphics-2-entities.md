# Graphical Entities

Every sprite, shape, text, etc are entities displayable in the viewer. They implement diverse methods to be manipulated:

- Position
- Rotation
- Anchor
- Scale
- Opacity
- Z index

# Examples

## Creating a circle
```java
// Creates a green circle
Circle circle = entityModule.createCircle()
			.setRadius(50)
			.setLineWidth(0)
			.setFillColor(0x00FF00);
```
## Moving a circle
```java
MyPlayer player = gameManager.getPlayer(turn % 2);
circle
	.setX(player.getX())
	.setY(player.getY());
```

## Creating a group of sprites
```java
Sprite planet1 = entityManager.createSprite()
				.setImage("planet")
				.setX(-20);
Sprite planet2 = entityManager.createSprite()
				.setImage("planet")
				.setX(30);
				.setY(-10);
Sprite planet3 = entityManager.createSprite()
				.setImage("planet")
				.setY(20);

// The planets are around the point (960,540).
Group system = entityManager.createGroup(planet1, planet2, planet3)
					.setX(960)
					.setY(540);
```

## Spinning a group of spinning sprites around a point
```java
	planet1.setRotation(planet1.getRotation() - Math.PI / 4);
	planet2.setRotation(planet2.getRotation() + Math.PI);
	planet3.setRotation(planet3.getRotation() + Math.PI / 16);
	
	system.setRotation(system.getRotation() + Math.PI / 2);
```