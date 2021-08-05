     .d88888b.  8888888b.  d8b
    d88P" "Y88b 888   Y88b Y8P
    888     888 888    888
    888     888 888   d88P 888  .d88b.  888  888 .d8888b
    888     888 8888888P"  888 d88""88b 888  888 88K
    888 Y8b 888 888 T88b   888 888  888 888  888 "Y8888b.
    Y88b.Y8b88P 888  T88b  888 Y88..88P Y88b 888      X88
     "Y888888"  888   T88b 888  "Y88P"   "Y88888  88888P'
           Y8b



## Install

Install using the package manager for your desired environment(s):

``` bash
$ npm install --save qrious
# OR:
$ bower install --save qrious
```


## Examples

``` html
<!DOCTYPE html>
<html>
  <body>
    <canvas id="qr"></canvas>

    <script src="/path/to/qrious.js"></script>
    <script>
      (function() {
        var qr = new QRious({
          element: document.getElementById('qr'),
          value: 'https://github.com/neocotic/qrious'
        });
      })();
    </script>
  </body>
</html>
```

Open up `demo.html` in your browser to play around a bit.

## API

Simply create an instance of `QRious` and you've done most of the work. You can control many aspects of the QR code
using the following fields on your instance:

| Field           | Type    | Description                                        | Default       | Read Only |
| --------------- | ------- | -------------------------------------------------- | ------------- | --------- |
| background      | String  | Background color of the QR code                    | `"white"`     | No        |
| backgroundAlpha | Number  | Background alpha of the QR code                    | `1.0`         | No        |
| element         | Element | Element to render the QR code                      | `<canvas>`    | Yes       |
| foreground      | String  | Foreground color of the QR code                    | `"black"`     | No        |
| foregroundAlpha | Number  | Foreground alpha of the QR code                    | `1.0`         | No        |
| level           | String  | Error correction level of the QR code (L, M, Q, H) | `"L"`         | No        |
| mime            | String  | MIME type used to render the image for the QR code | `"image/png"` | No        |
| padding         | Number  | Padding for the QR code (pixels)                   | `null` (auto) | No        |
| size            | Number  | Size of the QR code (pixels)                       | `100`         | No        |
| value           | String  | Value encoded within the QR code                   | `""`          | No        |

``` javascript
var qr = new QRious();
qr.background = 'green';
qr.backgroundAlpha = 0.8;
qr.foreground = 'blue';
qr.foregroundAlpha = 0.8;
qr.level = 'H';
qr.padding = 25;
qr.size = 500;
qr.value = 'https://github.com/neocotic/qrious';
```

The QR code will automatically update when you change one of these fields, so be wary when you plan on changing lots of
fields at the same time. You probably want to make a single call to `set(options)` instead as it will only update the QR
code once:

``` javascript
var qr = new QRious();
qr.set({
  background: 'green',
  backgroundAlpha: 0.8,
  foreground: 'blue',
  foregroundAlpha: 0.8,
  level: 'H',
  padding: 25,
  size: 500,
  value: 'https://github.com/neocotic/qrious'
});
```

These can also be passed as options to the constructor itself:

``` javascript
var qr = new QRious({
  background: 'green',
  backgroundAlpha: 0.8,
  foreground: 'blue',
  foregroundAlpha: 0.8,
  level: 'H',
  padding: 25,
  size: 500,
  value: 'https://github.com/neocotic/qrious'
});
```

You can also pass in an `element` option to the constructor which can be used to generate the QR code using an existing
DOM element, which is the only time that you can specify read only options. `element` must either be a `<canvas>`
element or an `<img>` element which can then be accessed via the `canvas` or `image` fields on the instance
respectively. An element will be created for whichever one isn't provided or for both if no `element` is specified,
which means that they can be appended to the document at a later time.

``` javascript
var qr = new QRious({
  element: document.querySelector('canvas'),
  value: 'https://github.com/neocotic/qrious'
});

qr.canvas.parentNode.appendChild(qr.image);
```

A reference to the `QRious` instance is also stored on both of the elements for convenience.

``` javascript
var canvas = document.querySelector('canvas');
var qr = new QRious({
  element: canvas,
  value: 'https://github.com/neocotic/qrious'
});

qr === canvas.qrious;
//=> true
```

### `toDataURL([mime])`

Generates a base64 encoded data URI for the QR code. If you don't specify a MIME type, it will default to the one
passed to the constructor as an option or the default value for the `mime` option.

``` javascript
var qr = new QRious({
  value: 'https://github.com/neocotic/qrious'
});

qr.toDataURL();
//=> "data:image/png;base64,iVBOR...AIpqDnseH86KAAAAAElFTkSuQmCC"
qr.toDataURL('image/jpeg');
//=> "data:image/jpeg;base64,/9j/...xqAqIqgKFAAAAAq3RRQAUUUUAf/Z"
```

