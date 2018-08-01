# Vuex WebExtensions

[![NPM](https://nodei.co/npm/vuex-webextensions.png)](https://npmjs.org/package/vuex-webextensions)

[![Build Status](https://travis-ci.org/MitsuhaKitsune/vuex-webextensions.svg?branch=master)](https://travis-ci.org/MitsuhaKitsune/vuex-webextensions)

A Node.JS module to use Vuex on WebExtensions on "shared" context, the module allows you to start several instances of Vuex store and keep them synchronized throught WebExtensions messaging API.

Uses the Vuex store instance on background script as master, and replicate the state of master to others instances on diferent context (popup or content scripts), when you commit any mutation to any store instance the rest will also be updated automatically.

You can work with the Vuex store like a unic instance (or standart Vue.js application), without worry for the different WebExtensions contexts, the module gona solve all WebExtensions problems for you automatically.

## Installation

Run the following command inside your WebExtensions project to install the module:

`npm install vuex-webextensions --save`

## Usage

Import the module into your store file:

```javascript
import VuexWebExtensions from "vuex-webextensions";
```

Then add it as plugin on Vuex store initialization:

```javascript
export default new Vuex.Store({
  ...
  plugins: [VuexWebExtensions()]
});
```

All done!

## Persistent states

> ⚠ Persistent states make use of `LocalStorage` to save the states in your browser, to use it, you should grant `storage` permision to your webextension

You can establish through the options of the plugin the states that you want to be persistent, your data will be preserved after the restart of the extension or the browser.

It is established passing the state names through persistentStates option in array:

```javascript
export default new Vuex.Store({
  ...
  plugins: [VuexWebExtensions({
      persistentStates: ['stateone', 'statetwo']
    })]
});
```

Then `stateone` and `statetwo` gona have the value commited by last mutation after extension or browser restart.

## Changelog

##### 1.1.1

- Fix plugin initialization on injected content scripts

##### 1.1.0

- Implemented optional persistence of states
- Now the plugin are minimized on build

##### 1.0.2

- Cleanup of redundant code

##### 1.0.1

- Remove old files from distribution

##### 1.0.0

> ⚠ This version have a breaking changes please check the new install method and remove the old install on your scripts

- Convert module as "true" plugin of vuex

##### 0.1.1

- Added lint and some prepublish methods to the package
- Solve some issues detected by linter
- Added Travis CI for automatic build and tests

##### 0.1.0

- First version

## Contribute

If you encounter a problem, issue or question feel free to open a new issue on this repository.

If you have some improvements, new features or fixes feel free to fork this repository and send a pull request.

## Pending work

- Improve example
- Add tests and coverage
- Publish to Awesome Vue.js lists when no more pending work
