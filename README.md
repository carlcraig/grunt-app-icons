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


Advanced Configuration
----------------------

Additional arguments may be passed to the `convert` command as needed as an array or function. The `%size%` placeholder is interpolated with the `wxh` dimensions of the icon being processed. For example, to apply a scalable overlay to the icons (where 120x120 is the size of the SVG):

```js
appIcons: {
  mobile_beta: {
    src: 'src/icon/app-icon.png',
    dest: 'src/icon/',
    options: {
      createDirectories: true,
      type: ['ios', 'android'],
      args: [
        '-background', 'none',
        '-size', '120x120',
        'src/icon/app-icon-beta-overlay.svg',
        '-resize', '%size%',
        '-composite'
      ]
    }
  }
}
```

Similarly, to create rounded corners on Android:

```js
appIcons: {
  mobile_beta: {
    src: 'src/icon/app-icon.png',
    dest: 'src/icon/',
    options: {
      createDirectories: true,
      type: ['android'],
      args: function (size) {
        if (size) {
          var dimensions = size.split('x');
          var cornerRadius = Math.round(100 * dimensions[0] * 20 / 114) / 100;

          return [
            // Create a 1px transparent border around the image to improve
            // antialiasing
            '(',
              '-size', '%size%',
              'xc:none',
              '-draw', 'fill white rectangle 1,1 ' + (dimensions[0] - 2) + ',' + (dimensions[1] - 2),
            ')',
            '-compose', 'CopyOpacity',
            '-composite',

            // Mask off the four corners
            '(',
              '+clone',
              '-alpha', 'extract',
              '-draw', 'fill black rectangle 1,1 ' + cornerRadius + ',' + cornerRadius + ' fill white circle ' + cornerRadius + ',' + cornerRadius + ' ' + cornerRadius + ',1',
              '(',
                '+clone', '-flip',
              ')', '-compose', 'Multiply', '-composite',
              '(',
                '+clone', '-flop',
              ')', '-compose', 'Multiply', '-composite',
            ')',
            '-alpha', 'off',
            '-compose', 'CopyOpacity',
            '-composite'
          ];
        }
        return [];
      }
    }
  }
}
```

Note that the favicon type does not support size interpolation and uses a significantly different convert command than the other icons that are simple resize operations.

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