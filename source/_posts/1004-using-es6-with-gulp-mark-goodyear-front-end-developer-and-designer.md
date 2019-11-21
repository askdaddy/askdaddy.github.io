---
title: "Using ES6 with gulp — Mark Goodyear —\_Front-end developer and designer"
tags:
  - es6
  - h5
  - Javascript
url: 1004.html
id: 1004
date: 2016-11-23 03:53:59
---

Jun 24, 2015 With gulp 3.9, we are now able to use ES6 (or ES2015 as it's now named) in our gulpfile—thanks to the awesome Babel transpiler. Firstly make sure you have at least version 3.9 of both the CLI and local version of gulp. To check which version you have, open up terminal and type:

    gulp -v

This should return:

    CLI version 3.9.0
    Local version 3.9.0

If you get any versions lower than 3.9, update gulp in your `package.json` file, and run the following to update both versions:

    npm install gulp && npm install gulp -g

### Creating an ES6 gulpfile

To leverage ES6 you will need to install Babel (make sure you have Babel 6) as a dependency to your project, along with the es2015 plugin preset:

    npm install babel-core babel-preset-es2015 --save-dev

Once this has finished, we need to create a `.babelrc` config file to enable the es2015 preset:

    touch .babelrc

And add the following to the file:

    {
      "presets": ["es2015"]
    }

We then need to instruct gulp to use Babel. To do this, we need to rename the `gulpfile.js` to `gulpfile.babel.js`:

    mv "gulpfile.js" "gulpfile.babel.js"

We can now use ES6 via Babel! An example of a typical gulp task using new ES6 features:

    'use strict';
    
    import gulp from 'gulp';
    import sass from 'gulp-sass';
    import autoprefixer from 'gulp-autoprefixer';
    import sourcemaps from 'gulp-sourcemaps';
    
    const dirs = {
      src: 'src',
      dest: 'build'
    };
    
    const sassPaths = {
      src: `${dirs.src}/app.scss`,
      dest: `${dirs.dest}/styles/`
    };
    
    gulp.task('styles', () => {
      return gulp.src(paths.src)
        .pipe(sourcemaps.init())
        .pipe(sass.sync().on('error', plugins.sass.logError))
        .pipe(autoprefixer())
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest(paths.dest));
    });

Here we have utilised ES6 [import/modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import), [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings) and [constants](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const). If you’d like to check out more ES6 features, [es6-features.org](http://es6-features.org/) is a handy resource.