If you get error when using Bootstrap in Aurelia

Error: (SystemJS) Bootstrap's JavaScript requires jQuery(…)

AshleyGrant commented on Jun 22
I helped you with this question on Stack Overflow, but I've since investigated a bit more. You can actually remove jQuery as a dependency for your application (so delete it from the dependencies in your package.json). After doing this, I recommend removing the map section of config.js, deleting the jspm_packages folder, and rerunning jspm install.

After doing this, you can actually access bootstrap's jQuery by doing this:

import $ from 'bootstrap';
If doing this doesn't work for you, then your best bet would be to file an issue with JSPM, as the issue you're experiencing is with JSPM and not Aurelia. https://github.com/jspm/jspm-cli
