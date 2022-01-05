# Many Webcams Eyetracking (Web Hosting)

> A docker-less version of https://github.com/adriansteffan/mb2-webcam-eyetracking.

## Requirements

- You need a web server (ask your IT staff)

## Setup

1. Download this repo as zip or [click here](https://github.com/ccp-eva/many-webcams-frontend/archive/refs/heads/main.zip)
2. Extract the zip file
3. Open the file `manywebcams/write_data.php` and change line 8 to point to the `data` folder on server `$rootpath = '/serverpath/to/your/manywebcams/data/';`. Usual server paths are:
   1. `/srv/manywebcams/`
   2. `/srv/www/manywebcams/`
   3. `/var/www/html/manywebcams/`
4. Copy your local `manywebcams` directory to your web server.

## Notes

### URL Parameters

#### `id`

You can modify the outcoming filename by defining an `id` URL parameter. That value is being used as a prefix in the outcoming filenames. For example, if your manywebcams URL is: `https://example.com/manywebcams` you can set the parameter as such: `https://example.com/manywebcams?id=mycustomcode123456`. The outcoming files are now prepended with `mycustomcode123456_`. Note that `id` **is case sensitive**, that means `ID` will not work nor other parameters (`code`, `uid`, etc.).

#### `lang`

You can modify the language by providing a `lang` URL parameter. If no parameter is specified the app defaults to english (i.e., `en`). Right now there are only two languages available (see [lang directory](https://github.com/adriansteffan/mb2-webcam-eyetracking/tree/main/src/lang)).

#### Combine Parameters

URL parameters can be combined with an `&`. Let’s say your experiment should be in German (i.e., `lang=de`) and you want to specify your own ID (e.g., `id=mycustomcode123456`), then your URL becomes: `https://example.com/manywebcams?lang=de&id=mycustomcode123456`

### Fix scrubbing issue (affects all browsers)

For recording in the browser (using MediaRecorder API) there is a scrubbing bug for the video files. That means the videos files are not seekable/scrubbable (see here: https://bugs.chromium.org/p/chromium/issues/detail?id=569840). Re-encoding the files fixes this issue. Use handbrake (macOS) or any encoder of your choice.

#### Broken webm to working mp4 using `ffmpeg`:

```
ffmpeg -i yourbrokenvideo.webm -crf 24 -c:v libx264 working.mp4
```
