# Configuring your game

## General configuration

This section introduces configuration for any type of game.

For type-specific configuration, see:
- [Multiplayer Game Configuration](#multiplayer-game-configuration)
- [Solo Game Configuration](#solo-game-configuration)
- [Optimization Game Configuration](#optimization-game-configuration) 
>Note that an Optimization game *is* a Solo game with more settings

### pom.xml configuration

In order to use the CodinGame SDK, you need to correctly configure the file `pom.xml`.

A good start would be to check the [game skeleton' pom.xml](https://github.com/CodinGame/game-skeleton/blob/master/pom.xml). It contains all you need to start your project.

Think of updating the `artifactId` value with the name of your game in case you want to create several games.

### Config.ini

This is the main configuration file. It must be located in the `config` folder at the root of your project.

Example of `config.ini`.
```
title=Game Example
type=multi
min_players=2
max_players=2
```
- **title**: The title of the question
- **type**: The type of the game, must be either `multi`, `solo` or `opti`
- **min_players**: The minimum number of players to play the game. Must be 1 for Solo and Optimization games, up to 8 for Multiplayer games.
- **max_players**: The maximum number of players to play the game. Must be 1 for Solo and Optimization games, up to 8 for Multiplayer games. Of course, you cannot have max_players &lt; min_players.

>This configuration can be done through a form when exporting the game, if the file `config.ini` is missing or misconfigured.

### Code Stub

You may add to the config/ folder a text file named `stub.txt`. If the contents of this file is a syntaxically valid **CodinGame Stub Generator** input, the IDE will be prefilled with input/output code.

See [Stub Generator Syntax](https://github.com/CodinGame/codingame-game-engine/blob/master/stubGeneratorSyntax.md) for details.

### Loading assets

Assets are expected to be placed in the `src/main/resources/view/assets` folder of your game's project.

You can then use the images in the texture cache with the [Graphic Entity Module](../modules/entities/):
```java
entityManager.createSprite.setImage("background.png");
```

### Other resources

You might need to upload other resources such as text files, csv or whatever your creativity will bring you to create.

Once you upload your game on [CodinGame](www.codingame.com), your project will not have the same file system as the one you use on your computer. In order to read your files, you must place them in the `src/main/resources` folder and use Java's `ClassLoader`:

```java
InputStream in = ClassLoader.getSystemResourceAsStream("my_awesome_file.txt");
```

### Levels & Leagues

You have the possibility to create several levels (also named leagues). A new level allows you to set a different configuration and different rules (you can get the league level in the Referee with the [Game Manager](core-concepts/core-4-game-manager.md)).

There is a difference between multiplayer and solo game levels:
- In a **multiplayer** game, your levels become leagues. The players will need to beat your Boss in the leaderboard to access the next league.
- In a **solo** game, they are several questions. Players can switch between the different questions as they wish to.

To create new levels, you need to make new folders named `level<number>` in the `config` directory. Each level can be configured like the `config` directory, which allow you to have different statements, stubs, titles, etc.

Please note that you **cannot** have two different types of game in your levels. *Optimization* games are an exception: you can have several levels as long as you have a unique *opti* level (the others must be *solo* games).

### Viewer configuration <a name="viewer-configuration"></a>

You can change the default player colors to whatever you wish by adding an export to `config.js`:
```javascript
export const playerColors = [
      '#ff1d5c', // radical red
      '#22a1e4', // curious blue
      '#ff8f16', // west side orange
      '#6ac371', // mantis green
      '#9975e2', // medium purple
      '#3ac5ca', // scooter blue
      '#de6ddf', // lavender pink
      '#ff0000'  // solid red
    ];
```
The colors must respect the above format.

You can change the identifier of your game for the IDE's cache by adding an export to `config.js`:
```javascript
export const gameName = 'MyGame';
```
This doesn't have any effect on user experience yet.

### Statement

Place a file named `statement_en.html` in the `config/` directory and it will be used for as the statement of your game.

For a game with multiple leagues, you may place a file named `statement_en.html.tpl` in the `config/` directory and it will be used as a basis for the statement of each league when you click the export button.

Within the `.tpl` file, you may place special comment blocks to indicate whether a block of html should be included for any specified league.

Optionally, you can tranlate your statements in French using `statement_fr.html` files.

#### Example

This `statement_en.html.tpl`:
```html
<!-- LEAGUES level1 level2 level3 -->
<div>
  <p> Always included </p>
  <!-- BEGIN level1 -->
    <p> Included in first league </p>
  <!-- END -->
  <!-- BEGIN level2 -->
    <p> Included in second league </p>
  <!-- END -->
  <!-- BEGIN level1 level2 -->
    <p> Included both first and second league </p>
  <!-- END -->
</div>
```

Will result in these three statements for a three-league game:

First league in `config/level1/statement_en.html`:
```html
<div>
  <p> Always included </p>
    <p> Included in first league </p>
    <p> Included both first and second league </p>
</div>
```

Second league in `config/level2/statement_en.html`:
```html
<div>
  <p> Always included </p>
    <p> Included in second league </p>
    <p> Included both first and second league </p>
</div>
```

Third league in `config/level3/statement_en.html`:
```html
<div>
  <p> Always included </p>
</div>
```


### Activating game logs

You can view the data that the Referee and the Players send each other by editing the built-in logger's settings.
To do this, open `log4j2.properties` in the root of your project and replace ```rootLogger.level = warn``` with ```rootLogger.level = info```.
Additionally, if you would like to see the output of the different modules, you can use:
`rootLogger.level = trace`.


# Multiplayer Game Configuration <a name="multiplayer-game-configuration"></a>


### Welcome popup

Welcome popups can be used in **Multiplayer** games with multiple leagues. They will be displayed when a player is promoted to the next league.

Place a file named `welcome_en.html` in every `config/level<number>` directory you want the popup to be used in.

You can display images using `<img src="your_image.jpg"/>`. The image files must be located in the same directory.

Optionally, you can tranlate your popups in French using `welcome_fr.html` files.

#### Example

`TODO`


# Solo Game Configuration <a name="solo-game-configuration"></a>


### Test case file <a name="test-case-file"></a>

You will need to create test case files to run your **Solo** game.

Your test cases must be named `test<number>.json` and placed in the `config` directory. Their `<number>` determine the order they will be listed in the CodinGame IDE. Here is an example:

`test1.json`
```json
{
	"title": {
		"2": "One path",
		"1": "Un seul chemin"
	},
	"testIn": ".o...\\n.ooo.\\n...o.",
	"isTest": "true",
	"isValidator": "false"
}
```
- **title:**
    - **2:** English title, this parameter is mandatory.
    - **1:** French title, optional.
- **testIn:** The content of your test case. It can contain multiple lines separated with `\\n`.
- **isTest:** If true, this test will be visible and used as a regular test case.
- **isValidator:** If true, this test will be use to validate the player's code. You can use this to avoid hardcoded solutions.


## Optimization Game Configuration <a name="optimization-game-configuration"></a>


**Optimization** games are **Solo** games with additional configuration.

First, you will need to add a `criteria` and a `sorting_order` property in `config.ini`.
- The `criteria` corresponds to the label of the player's score. For example, it can be `Points`, `Fuel` or `Distance`.
- The `sorting_order` determines the ranking order. Its value must be either `asc` or `desc`. If the player whose Fuel quantity is higher should be first, choose `asc`. If the goal is to win the game in the shortest time, choose `desc`.

You can also choose to translate your criteria in French by using the optional properties `criteria_en` and `criteria_fr`.

>This configuration can be done through a form when exporting the game, if the file `config.ini` is missing or misconfigured.

Once this configuration is done, you will need to send your player's score with the [Game Manager](core-3-game-manager.md#optimization-game-features)