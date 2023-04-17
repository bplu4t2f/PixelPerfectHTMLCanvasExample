# PixelPerfectHTMLCanvasExample
Because getting the physical pixel size of a canvas for rendering is still difficult in 2023

This works for WebGL contexts too.

# NOTE: Multiplying by devicePixelRatio is WRONG

tl;dr the specs don't tell you how to round. You won't be able to make it display correctly on all devices and DPI settings because of subpixel accuracy.

SEE ALSO:

https://github.com/KhronosGroup/WebGL/issues/2460

https://github.com/w3c/csswg-drafts/issues/3554

... and countless stackoverflow questions etc.
