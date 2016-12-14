# premailer-gulp-juice

[![build status](https://secure.travis-ci.org/premailer/gulp-juice.png)](http://travis-ci.org/premailer/gulp-juice) [![npm downloads](https://img.shields.io/npm/dm/premailer-gulp-juice.svg)](https://www.npmjs.com/package/premailer-gulp-juice)

Stream html files through [juice](https://www.npmjs.org/package/juice) to
inline CSS.

## Examples

```bash
npm install premailer-gulp-juice --save-dev 
```

```js
const juice = require('premailer-gulp-juice');

gulp.task('bootloader', function(){
  gulp.src('./.build/bootloader.html')
    .pipe(juice({}))
    .pipe(gulp.dest('./.build/bootloader.inline.html'));
});

gulp.task('deploy', ['build', 'manifest', 'bootloader', 'publishtoS3']);
```

Protip when using with a template renderer: need to pipe to dest first as
you probably want `juice` resolving css relative to our actual build output:

```js
const juice = require('premailer-gulp-juice'),
  pug = require('gulp-pug');

gulp.task('bootloader', function(){
  gulp.src('./app/templates/bootloader.pug')
    .pipe(pug({pretty: true}))
    .pipe(gulp.dest('./.build'))
    .pipe(juice())
    .pipe(gulp.dest('./.build'));
});

gulp.task('deploy', ['build', 'manifest', 'bootloader', 'publishtoS3']);
```

## License

MIT
