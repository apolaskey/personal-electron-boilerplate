[![Gitter](https://badges.gitter.im/apolaskey/personal-electron-boilerplate.svg)](https://gitter.im/apolaskey/personal-electron-boilerplate?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)
[![Dependencies](https://david-dm.org/apolaskey/personal-electron-boilerplate.svg)](https://david-dm.org/apolaskey/personal-electron-boilerplate#info=dependencies)
[![img](https://david-dm.org/apolaskey/personal-electron-boilerplate/dev-status.svg)](https://david-dm.org/apolaskey/personal-electron-boilerplate/#info=devDependencies)
[![img](https://david-dm.org/apolaskey/personal-electron-boilerplate/peer-status.svg)](https://david-dm.org/apolaskey/personal-electron-boilerplate/#info=peerDependenciess)
[![Known Vulnerabilities](https://snyk.io/test/github/apolaskey/personal-electron-boilerplate/badge.svg)](https://snyk.io/test/github/apolaskey/personal-electron-boilerplate)
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)
[![Unix Status](https://travis-ci.org/apolaskey/personal-electron-boilerplate.svg?branch=master)](https://travis-ci.org/apolaskey/personal-electron-boilerplate)

# Motivation
To create a boilerplate for rapid prototyping of ideas with a fairly robust platform

# Completed / Planned Feature List
- [x] Electron Installation and Setup
- [x] React Framework w/Redux support added
- [ ] React DevTools support added
- [ ] Electron DevTools support added
- [x] Babel w/ES6 + 7 support
- [ ] Spectron (Electron Functional Testing)
- [x] Ava (Concurrent Test Runner)
- [x] Webpack Integration
- [x] BluebrintJS Integration (React Components)
- [x] Bulma CSS Integration (Grid Framework support largely)
- [ ] Electron Persistent Store Support (Configs)


## Developing
The below should over a no bullshit setup experience if followed; otherwise open an issue and let me know what you encountered.

## Usage
To make this feel like your project the following actions should be done

* Fork or clone + copy files to a new repository
* Edit "package.json" and change the following JSON fields: ``author`` ``name`` ``productName`` ``description`` ``repository -> url``
* Edit "index.ejs" with a new title (This is an HTML template to bootstrap the application off of)
* From here you can follow the frontend application flow starting from ``app -> index.jsx``
* Electron application flow will always start at ``app -> main.js``
* ANY QUESTIONS YOU CAN JUST OPEN AN ISSUE :)

### First Time Setup

The below are global tools that must be installed to build / package this application

[NodeJS](https://nodejs.org/en/download/) :: ``version must be >= 6.6.0``

[Electron Setup](https://electron.atom.io/) :: ``npm install -g electron``

[Ava](https://github.com/avajs/ava) :: ``npm install -g ava``

[Run-All](https://github.com/mysticatea/npm-run-all/blob/master/docs/run-p.md) :: ``npm install -g npm-run-all``

Build Project Setup & Scripts :: ``npm install && npm run build``

### Build Scripts
Start application in prod mode :: ``npm start``

Start application in dev mode :: ``npm run start-dev``

Start electron only :: ``npm run start-dev:electron``
* Cavaet to this is the bootstrap index.js might get out-of-date since that's not HMR'd

Start webpack HMR only :: ``npm run hot``

Build output :: ``npm run build``

Lint source :: ``npm test``

Run integration tests :: ``npm run build && npm run it-test``

Package application :: ``npm run package:${os-type}`` where ``${os-type}`` is "windows", "linux", "osx"

## Patterns and Practices
Below are the basic towards how the project is setup and in general just how things work.

### Project Directory Structure Overview

All test scripts are to go to ``tests/**`` and be suffixed with ``.test.js`` ie. ``FooBar.test.js``

Anything related to UI for the application goes into ``app/renderer/**``

Anything related to just general purpose work goes into ``app/main/**``

Branching / Merging is Gitflow with two defined core branches

* ``master`` :: Stable Release (Build that passed everything)

* ``stable`` :: Nightly Release (Build that passed automated tests)

* ``latest`` :: Unstable Release (Purely staged work; might work, might not)

Application "Main" is at ``app/index.js``

Application routing is configured at ``app/renderer/editor-routes.js``

# Known Issues

Working from a synchronized workspace:
* If your working out of a dropbox folder on multiple machines you may need to remove the node_modules folder and reinstall
when switching between Windows / Mac / Linux you can quickly attempt an ``npm rebuild`` but I can't gurantee it will work.

White page when running ``npm run start-dev``
* This usually happens if the Electron Window is minimized while Webpack is building out the HMR server
just refresh the page (Ctrl/Cmd R or View -> Reload)

Webpack HMR not working for index.ejs or index.js
* I didn't spend a ton of effort getting these to be replaceable just because it's rare to go in here and Electron
requires these to be present on startup.

Warning like: ``npm WARN invalid config loglevel="notice"``
* To fix the above just run ``npm config set loglevel warn`` the above occurs on Windows environments
running NPM >= 6 due to the newer auto-enabled package-lock.json functionality

Warning like: ``MaxListenersExceededWarning: Possible EventEmitter memory leak detected. `` is displayed
* To fix the above issue update NPM to ``>= 4.4.4`` can be done by doing ``npm update -g npm``