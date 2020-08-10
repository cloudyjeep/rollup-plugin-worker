# rollup-plugin-worker

Adds code splitting for module Workers and Worklets to Rollup.

## Notes

* Only for Rollup >= 1.11.0
* Does not include any module loader. See [example](example)
* Worklet calls must follow format `*.*Worklet.addModule(...)`
* File paths are resolved using Rollup

## Installation

```sh
yarn add -D git+https://github.com/cloudyjeep/rollup-plugin-worker#semver:^2.0.0
```

## Usage

**rollup.config.js**

```javascript
import worker from 'rollup-plugin-worker';

export default {
  input: 'main.js',
  output: {
    dir: 'dist/system',
    format: 'system'
  },
  plugins: [
    worker()
  ]
};
```

**main.js**

```javascript
// workers have to be of `type: 'module'`
new Worker('./dedicated-worker.js', { type: 'module' })
new SharedWorker('./shared-worker.js', { type: 'module' })
navigator.serviceWorker.register('./sw.js', { type: 'module' })

// worklets are always modules
myAudioContext.audioWorklet.addModule('./audio-worklet.js')
CSS.paintWorklet.addModule('./paint-worklet.js')
CSS.layoutWorklet.addModule('./layout-worklet.js')
CSS.animationWorklet.addModule('./animation-worklet.js')
```
