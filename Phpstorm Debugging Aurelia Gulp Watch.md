# Aurelia Gulp Watch PhpStorm Debugging #

# Setup Phpstorm #
Create a debug config

Run > Edit Configurations > Plus Sign > Javascript Debug

Name: gulp-watch or whatever

Url: localhost:9000

## Source Maps ##
You will not hit break point if your sourcemaps are not configured correctly

## Not hitting breakpoints becuase folder is in subfolder like client ##
Mark folder as resource root

**Make sure the source path is correct in the gulp write sourcmaps**

In Aurelia Navigation Skeleton tasks/build the     .pipe(sourcemaps.write('.', {includeContent: false, sourceRoot: '../src'}))

 sourceRoot: '/src' is wrong make sure it points to your source folder replace with sourceRoot: '../src'
For whatever reason debugging only works in sourceRoot is a relative path to your output folder
 

## Infinate loop on breakpoint ##

infinite loop happens on dirty checked getter values such as below statement in welcome.js

     get fullName() {
    return `${this.firstName} ${this.lastName}`;
      }

**Fix by** 

uncomment

  @computedFrom('firstName', 'lastName')
and 
import {computedFrom} from 'aurelia-framework';

As per below instructions

  //Getters can't be directly observed, so they must be dirty checked.
  //However, if you tell Aurelia the dependencies, it no longer needs to dirty check the property.
  //To optimize by declaring the properties that this getter is computed from, uncomment the line below
  //as well as the corresponding import above.
  @computedFrom('firstName', 'lastName')
