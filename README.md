# React Native Module / FFMPEG binary commandline / Android

Uses binary from `android/src/main/res/raw/ffmpeg` running from shell with supplied command from JS.

Requires absolute paths to input / output file and permissions to write to output destination.


## runCommand

```
import {NativeModules} from 'react-native';

const {FFMPEGCommandline} = NativeModules;

// ... inputPath, outputPath

FFMPEGCommandline
    .runCommand ([
        '-ss', '1', // trim start [1 sec]
        '-t', '10', // trim length [10 sec]
        '-i', inputPath,
        '-movflags', '+faststart',
        '-preset', 'ultrafast',
        '-strict', '-2',
        '-y',
        '-filter:v', 'crop=640:720:270:0,scale=360:360',
        '-crf', '26',
        '-c:a', 'copy',
        inputPath
    ])
        .then ((result) => {
            console.log ('result', result);
        })
        .catch ((err) => {
            console.error ('error', err);
        });
```


## Constants

`FILES_DIR_PATH` - application files absolute path

`CACHE_DIR_PATH` - application cache absolute path

Module can write to both folders without additional permissions


## Events

`ffmpeg:init` - result of binary ffmpeg installation / exists check

`ffmpeg:message` - shell output from ffmpeg binary

```
import {DeviceEventEmitter} from 'react-native';

DeviceEventEmitter
    .addListener ('ffmpeg:message', (message) => {
        console.log ('ffmpeg message', message)
    });
```

