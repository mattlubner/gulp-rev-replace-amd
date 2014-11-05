gulp-rev-replace-amd
================

Fork of [gulp-rev-replace](https://github.com/jamesknelson/gulp-rev-replace).

[Gulp](https://github.com/gulpjs/gulp) plugin to rewrite occurrences of RequireJS modules which have been renamed by [gulp-rev](https://github.com/sindresorhus/gulp-rev).


## Install

```bash
$ npm install --save-dev gulp-rev-replace-amd
```


## Usage

Pipe through a stream which has both the files you want to be updated, as well as the files which have been renamed.

```js
  return gulp.src([
      'app/**/*.{html,js,hbs}',
      '.tmp/**/*.*' // take care to NOT include directories !!
    ])
    .pipe($.rev())
    // RJS assets need to be rev-replaced w/o .js extension
    .pipe(revReplaceAmd({
      replaceBasePath: 'assets' // <- set to 'require.config.baseUrl'
    }))
    .pipe(gulp.dest(paths.dest));
});
```


## API

### revReplace(options)

#### options.canonicalUris
Type: `boolean`

Default: `true`

Use canonical URIs when replacing paths; e.g., when working with paths with non-forward-slash (`/`) path separators, replace with forward slashes.

#### options.replaceBasePath
Type: `String`

Default: `''`

Base path of assets; ignored during replacements. Set this to your RequireJS config's baseUrl.

#### options.replaceInExtensions
Type: `Array`

Default: `['.js', '.html', '.hbs']`

Only substitute reved filenames in files of these types.

#### options.replaceSansExtensions
Type: `Array`

Default: `['.js']`

Replace references to these types of files, even when those references lack a file extension.

#### options.skipBaseFiles
Type: `boolean`

Default: `true`

Don't replace filenames in the replaceBasePath (no subpath).

!! WARNING !! Be wary of disabling this setting, as it can significantly increase the likelihood of erroneous string replacements.


## License

[MIT](http://opensource.org/licenses/MIT) © [Matt Lubner](http://mattlubner.com/), [James K Nelson](http://jamesknelson.com/)
