[Back to Home](README)
# Collaboration

## Overview

This section is dedicated to shed some light on tools we use to make development in teams more streamlined and convenient, and development output consistent.

## GIT
*Git* is currently the most popular implementation of a distributed version control system, an actively maintained open source project originally developed in 2005 by Linus Torvalds, the creator of the Linux operating system kernel. There are many articles and tutorials dedicated to what is Git, what it does and how to use it - the basics of Git can be found for example [here](https://gist.github.com/blackfalcon/8428401). We strongly advise to get familiar at least with these basics, it will make your life easier (and consequently lives of your "teammates" as well).


### Setting your email address for *every* repository on your computer ###
```
#!bash

git config --global user.email "developer@sld.gs"
```

### Setting your email address for a single repository ###

This will override your global email we set earlier for one repository.
```
#!bash

git config user.email "developer@sld.gs"
```

## GULP.JS ##
Taken from [gulp.js](http://gulpjs.com/): "*Gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something.*". What this means is that gulp solves the problem of repetition. Many of the tasks that web developers find themselves doing over and over on a daily basis can be simplified by becoming automated. Automating repetitive tasks = more time to do non repetitive tasks = more productivity.

Gulp is a javascript task runner that lets you automate tasks such as:

* bundling and minifying libraries and stylesheets
* refreshing your browser when you save a file
* quickly running unit tests
* running code analysis
* Less/Sass to CSS compilation
* copying modified files to an output directory

There are a lot of articles and tutorials for using gulp ([this is one of the more comprehensive ones](https://css-tricks.com/gulp-for-beginners/)), so feel free to google for the one that suits your style of learning the most.
