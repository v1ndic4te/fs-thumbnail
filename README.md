# fs-thumbnail

Node.js library that generates thumbnails for files in the file system.

# Overview

`fs-thumbnail` was designed for [Ogma](https://github.com/TimboKZ/Ogma). It generates thumbnails based on file system
paths of files. It tries several different libraries and uses the best match to generate the thumbnail. Libraries used
(the ones labelled as *peer dependency* must be installed separately):
* **[sharp](https://github.com/lovell/sharp)** (peer dependency). Used for JPEG, PNG, WebP, TIFF, GIF and SVG images.

# Installing

Install the main package:
```bash
npm install fs-thumbnail
```

Install some subset of peer dependencies that is relevant to your project:
```bash
# On all machines
npm install sharp@0

# On Debian/Ubuntu
apt install ffmpeg
```

Now you can use the library:
```js
const ThumbnailManager = require('./ThumbnailManager');
const thumbManager = new ThumbnailManager({
    verbose: true, // Whether to print out warning/errors
    size: [500, 300], // Default size, either a single number of an array of two numbers - [width, height].
    quality: 70, // Default quality, between 1 and 100
});

thumbManager.getThumbnail({
    path: '/path/to/my/image.png',
    output: '/thumbnail/folder/thumbnail.jpg',
    size: 300,
    quality: 70,
})
    .then(thumbnailPath => {
        if (!thumbnailPath) console.log('Could not generate the thumbnail!');
        else console.log(`Thumbnail generated! Find it here: ${thumbnailPath}`);
    });
```