---
project: store.js
stars: 14023
description: Cross-browser storage for all use cases, used across the web.
url: https://github.com/marcuswestin/store.js
---

Store.js
========

Cross-browser storage for all use cases, used across the web.

Store.js has been around since 2010 (first commit, v1 release). It is used in production on tens of thousands of websites, such as cnn.com, dailymotion.com, & many more.

Store.js provides basic key/value storage functionality (`get/set/remove/each`) as well as a rich set of plug-in storages and extra functionality.

1.  Basic Usage
    -   All you need to get started
    -   API
    -   Installation
2.  Supported Browsers
    -   All of them, pretty much :)
    -   List of supported browsers
3.  Plugins
    -   Additional common functionality
    -   List of all Plugins
    -   Using Plugins
    -   Write your own Plugin
4.  Builds
    -   Choose which build is right for you
    -   List of default Builds
    -   Make your own Build
5.  Storages
    -   Storages provide underlying persistence
    -   List of all Storages
    -   Storages limits
    -   Write your own Storage

Basic Usage
-----------

All you need to know to get started:

### API

store.js exposes a simple API for cross-browser local storage:

// Store current user
store.set('user', { name:'Marcus' })

// Get current user
store.get('user')

// Remove current user
store.remove('user')

// Clear all keys
store.clearAll()

// Loop over all stored values
store.each(function(value, key) {
	console.log(key, '==', value)
})

### Installation

Using npm:

npm i store

// Example store.js usage with npm
var store \= require('store')
store.set('user', { name:'Marcus' })
store.get('user').name \== 'Marcus'

Using script tag (first download one of the builds):

<!-- Example store.js usage with script tag -->
<script src\="path/to/my/store.legacy.min.js"\></script\>
<script\>
store.set('user', { name:'Marcus' })
store.get('user').name \== 'Marcus'
</script\>

Supported Browsers
------------------

All of them, pretty much :)

To support all browsers (including IE 6, IE 7, Firefox 4, etc.), use `require('store')` (alias for `require('store/dist/store.legacy')`) or store.legacy.min.js.

To save some kilobytes but still support all modern browsers, use `require('store/dist/store.modern')` or store.modern.min.js instead.

### List of supported browsers

-   Tested on IE6+
-   Tested on iOS 8+
-   Tested on Android 4+
-   Tested on Firefox 4+
-   Tested on Chrome 27+
-   Tested on Safari 5+
-   Tested on Opera 11+
-   Tested on Node (with https://github.com/coolaj86/node-localStorage)

Plugins
-------

Plugins provide additional common functionality that some users might need:

### List of all Plugins

-   all.js: All the plugins in one handy place.
-   defaults.js: Declare default values. Example usage
-   dump.js: Dump all stored values. Example usage
-   events.js: Get notified when stored values change. Example usage
-   expire.js: Expire stored values at a given time. Example usage
-   observe.js: Observe stored values and their changes. Example usage
-   operations.js: Useful operations like push, shift & assign. Example usage
-   update.js: Update a stored object, or create it if null. Example usage
-   v1-backcompat.js: Full backwards compatibility with store.js v1. Example usage

### Using Plugins

With npm:

// Example plugin usage:
var expirePlugin \= require('store/plugins/expire')
store.addPlugin(expirePlugin)

If you're using script tags, you can either use store.everything.min.js (which has all plugins built-in), or clone this repo to add or modify a build and run `make build`.

### Write your own plugin

A store.js plugin is a function that returns an object that gets added to the store. If any of the plugin functions overrides existing functions, the plugin function can still call the original function using the first argument (super\_fn).

// Example plugin that stores a version history of every value
var versionHistoryPlugin \= function() {
	var historyStore \= this.namespace('history')
	return {
		set: function(super\_fn, key, value) {
			var history \= historyStore.get(key) || \[\]
			history.push(value)
			historyStore.set(key, history)
			return super\_fn()
		},
		getHistory: function(key) {
			return historyStore.get(key)
		}
	}
}
store.addPlugin(versionHistoryPlugin)
store.set('foo', 'bar 1')
store.set('foo', 'bar 2')
store.getHistory('foo') \== \['bar 1', 'bar 2'\]

Let me know if you need more info on writing plugins. For the moment I recommend taking a look at the current plugins. Good example plugins are plugins/defaults, plugins/expire and plugins/events.

Builds
------

Choose which build is right for you!

### List of default builds

-   store.everything.min.js: All the plugins, all the storages. Source
-   store.legacy.min.js: Full support for all tested browsers. Add plugins separately. Source
-   store.modern.min.js: Full support for all modern browsers. Add plugins separately. Source
-   store.v1-backcompat.min.js: Full backwards compatibility with store.js v1. Source

### Make your own Build

If you're using npm you can create your own build:

// Example custom build usage:
var engine \= require('store/src/store-engine')
var storages \= \[
	require('store/storages/localStorage'),
	require('store/storages/cookieStorage')
\]
var plugins \= \[
	require('store/plugins/defaults'),
	require('store/plugins/expire')
\]
var store \= engine.createStore(storages, plugins)
store.set('foo', 'bar', new Date().getTime() + 3000) // Using expire plugin to expire in 3 seconds

Storages
--------

Store.js will pick the best available storage, and automatically falls back to the first available storage that works:

### List of all Storages

-   all.js All the storages in one handy place.
-   localStorage.js Store values in localStorage. Great for all modern browsers.
-   sessionStorage.js Store values in sessionStorage.
-   cookieStorage.js Store values in cookies. Useful for Safari Private mode.
-   memoryStorage.js Store values in memory. Great fallback to ensure store functionality at all times.
-   oldFF-globalStorage.js Store values in globalStorage. Only useful for legacy Firefox 3+.
-   oldIE-userDataStorage.js Store values in userData. Only useful for legacy IE 6+.

### Storages limits

Each storage has different limits, restrictions and overflow behavior on different browser. For example, Android has has a 4.57M localStorage limit in 4.0, a 2.49M limit in 4.1, and a 4.98M limit in 4.2... Yeah.

To simplify things we provide these recommendations to ensure cross browser behavior:

Storage

Targets

Recommendations

More info

all

All browsers

Store < 1 million characters

(Except Safari Private mode)

all

All & Private mode

Store < 32 thousand characters

(Including Safari Private mode)

localStorage

Modern browsers

Max 2mb (~1M chars)

limits, android

sessionStorage

Modern browsers

Max 5mb (~2M chars)

limits

cookieStorage

Safari Private mode

Max 4kb (~2K chars)

limits

userDataStorage

IE5, IE6 & IE7

Max 64kb (~32K chars)

limits

globalStorage

Firefox 2-5

Max 5mb (~2M chars)

limits

memoryStorage

All browsers, fallback

Does not persist across pages!

### Write your own Storage

Chances are you won't ever need another storage. But if you do...

See storages/ for examples. Two good examples are memoryStorage and localStorage.

Basically, you just need an object that looks like this:

// Example custom storage
var storage \= {
	name: 'myStorage',
	read: function(key) { ... },
	write: function(key, value) { ... },
	each: function(fn) { ... },
	remove: function(key) { ... },
	clearAll: function() { ... }
}
var store \= require('store').createStore(storage)
