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
kill process Awesome...

Just for good measure check to make sure you don't have excess bash processes running