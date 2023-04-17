# PixelPerfectHTMLCanvasExample
Because getting the physical pixel size of a canvas for rendering is still difficult in 2023

This works for WebGL contexts too.

# NOTE: Multiplying by devicePixelRatio is WRONG

tl;dr the specs don't tell you how to round. You won't be able to make it display correctly on all devices and DPI settings because of subpixel accuracy. There were plans to fix it by adding new properties for the resolved bounds of things but w3c ditched them. The problem gets worse if the canvas is percent-scaled by CSS or something like that.

SEE ALSO:

https://github.com/KhronosGroup/WebGL/issues/2460

https://github.com/w3c/csswg-drafts/issues/3554

... and countless stackoverflow questions etc.

# The approach presented uses ResizeObserver with devicePixelContentBoxSize

This feature is relatively new and probably won't work in out-of-date browsers.

```
let observer = new ResizeObserver(entries =>
{
    let entry = entries.find(entry => entry.target == canvas);
    let w = entry.devicePixelContentBoxSize[0].inlineSize;
    let h = entry.devicePixelContentBoxSize[0].blockSize;

    canvas.width = w;
    canvas.height = h;

    // ...
});
observer.observe(canvas, { box: ["device-pixel-content-box"] });
```

Unfortunately this isn't synchronous.
