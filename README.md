Grunt App Icons
===============

Will create icons for your project.

- Favicon
- Touch Icons
- iOS Icons
- Android Icons


Installation
------------

```sh
npm install grunt-app-icons --save-dev
```

```js
grunt.loadNpmTasks('grunt-app-icons');
```



Example Configuration
---------------------

```js
appIcons: {
  all: {
    src: 'src/icon/app-icon.png',
    dest: 'src/icon/',
    options: {
      createDirectories: true,
      type: ['all']
    }
  },
  www: {
    src: 'src/icon/app-icon.png',
    dest: 'www/',
    options: {
      type: ['touch', 'favicon'] // android, ios
    }
  }
}
```

Html
----

```html
<link rel="icon" sizes="192x192" href="touch-icon-192x192.png">
<link rel="apple-touch-icon-precomposed" sizes="180x180" href="apple-touch-icon-180x180-precomposed.png">
<link rel="apple-touch-icon-precomposed" sizes="152x152" href="apple-touch-icon-152x152-precomposed.png">
<link rel="apple-touch-icon-precomposed" sizes="120x120" href="apple-touch-icon-120x120-precomposed.png">
<link rel="apple-touch-icon-precomposed" sizes="76x76" href="apple-touch-icon-76x76-precomposed.png">
<link rel="apple-touch-icon-precomposed" href="apple-touch-icon-precomposed.png">
```

License
=======

grunt-app-icons is licensed with the MIT license.

See LICENSE-MIT for more details.