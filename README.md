# Mac OS X Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up [Node](http://nodejs.org/) (JavaScript), [Python](http://www.python.org/), and [Ruby](http://www.ruby-lang.org/) environments, mainly for JavaScript and Python development. Even if you don't program in all three, it is good to have them as many command-line tools use one of them. As you read  and follow these steps, feel free to send me any feedback or comments you may have.

The document assumes you are new to Mac. The steps below were tested on **OS X Mountain Lion**.

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Google Chrome](#google-chrome)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [Git](#git)
- [Git-Flow](#git-flow)
- [Sublime Text](#sublime-text)
- [Node.js](#nodejs)
- [LESS](#less)
- [Heroku](#heroku)
- [MongoDB](#mongodb)
- [Redis](#redis)
- [7zip](#p7zip)

## System update

First thing you need to do, on any OS acutally, is update the system! For that: **Apple Icon > Software Update...**

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Google Chrome

Install your favorite browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode. To do this you need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

If running Mavericks+, install via terminal

    $ xcode-select --install

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open an new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought **Microsoft Office for Mac**, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

    $ brew install cabextract
    $ cd ~/Downloads
    $ mkdir consolas
    $ cd consolas
    $ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
    $ cabextract PowerPointViewer.exe
    $ cabextract ppviewer.cab
    $ open CONSOLA*.TTF

And click **Install Font**. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Let's go ahead and start by changing the font. In **iTerm > Preferences...**, under the tab **Profiles**, section **Text**, change both fonts to **Consolas 13pt**.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `iterm2-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets... > Import...**, find and open the two **.itermcolors** files we downloaded.
- Go back to **Load Presets...** and select **Solarized Dark** to activate it. Voila!

**Note**: You don't have to do this, but there is one color in the **Solarized Dark** preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. **R 83 G 104 B 112**.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.github.com/rfvgyhn/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.github.com/rfvgyhn/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.github.com/rfvgyhn/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

    $ cd ~
    $ curl -O https://raw.github.com/rfvgyhn/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.github.com/rfvgyhn/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.github.com/rfvgyhn/mac-dev-setup/master/.aliases
    
With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Nicolas's MacBook Air" to just "MacBook Air", so it shows up as `MacBook-Air` in the terminal.

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](/rfvgyhn/mac-dev-setup/blob/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.github.com/rfvgyhn/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](/rfvgyhn/mac-dev-setup/blob/master/.gitignore) file for inspiration.
    
### Bash Completion
Adds git completion to shell.

    $ brew update
    $ brew install bash-completion


Update `.bash_profile` to include

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
    . $(brew --prefix)/etc/bash_completion
fi
```

**Note**: The above snippet is already included in the `.bash_profile` within the repository.

## Git-Flow

Git workflow [git-flow](https://github.com/nvie/gitflow)

    $ brew update
    $ brew install git-flow

### Bash Completion
Adds [git-flow completion](https://github.com/bobthecow/git-flow-completion) to shell. Requires git bash completion mentioned above.

    $ mkdir ~/bash-completion.d
    $ curl -o ~/bash-completion.d/git-flow-completion.bash https://raw.githubusercontent.com/bobthecow/git-flow-completion/master/git-flow-completion.bash

## Sublime Text

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

Go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shorcut on the OS X Dock for both for Sublime Text and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $60 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool. :)

Just like the terminal, let's configure our editor a little. Go to **Sublime Text 2 > Preferences > Settings - User** and paste the following in the file that just opened:

```json
{
    "font_face": "Consolas",
    "font_size": 13,
    "highlight_line": true,
    "bold_folder_labels": true,
    "highlight_modified_tabs": true,
    "tab_size": 4,
    "translate_tabs_to_spaces": true,
    "word_wrap": false,
    "indent_to_bracket": true
}

```

Feel free to tweak these to your preference. When done, save the file and close it.

Let's create a shortcut so we can launch Sublime Text from the command-line:

    $ cd ~
    $ mkdir bin
    $ ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" ~/bin/subl

Now I can open a file with `$ subl myfile.py` or start a new project in the current directory with `$ subl .`. Pretty cool.

Sublime Text is very extensible. For now we'll leave it like that, we already have a solid installation. To add more in the future, a good place to start would be to install the [Sublime Package Control](http://wbond.net/sublime_packages/package_control/installation).

## Node.js

Install [Node.js](http://nodejs.org/) via [nvm](https://github.com/creationix/nvm):

    $ curl https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
    $ nvm install 0.10
    $ nvm alias default 0.10

### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>`

## LESS

CSS preprocessors are becoming quite popular, the most popular processors are [LESS](http://lesscss.org/) and [SASS](http://sass-lang.com). Preprocessing is a lot like compiling code for CSS. It allows you to reuse CSS in many different ways. Let's start out with using LESS as a basic preprocessor, it's used by a lot of popular CSS frameworks like [Bootstrap](http://getbootstrap.com/).

### Install

To install LESS you have to use NPM / Node, which you installed earlier using Homebrew. In the terminal use:

    $ npm install less --global

Note: the `--global` flag is optional but it prevents having to mess around with file paths. You can install without the flag, just know what you're doing.

You can check that it installed properly by using:

    $ lessc --version

This should output some information about the compiler:

    lessc 1.5.1 (LESS Compiler) [JavaScript]

Okay, LESS is installed and running. Great! 

### Usage

There's a lot of different ways to use LESS. Generally I use it to compile my stylesheet locally. You can do that by using this command in the terminal:

    $ lessc template.less template.css

The two options are the "input" and "output" files for the compiler. The command looks in the current directory for the LESS stylesheet, compiles it, and outputs it to the second file in the same directory. You can add in paths to keep your project files organized:

    $ lessc less/template.less css/template.css

Read more about LESS on their page here: http://lesscss.org/

## Heroku

[Heroku](http://www.heroku.com/), if you're not already familiar with it, is a [Platform-as-a-Service](http://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) that makes it really easy to deploy your apps online. There are other similar solutions out there, but Heroku was among the first and is currently the most popular. Not only does it make a developer's life easier, but I find that having Heroku deployment in mind when building an app forces you to follow modern app development [best practices](http://www.12factor.net/).

### Install

Assuming that you have an account (sign up if you don't), let's install the [Heroku Client](https://devcenter.heroku.com/articles/using-the-cli) for the command-line. Heroku offers a Mac OS X installer, the [Heroku Toolbelt](https://toolbelt.heroku.com/), that includes the client. But for these kind of tools, I prefer using Homebrew. It allows us to keep better track of what we have installed. Luckily for us, Homebrew includes a `heroku-toolbelt` formula:

    $ brew install heroku-toolbelt
    
The formula might not have the latest version of the Heroku Client, which is updated pretty often. Let's update it now:

    $ heroku update
    
Don't be afraid to run `heroku update` every now and then to always have the most recent version.

### Usage

Login to your Heroku account using your email and password:

    $ heroku login
    
If this is a new account, and since you don't already have a public **SSH key** in your `~/.ssh` directory, it will offer to create one for you. Say yes! It will also upload the key to your Heroku account, which will allow you to deploy apps from this computer.

If it didn't offer create the SSH key for you (i.e. your Heroku account already has SSH keys associated with it), you can do so manually by running:

     $ mkdir ~/.ssh
     $ ssh-keygen -t rsa
     
Keep the default file name and skip the passphrase by just hitting Enter both times. Then, add the key to your Heroku account:

    $ heroku keys:add
    
Once the key business is done, you're ready to deploy apps! Heroku has a great [Getting Started](https://devcenter.heroku.com/articles/python) guide, so I'll let you refer to that (the one linked here is for Python, but there is one for every popular language). Heroku uses Git to push code for deployment, so make sure your app is under Git version control. A quick cheat sheet (if you've used Heroku before):

    $ cd myapp/
    $ heroku create myapp
    $ git push heroku master
    $ heroku ps
    $ heroku logs -t
    
The [Heroku Dev Center](https://devcenter.heroku.com/) is full of great resources, so be sure to check it out!

## MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

### Install

Installing it is very easy through Homebrew:

    $ brew update
    $ brew install mongo

### Usage

In a terminal, start the MongoDB server:

    $ mongod

In another terminal, connect to the database with the Mongo shell using:

    $ mongo

I'll let you refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!

## Redis

[Redis](http://redis.io/) is a blazing fast, in-memory, key-value store, that uses the disk for persistence. It's kind of like a NoSQL database, but there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it that would be hard or inefficient with other database solutions. For example, it's often used as session management or caching by web apps, but it has many other uses.

### Install

To install Redis, use Homebrew:

    $ brew update
    $ brew install redis

### Usage

Start a local Redis server using the default configuration settings with:

    $ redis-server

For advanced usage, you can tweak the configuration file at `/usr/local/etc/redis.conf` (I suggest making a backup first), and use those settings with:

    $ redis-server /usr/local/etc/redis.conf

In another terminal, connect to the server with the Redis command-line interface using:

    $ redis-cli

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

## p7zip

[p7zip](http://p7zip.sourceforge.net/) is a port of 7za.exe for POSIX systems like Unix (Linux, Solaris, OpenBSD, FreeBSD, Cygwin, AIX, ...), MacOS X and also for BeOS and Amiga.

### Install

To install p7zip, use Homebrew:

    $brew update
    $brew install p7zip
    
### Usage

Extract

    $ 7za x archive.7z -o/OutputDir