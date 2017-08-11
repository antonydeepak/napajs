[![Build Status for Linux/MacOS](https://travis-ci.org/Microsoft/napajs.svg?branch=master)](https://travis-ci.org/Microsoft/napajs)
[![Build Status for Windows](https://ci.appveyor.com/api/projects/status/github/Microsoft/napajs?branch=master&svg=true)](https://ci.appveyor.com/project/daiyip/napajs)
[![npm version](https://badge.fury.io/js/napajs.svg)](https://www.npmjs.com/package/napajs)
[![Downloads](https://img.shields.io/npm/dm/napajs.svg)](https://www.npmjs.com/package/napajs)

# Napa.js
Napa.js is a multi-threaded JavaScript runtime built on [V8](https://github.com/v8/v8). Napa was originally designed to develop highly iterative services with non-compromised performance in Bing. As it evolved, we found it useful to complement [Node.js](https://nodejs.org) in CPU-bound tasks by executing JavaScript in multiple isolated V8 zones and administering communications among them. Even though Napa.js is a Node.js module, it can also be embedded in a host process without a Node.js dependency.

## Supported OS and Compilers
Napa.js requires C++ compiler that supports [C++14](https://en.wikipedia.org/wiki/C%2B%2B14), currently we have tested following OS/compiler combinations: 
* Windows: 7+ with VC 2015+ (MSVC14.0+)
* Linux: Ubuntu 14.04 LTS, 16.04 TLS, with gcc 5.4+ 
* OSX: 10.11 (Yosemite), Apple LLVM 7.0.2 (clang-700.1.18)

## Installation
### Prerequisites
* Install C++ compilers that support C++14:
    * Windows: Visual C++ Build Tools [2015](http://landinghub.visualstudio.com/visual-cpp-build-tools) / [2017](https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017), or [Visual Studio](https://www.visualstudio.com/vs/cplusplus/)
    * Linux: [via Apt-get](https://askubuntu.com/questions/618474/how-to-install-the-latest-gcurrently-5-1-in-ubuntucurrently-14-04)
    * OSX: `xcode-select --install`
* Install CMake: 
    * Linux: [via Apt-get](https://askubuntu.com/questions/355565/how-to-install-latest-cmake-version-in-linux-ubuntu-from-command-line)
    * OSX: [via brew](http://macappstore.org/cmake/)
    * [Download or build](https://cmake.org/install/)
* Install cmake-js: `npm install -g cmake-js`

### Install Napa.js
```
npm install napajs
```
\* *You can also [build Napa.js from source](https://github.com/Microsoft/napajs/wiki/build-napa.js-from-source).*

## Quick Start
```js
var napa = require('napajs');
var zone1 = napa.zone.create('zone1', { workers: 4} );

// Broadcast code to all 4 workers in 'zone1'.
zone1.broadcast('console.log("hello world");');

// Execute an anonymous function in any worker thread in 'zone1'.
zone1.execute(
    (text) => {
        return text;
    }, 
    ['hello napa'])
    .then((result) => {
        console.log(result.value);
    });
```
More examples:
* [Estimate PI in parallel](./examples/tutorial/estimate-pi-in-parallel)
* [Recursive Fibonacci with multiple JavaScript threads](./examples/tutorial/recursive-fibonacci)
* [Max sub-matrix of 1s with layered parallelism](./examples/tutorial/max-square-sub-matrix)

## Features
- Multi-threaded JavaScript runtime
- Node.js compatible module architecture with NPM support
- API for object transportation, object sharing and synchronization across JavaScript threads
- API for pluggable logging, metric and memory allocator
- Distributed as a Node.js module, as well as supporting embed scenarios

## Documentation
- [Napa.js Home](https://github.com/Microsoft/napajs/wiki)
- [API Reference](./docs/api/index.md)

# Contribute
You can contribute to Napa.js in following ways:

* [Report issues](https://github.com/Microsoft/napajs/issues) and help us verify fixes as they are checked in.
* Review the [source code changes](https://github.com/Microsoft/napajs/pulls).
* Contribute bug fixes.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact opencode@microsoft.com with any additional questions or comments.

# Contacts
* [Mailing list](https://groups.google.com/forum/#!forum/napajs)
