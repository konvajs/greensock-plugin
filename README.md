# GreenSock plugin for Konva.js

This is forked plugin from [KineticJS GreenSock Plugin](http://greensock.com/docs/#/HTML5/Plugins/KineticPlugin/)

Demo: [http://konvajs.github.io/docs/tweens/Complex_Tweening.html](http://konvajs.github.io/docs/tweens/Complex_Tweening.html)

Enables `TweenLite` and `TweenMax` to animate properties of `Konva` objects (see [http://konvajs.github.io/](http://konvajs.github.io/)) in a much easier and high-performance manner than doing so directly through the Konva API. The native Konva API gives you very limited ability to build and control sequences or animate along Bezier paths or do directional rotation or all sorts of things that GSAP delivers in spades. Using GSAP with this the KonvaPlugin gives you a far more robust toolset for animating in KonvaJS.

## Benefits of using the KonvaPlugin

It automatically manages the `draw()` calls for the appropriate layers, optimizing performance (only calling draw() once per frame per layer regardless of how many tweens or objects).
It automatically figures out how to tween color-related values which you can define in pretty much any format, like `#F00`, `#FF0000`, `rgb(255,0,0)`, `"red"`, or `"hsl(20, 50%, 70%)"`, or even `rgba()` and `hsla()`.
It integrates with `BezierPlugin` so that you can animate along Bezier paths, including the autoRotate feature.
It integrates with `DirectionalRotationPlugin` so that you can append `"_cw"` (clockwise), `"_ccw"` (counter-clockwise) or `"_short"` (whichever is shortest) to your rotational values and get the behavior you want.

It integrates with `RoundPropsPlugin` to [optionally] round values to the closest integer as they're applied during the tween. You can do this on a per-property basis.
Of course you could animate things without the plugin and your code could look like this:

```javascript
// without the plugin, your code is longer and more clumsy like this:
TweenLite.to(star, 5, {x:500, y:100, innerRadius:15, rotation:360, ease:Power4.easeOut, onUpdate:drawLayer});
function drawLayer() {
    layer.draw();
}
```

But with the plugin, things are simplified to this:

```javascript
// with the plugin, it's more intuitive and concise:
TweenLite.to(star, 5, {konva:{x:500, y:100, innerRadius:15, rotation:360}, ease:Power4.easeOut});
```

Plus, without the plugin it's more difficult to tween colors or do Bezier tweening or directional rotation, rounding property values, etc.

*Note: a common mistake is to forget to wrap KonvaJS-related properties in a "konva:{}" object which is essential for helping TweenLite/Max understand your intent.*

You can tween virtually any of the properties that you would normally set using the standard `Konva` API.

If you'd like to manage the `Konva` draw() calls yourself instead of having the plugin do it for you, simply pass autoDraw:false into the Konva object, like `TweenLite.to(star, 5, {konva:{autoDraw:false, x:200, y:500}});`
