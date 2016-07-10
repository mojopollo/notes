# Web Development Standards

Environment setup, notes, guidelines and standards.

***

## Third Party Development Applications - (Mac)
* SSH Terminal https://iterm2.com/downloads.html
* Spolight Replacement http://www.alfredapp.com/#download
* MySQL Database Management Client - http://www.sequelpro.com/

***

## Install Your Local Package Manager
* Mac OS X: Follow instructions and install http://brew.sh/
* Windows: Follow instructions and install https://chocolatey.org/
* Ubuntu/Debian: You already have apt-get
* Red Hat/CentOS: You already have yum

***

## Install required binaries
* Mac OS X : ```brew install <package-name>```
* Windows: ```choco install <package-name>```
* Ubuntu/Debian : ```sudo apt-get install <package-name>```
* Red Hat/CentOS : ```sudo yum install <package-name>```
* Install the following packages (Mac OS X Example)
```bash
brew update
brew install bash-completion imagemagick ghostscript mcrypt node php55 php55-mcrypt s3cmd ssh-copy-id wget git
```
* Mac OS X / Homebrew, required steps:
```bash
brew install homebrew/php/php55 php55-mcrypt
```

***

## Third Party Development Applications - (Windows)
* SSH Terminal http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
* MySQL Database Management Client - http://www.heidisql.com/

***

