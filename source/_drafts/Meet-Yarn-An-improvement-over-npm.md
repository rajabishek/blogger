---
title: Meet Yarn - improvement over npm
tags:
---
## What is this ?
Yarn is the newest package manager from facebook as a replacement for npm. It improves over features provided by the npm package manager.

<!-- more -->

## Whats the problem with npm ?
It seems like almost every other week there is a new JavaScript library taking the web community by storm. The community is increasingly vibrant, diverse and is moving rapidly on multiple fronts.

As we all know NPM was introduced to solve dependency management for JavaScript and then it quickly became the default package manager for Node.js. Since inception developers have been using npm for both frontend and backend dependency management. Sometimes good is not good enough. The NPM package manager had the following problems:
- The packages installed via npm were stored in the `node_modules` directory. Running `npm install` from the console after deleting the `node_modules` directory **re-downloaded each and every package** along with their dependencies, **taking up a lot of time**.
- NPM always installs each dependency one after the other. Remember when we were grabbing a coffee after running `npm install` on console. Why can't the downloads be parallelized ?
- The npm package manager does not provide **offline installation** from any local cache.

## Meet Yarn
The yarn package manager was designed with keeping these 3 principles in mind.
1. Speed
1. Security
1. Reliability

The yarn package manager is 2 to 7x faster when compared to npm. This good performance comes from an interesting cache implementation. Whenever we install a package through yarn it caches it, so anytime we request for an installation of a package, it will first try to install it from its cache. It also executes the package downloads in parallel threads to make the best use of resources.