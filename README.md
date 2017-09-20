Flexible ascii progress bar with 9 different head characters based on progress

## Installation

```bash
$ npm install progress-softbar
```

## Usage

First we create a `ProgressBar`, giving it a format string
as well as the `total`, telling the progress bar when it will
be considered complete. After that all we need to do is `tick()` appropriately.

```javascript
var ProgressBar = require('progress-softbar');

var bar = new ProgressBar(':bar', { total: 10 });
var timer = setInterval(function () {
  bar.tick();
  if (bar.complete) {
    console.log('\ncomplete\n');
    clearInterval(timer);
  }
}, 100);
```

### Options

These are keys in the options object you can pass to the progress bar along with
`total` as seen in the example above.

- `curr` current completed index
- `total` total number of ticks to complete
- `width` the displayed width of the progress bar defaulting to total
- `stream` the output stream defaulting to stderr
(- `head` head character defaulting to complete character now OBSOLETE for progress-softbar)
- `complete` completion character defaulting to "="
- `incomplete` incomplete character defaulting to "-"
- `renderThrottle` minimum time between updates in milliseconds defaulting to 16
- `clear` option to clear the bar on completion defaulting to false
- `callback` optional function to call when the progress bar completes

### Tokens

These are tokens you can use in the format of your progress bar.

- `:bar` the progress bar itself
- `:current` current tick number
- `:total` total ticks
- `:elapsed` time elapsed in seconds
- `:percent` completion percentage
- `:eta` estimated completion time in seconds
- `:rate` rate of ticks per second

### Custom Tokens

You can define custom tokens by adding a `{'name': value}` object parameter to your method (`tick()`, `update()`, etc.) calls.

```javascript
var bar = new ProgressBar(':current: :token1 :token2', { total: 3 })
bar.tick({
  'token1': "Hello",
  'token2': "World!\n"
})
bar.tick(2, {
  'token1': "Goodbye",
  'token2': "World!"
})
```
The above example would result in the output below.

```
1: Hello World!
3: Goodbye World!
```

## Examples

```
checking ▕██▏                                      ▏ 6% 233.9s
```
For more info see the original progress npm.

## License

MIT
