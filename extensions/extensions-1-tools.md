# Extend the CodinGame SDK

Although the CodinGame SDK already includes the [GraphicEntityModule](graphics-1-introduction.md), you can add your own Modules to your game.

This section presents a few modules that you can add to your game. You can find their source code on Github: [https://github.com/CodinGame/codingame-sdk-modules](https://github.com/CodinGame/codingame-sdk-modules)

## Drawer
### Reference API

Three javascript exports are available for your Modules that interact with the viewer.

#### constants.js
Contains general purpose constants.

```javascript
// The size of the drawspace on the viewer's canvas.
const WIDTH = 1920;
const HEIGHT = 1080;
```

#### utils.js
Contains general purpose utility functions.

```java
/**
 * return word padded to width with char characters
 */
function paddingString(word, width, char)

/**
 * Returns a random integer from [0;a[ if b is null.
 * Returns a random integer from [a;b[ if b is not null.
 */
function randInt(a, b=null)

/**
 * Gets the number from [a;b] at percentage u
 */
function lerp(a, b, u)

/**
 * Gets the percentage position in [a;b] of number v
 */
function unlerpUnclamped(a, b, v)

/**
 * Gets the angle between start & end at percentage amount
 */
function lerpAngle(start, end, amount, maxDelta)

/**
 * Gets the x,y coordinate between 2 points at percentage p
 */
function lerpPosition(from, to, p)

/**
 * Gets a color which is the RGB interpolation between start and end by percentage amount
 */
function lerpColor(start, end, amount)
/**
 * Gets the percentage position in [a;b] of number v, clamped into [0;1]
 */
function unlerp(a, b, v)

/**
 * calls self.push on all elements of arr
 */
function pushAll(self, arr)

/**
 * Returns the scale needed to fit (srcWidth, srcHeight) inside (maxWidth, maxHeight)
 */
function fitAspectRatio(srcWidth, srcHeight, maxWidth, maxHeight, padding)
```
#### transitions.js
Contains interpolation functions that map a [0;1] input to a [0;1] output.

```java
/**
 * Traces a bell shaped curve
 */
function bell(x)

/**
 * The output value quickly increseas and wobbles around 1 a little before settling.
 */
function elastic(t)

/**
 * The output value slowly increases and decreases
 */
function ease(t)
```

