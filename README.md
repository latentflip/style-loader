# style noreuse loader for webpack

Umm, sorry about the crappy name, couldn't think of a better one.

This is a fork of style-loader which does the same thing, except:

1. doesn't support hot loaders
2. doesn't worry about singletons, or the useable etc options
3. doesn't reuse style tags when encountering the same module id

**Why?**

The why for this module is that I currently haven't figured out a better way to deal with a problem I'm having.

I'm publishing a library of react components, that want to have their own css modules bundled, but don't want to depend on an end user properly configuring webpack for me. So I'm pre-bundling components, and setting it's dependencies as webpack externals.

The trouble is, that if a prebundled component is used inside another webpack app, that basically works except module.ids get reused. That's normally not a problem as they're scoped within the component, _but_ the module.id _is_ shared with style-loader, who will just replace styles if it encounters styles for the same id as it had previously.


## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

### Simple API

``` javascript
require("style!raw!./file.css");
// => add rules in file.css to document
```

It's recommended to combine it with the [`css-loader`](https://github.com/webpack/css-loader): `require("style!css!./file.css")`.

It's also possible to add a URL instead of a CSS string:

``` javascript
require("style/url!file!./file.css");
// => add a <link rel="stylesheet"> to file.css to document
```

### Options

#### `insertAt`

By default, the style-loader appends `<style>` elements to the end of the `<head>` tag of the page. This will cause CSS created by the loader to take priority over CSS already present in the document head. To insert style elements at the beginning of the head, set this query parameter to 'top', e.g. `require('../style.css?insertAt=top')`.

## Install

```
npm install style-noreuse-loader
```

## License

MIT (http://www.opensource.org/licenses/mit-license.php)
