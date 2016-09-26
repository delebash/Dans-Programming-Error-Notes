When trying to run a cmd file in the .bin folder of node_modules

If you are on a bash prompt that I have changed terminal in PhpStrom you don't need the .cmd extension else if running in normal cmd add the extensionS

The below command works
./node_modules/.bin/electron-rebuild -w leveldown -p

The standard command does not
./node_modules/.bin/electron-rebuild

Also for help
./node_modules/.bin/electron-rebuild -h

