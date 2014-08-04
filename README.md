# fontfaceonload

[![Build Status](https://img.shields.io/travis/zachleat/fontfaceonload/master.svg)](https://travis-ci.org/zachleat/fontfaceonload)
[![Dependency Status](https://david-dm.org/zachleat/fontfaceonload.svg?theme=shields.io)](https://david-dm.org/zachleat/fontfaceonload)
[![devDependency Status](https://david-dm.org/zachleat/fontfaceonload/dev-status.svg?theme=shields.io)](https://david-dm.org/zachleat/fontfaceonload#info=devDependencies)

## Usage

Use with any existing @font-face declaration.

```
@font-face {
	font-family: My Custom Font Family;
	/* src and other properties as normal */
}
```

Include the library. Call the JavaScript.

```
FontFaceOnload( "My Custom Font Family", {
	success: function() {},
	error: function() {},
	timeout: 5000, // in ms. Optional, default is 10 seconds
	glyphs: "\uE600\uE601\uE602\uE605" // Optional, default is "". Useful for icon fonts: a few code points from your custom font icon.
});
```

## How it Works

This uses the [CSS Font Loading Module](http://dev.w3.org/csswg/css-font-loading/) when available (currently in Chrome 35+ and Opera 22+). When that isn’t available, it uses a very similar approach to the one used in the [TypeKit Web Font Loader](https://github.com/typekit/webfontloader) (which is currently 7.1KB GZIP).

Basically, it creates an element with a font stack including the web font and a default serif/sans-serif typeface.  It then uses a test string and measures the dimensions of the element at a certain interval. When the dimensions are different than the default fallback fonts, the font is considered to have loaded successfully.

If you’d like a full polyfill for the CSS Font Loading Module, follow along with [Bram Stein’s Font Loader](https://github.com/bramstein/fontloader). I believe the specification has changed since he launched this polyfill, but he’s working on an updated version.

## Building the project

Run these commands:

 * `npm install`
 * `bower install`
 * `grunt init`
 * `grunt` as normal.

## Configuring Grunt

Rather than one giant `Gruntfile.js`, this project is using a modular Grunt setup. Each individual grunt configuration option key has its own file located in `grunt/config-lib/` (readonly upstream configs, do not modify these directly) or `grunt/config/` (project specific configs). You may use the same key in both directories, the objects are smartly combined using [Lo-Dash merge](http://lodash.com/docs#merge).

For concatenation in the previous Gruntfile setup, you’d add another key to the giant object passed into `grunt.initConfig` like this: `grunt.initConfig({ concat: { /* YOUR CONFIG */ } });`. In the new configuration, you’ll create a `grunt/config/concat.js` with `module.exports = { /* YOUR CONFIG */ };`.

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
