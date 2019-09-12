# DotFiles
 My personal DotFiles

 ## Introduction

 Dotfiles are plain text configuration files on Unix-y systems for things like our shell, `~/.zshrc`, our editor in `~/.vimrc`, and many others. They are called "dotfiles" as they typically are named with a leading `.` making them hidden files on your system, although this is not a strict requirement. Since these files are all plain text, we can gather them together in a git repository and use that to track the changes we make over time.

 ## thoughtbot DotFiles

 The thoughtbot dotfiles are a shared repository used by many of the developers at thoughtbot. They are purposefully somewhat limited in how far they go with configuration and customization as they are intended to be used as a base.
 ## Local Overrides

 Each of the config files in the thoughtbot dotfiles provides a base configuration but will also read in a "local" file to allow for additional, more personalized configuration.
 For example, thoughtbot's dotfiles contain a `~/.vimrc` file will the base that will optionally source in a `~/.vimrc.local` file if available. We can use this  `~/.vimrc.local` file to override and add to the configurations provided by the base `~/.vimrc` file.

 ## rcm dotfile management utility

 The thoughtbot dotfiles use a utility called [rcm](https://github.com/thoughtbot/rcm), written by a collection of thoughtboters, that automates the management and linking of the various individuals files from their homes in the repos, to the expected locations in our home directory.
 Even if we're not using the thoughtbot dotfiles, rcm is a great tool for managing our own dotfile setup.

 ## Distributed DotFile Convention

 One approach is to break apart the otherwise very large config files into smaller, more manageable config files:
- Gabe's vimrc references [all the other Vim config files he has](https://github.com/gabebw/dotfiles/blob/7c5ba2fd230df4dd2432019c72c3def2b75f1d45/vimrc#L20-L23), which are themselves stored [elesewhere in his Vim configuration](https://github.com/gabebw/dotfiles/tree/7c5ba2fd230df4dd2432019c72c3def2b75f1d45/vim).
- Similarly, his zshrc [sources in](https://github.com/gabebw/dotfiles/blob/7c5ba2fd230df4dd2432019c72c3def2b75f1d45/zshrc#L7-L13) all the [other zsh config files](https://github.com/gabebw/dotfiles/tree/7c5ba2fd230df4dd2432019c72c3def2b75f1d45/zsh) he has.
- A particular case is Gabe's [vundle.vim](https://github.com/gabebw/dotfiles/blob/7c5ba2fd230df4dd2432019c72c3def2b75f1d45/vim/vundle.vim) files which contains the plugin list used by [Vundle](https://github.com/VundleVim/Vundle.vim) to manage all of his plugins.

This has the benefit of allowing for a bit more structure and organization of these config files than would otherwise be the case if all the configuration were in a single file.
## Note

 - Be sure to checkout the [Onramp to Vim](https://upcase.com/onramp-to-vim) trail to level up your Vim game,especially the videos on [Configuration](https://upcase.com/onramp-to-vim) and [Plugins](https://upcase.com/videos/onramp-to-vim-plugins).

## Vim Filetype Configuration

There are a few special directories thet Vim will look in to define specific configurations.
- ## ftdetect
 - If you have files in an `~/.vim/ftdetect` folder, Vim will automatically run those files every time a new file is opened to allow you to dynamically detect and set the filetype. This is useful for files like markdown (`*.md`) which Vim would otherwise mistakenly treat as "modula2" files.

- ## ftplugin
 - The files in this directory will be run based on their filename for a given filetype. For instance, a `~/.vim/ftplugin/markdown.vim` config file will be run for all markdown files. This allows for filetype specific configurations.

## Zsh configuration
Similar to Vundle for Vim, there is [Antigen for zsh](https://github.com/zsh-users/antigen) which acts as a plugin downloader and manager for zsh. It can target anything in [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) allowing to pick and choose specific pieces without needing to install the full oh-my-zsh.

## Git configuration

## Aliases

Git allows us to define custom aliases that run just like git commands. These are stored in our `~/.gitconfig` file in the aliases section and can be defined by either directly editing that file, or running a command like:
```bash
# Create a git alias, runnable as `git unstage` to unstage files.
$ git config --global alias.unstage 'reset HEAD --'
```
## Scripts

Git will automatically run any script that matches the subcommand name which allows us to create more complex git commands ourself. For example, if we run `git newbranch`, git will look on our PATH for any script called `git-newbranch` and will execute it if found.

## Fall through g alias

The thoughtbot dotfiles (as well as Chris, Gabe's, Ben's, pretty much everybody's) contain a usefull shell alias that makes interacting with git much easier. We can view [the alias on github in the thoughtbot dotfiles](https://github.com/thoughtbot/dotfiles/blob/6a034a7d659ef332345d17d55aaf47994aa9f96b/zsh/functions/g), and I've included it as well:

```bash
# No arguments: `git status`
# With arguments: acts like `git`
g(){
    if [[ $# > 0]]; then
        git $@
    else
        git status
    fi
}

# Complete go like git
compdef g=git

```
The alias `g` and can be run with or without arguments:
- Without Arguments - Running just `g` in the shell will run `git status`
- With Arguments - The arguments / command are passed through to git, so running `g merge -` is the same as running `git merge -`.

This may not seem like a lot, but when we consider how much we use git everyday, each of those 2 character savings (9 in the case of bare `g`!) adds up.

## Dotfiles Philosophy

The following are some guidelines that I recommend. These are, of course, not hard and fast rules, but instead rules of thumb that we would likely want to follow unless we have a specific reason not to.
## Avoid automation

While this may sound heretical in a video about dotfiles, I actually recommend not jumping to  automate and configure too quickly. All automation has a cost (maintenance, initial setup and tweaking time, etc) so be wary of automating too quickly.
## Rule of 3

Chris employs a rule of 3 to determine when to automate. If he feels the same annoyance or friction 3 times in recent memory, then the time has come to automate.
## Use Time Boxed Spikes

Once something hits the magic 3 annoyance count, give yourself a short (5-10 minutes) boxed window of time to take a stab at a first solution. When you are in context feeling the friction you are often in the best place to solve something that might otherwise never be handled.
## Capture Notes

Chris uses his [dotfiles repo issues](https://github.com/christoomey/dotfiles/issues) as a place to track bigger problems or updates he'd like to tackle. This has a number of benefits:
Capture annoyances that would take too much time to solve.
Allow some time to pass to make sure this annoyance is truly worth fixing.
Capture any work you've done thus far. Maybe you were able to get a partial solution in your 5-10 minute time box. Save off what you have so you can come back when you have more time. Allow the future, smarter you to solve this problem. You may not have the knowledge to solve a particular problem when you first encounter it, but down the road you might!
## Share Your Dotfiles

Nearly all dotfiles repos are a collection of bits borrowed or copied from others, so it only makes sense to shares yours back. This is a easy as sharing them as a public repo on GitHub. [Dotfiles are meant for sharing](https://zachholman.com/2010/08/dotfiles-are-meant-to-be-forked/) after all.
## Don't Use Someone Else's Dotfiles

In general, dotfiles end up being extremely specific to an individual developers workflows and preferences. As such, it's probably not a great idea to grab those and run with them. One particular case where this is not true is the [thoughtbot dotfiles](https://github.com/thoughtbot/dotfiles). These are specifically designed to provide a minimal (but highly useful and curated!) foundation you are then expected to layer your more specific configurations and preferences on top of.

## Levelling Up Your Dotfiles

One great way to level up your dotfiles knowledge is just to [watch another user's dotfiles](https://help.github.com/en/articles/watching-and-unwatching-repositories) and see what sort of things they are doing. In addition, remember that dotfiles are a long game, something that you're constantly going to be tweaking, updating, and refining rather then finishing in a long weekend. That said, there are a few resources I'd recommend for learning more about configuring specific tools:
- There own [Onramp to Vim](https://upcase.com/onramp-to-vim) trail on [Upcase](https://upcase.com/)
- [Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com/)
- [Git Ready](http://gitready.com/) - Graet collection of answers to "how do I do X in git"
- There [Tmux Course](https://upcase.com/tmux) here on [Upcase](https://upcase.com/)

## NOTE

It was all about [gabebw dotefiles](https://github.com/gabebw). Now I will share my personal dotfiles.


## Rohit's DotFiles

I want to feel like `~` no matter what so here is my personal collection of settings.

## Installation

You can clone this repository, init the submodules and run the script. Almost all the configuartion will be symlinked to your home, backing up the originals founded in there.

```bash
$ git clone git@github.com:TeAmP0is0N/DotFiles.git & cd DotFiles
$ git submodule update --init --recursive
```
The installation is made from a `Rakefile` and you can run just the parts that you want. To check what is avaliable:

```bash
$ rake -T
rake configure                                    # Run all configuration tasks
rake configure:git                              # Configure git related DotFiles
rake configure:osx                            # Configure OSX (run once)
rake configure:tmux                         # Configure TMUX
rake configure:vim                           # Configure Vim with Vundler and plugins
rake configure:zsh                            # Configure ZSH and bootstrap aliases, functions, etc
rake install                                        # Run all install tasks
rake install:binaries                          # Copy binaries to home folder
rake install:homebrew                     # Install homebrew and useful packages
rake install:oh_my_zsh                   # Install oh my zsh, pure prompt and syntax highlighter
rake setup                                        # Run everything
```

So if you want to setup everything just run:

```bash
$ rake setup
```

Or, if you want to run just the zsh configuration for example you can do:

```bash
$ rake configure:zsh
```

All the changes will try to backup a copy of your original configuration but in some cases it's not possible (ie the osx configuration). Be aware of it.

## Notes

- I prefer `zsh` over `bash` so if you configure it your prompt will change.
- If you install *oh my zsh* you'll also get the neat prompt [Pure](https://github.com/sindresorhus/pure) by Sindre Sorhus.
- I encourage you to change the config files to your needs, specially the `osx.sh` script, which is grabbed from awesome [Mathias Bynens dotfiles](https://github.com/mathiasbynens/dotfiles).
- The OSX script will install in your iTerm2 the theme [Solarized](http://ethanschoonover.com/solarized) and the font Monaco, but you will have to select them from the settings. Also it will link your sublime to a `subl` command.
- If you install Brew you'll get a bunch of useful packages which can take a while in install.

## Attributions

I've tried to take the best from every dotfiles I've found but I get inspired (and grab some code) from [Gabe Berke-Williams](https://github.com/javivelasco/dotfiles), [Ryan Bates](https://github.com/ryanb/dotfiles), [Mathias Bynens](https://github.com/mathiasbynens/dotfiles), [Zach Holman](https://github.com/holman/dotfiles) and [YADR](https://github.com/skwp/dotfiles). Thanks to all of them.
