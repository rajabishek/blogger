---
title: Meet Yarn - improvement over npm
date: 2016-11-30 19:50:35
tags:
---

## Whats the problem with npm ?
It seems like almost every other week there is a new JavaScript library taking the web community by storm. The community is increasingly vibrant, diverse and is moving rapidly on multiple fronts.

<!-- more -->

As we all know NPM was introduced to solve dependency management for JavaScript and then it quickly became the default package manager for Node.js. Since inception developers have been using npm for both frontend and backend dependency management. Sometimes good is not good enough. The NPM package manager had the following problems:
- The packages installed via npm were stored in the `node_modules` directory. Running `npm install` from the console after deleting the `node_modules` directory **re-downloaded each and every package** along with their dependencies, **taking up a lot of time**.
- NPM always installs each dependency one after the other. Remember when we were grabbing a coffee after running `npm install` on console. Why can't the downloads be parallelized ?
- The npm package manager does not provide **offline installation** from any local cache.

## Meet Yarn
Yarn is the newest package manager from facebook as a replacement for npm. It improves over features provided by the npm package manager. The yarn package manager was designed with keeping 3 principles in mind - Speed, Security & Reliability. Its important to remember here that yarn is an improvement over npm. The packages are the same as on the NPM registry. Yarn is basically a new installer, where NPM structure and **registry is the same**.

## Speed

The yarn package manager is **2 to 7x faster** when compared to npm. This good performance comes from an interesting cache implementation. Whenever we install a package through yarn it caches it, so anytime we request for an installation of a package, it will first try to install it from its cache. By caching the packages in this way the npm packages can be installed without an internet connection with yarn. This comes in handy reducing the build time in Continuous Integration(CI) servers. They no longer rely on an internet connection and the npm registry, and your tests will pass even when npm goes down. It also executes the package downloads in parallel threads to make the best use of resources. 

## Security
The package installation process is secure. Anytime a package is installed and is about to be executed, it verifies the integrity of the package by using the **package’s checksum**. The same checksum method is also used to check if the caching process of the package was successful or not. When an incorrect checksum is detected, the packages is again re-downloaded from the original source.

## Reliability
When you run `yarn` from console(equivalent to `npm install`), it creates `yarn.lock` file. This file guarantees that an install that worked on one system will work exactly the same way on any other system. The lock file keeps track of the exact package version installed in `node_modules` directory. It is recommended to add this file to version control since it gives the package version consistency across all environments.

## Installation
You can install `yarn` globally through npm.
```
npm install -g yarn
```
To update and keep up with the latest version of yarn, you can run the following.
```
yarn self-update
```

## NPM vs Yarn Cheat Sheet
The yarn CLI replaces npm in your development workflow, either with a matching command or a new, similar command.
- `npm install` === `yarn`
Installation is the default behavior.
- `npm install babel-cli --save` === `yarn add babel-cli`
The babel-cli package is downloaded in the `node_modules` directory and saved to the package.json in the dependencies section immediately.
- `npm uninstall babel-cli --save` === `yarn remove babel-cli`
To not use --save option explicitly while uninstalling a package to remove the entry from the package.json file can be defaulted in NPM by running the command `npm config set save true` on console. But this is not needed in the yarn package manager, adding and removing entries from package.json is default in yarn.
- `npm install babel-cli --save-dev` === `yarn add babel-cli --dev`
The babel-cli package is downloaded in the `node_modules` directory and saved to the package.json in the dev dependencies section immediately.
- `npm update --save` === `yarn upgrade`
The package version number moves up and an upgrade is happening. Its good that yarn called it `upgrade` instead of `update` since that is what is happening.
- `npm install babel-cli --global` === `yarn global add babel-cli`
This installs the package globally. Infact you can use yarn to manage itself globally by running `yarn global add yarn` from the console. For following commands, if you know NPM you are ready to go.
```
npm init        → yarn init
npm link        → yarn link
npm outdated    → yarn outdated
npm publish     → yarn publish
npm run         → yarn run
npm cache clean → yarn cache clean
npm login       → yarn login
npm logout      → yarn logout
npm test        → yarn test
```

## New features
Yarn has some great new features that NPM doesn’t have. You can check the licenses of your dependencies and you can also generate your license dependencies using the following commands.
```
yarn licenses 
yarn licenses generate
```
From the console you can also run `yarn why <package-name>` to identify why this package is installed and which other packages are dependent on it. If you have some time, thank [Oliver Combe](https://github.com/ocombe) for this feature.
```
yarn why babel-cli
```

## Conclusion
Yarn in its infancy has already brought significant improvements in the way JavaScript packages are fetched from global registries into local environments, especially with regard to speed and security. As far as I have worked with yarn it looks amazing and I have no complaints. Moreover the project being backed by big tech giants like Google and Facebook makes me feel positive that it can become the official npm package manager soon.