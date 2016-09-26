When trying to run a cmd file in the .bin folder of node_modules

If you are on a bash prompt such as the build in terminal in PhpStrom when I have that set to use sh.exe then use the forward / and no .cmd extension 

Like this paste  ./node_modules/.bin/electron-rebuild in the terminal window.  Nothing before this ie not npm run or node just paste above line

In non sh.exe ie regular command prompt in windows use 
 .\node_modules\.bin\electron-rebuild.cmd

