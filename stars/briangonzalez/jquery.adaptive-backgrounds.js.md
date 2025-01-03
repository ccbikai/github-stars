---
project: jquery.adaptive-backgrounds.js
stars: 6527
description: 🦎 A jQuery plugin for extracting the dominant color from images and applying the color to their parent.
url: https://github.com/briangonzalez/jquery.adaptive-backgrounds.js
---

> jquery.adaptive-backgrounds.js

_A simple jQuery plugin to extract the dominant color of an image and apply it to the background of its parent element._

**Check it out on the web!**

Getting Started
---------------

Install via bower:

```
bower install --save adaptive.background
```

Then simply include jQuery and the script in your page, and invoke it like so:

$(document).ready(function(){
  $.adaptiveBackground.run();
});

The script looks for image(s) with the `data-adaptive-background` attribute:

<img src\="/image.jpg" data-adaptive-background\>

### Using an element with a CSS background image

Instead of using an `<img>` element nested inside of parent element, AB supports grabbing the dominant color of a background image of a standalone element, then applying the corresponding dominant color as the background color of said element.

Enable this functionality by adding a data property, `data-ab-css-background` to the element. See the example below:

<div style\='background-image: url(/some-image.jpg)' data-adaptive-background data-ab-css-background\></div\>

Demo
----

Here's a little demo of how it works. (1) The page loads (2) the dominant background color of the image is extracted (3) said color is applied to parent of image. _Demo drastically slowed down to show effect_.

* * *

API
---

This plugin exposes one method:

-   **$.adaptiveBackground.run(opts)** _arg: opts (Object)_ an optional argument to be merged in with the defaults.

Default Options
---------------

-   **selector** String _(default: `'img[data-adaptive-background="1"]'`)_ a CSS selector which denotes which images to grab/process. Ideally, this selector would start with _img_, to ensure we only grab and try to process actual images.
-   **parent** falsy _(default: `null`)_ a CSS selector which denotes which parent to apply the background color to. By default, the color is applied to the parent one level up the DOM tree.
-   **normalizeTextColor** boolean _(default: `false`)_ option to normalize the color of the parent text if background color is too dark or too light.
-   **normalizedTextColors** Object Literal _(default: `{dark: '#000', light: '#fff'}`)_ text colors used when background is either too dark/light.
-   **shadeVariation** `blend|true|false` (default) option to shade the color of the parent ligher or darker (see shadePercentage) or blend the color of the parent with another color by a certain percentage (see shadeColors).
-   **shadePercentage** float (default: `0`) sets the percentage of shading or blending used. Can be adjusted from -1.00 to 1.00.
-   **shadeColors** Object Literal ( default: `{light:'rgb(255,255,255)',dark:'rgb(0,0,0)'}` ) sets the color that will be used to blend the background color with. Two values are provided to account for the background color to be light or dark to start with.
-   **transparent** Transparent dominant color. Can be adjusted from 0.01 to 0.99.

**Example:** Call the `run` method, passing in any options you'd like to override.

var defaults      \= {
  selector:             '\[data-adaptive-background="1"\]',
  parent:               null,
  exclude:              \[ 'rgb(0,0,0)', 'rgba(255,255,255)' \],
  shadeVariation:   false,
  shadePercentage:  0,
  shadeColors:  {
    light:      'rgb(255,255,255)',
    dark:       'rgb(0,0,0)' 
  },
  normalizeTextColor:   false,
  normalizedTextColors:  {
    light:      "#fff",
    dark:       "#000"
  },
  lumaClasses:  {
    light:      "ab-light",
    dark:       "ab-dark"
  },
  transparent: null
};
$.adaptiveBackground.run(defaults)

Events Emitted
--------------

-   **ab-color-found** Event This event is fired when the dominant color of the image is found. The payload includes the dominant color as well as the color palette contained in the image.

**Example:** Bind to the `ab-color-found` event like so:

$('img.my-image').on('ab-color-found', function(ev,payload){
  console.log(payload.color);   // The dominant color in the image.
  console.log(payload.palette); // The color palette found in the image.
  console.log(ev);   // The jQuery.Event object
});

Success Callback
----------------

You may wish to supply a callback function which is called once the magic has been performed.

$.adaptiveBackground.run({
  success: function($img, data) {
    console.log('Success!', $img, data);
  }
});

Note, this callback is called _once_ for each image.

Caveats
-------

This plugin utlizes the `<canvas>` element and the `ImageData` object, and due to cross-site security limitations, the script will fail if one tries to extract the colors from an image not hosted on the current domain, _unless_ the image allows for Cross Origin Resource Sharing.

**Enabling CORS on S3**

To enable CORS for images hosted on S3 buckets, follow the Amazon guide here; adding the following to the bucket's CORS configuration:

<CORSRule\>
 <AllowedOrigin\>\*</AllowedOrigin\>
 <AllowedMethod\>GET</AllowedMethod\>
</CORSRule\>

For all images, you can optionally also include a cross-origin attribute in your image. This is not absolutely necessary since the `anonymous` origin is set in the Javascript code, but kudos to you for being a super-developer.

<img src\="/image.jpg" data-adaptive-background cross-origin\="anonymous"/>

Credit
------

This plugin is built on top of a script called RGBaster.

Collaborators
-------------

Brian Gonzalez

Scott Stern

Alfred J Kwack

This project exists thanks to all the people who contribute. \[Contribute\].

Backers
-------

Thank you to all our backers! 🙏 \[Become a backer\]

Sponsors
--------

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

License
-------

MIT, yo.
