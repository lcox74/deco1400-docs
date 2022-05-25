I came across a cool graphics library called Netpbm, it's a collection of open-source graphics protocls that are very very simple to implement. So simple that you can make images by hand. The only issue is that not many image viewers support the collection, though if you use GIMP you'll be able to view it just fine.

Out of the collection the one I want to look at in particular is the PPM protocol which allows us to create RGB images pixel by pixel. There are a couple things that are required to do this:

1. The "Magic Number"; in our case its `P3` meaning **PPM** and **ASCII**
2. The Width and Height; lets say we want a 3x2 pixel image then that
    would be `3 2`
3. The Max Value; lets say we want `0-255` for each Red, Green and Blue
value, then it would be  `255`
4. The Data; These can be on a single line or across multiple, but whats
    important to remember is that you must do the value for each RGB 
for each pixel.

Lets bring it together to see how is would look in a file. Lets call this file
 `example.ppm` :

```bash
P3
3 2
255
255 0 0      # Red Pixel
0 255 0      # Green Pixel
0 0 255      # Blue Pixel
255 255 0    # Yellow Pixel
255 255 255  # White Pixel
0 0 0        # Black Pixel
```

> **Note:** You can use the `#` symbol to add comments

Using this example PPM file, we can open it in GIMP and get the following result. Though you will have to zoom in alot to view it properly.

![Example Image Created](https://github.com/lcox74/Netpbm/raw/main/res/simpleexample.PNG)

The wikipeadia page on [Netpbm](https://en.wikipedia.org/wiki/Netpbm) is quite detailed and explains the other protocols such as PBM and PGM which are black and white as well as grey scale versions respectively of PPM. I've created a C header file which allows you to easily create high resolution images in all of these protocols, this is avaliable at my [lcox74/Netpbm](https://github.com/lcox74/Netpbm) repo on github.
