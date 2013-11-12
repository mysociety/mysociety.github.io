---
layout: page
title: Retina Images
---

### Overview

An increasing number of devices, especially mobile devices, are now using high-
DPI displays (known popularly as [Retina
displays](http://en.wikipedia.org/wiki/Retina_Display) due to Apple's usage of
the term in marketing). They are generally characterised by operating at a
higher pixel density than the average human eye can discern at an average
viewing distance, and have particular design considerations.

The most important thing to realise when designing for a Retina display is that
the physical pixels in the display do not always correspond to pixels in terms
of design. For Apple devices the ratio is 2/1, in that two physical pixels are
used to display one virtual pixel's worth of distance, meaning that images and
text are rendered at twice the resolution but in the same amount of space. The
ratio varies across other devices, but generally speaking mySociety considers
anything above a ratio of 1.3/1 to be "high resolution" and a potential
candidate for Retina image assets.

### Designing for Retina

The simplest way to design for Retina devices is to ensure that source artwork
is available at twice the size of the space it is expected to occupy. For
example, an image which is expected to fill a 200px by 50px space should be
400px by 100px, and its size on the page specified using CSS.

Generally speaking the use of vector-based artwork is preferable as this can be
rescaled freely as necessary, as well as exported as native vector formats for
compatible browsers.

### When to use Retina

Retina artwork should be used wherever a change in resolution will be
particularly obvious, such as logos or other artwork where there are clean lines
or sharp changes in colour. Generally speaking photographic assets are safe in
lower resolutions, but they should be considered for Retina where they are
expected to be a focus of attention.

### Methods for including Retina

There are several ways to include Retina-ready artwork, and which is most
appropriate will vary based factors such as target devices and the type of
image.

#### Use high-resolution artwork by default

For cases where the size difference between non-Retina and Retina assets is
minimal (this is often the case in logo images) you should consider simply
serving the high-resolution artwork to all clients and specify its on-screen
dimensions explicitly. This saves subsequent HTTP requests over image-swapping
solutions and avoids a flash of low-resolution content.

#### Use SVG artwork

In many cases artwork can be replaced with an SVG vector version, which will
render in the highest possible resolution as well as often being smaller in
terms of file size.

It is worth noting that although [all modern browsers support
SVG](http://caniuse.com/#search=svg), IE 8 has no support and still has a
significant install base. You may wish to consider plugins such as
[SVGeezy](http://benhowdle.im/svgeezy/) to exchange SVG for a raster image
format, although this does mean that browsers with neither SVG or JavaScript
will see no content.

#### Use resolution-aware CSS

CSS media queries can determine the pixel density of the display and load the
appropriate asset accordingly. The following CSS is an example which replaces
`image.png` with `image@2x.png` on Retina displays.

{% highlight css %}
.class {
  background-image: url(image.png);
  @media (min--moz-device-pixel-ratio: 1.3),
    (-o-min-device-pixel-ratio: 2.6/2),
    (-webkit-min-device-pixel-ratio: 1.3),
    (min-device-pixel-ratio: 1.3),
    (min-resolution: 1.3dppx) {
    background-image: url(image@2x.png);
  }
}

{% endhighlight %}

#### Use an image-swapping plugin

Javascript plugins exist which can detect when a page is viewed on a Retina
display and swap image assets for higher quality ones. This does however require
JavaScript, create a second HTTP request, usually involve the download of both
original and high-resolution assets, and often creates a flash of low-
resolution content. It should therefore be used with care.
