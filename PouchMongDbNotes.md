In main.js you need to remove the requires and replace them with

Replace

    var app = require('app');
    var BrowserWindow = require('browser-window');


With This

	const electron = require('electron');
    // Module to control application life.
    const app = electron.app;
    // Module to create native browser window.
    const BrowserWindow = electron.BrowserWindow

Same thing in 

Replace 

    var app, Menu, ApplicationMenu;
    
    app = require('app');
    Menu = require('menu');

With
    
    var  Menu, ApplicationMenu;
    
    const electron = require('electron');
    const app = electron.app;
    Menu = electron.Menu;