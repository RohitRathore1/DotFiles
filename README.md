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
## Note - Be sure to checkout the [Onramp to Vim](https://upcase.com/onramp-to-vim) trail to level up your Vim game,especially the videos on [Configuration](https://upcase.com/onramp-to-vim) and [Plugins](https://upcase.com/videos/onramp-to-vim-plugins).

## Vim Filetype Configuration

There are a few special directories thet Vim will look in to define specific configurations.
- ## ftdetect - If you have files in an `~/.vim/ftdetect` folder, Vim will automatically run those files every time a new file is opened to allow you to dynamically detect and set the filetype. This is useful for files like markdown (`*.md`) which Vim would otherwise mistakenly treat as "modula2" files.

- ## ftplugin - The files in this directory will be run based on their filename for a given filetype. For instance, a `~/.vim/ftplugin/markdown.vim` config file will be run for all markdown files. This allows for filetype specific configurations.

## Zsh configuration
Similar to Vundle for Vim, there is [Antigen for zsh](https://github.com/zsh-users/antigen) which acts as a plugin downloader and manager for zsh. It can target anything in [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) allowing to pick and choose specific pieces without needing to install the full oh-my-zsh.

## Git configuration

## Aliases

Git allows us to define custom aliases that run just like git commands. These are stored in our `~/.gitconfig` file in the aliases section and can be defined by either directly editing that file, or running a command like:
```bash
# Create a git alias, runnable as `git unstage` to unstage files.
$ git config --global alias.unstage 'reset HEAD --'

## Scripts

Git will automatically run any script that matches the subcommand name which allows us to create more complex git commands ourself. For example, if we run `git newbranch`, git will look on our PATH for any script called `git-newbranch` and will execute it if found.

## Fall through g alias

The thoughtbot dotfiles (as well as Chris, Gabe's, Ben's, pretty much everybody's) contain a usefull shell alias that makes interacting with git much easier. We can view [the alias on github in the thoughtbot dotfiles](https://github.com/thoughtbot/dotfiles/blob/6a034a7d659ef332345d17d55aaf47994aa9f96b/zsh/functions/g), and I've included it as well:
