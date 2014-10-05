================
TinTin++ Modules
================
The included modules are super alpha and currently for demonstration purposes only.

Note: Some of what is covered below is not yet finished or committed to the repository. This documentation is meant to describe how things _will_ work.

-----
About
-----
Most of us keep our own set of scripts, hardcoded with our own personal settings. They're not portable, we can't share them, and we can't collaboratively test them. The intent of this repository is to overcome that by establishing a set of standards and methods for building redistributable TinTin++ scripts.

To do this, we have to separate all configuration from function (tricky with the TinTin toy language). I've come up with some basic methods for doing this and hopefully by sharing them, others may come up with even better ideas.


This repository is divided into "libs" and "modules."  Libs consists of a set of small routines that perform common tasks. These are two small to be their own modules, and they provided aliases and routines as dependencies for the modules.

Modules are standard, non-specific features, that are commonly implemented over and over by different users.

------------
Installation
------------
To install the modules, clone this repository into your existing code base::

    cd <your-tintin-files>
    git clone git@github.com:tintinplusplus/tintinplusplus-modules.git shared

This will clone the modules framework into your code base in the 'shared' directory.


-----
Usage
-----
The cfg directory includes sample configuration files for the included modules. These should be copied to your own cfg directory (outside of the repository), and modified for your personal use.
To include the shared modules in your own code, add the following to your existing configuration::

    #var MODULES.PATHS.ROOT {shared};
    #var MODULES.PATHS.CFG  {cfg};
    #var MODULES.PATHS.DATA {var};
    #var MODULES.PATHS.TMP  {/tmp/tintin};

    #nop A table containing the modules we want to load. Set to 1 for enable, 0 for disable.;
    #var MODULES.ENABLE {module_manager}{1};
    #var MODULES.ENABLE {session_manager}{1};
    #var MODULES.ENABLE {reload}{1};
    #var MODULES.ENABLE {tmuxui}{1};
    #var MODULES.ENABLE {mapper}{1};
    #var MODULES.ENABLE {parserooms}{1}
    #var MODULES.ENABLE {multisession}{1};
    #var MODULES.ENABLE {monsterdb}{1};
    #var MODULES.ENABLE {itemdb}{1};

    #nop Initialize the shared modules. ;
    #read shared/init.tin;

All modules are optional. Once loaded, you can use "help modules" to get started.