## Setting Up Bash Environment - (Mac)
* modify or create your bash profile via the terminal: ```nano ~/.bash_profile```
```bash
# Start - Git branch on bash prompt
function parseGitBranch {
        git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ \[\1\]/'
}

function setBashPrompt {

        local        BLUE="\[\033[0;34m\]"

        # OPTIONAL - if you want to use any of these other colors:
        local RED="\[\033[0;31m\]"
        local LIGHT_RED="\[\033[1;31m\]"
        local GREEN="\[\033[0;32m\]"
        local LIGHT_GREEN="\[\033[1;32m\]"
        local WHITE="\[\033[1;37m\]"
        local LIGHT_GRAY="\[\033[0;37m\]"
        # END OPTIONAL

        local     DEFAULT="\[\033[0m\]"

        # old git prompt
        #PS1="\h:\W \u$BLUE\$(parseGitBranch) $DEFAULT\$"

        # new path prompt
        export PS1="\u@\h \w$LIGHT_GREEN\$(parseGitBranch) $DEFAULT$ "
}

setBashPrompt
# End - Git branch on bash prompt

export CLICOLOR=1
export LSCOLORS=gxBxhxDxfxhxhxhxhxcxcx

alias ll="ls -lah"

# Put color in these commands
alias composer='composer --ansi'
alias grep='grep --color'

# brew bash completion
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

* Now your path inside a Git repo in terminal will more like this:
```bash
mojo@m ~/www/shindiig/website/repo [devel] $
```

***

## Create your default SSH Key
* ```mkdir ~/.ssh/```
* ```cd ~/.ssh/```
* ```ssh-keygen -t rsa``` and press enter 3 times (no password needed, id_rsa is the default name of your key)
* You will now have 2 files in you ~/.ssh/ folder: ```~/.ssh/id_rsa``` and ```~/.ssh/id_rsa.pub```

***

## Update Your Bitbucket SSH Key
* To view your public SSH key, you execute following command:
```bash
cat ~/.ssh/id_rsa.pub
```
* Login into bitbucket.org (Manage Account -> SSH Keys) and add your ```id_rsa.pub```.

***

## Install Composer (PHP)
Download the composer phar file:
```bash
curl -s https://getcomposer.org/installer | php
```
Move the phar file into the bin folder :
```bash
mv composer.phar /usr/local/bin/composer
```
Now you have composer installed :
```bash
composer --version
```

***

## Install Node.js
```bash
brew install node
```
* Note: this also installs the ```npm``` command which allows you install node packages later on.

***

## Check Node.js Version

* We currently use Node.js 0.10.* for appgyver development
* Check that your version of node is 0.10.* with ```node --version```
* If you need to downgrade node, do the following
```bash
brew remove node
brew tap homebrew/boneyard
brew tap homebrew/versions
cd /usr/local/
brew versions node
git checkout 51c3f4d Library/Formula/node.rb
brew install node
```
* Note "git checkout ..." was executed for the specific node version we wanted from the "brew versions node" results: ```0.10.35  git checkout 51c3f4d Library/Formula/node.rb```

***

## Install Bower (Node package)
* Install Bower
```bash
npm install -g bower
```

***

## Install Grunt (Node package)
* Install Bower
```bash
npm install -g grunt
```

***

## Bower (Install jQuery Package Example)
Instead of manually downloading the library/framework and committing in your repository, use the ```bower``` command to manage it for you:
```bash
mkdir my-bower-test
cd my-bower-test
```
Create your bower.json file, this will hold the library names and their prespective versions of all packages installed in your project.
You can just press ```Enter``` through all of the following questions asked to use the default answers.
```bash
bower init
```
To install jQuery use the following command :
```bash
bower install jquery --save
```
the ```--save``` flag will update your bower.json file with the latests version of jQuery.
```bash
cat bower.json
```
will now show your installed library
```json
{
  "dependencies": {
    "jquery": "~2.1.3"
  }
}
```
If for example, you would like to use a different version of jQuery, you change the version in bower.json to
```json
{
  "dependencies": {
    "jquery": "~1.8.0"
  }
}
```
Then use the install sub command which will re-download the libraries with the version specified.
```bash
bower install
```

***

## Sublime Text 3 - Install
* Download latests at http://www.sublimetext.com/3
* Install package control from: https://packagecontrol.io/installation

***

## Sublime Text 3 - Command line shortcut

* In terminal run the following command ```whoami``` and replace the ```<username>``` below with your username
```bash
mkdir ~/bin/
ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl ~/bin/subl
export PATH=/Users/<username>/bin:$PATH
```

***

## Sublime Text 3 - Installing packages
For any packages that need to be installed you will do the following shortcuts:

Note: "Cmd" for Mac's, "Ctrl" for everything else

* Cmd/Ctrl + Shift + P
* Install Package + Enter
* **<package name>** + Enter

***

## JavaScript - Setup linter (JSLint)
* Install sublime package: **JSLint**
* Go to: Sublime -> Preferences -> Package Settings -> JSLint -> "Settings - Default"
* Then go to: Sublime -> Preferences -> Package Settings -> JSLint -> "Settings - User"
* Copy all contents from "Settings - Default" tab to "Settings - User" tab and Save
* In "Settings - User" replace the "options" array with the following and Save:
```json
{
    "options" : [
       "--predef", "['angular', 'document', '\\$', '_', 'JQuery', 'FB']"
        ,"--indent", "2"
        ,"--node"
    ]
}
```
* From now on, all javascript files on Save, will run through JSLint and output errors until you follow the strict guidelines
* Get familiar with common errors and guidelines here: http://www.jslint.com/lint.html
* Get help on fixing the errors here: http://jslinterrors.com/
* The goal is to have "0 errors" on Save

***

***

## CoffeeScript - Setup linter (Part 1 of 3 : Better CoffeeScript)
* Install CoffeeScript :
```bash
$ npm install -g coffee-script
```
* Install sublime package: **Better CoffeeScript**
* Go to: Sublime -> Preferences -> Package Settings -> Better CoffeeScript -> "Settings - User"
* In "Settings - User" , set the following :
```json
{
    "binDir": "coffeescript-install-directory"
}
```
set coffeescript-install-directory to the install directory of the **coffee** command, for example the command :
```bash
$ which coffee
```
returns
```bash
/usr/local/bin/coffee
```
the CoffeeScript install directory is ```/usr/local/bin/``` (without the word "coffee"), so the config looks like:
```json
{
    "binDir": "/usr/local/bin/"
}
```

* Note: ```Alt + Shift + D``` will preview the compiled CoffeeScript code
* Note: this package adds syntax highlight ```Better CoffeeScrip -> CoffeeScript``` which is the syntax you must have lighting for the linter in Part 3 t work

***

## CoffeeScript - Setup linter (Part 2 of 3 : SublimeLinter)
* Install sublime package: **SublimeLinter**

***

## CoffeeScript - Setup linter (Part 3 of 3 : SublimeLinter-coffee)
* Install sublime package: **SublimeLinter-coffee**
* Go to: Sublime -> Preferences -> Package Settings -> SublimeLinter -> "Settings - User"
* make sure the following paths are set to your ```coffee``` binary and ```node``` binary
```json
{
    "coffee_path": "/usr/local/lib/node_modules/coffee-script/bin",
    "node_path": "/usr/local/bin"
}
```
* Note: For this linter to work you must have syntax highlighting set to ```Better CoffeeScript -> CoffeeScript``` in order for the coffee linter to work

***

## CoffeeScript - Autocomplete triggers
* Go to: Sublime -> Preferences -> "Settings - User"
* adding the following will enable autocomplete
```json
{
    "auto_complete_triggers":
    [
        {
            "characters": ".@",
            "selector": "source.coffee, source.litcoffee, source.coffee.md"
        }
    ]
}
```
* Note: you can add other syntax like ```*.php``` would be ```source.php``` and the auto complete behavior woud be the same for php syntax files

***

## Sublime Text 3 - Indentation & white-space trimming
* Go to: Sublime -> Preferences -> "Settings - User"
```json
{
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true,
    "ensure_newline_at_eof_on_save": true
}
```
* Quit and reopen Sublime Text 3

***

## Sublime Text 3 - Optional helpful preferences
* Go to: Sublime -> Preferences -> "Settings - User"
```json
{
    "highlight_line": true,
    "line_numbers": true,
    "show_full_path": true,
    "highlight_modified_tabs": true,
    "enable_tab_scrolling": false,
    "bold_folder_labels": true
}
```
* Quit and reopen Sublime Text 3

***

## Coding Style Guide (PHP)
* Study and follow the following :
* Basic Coding Standard http://www.php-fig.org/psr/psr-1/
* Coding Style Guide http://www.php-fig.org/psr/psr-2/

***

## Git - Creating Your feature/* Branch From The devel Branch
* Name your branch according to the feature you are implementing, for example if you are implementing the calendar in the profile view, name it ```feature/profile-calendar```
```bash
git checkout devel
git pull
git checkout -b feature/profile-calendar
git push -u origin feature/profile-calendar
```

***

## Git - Pushing Your Changes In feature/* Branch Over To Bitbucket
* If for example the branch you working with is named ```feature/profile-calendar```
```bash
git checkout feature/profile-calendar
*** Edit some files ***
git status
git add --all
git commit -am "these are my comments regarding my updates"
git status
git push
git status
```
* Note: ```git status``` should always show the messages ```nothing to commit, working directory clean``` and ```Your branch is up-to-date with ...``` , this means you have pushed all changes to bitbucket correctly

***

## Git - Updating Your feature/* Branches With The Latests From The devel Branch
* If for example the branch you working with is named ```feature/profile-calendar```
```bash
git checkout devel
git pull
git checkout feature/profile-calendar
git rebase devel
git push
```
* Note: The rebase command should get the latests from devel without issues if there are no conflicts. If you get a message like "Your branch is in rebase mode" or "git rebase --continue" do the following
```bash
git rebase --abort
git merge devel
git push
```

***

## Git - Merging A feature/* Branch To The devel Branch
* If you are responsible for auditing the feature/* branches and are ready to merge a approved branch over to the devel branch :
```bash
git checkout devel
git pull
git merge --no-ff feature/profile-calendar
git push
```

***

## Git - Deleting feature/* Branches
* If for example you have already merged ```feature/profile-calendar``` into ```devel``` branch, you can now delete this branch as it no longer will be worked on
```bash
git checkout devel
git branch -d feature/profile-calendar
git push origin :feature/profile-calendar
```
* Note: be sure to include the ```:``` colon before your branch name
* For this branch delete to take effect on everyone elses repository, they need to run the following command:
```bash
git fetch --prune
```

***

## Git Branching Methodology

* http://nvie.com/posts/a-successful-git-branching-model/

![Git Branching Methodology](http://nvie.com/img/git-model@2x.png)

***

## Angular Style Guide
Use the following guide(s) when creating your angular projects:
* https://github.com/mgechev/angularjs-style-guide

***
