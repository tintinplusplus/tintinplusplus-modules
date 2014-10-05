================
TinTin++ Modules
================
The included modules are super alpha and currently for demonstration purposes only.

Note: Some of what is covered below is not yet finished or committed to the repository. **This documentation is meant to describe how modules are intended to work.**

-----
About
-----
Most of us keep our own set of scripts, hard-coded with our own personal settings. They're not portable, we can't share them, and we can't collaboratively test them. The intent of this repository is to overcome that by establishing a set of standards and methods for building redistributable TinTin++ scripts.

To do this, we have to separate all configuration from function (tricky with the TinTin toy language). I've come up with some basic methods for doing this and hopefully by sharing them, others may come up with even better ideas.

This is done through conforming to acknowledged standards and a liberal amount of TinTin hackery.

This repository is divided into "libs" and "modules."  Libs consists of a set of small routines that perform common tasks. These are two small to be their own modules, and they provided aliases and routines as dependencies for the modules.

Modules are standard, non-specific features, that are commonly implemented over and over by different users.

------------
Installation
------------
There are several ways to add the modules to your existing library.
NOTE: Because TinTin user's are not necessarily comfortable with git, I've added explicit setup instructions.

**Installing as a Static Archive (best for users not comfortable with git)**::

    cd $MUDFILES
    wget https://github.com/tintinplusplus/tintinplusplus-modules/archive/master.zip
    unzip master.zip
    unzip master.zip
    mv tintinplusplus-modules-master share
    rm -i master.zip

The repository will be static and not managed through a version control tool. You'll need to manually check for updates and replace this directory as necessary. In the future, I will work on including a module that will allow users to update the repository through a command that can be run directly in TinTin++.

**Installing as a Standalone Git Repository**::

    cd $MUDFILES
    git clone https://github.com/tintinplusplus/tintinplusplus-modules.git share

If your existing codebase is already a git repository, then you'll want to make it ignore the 'share' directory::

    echo "\n# Do not track share directory"
    echo "share\n" >> .gitignore

To update your modules (share directory)::

    cd share
    git pull

If the share directory has changes that should be discarded when updating, you can discard those changes and update to the latest release with::

    cd share
    git fetch origin
    git reset --hard origin/master


**Installing as a Submodule with Branch Tracking (Best for Contributors)**::

    cd $MUDFILES
    git submodule add git@github.com:tintinplusplus/tintinplusplus-modules.git share
    git config -f .gitmodules submodule.share.branch master
    cd share && git branch -u origin/master master
    cd .. && git add .gitmodules share
    git commit .gitmodules share -m 'added share as tracked submodule'

This configures the modules repository (share directory) as a submodule in your existing git repository, with branch tracking (without branch tracking, the head will become detached every time a change is made). The branch tracking assumes that you're intending to commit directly to master, which is what is happening now as the modules repository is early alpha and there is not yet a production release.


-----
Usage
-----
The cfg directory includes sample configuration files for the included modules. These should be copied to your own cfg directory (outside of the repository), and modified for your personal use.
To include the shared modules in your own code, add the following to your existing configuration::

    #var MODULES.PATHS.ROOT {share};
    #var MODULES.PATHS.CFG  {cfg};
    #var MODULES.PATHS.DATA {data};
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
