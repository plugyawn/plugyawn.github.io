---
layout: page
title: Pineapple NES Emulator
description: A C++ based emulator for the CPU of the Nintendo Entertainment System that ran on the Ricoh 2A03, with limited PPU capabilities.
img: https://user-images.githubusercontent.com/76529011/194703131-31f83e29-e1cc-4877-ab12-e358750ab697.png
importance: 3
category: work
---

[![forthebadge made-with-python](https://forthebadge.com/images/badges/built-with-love.svg)](https://www.python.org/)
[![forthebadge](https://forthebadge.com/images/badges/made-with-c-plus-plus.svg)](https://forthebadge.com)

<div align = center>
<a href = "github.com/plugyawn"><img width="400px" src= "https://user-images.githubusercontent.com/76529011/194703131-31f83e29-e1cc-4877-ab12-e358750ab697.png"></a>
</div>

## ```pineapple-EMU``` is a test ```MOS 6502``` processor emulator for NES ROMs.

We wanted to play Mario on the NES but couldn't, so we wrote an emulator for the NES on our own -- or tried to, anyway. This is an abridged version of ```OneLoneCoder```'s tutorial on a complete NES emulation, implemented and tested for the ```MOS 6502``` chip aboard the original NES.

The snapshot below captures our emulator using the ```OLCPixelEngine``` to blit a live-feed of the emulation process.

![Our NES Emulator](https://user-images.githubusercontent.com/76529011/194702025-4a96385f-1cfb-4b26-83f1-acc92824bba5.png)

## Aside: A little note from the devs.

Note that While we have a functioning Picture Processing Unit too, we were not able (yet) to connect the PPU
to the cartridge, which is how sprites are blitted onto the screen.
 
In essence, each peripheral of the NES is to be thought of as an object connected to the Bus, which
as most online resources rightly call, is the heart of the architecture of the NES.

We have emulated the processor (the ’6502), the PPU (the ’2C02), as well as the general functioning
of the cartridges and the different kinds of RAM accessed by the bus during the working of the NES.
Right now, our emulator can output to some degree of accuracy the functioning of the processor when
given a .NES file, which is essentially a dump from a physical NES cartridge. We have tested it out with
the NES testing suite, and our results corroborate well with the sources that we referred to. We believe our
emulation is acccurate.

Paired with a disassembler function, our project is a good way to look at actual programs from the
1980s and see how they were written and structured.

The project would not have been possible without OneLoneCoder’s PixelGameEngine, which is an
open-source tool that we used to display our emulated data on the screen.




<!-- 
Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %} -->
