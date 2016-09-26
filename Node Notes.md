When trying to run a cmd file in the .bin folder of node_modules

If you are on a bash prompt that I have changed terminal in PhpStrom you don't need the .cmd extension else if running in normal cmd add the extensionS

The below command works

    ./node_modules/.bin/electron-rebuild -w leveldown -p
also just -w works no -p needed

Also for help

    ./node_modules/.bin/electron-rebuild -h


The command below on electron-rebuild site does not work use above
./node_modules/.bin/electron-rebuild

Also if the node_modules keeps being added in case you need to delete it
Restart PhpStorm
kill process Awesome...
kill any bash processes

Maybe just try closing PhpStorms terminal

NEVER MIND just restart pc maybe later I can figure out which process is still running