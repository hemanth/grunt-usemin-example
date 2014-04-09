> [grunt-usemin](https://github.com/yeoman/grunt-usemin) example.

P.S: This is a minimalist usage of grunt-usemin, do read the usemin [README](https://github.com/yeoman/grunt-usemin/blob/master/README.md) for more details.


The directory structure looks like:

```sh
.
├── assets
│   ├── css
│   │   └── style.css
│   └── js
│       ├── bar.js
│       └── foo.js
├── gruntfile.js
├── index.html
└── package.json
```

Where `style.css` includes bare minimal CSS and `bar.js` and `foo.js` are simple javascript files.

The `index.html` looks like:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Usemin test</title>
    <!-- build:css assets/css/style.min.css -->
      <link rel="stylesheet" type="text/css" href="./assets/css/styles.css" media="screen" />
    <!-- endbuild -->
  </head>
  <body>
  
  </body>
  <!-- build:js assets/js/optimized.js -->
    <script src="./assets/js/foo.js"></script>
    <script src="./assets/js/bar.js"></script>
  <!-- endbuild -->  
</html>
```

__On grunting__: 

```sh
$ grunt
Running "copy:html" (copy) task
Copied 1 file

Running "useminPrepare:html" (useminPrepare) task
Going through index.html to update the config
Looking for build script HTML comment blocks

Configuration is now:

  concat:
  { generated: 
   { files: 
      [ { dest: '.tmp/concat/assets/css/style.min.css',
          src: [ 'assets/css/style.css' ] },
        { dest: '.tmp/concat/assets/js/optimized.js',
          src: [ 'assets/js/foo.js', 'assets/js/bar.js' ] } ] } }

  uglify:
  { generated: 
   { files: 
      [ { dest: 'dist/assets/js/optimized.js',
          src: [ '.tmp/concat/assets/js/optimized.js' ] } ] } }

  cssmin:
  { generated: 
   { files: 
      [ { dest: 'dist/assets/css/style.min.css',
          src: [ '.tmp/concat/assets/css/style.min.css' ] } ] } }

Running "concat:generated" (concat) task
File ".tmp/concat/assets/css/style.min.css" created.
File ".tmp/concat/assets/js/optimized.js" created.

Running "uglify:generated" (uglify) task
File dist/assets/js/optimized.js created: 75 B → 58 B

Running "cssmin:generated" (cssmin) task
File dist/assets/css/style.min.css created: 48 B → 39 B

Running "usemin:html" (usemin) task

Processing as HTML - dist/index.html
Update the HTML to reference our concat/min/revved script files
Update the HTML with the new css filenames
Update the HTML with the new img filenames
Update the HTML with data-main tags
Update the HTML with data-* tags
Update the HTML with background imgs, case there is some inline style
Update the HTML with anchors images
Update the HTML with reference in input

Done, without errors.
```

Do notice that `default` task:

```sh
	grunt.registerTask('default',[
		'copy:html',
		'useminPrepare',
		'concat',
		'uglify',
        'cssmin',
		'usemin'
    ]);
```

The new dir structure will be:

```sh
.
├── assets
│   ├── css
│   │   └── style.css
│   └── js
│       ├── bar.js
│       └── foo.js
├── dist
│   ├── assets
│   │   ├── css
│   │   │   └── style.min.css
│   │   └── js
│   │       └── optimized.js
│   └── index.html
├── gruntfile.js
├── index.html
```

`dist/index.html` would now look like:

```html 
<!DOCTYPE html>
<html>
  <head>
    <title>Usemin Example</title>
    <link rel="stylesheet" href="assets/css/style.min.css" media="screen"/>
  </head>
  <body>
  
  </body>
  <script src="assets/js/optimized.js"></script>
</html>
```

`css` is minifed and `js` is concated and minifed. Have a look the `dist` and `.tmp` dir that are added for your refference.

Hope this helped you to get started with usemin!



