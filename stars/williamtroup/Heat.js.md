---
project: Heat.js
stars: 538
description: 🌞 A lightweight JavaScript library that generates customizable heat maps, charts, and statistics to visualize date-based activity and trends.
url: https://github.com/williamtroup/Heat.js
---

Heat.js


=========

> 🌞 A lightweight JavaScript library that generates customizable heat maps, charts, and statistics to visualize date-based activity and trends.
> 
> v4.2.2

  

  
  

What features does Heat.js have?
================================

-   Zero-dependencies and extremely lightweight!
-   Written in TypeScript, allowing greater support for React, Angular, and other libraries!
-   Full API available via public functions.
-   Fully styled in CSS/SASS, fully responsive, and compatible with the Bootstrap library.
-   Full CSS theme support (using :root variables).
-   4 views supported: Map, Chart, Days, and Statistics!
-   Configuration dialog support per view.
-   Fully configurable per DOM element.
-   Toggling colors on/off support.
-   Export all data to CSV, JSON, XML, and TXT.
-   Import data from JSON, TXT, and CSV.
-   51 language translations available!
-   Trend types allows data to be split up and viewed separately.
-   Customizable tooltips.
-   12 additional themes available (for dark and light mode).
-   Data pulling (does not support trend types).
-   Color ranges support different colors per view.

  
  

Where can I find the documentation?
===================================

All the documentation can be found here.  
  

What browsers are supported?
============================

All modern browsers (such as Google Chrome, FireFox, and Opera) are fully supported.  
  

What languages are supported?
=============================

-   `af` Afrikaans
-   `ar` Arabic
-   `hy` Armenian
-   `be` Belarusian
-   `bn` Bengali
-   `bg` Bulgarian
-   `ca` Catalan
-   `zh` Chinese (simplified)
-   `da` Danish
-   `nl` Dutch
-   `en` English (default)
-   `eo` Esperanto
-   `et` Estonian
-   `fa` Farsi
-   `fi` Finnish
-   `fr` French
-   `fy` Frisian
-   `gl` Galician
-   `ka` Georgian
-   `de` German
-   `el` Greek
-   `he` Hebrew
-   `hi` Hindi
-   `hu` Hungarian
-   `is` Icelandic
-   `id` Indonesian
-   `ga` Irish
-   `it` Italian
-   `ja` Japanese
-   `ko` Korean
-   `lv` Latvian
-   `lt` Lithuanian
-   `lb` Luxembourgish
-   `ms` Malay
-   `ne` Nepali
-   `no` Norwegian
-   `pl` Polish
-   `pt` Portuguese
-   `ro` Romanian
-   `si` Sinhalese
-   `sk` Slovak
-   `sl` Slovenian
-   `es` Spanish
-   `sv` Swedish
-   `tl` Tagalog
-   `ta` Tamil
-   `zh-tw` Taiwanese
-   `te` Telugu
-   `th` Thai
-   `tr` Turkish
-   `uk` Ukrainian

  
  

What are the most recent changes?
=================================

To see a list of all the most recent changes, click here.  
  

How do I install Heat.js?
=========================

You can install the library with npm into your local modules directory using the following command:

npm install jheat.js

Or, you can download the latest zipped up version here.

Or, you can also use the following CDN links:

https://cdn.jsdelivr.net/gh/williamtroup/Heat.js@4.2.2/dist/heat.min.js
https://cdn.jsdelivr.net/gh/williamtroup/Heat.js@4.2.2/dist/heat.js.min.css

  
  

How do I get started?
=====================

To get started using Heat.js, do the following steps:  
  

### 1\. Prerequisites:

Make sure you include the "DOCTYPE html" tag at the top of your HTML, as follows:

<!DOCTYPE html\>

  

### 2\. Include Files:

<link rel\="stylesheet" href\="dist/heat.js.css"\>
<script src\="dist/heat.js"\></script\>

  

### 3\. DOM Element Binding:

<div id\="heat-map" data-heat-js\="{ 'views': { 'map': { 'showDayNames': true } } }"\>
    Your HTML.
</div\>

To see a list of all the available binding options you can use for "data-heat-js", click here.

To see a list of all the available custom triggers you can use for "data-heat-js", click here.

  

### 4\. Adding Dates:

Now, you can add/remove dates, which will update the heat map automatically!

<script\>
  var newDateObject \= new Date();

  $heat.addDate( "heat-map", newDateObject, "Trend Type 1", true );
  $heat.removeDate( "heat-map", newDateObject, "Trend Type 1", true );
</script\>

  
  

### 5\. Finishing Up:

That's it! Nice and simple. Please refer to the code if you need more help (fully documented).  
  

How do I go about customizing Heat.js?
======================================

To customize, and get more out of Heat.js, please read through the following documentation.  
  

### 1\. Public Functions:

To see a list of all the public functions available, click here.  
  

### 2\. Configuration:

Configuration options allow you to customize how Heat.js will function. You can set them as follows:

<script\> 
  $heat.setConfiguration( {
      safeMode: false
  } );
</script\>

To see a list of all the available configuration options you can use, click here.
