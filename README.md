# React HLS Player

![NPM Downloads](https://img.shields.io/npm/dm/@marcosalberto/react-hls-player?style=flat-square)
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)
![Libraries.io dependency status for latest release](https://img.shields.io/librariesio/release/npm/@marcosalberto/react-hls-player)
![npm bundle size](https://img.shields.io/bundlephobia/min/@marcosalberto/react-hls-player)

## Fork

This fork was made to update the hls.js version to a newer one, its using the 1.2.3

## Introduction

`react-hls-player` is a simple HLS live stream player.
It uses [hls.js](https://github.com/video-dev/hls.js) to play your hls live stream if your browser supports `html 5 video` and `MediaSource Extension`.

## Examples

### Using the ReactHlsPlayer component

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import ReactHlsPlayer from '@marcosalberto/react-hls-player';

ReactDOM.render(
  <ReactHlsPlayer
    src="https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8"
    autoPlay={false}
    controls={true}
    width="100%"
    height="auto"
  />,
  document.getElementById('app')
);
```

### Using hlsConfig (advanced use case)

All available config properties can be found on the [Fine Tuning](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning) section of the Hls.js API.md

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import ReactHlsPlayer from '@marcosalberto/react-hls-player';

ReactDOM.render(
  <ReactHlsPlayer
    src="https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8"
    hlsConfig={{
      maxLoadingDelay: 4,
      minAutoBitrate: 0,
      lowLatencyMode: true,
    }}
  />,
  document.getElementById('app')
);
```

### Using playerRef

The `playerRef` returns a ref to the underlying video component, and as such will give you access to all video component properties and methods.

```javascript
import React from 'react';
import ReactHlsPlayer from '@marcosalberto/react-hls-player';

function MyCustomComponent() {
  const playerRef = React.useRef();

  function playVideo() {
    playerRef.current.play();
  }

  function pauseVideo() {
    playerRef.current.pause();
  }

  function toggleControls() {
    playerRef.current.controls = !playerRef.current.controls;
  }

  return (
    <ReactHlsPlayer
      playerRef={playerRef}
      src="https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8"
    />
  );
}

ReactDOM.render(<MyCustomComponent />, document.getElementById('app'));
```

You can also listen to events of the video

```javascript
import React from 'react';
import ReactHlsPlayer from '@marcosalberto/react-hls-player';

function MyCustomComponent() {
  const playerRef = React.useRef();

  React.useEffect(() => {
    function fireOnVideoStart() {
      // Do some stuff when the video starts/resumes playing
    }

    playerRef.current.addEventListener('play', fireOnVideoStart);

    return playerRef.current.removeEventListener('play', fireOnVideoStart);
  }, []);

  React.useEffect(() => {
    function fireOnVideoEnd() {
      // Do some stuff when the video ends
    }

    playerRef.current.addEventListener('ended', fireOnVideoEnd);

    return playerRef.current.removeEventListener('ended', fireOnVideoEnd);
  }, []);

  return (
    <ReactHlsPlayer
      playerRef={playerRef}
      src="https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8"
    />
  );
}

ReactDOM.render(<MyCustomComponent />, document.getElementById('app'));
```

## Props

All [video properties](https://www.w3schools.com/tags/att_video_poster.asp) are supported and passed down to the underlying video component

| Prop                     | Description                                                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| src `String`, `required` | The hls url that you want to play                                                                                       |
| autoPlay `Boolean`       | Autoplay when component is ready. Defaults to `false`                                                                   |
| controls `Boolean`       | Whether or not to show the playback controls. Defaults to `false`                                                       |
| width `Number`           | Video width. Defaults to `100%`                                                                                         |
| height `Number`          | Video height. Defaults to `auto`                                                                                        |
| hlsConfig `Object`       | `hls.js` config, you can see all config [here](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning) |
| playerRef `React Ref`    | Pass in your own ref to interact with the video player directly. This will override the default ref.                    |

### Additional Notes

By default, the HLS config will have `enableWorker` set to `false`. There have been issues with the HLS.js library that breaks some React apps, so I've disabled it to prevent people from running in to this issue. If you want to enable it and see if it works with your React app, you can simply pass in `enableWorker: true` to the `hlsConfig` prop object. [See this issue for more information](https://github.com/video-dev/hls.js/issues/2064)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://www.marcochavez.info/"><img src="https://avatars0.githubusercontent.com/u/43889446?v=4" width="100px;" alt=""/><br /><sub><b>Marco Chavez</b></sub></a><br /><a href="https://github.com/devcshort/react-hls/commits?author=mxrcochxvez" title="Code">💻</a></td>
    <td align="center"><a href="https://www.chrisrshort.com"><img src="https://avatars3.githubusercontent.com/u/13677134?v=4" width="100px;" alt=""/><br /><sub><b>Chris Short</b></sub></a><br /><a href="https://github.com/devcshort/react-hls/commits?author=devcshort" title="Code">💻</a> <a href="#projectManagement-devcshort" title="Project Management">📆</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
