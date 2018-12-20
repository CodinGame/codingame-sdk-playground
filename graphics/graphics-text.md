# Displaying text

The Graphic Entity Module includes two different classes to display text, here's how they work.

## Text

The basic class to display text, it will be displayed as a label on you screen.

```java
graphicEntityModule.createText("Hello World")
    .setFontFamily("Lato")
    .setStrokeThickness(5) // Adding an outline
    .setStrokeColor(0xffffff) // a white outline
    .setFontSize(50)
    .setFillColor(0x000000); // Setting the text color to black
```
You'll see in this example that you have a lot of options to manipulate the text, but this class has one downside :
the font is not garanteed to be the good one, since the client browser has to provide it.
So it doesn't support a lot of fonts and your font will probably be replaced by the default one of the browser.

## BitmapText

This class is used to display text using a bitmap font in your assets folder.
The downside is that you have less options to manipulate it,
but this is compensated by the fact that you can use any font you want.

```java
graphicEntityModule.createBitmapText()
    .setText("Hello World")
    .setFontFamily("myCustomFont")
    // Assuming that you have a working 'myCustomFont.fnt' and 'myCustomFont.png' in your assets folder
    .setFontSize(50)
    .setTint(0xff0000); // Tinting it in red
```

Extra tips :
- A little help to turn fonts into bitmap fonts : http://kvazars.com/littera/
- You can put your font in a sub folder of the assets repository whithout modifying any code