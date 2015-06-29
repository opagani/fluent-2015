# Using ES6 with React
[Brian Holt (Netflix)](http://netflix.com/)  
[Details](http://fluentconf.com/javascript-html-2015/public/schedule/detail/39074)  
[Slides](http://cdn.oreillystatic.com/en/assets/1/event/125/Gitting%20More%20Out%20of%20Git%20Presentation.pdf)  
[Github](https://github.com/btholt/es6-react-pres)  

Learn about React.js with ES6.

## Notes

## Summary

The point of this presentation is to:

- Teach you React. It assumes no prior knowledge.
- Teach you JSX. It makes writing React so much more pleasant.
- Teach you (some) ES6. This presentation only assumes ES5 familiarity.
- Teach you React with ES6. It shows you the newer paradigm of coding React using ES6 classes.
- Teach you server-side rendering on React using Koa.
- **Not** teach you Flux. We won't be going over it during this workshop.

## How it works

The completed project lives in the [completed/](https://github.com/btholt/es6-react-pres/tree/master/completed) directory. I've left for you a skeleton of the project to code up in the [empty/](https://github.com/btholt/es6-react-pres/tree/master/empty) directory. You can recreate the presentation without me there using [speakersNotes.md](https://github.com/btholt/es6-react-pres/tree/master/speakersNotes.md).

## Requirements

You need to install [iojs](https://iojs.org) which is an npm compatible platform originally based on node.js and brings ES6 capabilities.

Install React developer tools chrome plugin:  https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

### How to Run

0. `npm -g install gulp` 
1. `git clone https://github.com/btholt/es6-react-pres.git`
2. `cd es6-react-pres`
1. `npm install`
2. `npm install aliasify --save-dev`
3. `ln -s node_modules/font-awesome/ empty/fa`
4. `cd completed`
5. `gulp scripts`
6. `iojs app.js`
7. Navigate to `localhost:3000` in web browser and you should see the Netflix app running

Note:  In our workshop we will creating the same app in the empty directory.

## How to run in offline mode

In order to switch to offline mode (which doesn't rely on the omdb API but instead serves dummy data) change all references of `var omdb = require('omdb-client');` to `var omdb = require('./fake-omdb-client');`. You may also have to mess with the paths to images a bit.

## OMDb

The example app makes use of the [OMDb API](http://www.omdbapi.com/).