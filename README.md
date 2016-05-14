# audio-player [![npm](https://img.shields.io/npm/v/audio-player.svg)](https://www.npmjs.com/package/audio-player)

[![Build Status](https://travis-ci.org/danigb/audio-player.svg?branch=master)](https://travis-ci.org/danigb/audio-player) [![Code Climate](https://codeclimate.com/github/danigb/audio-player/badges/gpa.svg)](https://codeclimate.com/github/danigb/audio-player) [![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](https://github.com/feross/standard) [![license](https://img.shields.io/npm/l/audio-player.svg)](https://www.npmjs.com/package/audio-player)

Flexible audio player for browser

```js
var ac = new AudioContext()
var player = require('audio-player')

var kick = player(ac, <AudioBuffer>)
kick.play()
```

## Features

#### Create players using a key to <AudioBuffer> object

```js
var drums = player(ac, {
  kick: <AudioBuffer>,
  snare: <AudioBuffer>,
  hihat: <AudioBuffer>
})
drums.play('kick')
drums.play('snare')
```

#### Map name notes to midi (and oposite)

```js
var samples = { 'C2': <AudioBuffer>, 'Db2': <AudioBuffer>, ... }
var piano = player(ac, samples, { midi: true })
piano.play(69) // => Plays 'A4'
piano.play('C#2') // => Plays 'Db2'
```

#### Start and stop control

Unlike AudioBufferSourceNode, you can call `start` several times. Also, the `stop` function stops all the sounds.

```js
var longSound = player(ac, <AudioBuffer>)
longSound.start() // one sample playing
longSound.start() // other sample playing (at same time)
longSound.stop() // stop both sounds
```

#### Events

```js
var drums = player(ac, { kick: ..., snare: ..., hihat ... })
drums.onstarted = function (e) {
  console.log('start', e.name)
}
drums.onended = function (e) {
  console.log('ended', e.name)
}
drums.start('kick') // console logs 'started kick'
// console.logs 'ended kick' when sound stops
```

#### Amplitude envelope control

#### Basic filtering

## Install

Via npm: `npm i --save audio-player` or grab the [browser ready file](https://raw.githubusercontent.com/danigb/audio-player/master/dist/audio-player.min.js) (4kb) which exports `loadAudio` as window global.

## Usage

<a name="load"></a>

The API is very simple: `player(ac, source, options)`

| Param | Type | Description |
| --- | --- | --- |
| ac | <code>AudioContext</code> | the audio context |
| source | <code>Object</code> | the object to be loaded |
| options | <code>Object</code> | (Optional) the load options for that object |


## Run tests and examples

To run the test, clone this repo and:

```bash
npm install
npm test
```

To run the example:

```bash
npm i -g beefy
beefy example/example.js
```

## License

MIT License
