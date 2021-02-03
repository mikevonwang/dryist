# Dryist

Dryist is a development tool that allows you to define any constants used in both your JS and SCSS files in one place (i.e. it lets you follow the "DRY" rule).

## Installation

`npm install dryist --save-dev`

## Usage and Example

After installation, there are 4 main steps to using Dryist:

**1.** At your project root, create a file called `dryfile.json`.

**2.** In `dryfile.json`, add the following properties:

```json
{
  "src": "",
  "output": {
    "js": "",
    "scss": ""
  }
}
```

`src` will be the JSON file where the constants you want to use in both your JS and SCSS are stored. Dryist will read this file.

`output.js` will be the filepath where Dryist will write out a JS file containing your constants.

`output.scss` will be the filepath where Dryist will write out an SCSS file containing your constants.

**3.** In the file you listed as `src` above, define your constants in this format:

```json
{
  "my-constant-1": [10, "px"],
  "my-constant-2": [25, "%"],
}
```

Note: dashes in the constants' names will be replaced with underscores in the outputted JS file.

**4.** Import Dryist into your gulpfile (or node script, etc.) and run it in series before any tasks that process your JS and SCSS files:

```js
// gulpfile.js

var gulp = require('gulp');
var dryist = require('dryist');

gulp.task('my_gulp_task', function(done) {
  dryist.run();
  done();
});
```

Dryist will output a JS file that looks something like this:

```js
export const my_constant_1 = 10;
export const my_constant_2 = 25;
```

and also an SCSS file that looks a little like this:

```scss
$my_constant_1: 10px;
$my_constant_2: 25%;
```

which you can then import into your project's JS and SCSS files.
