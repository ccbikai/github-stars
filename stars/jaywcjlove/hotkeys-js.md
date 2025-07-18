---
project: hotkeys-js
stars: 6906
description: |-
    ➷ A robust Javascript library for capturing keyboard input. It has no dependencies. 
url: https://github.com/jaywcjlove/hotkeys-js
---

# Hotkeys

<!--dividing-->

[![Buy me a coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-048754?logo=buymeacoffee)](https://jaywcjlove.github.io/#/sponsor)
[![](https://img.shields.io/npm/dm/hotkeys-js?logo=npm)](https://www.npmjs.com/package/hotkeys-js)
[![](https://img.shields.io/github/stars/jaywcjlove/hotkeys-js.svg)](https://github.com/jaywcjlove/hotkeys/stargazers)
![no dependencies](http://jaywcjlove.github.io/sb/status/no-dependencies.svg)
[![GitHub Actions CI](https://github.com/jaywcjlove/hotkeys-js/actions/workflows/ci.yml/badge.svg)](https://github.com/jaywcjlove/hotkeys-js/actions/workflows/ci.yml)
[![Coverage Status](https://coveralls.io/repos/github/jaywcjlove/hotkeys/badge.svg?branch=master)](https://coveralls.io/github/jaywcjlove/hotkeys?branch=master)
[![jaywcjlove/hotkeys-js](https://jaywcjlove.github.io/sb/lang/chinese.svg)](https://github.com/jaywcjlove/hotkeys-js/blob/master/README-zh.md)
[![jaywcjlove/hotkeys-js](https://jaywcjlove.github.io/sb/ico/gitee.svg)](https://gitee.com/jaywcjlove/hotkeys)

HotKeys.js is an input capture library with some very special features, it is easy to pick up and use, has a reasonable footprint ([~6kB](https://bundlephobia.com/result?p=hotkeys-js)) (gzipped: **`2.8kB`**), and has no dependencies. It should not interfere with any JavaScript libraries or frameworks. Official document [demo preview](https://jaywcjlove.github.io/hotkeys-js). [More examples](https://github.com/jaywcjlove/hotkeys-js/issues?q=label%3ADemo+).

```bash
╭┈┈╮          ╭┈┈╮  ╭┈┈╮
┆  ├┈┈..┈┈┈┈┈.┆  └┈╮┆  ├┈┈..┈┈┈┈┈..┈┈.┈┈..┈┈┈┈┈.
┆     ┆┆  □  ┆┆   ┈┤┆    < ┆  -__┘┆  ┆  ┆┆__ ┈┈┤
╰┈┈┴┈┈╯╰┈┈┈┈┈╯╰┈┈┈┈╯╰┈┈┴┈┈╯╰┈┈┈┈┈╯╰┈┈┈  ┆╰┈┈┈┈┈╯
                                  ╰┈┈┈┈┈╯
```

## Usage

You will need `Node.js` installed on your system.

```bash
npm install hotkeys-js --save
```

```js
import hotkeys from 'hotkeys-js';

hotkeys('f5', function(event, handler){
  // Prevent the default refresh event under WINDOWS system
  event.preventDefault()
  alert('you pressed F5!')
});
```

Or manually download and link **hotkeys.js** in your HTML, It can also be downloaded via [UNPKG](https://unpkg.com/hotkeys-js/dist/):

CDN: [UNPKG](https://unpkg.com/hotkeys-js/dist/) | [jsDelivr](https://cdn.jsdelivr.net/npm/hotkeys-js@3.7.3/) | [Githack](https://raw.githack.com/jaywcjlove/hotkeys/master/dist/hotkeys.min.js) | [Statically](https://cdn.statically.io/gh/jaywcjlove/hotkeys/master/dist/hotkeys.min.js) | [bundle.run](https://bundle.run/hotkeys-js@3.7.3)

```html
<script src="https://unpkg.com/hotkeys-js/dist/hotkeys.min.js"></script>
<script type="text/javascript">
hotkeys('ctrl+a,ctrl+b,r,f', function (event, handler){
  switch (handler.key) {
    case 'ctrl+a': alert('you pressed ctrl+a!');
      break;
    case 'ctrl+b': alert('you pressed ctrl+b!');
      break;
    case 'r': alert('you pressed r!');
      break;
    case 'f': alert('you pressed f!');
      break;
    default: alert(event);
  }
});
</script>
```

### Used in React

[react-hotkeys](https://github.com/jaywcjlove/react-hotkeys) is the React component that listen to keydown and keyup keyboard events, defining and dispatching keyboard shortcuts. Detailed use method please see its documentation [react-hotkeys](https://github.com/jaywcjlove/react-hotkeys).

[react-hotkeys-hook](https://github.com/JohannesKlauss/react-hotkeys-hook) - React hook for using keyboard shortcuts in components. Make sure that you have at least version 16.8 of react and react-dom installed, or otherwise hooks won't work for you.

## Browser Support

Hotkeys.js has been tested and should work in.

```shell
Internet Explorer 6+
Safari
Firefox
Chrome
```

## Supported Keys

HotKeys understands the following modifiers: `⇧`, `shift`, `option`, `⌥`, `alt`, `ctrl`, `control`, `command`, and `⌘`.

The following special keys can be used for shortcuts: backspace, tab, clear, enter, return, esc, escape, space, up, down, left, right, home, end, pageup, pagedown, del, delete, f1 through f19, num_0 through num_9, num_multiply, num_add, num_enter, num_subtract, num_decimal, num_divide.

`⌘` Command()
`⌃` Control
`⌥` Option(alt)
`⇧` Shift
`⇪` Caps Lock(Capital)
~~`fn` Does not support fn~~
`↩︎` return/Enter space

## Defining Shortcuts

One global method is exposed, key which defines shortcuts when called directly.

```js
hotkeys([keys:<String>], [option:[string|object|function]], [callback:<function>])
```


```js
hotkeys('f5', function(event, handler) {
  // Prevent the default refresh event under WINDOWS system
  event.preventDefault();
  alert('you pressed F5!');
});

// Returning false stops the event and prevents default browser events
// Mac OS system defines `command + r` as a refresh shortcut
hotkeys('ctrl+r, command+r', function() {
  alert('stopped reload!');
  return false;
});

// Single key
hotkeys('a', function(event,handler){
  //event.srcElement: input
  //event.target: input
  if(event.target === "input"){
      alert('you pressed a!')
  }
  alert('you pressed a!')
});

// Key Combination
hotkeys('ctrl+a,ctrl+b,r,f', function (event, handler){
  switch (handler.key) {
    case 'ctrl+a': alert('you pressed ctrl+a!');
      break;
    case 'ctrl+b': alert('you pressed ctrl+b!');
      break;
    case 'r': alert('you pressed r!');
      break;
    case 'f': alert('you pressed f!');
      break;
    default: alert(event);
  }
});

hotkeys('ctrl+a+s', function() {
    alert('you pressed ctrl+a+s!');
});

// Using a scope
hotkeys('*','wcj', function(event){
  console.log('do something', event);
});
```

#### option

- `scope<String>`: Sets the scope in which the shortcut key is active
- `element<HTMLElement>`: Specifies the DOM element to bind the event to
- `keyup<Boolean>`: Whether to trigger the shortcut on key release
- `keydown<Boolean>`: Whether to trigger the shortcut on key press
- `splitKey<String>`: Delimiter for key combinations (default is `+`)
- `capture<Boolean>`: Whether to trigger the listener during the capture phase (before the event bubbles down)
- `single<Boolean>`: Allows only one callback function (automatically unbinds previous one)

```js
hotkeys('o, enter', {
  scope: 'wcj',
  element: document.getElementById('wrapper'),
}, function() {
  console.log('do something else');
});

hotkeys('ctrl-+', { splitKey: '-' }, function(e) {
  console.log('you pressed ctrl and +');
});

hotkeys('+', { splitKey: '-' }, function(e){
  console.log('you pressed +');
})
```

**keyup**

**key down** and **key up** both perform callback events.

```js
hotkeys('ctrl+a,alt+a+s', {keyup: true}, function(event, handler) {
  if (event.type === 'keydown') {
    console.log('keydown:', event.type, handler, handler.key);
  }

  if (event.type === 'keyup') {
    console.log('keyup:', event.type, handler, handler.key);
  }
});
```

## API REFERENCE

Asterisk "*"

Modifier key judgments

```js
hotkeys('*', function() {
  if (hotkeys.shift) {
    console.log('shift is pressed!');
  }

  if (hotkeys.ctrl) {
    console.log('ctrl is pressed!');
  }

  if (hotkeys.alt) {
    console.log('alt is pressed!');
  }

  if (hotkeys.option) {
    console.log('option is pressed!');
  }

  if (hotkeys.control) {
    console.log('control is pressed!');
  }

  if (hotkeys.cmd) {
    console.log('cmd is pressed!');
  }

  if (hotkeys.command) {
    console.log('command is pressed!');
  }
});
```

### setScope

Use the `hotkeys.setScope` method to set scope. There can only be one active scope besides 'all'.  By default 'all' is always active.

```js
// Define shortcuts with a scope
hotkeys('ctrl+o, ctrl+alt+enter', 'issues', function() {
  console.log('do something');
});
hotkeys('o, enter', 'files', function() {
  console.log('do something else');
});

// Set the scope (only 'all' and 'issues' shortcuts will be honored)
hotkeys.setScope('issues'); // default scope is 'all'
```

### getScope

Use the `hotkeys.getScope` method to get scope.

```js
hotkeys.getScope();
```

### deleteScope

Use the `hotkeys.deleteScope` method to delete a scope. This will also remove all associated hotkeys with it.

```js
hotkeys.deleteScope('issues');
```
You can use second argument, if need set new scope after deleting.

```js
hotkeys.deleteScope('issues', 'newScopeName');
```

### unbind

Similar to defining shortcuts, they can be unbound using `hotkeys.unbind`.

```js
// unbind 'a' handler
hotkeys.unbind('a');

// Unbind a hotkeys only for a single scope
// If no scope is specified it defaults to the current scope (hotkeys.getScope())
hotkeys.unbind('o, enter', 'issues');
hotkeys.unbind('o, enter', 'files');
```

Unbind events through functions.

```js
function example() {
  hotkeys('a', example);
  hotkeys.unbind('a', example);

  hotkeys('a', 'issues', example);
  hotkeys.unbind('a', 'issues', example);
}
```

To unbind everything.

```js
hotkeys.unbind();
```

### isPressed

For example, `hotkeys.isPressed(77)` is true if the `M` key is currently pressed.

```js
hotkeys('a', function() {
  console.log(hotkeys.isPressed('a')); //=> true
  console.log(hotkeys.isPressed('A')); //=> true
  console.log(hotkeys.isPressed(65)); //=> true
});
```

### trigger

trigger shortcut key event

```js
hotkeys.trigger('ctrl+o');
hotkeys.trigger('ctrl+o', 'scope2');
```

### getPressedKeyCodes

Returns an array of key codes currently pressed.

```js
hotkeys('command+ctrl+shift+a,f', function() {
  console.log(hotkeys.getPressedKeyCodes()); //=> [17, 65] or [70]
})
```

### getPressedKeyString

Returns an array of key codes currently pressed.

```js
hotkeys('command+ctrl+shift+a,f', function() {
  console.log(hotkeys.getPressedKeyString()); //=> ['⌘', '⌃', '⇧', 'A', 'F']
})
```

### getAllKeyCodes

Get a list of all registration codes.

```js
hotkeys('command+ctrl+shift+a,f', function() {
  console.log(hotkeys.getAllKeyCodes());
  // [
  //   { scope: 'all', shortcut: 'command+ctrl+shift+a', mods: [91, 17, 16], keys: [91, 17, 16, 65] },
  //   { scope: 'all', shortcut: 'f', mods: [], keys: [42] }
  // ]
})
```

### filter

By default hotkeys are not enabled for `INPUT` `SELECT` `TEXTAREA` elements. `Hotkeys.filter` to return to the `true` shortcut keys set to play a role, `false` shortcut keys set up failure.

```js
hotkeys.filter = function(event){
  return true;
}
//How to add the filter to edit labels. <div contentEditable="true"></div>
//"contentEditable" Older browsers that do not support drops
hotkeys.filter = function(event) {
  var target = event.target || event.srcElement;
  var tagName = target.tagName;
  return !(target.isContentEditable || tagName == 'INPUT' || tagName == 'SELECT' || tagName == 'TEXTAREA');
}

hotkeys.filter = function(event){
  var tagName = (event.target || event.srcElement).tagName;
  hotkeys.setScope(/^(INPUT|TEXTAREA|SELECT)$/.test(tagName) ? 'input' : 'other');
  return true;
}
```

### noConflict

Relinquish HotKeys’s control of the `hotkeys` variable.

```js
var k = hotkeys.noConflict();
k('a', function() {
  console.log("do something")
});

hotkeys()
// -->Uncaught TypeError: hotkeys is not a function(anonymous function)
// @ VM2170:2InjectedScript._evaluateOn
// @ VM2165:883InjectedScript._evaluateAndWrap
// @ VM2165:816InjectedScript.evaluate @ VM2165:682
```

## Development

To develop, Install dependencies, Get the code:

```shell
$ git https://github.com/jaywcjlove/hotkeys.git
$ cd hotkeys     # Into the directory
$ npm install    # or  yarn install
```

To develop, run the self-reloading build:

```shell
$ npm run watch
```

Run Document Website Environment.

```shell
$ npm run doc
```

To contribute, please fork Hotkeys.js, add your patch and tests for it (in the `test/` folder) and submit a pull request.

```shell
$ npm run test
$ npm run test:watch # Development model
```

## Contributors

As always, thanks to our amazing contributors!

<a href="https://github.com/jaywcjlove/hotkeys-js/graphs/contributors">
  <img src="https://jaywcjlove.github.io/hotkeys-js/CONTRIBUTORS.svg" />
</a>

Made with [github-action-contributors](https://github.com/jaywcjlove/github-action-contributors).

## License

[MIT © Kenny Wong](./LICENSE)

