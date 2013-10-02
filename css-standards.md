---
layout: page
title: CSS Guidelines
---

CSS is constantly changing, these are some summarised notes on what we consider to be *The Right Thing* at the moment. Obviously this applies mostly when starting brand new projects. When working on an existing project, use whatever practices that project uses already, for consistency.

### Assumed

Things this document assumes you already are trying to achieve with your CSS are:

* As cross-browser as the project requires (this almost always means IE something < 9)
* Progressive enhancement
* Readable code (HTML and CSS)
* Minimal hacks
* Efficient selectors
* Modular and re-usable styles
* Responsive design where necessary

Therefore, the following points cover specifics in *how* to achieve those goals.

### What do you need?

The first actual step is to decide if you need to 'support' IE6 and IE7. What is the output of the project, who will be viewing it, will it need full IE6 support, or will getting a viewable but looks-quite-different version be okay? That is a project-specific decision to be made based upon user need.

Secondly, decide whether it needs to be responsive, and if there are any other design/content constraints that will affect your CSS.

#### I don't care about IE6/7

A basic start without a framework (not inventing your own, just not having one) is straightforward, especially if you don't mind about IE6/7:

1. Use [normalize.css](http://necolas.github.com/normalize.css/).

2. Set `* { box-sizing: border-box; }` (and [vendor-sepecific variants](http://paulirish.com/2012/box-sizing-border-box-ftw/)).

3. If you don't worry about IE6/7, you now have `display: table`, `position: fixed`, widths include their padding/border, and not really many browser bugs to worry about. Hooray!

#### I need to care about old IE

1. There is a version of normalise.css for old IE, use that.
2. Use conditional comments, or conditional body classes, to target specific IE issues.
3. You can use SASS mixins to output your ie-conditional stylesheets and then include them with [conditional comments](http://jakearchibald.github.com/sass-ie/).
4. Don't be tempted by [box-sizing-polyfill](https://github.com/Schepp/box-sizing-polyfill) - it has [issues](https://github.com/Schepp/box-sizing-polyfill/issues/23) when you need it most.

#### I need responsive and old IE

* IE < 9 does not support media queries, so can't do responsive design in that sense, there are various options.
* IE 6-8 support for media query - http://jakearchibald.github.com/sass-ie/ or http://adactio.com/journal/4494/ (the latter is used on FixMyStreet);
* Also see - http://adactio.com/journal/5964/ and follow-up http://adactio.com/journal/5969/ as again to be considering what you should do about old-IE.

### Grid Systems

A grid system is generally a *Good Idea*, but there is not one grid system to rule them all. Especially if you are working with a large variation in screen sizes. They [don't have to be complicated](http://css-tricks.com/dont-overthink-it-grids/) (at least when working with IE8+, see more about that below).

The CSS-tricks article above is nice, (as is [inuit.css](http://inuitcss.com/) which does similar things) but they mix presentation with content by adding classes like col-1-3 to the HTML, and you can end up with lots of CSS classes to define your grid at different screen widths (if it's col-1-3 at one size then col-full-width at another, etc). Furthermore, what happens when you decide that div should be full-width everywhere?

To improve upon this, using SASS mixins to create the same effect would generally be the preference for the Right Thing, similar to the [BBC News way of doing things](http://blog.responsivenews.co.uk/blog/2011/11/08/responsive-css-that-scales/).

An example that takes the CSS-tricks column above and does it using SASS is available at [amperedesign.com/blog/more-responsive-grid-systems](http://amperedesign.com/blog/more-responsive-grid-systems/). There they just use `@extend` to inherit from the right presentational class at different widths (in media queries), but run into some problems with SASS limitations that make things a bit hairy with media queries. To take that one step further, and avoid the media queries problems, defining your grid classes as mixins instead allows them to be used anywhere with `@include`.

What this means is defining proportional mixins in your CSS (like, half-the-screen, third.., etc) and semantic classes in your html (like, results-list, hero, etc), then using SASS' `@include` to join them up, ideally joining them up differently at different widths, eg:

{% highlight sass %}

// Layout mixins
@mixin half-width() {
    display:inline;
    float:left;
    width:50%;
}

...

// Application of layout to content

.my-content {

    // Mobile first, two columns
    @include half-width();

    // Responsive for tablets or thereabouts
    @media screen and (min-width: 40em) {
        // Three columns
        @include third-width();
    }

    // Responsive for desktop or thereabouts
    @media screen and (min-width: 60em) {
        // Four columns
        @include quarter-width();
    }
}

{% endhighlight %}

That way, you can specify as little or as much grid system as you like or don't in your CSS, and have it work at multiple breakpoints without having to clutter up or confuse the HTML.

#### Grid Systems and Old IE

The above, and most of the available grid systems make use of the box-sizing tricks mentioned to make it possible to easily define grids with padding or margins, which is kind of necessary to give nice gutters to your grids. IE6/7 doesn't support this, and there isn't a good way to make it do so. In order to achieve something similar you essentially have two options:

1. Don't use the things that IE6/7 can't handle, ie: don't add padding or margins to your grid elements, so that they don't need to include them inside their nice widths.

   If it suits your design then this is very simple, you don't really need box-sizing, but you lose gutters. The easiest way to get these back is to add new inner html elements, which aren't so semantic, and it's kind of annoying to clutter up the HTML for everyone just to suit Old IE. Therefore, use this method if your design doesn't need gutters.

2. Use the box-sizing grids as normal, ignoring IE's issues, and then manually correct it using conditionally added stylesheets.

   This could be a chore, but if you're using sass mixins for your layout, and sass-ie to give Old IE a desktop version of the site at all times anyway, certain things can help.

   Firstly, your layout mixins can set a fixed width for your grid container in Old IE, which gives you a baseline to work from. Then you can get your trusty calculator out and set specific adjusted widths for your columns (adjusted for the fact that IE7 will include your margins/padding). Secondly, if you're using sass-ie, you have the helpful `old-ie()` mixin in which to declare these rules, so that they sit right next to your proper styles, for easy reference, and yet get output into a separate stylesheet so you don't need to use `*selector` hacks. You'll probably need to expand upon this a bit to get specific versions for IE7 (and IE6 if all hope has foresaken you), as currently it is just IE < 9.

### Syntax

SMACSS, OO-CSS and BEM style CSS syntax can all be good, use whichever you think suits the project and stick to it.

### Frameworks

Notes on specific frameworks and what they're good for.

#### [Foundation](http://foundation.zurb.com)

The Foundation framework provides a good basic grid, which is true mobile-first (ie the design renders cleanly on mobile unless you apply classes telling it to behave otherwise). It has good support for varying screen sizes, and a selection of optional JavaScript components to address common requirements around element sizing, modal dialogues, Retina image swapping etc.

Foundation provides fewer UI elements out of the box than some other frameworks. This might be exactly what you're looking for if you want to fine-tune the design yourself, but be aware you'll need to provide more styling yourself than you may be used to with a framework like Bootstrap.

The [gem](http://foundation.zurb.com/docs/sass.html) will bootstrap a site, including static assets and Compass configuration, which might be useful when getting started.

#### [Bootstrap](http://getbootstrap.com/)

**Bootstrap 3 does not support IE < 8. Use with caution.**

**Bootstrap uses LESS instead of SASS.** Be aware of this if you're planning on compiling assets or making anything more than simple changes.

Bootstrap certainly has its uses in quick prototyping, giving consistent look, and so on. It makes things look nice, quickly, and clients tend to find it inoffensive at worst.

When using it for layout, especially a responsive layout, beware that it doesn't do *anything* for any pixel width below 768px, it just linearises, when I would say any good responsive design can easily potentially have two columns at the classic 320px if that makes sense to do (see e.g. BBC News). All bootstrap does above 768 is give you 12 classes with set percentage columns.

You can certainly consider using Bootstrap so as not to worry about button design or whatever, or have some nice effects already written for you; but I'd worry about relying on things, rather than picking and using what is actually necessary for the project.

### Summary

So in summary:

* Start from the assumptions above
* Use normalise.css
* For IE8+ use the box-sizing rule to make box sizing more sane.
* Use SASS to make the CSS more modular, and help with media queries on old IE.
* Define proportional grid elements as mixins and then include them in semantic classes.
* Use whatever syntax model (SMACSS, OO-CSS, BEM, etc) makes the most sense to you, or don't use one, but be consistent and document your choices.
* Decide upon the level of responsiveness that you need, and define your own grid system to suit this.
* Use frameworks where they're appropriate for the project, but consider the debt of their constraints, and weight of what you won't use.
* Likewise, use fancy new CSS features when you can, but always have a fallback for less capable browsers
* Document your decisions