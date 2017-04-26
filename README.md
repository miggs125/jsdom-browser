# [jsdom-browser][repo-url] [![NPM][npm-img]][npm-url] [![MIT Licenses][mit-img]][mit-url] [![Build Status][travis-img]][travis-url] [![Build Status][appveyor-img]][appveyor-url] [![Coverage Status][coverage-img]][coverage-url]

Web browser simulator with [jsdom](https://github.com/tmpvar/jsdom).

## Install

```js
npm install jsdom jsdom-browser --save-dev
```

## Usage

### Simplest usage

The simplest usage of **BrowserConfig** and the way to simulate the default Web browser's behaviors are as follows:

```js
const { JSDOM } = require('jsdom')
const BrowserConfig = require('jsdom-browser')

const browserConfig = new BrowserConfig()
const window = new JSDOM().window
browserConfig.configure(window)
```

After this, you can use some features of the simulated Web browser that this module supports.

### Configuring parameters

To configure some parameters of the simulated Web browser, for example the window position, the window size, the size of the windows edge and so on, you can set a *initConfig* object as a parameter to **BrowserConfig#configure**:


```js
const browserConfig = new BrowserConfig()

const initConfig = {
  windowConfig: {
    top: 10, left: 50, width: 600, height: 400,
    frame: { edgeSize: { bottom: 40 } },
  },
  screenConfig: {
    width: 1280, height: 800, availTop: 23, availBottom: 0,
  },
}

const window = new JSDOM().window
browserConfig.configure(window, initConfig)
```

And you can change the configurations of the `window` later by changing the `browserConfig`'s properties:

```js
window.outerWidth // => 600
window.screen.width // => 1280

browserConfig.windowConfig.width = 800
browserConfig.screenConfig.width = 2048

window.outerWidth // => 800
window.screen.width // => 2048
```


### Configuring behaviours

To configure some behaviors of the simulated Web browser, you can extend and change the member classes of **BrowserConfig**:

```js
const browserConfig = new BrowserConfig()

class MyWindowConfig extends BrowserConfig.WindowConfig { ... }

browserConfig.WindowConfig = MyWindowConfig

const window = new JSDOM().window
browserConfig.configure(window)
```

## API

### BrowserConfig class

#### <u>*constructor* ()</u>

Constructs a `BrowserConfig` instance.

#### <u>.configure (window [, initConfig ])</u>

Configure to simulate a browser.

**Parameters:**

* **window** [object] : A Window object created by jsdom.
* **initConfig** [object | BrowserConfig] : A parameter tree to configure a browser. (optional)

More detail API of **BrowserConfig** and other classes are as follow:

* [BrowserConfig class](docs/api/BrowserConfig.md)
* [WindowConfig class](docs/api/WindowConfig.md)
* [ScreenConfig class](docs/api/ScreenConfig.md)

## Progress

- [Screen](https://www.w3.org/TR/cssom-view-1/#screen) &#x2713;
- [ScreenOrientation](https://www.w3.org/TR/screen-orientation/) *(Not yet)*
- [Window](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-window-interface)
    - screen &#x2713;
    - innerWidth, innerHeight, outerWidth, outerHeight, screenX, screenY,
      devicePixelRatio &#x2713;
    - scrollX, scrollY, pageXOffset, pageYOffset &#x2713;
    - moveTo, moveBy, resizeTo, resizeBy &#x2713;
    - scroll, scrollTo, scrollBy  &#x2713;
    - *open (Not yet)*
    - *matchMedia (Not yet)*

## References

- [CSSOM View Modules](https://www.w3.org/TR/cssom-view-1)
- [HTML Living Standard](https://html.spec.whatwg.org/multipage/)


## License

Copyright (C) 2017 Takayuki Sato

This program is free software under [MIT][mit-url] License.
See the file LICENSE in this distribution for more details.


[repo-url]: https://github.com/sttk/jsdom-browser/
[npm-img]: https://img.shields.io/badge/npm-v0.4.0-blue.svg
[npm-url]: https://www.npmjs.org/package/jsdom-browser/
[mit-img]: https://img.shields.io/badge/license-MIT-green.svg
[mit-url]: https://opensource.org/licenses.MIT
[travis-img]: https://travis-ci.org/sttk/jsdom-browser.svg?branch=master
[travis-url]: https://travis-ci.org/sttk/jsdom-browser
[appveyor-img]: https://ci.appveyor.com/api/projects/status/github/sttk/jsdom-browser?branch=master&svg=true
[appveyor-url]: https://ci.appveyor.com/project/sttk/jsdom-browser
[coverage-img]: https://coveralls.io/repos/github/sttk/jsdom-browser/badge.svg?branch=master
[coverage-url]: https://coveralls.io/github/sttk/jsdom-browser?branch=master
