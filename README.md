# Just Another Parallax
Smooth parallax scrolling effect for background images using ***CSS transforms*** with graceful degradation for old browsers. Parallax plugin with ***NO dependencies***. jQuery supported. ***Youtube*** and ***Vimeo*** parallax supported.

## [Demo](http://free.nkdev.info/jarallax/)

## Tested Browsers
* IE9+
* Safari 5.1.7+
* Opera 12+
* Latest browsers on Mac and Windows (Chrome, Firefox, Safari, IE, Edge)
* Latest Chrome on Android
* Latest Safari on iOs

## Getting Started
Include Jarallax plugin. Also include jQuery before jarallax if you want to use it.
```html
<!-- Jarallax -->
<script src='jarallax/jarallax.js'></script>

<!-- Include it if you want to use Video parallax -->
<script src='jarallax/jarallax-video.js'></script>
```

## Set up your HTML
```html
<!-- Image Parallax -->
<div class='jarallax' style='background-image: url(<background_image_url_here>)'>
    Your content here...
</div>

<!-- Video Parallax -->
<div class='jarallax' data-jarallax-video='https://www.youtube.com/watch?v=ab0TSkLe-E0'>
    Your content here...
</div>
```

### Additional styles
Mandatory requirement for plugin works properly - the selected item should be NOT position: static (for ex. relative).

This styles need to add relative position and correct background image position before Jarallax initialize end.
```css
.jarallax {
    position: relative;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
}
```

## Call the plugin

### A. Data attribute way
```html
<div data-jarallax='{"speed": 0.2}' class='jarallax' style='background-image: url(<background_image_url_here>)'>
    Your content here...
</div>
```

### B. JavaScript way
```javascript
jarallax(document.querySelectorAll('.jarallax'), {
    speed: 0.2
});
```

### C. jQuery way
```javascript
$('.jarallax').jarallax({
    speed: 0.2
});
```

# Options
Options can be passed in data attributes or in object when you initialize jarallax from script.

<table class='table table-bordered table-striped'>
    <thead>
        <tr>
            <th>name</th>
            <th>type</th>
            <th>default</th>
            <th style='width: 60%;'>description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>type</td>
            <td>string</td>
            <td>scroll</td>
            <td>scroll, scale, opacity, scroll-opacity, scale-opacity</td>
        </tr>
        <tr>
            <td>speed</td>
            <td>float</td>
            <td>0.5</td>
            <td>Parallax effect speed. Provide numbers from -1.0 to 2.0</td>
        </tr>
        <tr>
            <td>imgSrc</td>
            <td>path</td>
            <td>null</td>
            <td>Image path. By default used image from background.</td>
        </tr>
        <tr>
            <td>imgWidth</td>
            <td>number</td>
            <td>null</td>
            <td rowspan='2'>You can provide the natural width and natural height of an image to speed up loading.</td>
        </tr>
        <tr>
            <td>imgHeight</td>
            <td>number</td>
            <td>null</td>
        </tr>
        <tr>
            <td>enableTransform</td>
            <td>boolean</td>
            <td>true</td>
            <td>Enable transformations for effect if supported. When option is false - used background-position instead.</td>
        </tr>
        <tr>
            <td>zIndex</td>
            <td>number</td>
            <td>-100</td>
            <td>z-index of parallax container.</td>
        </tr>
        <tr>
            <td>noAndroid</td>
            <td>boolean</td>
            <td>false</td>
            <td>Disable parallax on Android devices.</td>
        </tr>
        <tr>
            <td>noIos</td>
            <td>boolean</td>
            <td>true</td>
            <td>Disable parallax on iOs devices. Jarallax disabled by default on iOs because of strong lags ;(</td>
        </tr>
    </tbody>
</table>

# Events
Evenets used the same way as Options.

<table class='table table-bordered table-striped'>
    <thead>
        <tr>
            <th>name</th>
            <th style='width: 60%;'>description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>onScroll</td>
            <td>Called when parallax working. Use first argument with calculations. More info <a href="#onscroll-event">see below</a>.
            </td>
        </tr>
        <tr>
            <td>onInit</td>
            <td>Called after init end.</td>
        </tr>
        <tr>
            <td>onDestroy</td>
            <td>Called after destroy.</td>
        </tr>
        <tr>
            <td>onCoverImage</td>
            <td>Called after cover image.</td>
        </tr>
    </tbody>
</table>

## onScroll event
```javascript
jarallax(document.querySelectorAll('.jarallax'), {
    onScroll: function(calculations) {
        console.log(calculations);
    }
});
```

Console Result:
```javascript
{
    // parallax section client rect (top, left, width, height)
    rect            : object,

    // see image below for more info
    beforeTop       : float,
    beforeTopEnd    : float,
    afterTop        : float,
    beforeBottom    : float,
    beforeBottomEnd : float,
    afterBottom     : float,

    // percent of visible part of section (from 0 to 1)
    visiblePercent  : float,

    // percent of block position relative to center of viewport from -1 to 1
    fromViewportCenter: float
}
```

Calculations example:
[![On Scroll Calculations](http://a.nkdev.info/jarallax/jarallax-calculations.jpg)](http://a.nkdev.info/jarallax/jarallax-calculations.jpg)


# Methods
<table class='table table-bordered table-striped'>
    <thead>
        <tr>
            <th>name</th>
            <th>result</th>
            <th style='width: 60%;'>description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>destroy</td>
            <td>-</td>
            <td>Destroy Jarallax and set block as it was before plugin init.</td>
        </tr>
        <tr>
            <td>isVisible</td>
            <td>boolean</td>
            <td>Check if parallax block is in viewport.</td>
        </tr>
        <tr>
            <td>clipContainer</td>
            <td>-</td>
            <td>Clip parallax container. Called on window resize and load.</td>
        </tr>
        <tr>
            <td>coverImage</td>
            <td>-</td>
            <td>Fit image in parallax container. Called on window resize and load.</td>
        </tr>
        <tr>
            <td>onScroll</td>
            <td>-</td>
            <td>Calculate parallax image position. Called on window scroll.</td>
        </tr>
    </tbody>
</table>

## Call methods example
### A. JavaScript way
```javascript
jarallax(document.querySelectorAll('.jarallax'), 'destroy');
```

### B. jQuery way
```javascript
$('.jarallax').jarallax('destroy');
```


# No conflict
If you already have global ***jarallax*** variable or ***jQuery.fn.jarallax***, you can rename plugin.
### A. JavaScript way
```javascript
var newJarallax = jarallax.noConflict();
```

### B. jQuery way
```javascript
jQuery.fn.newJarallax = jQuery.fn.jarallax.noConflict();
```


# Real Usage Examples
* [Youplay](http://wp.nkdev.info/youplay)
* [InLove](http://wp.nkdev.info/in-love/home-1/)
* [Flatness](http://wp.nkdev.info/in-love/flatness/)

# Images
All demo images from https://www.pexels.com/

# License
Copyright (c) 2016 _nK Licensed under the WTFPL license.
