# DotFiles
 My personal DotFiles

 ## Introduction

 Dotfiles are plain text configuration files on Unix-y systems for things like our shell, '~/.zshrc', our editor in '~/.vimrc', and many others. They are called "dotfiles" as they typically are named with a leading '.' making them hidden files on your system, although this is not a strict requirement. Since these files are all plain text, we can gather them together in a git repository and use that to track the changes we make over time.

 ##thoughtbot DotFiles

 The thoughtbot dotfiles are a shared repository used by many of the developers at thoughtbot. They are purposefully somewhat limited in how far they go with configuration and customization as they are intended to be used as a base.
 ##Local Overrides

 Each of the config files in the thoughtbot dotfiles provides a base configuration but will also read in a "local" file to allow for additional, more personalized configuration.
 For example, thoughtbot's dotfiles contain a '~/.vimrc' file will the base that will optionally source in a '~/.vimrc.local' file if available. We can use this '~/.vimrc.local' file to override and add to the configurations provided by the base '~/.vimrc' file.

 ##rcm dotfile management utility

 The thoughtbot dotfiles use a utility called [rcm](https://github.com/thoughtbot/rcm), written by a collection of thoughtboters, that automates the management and linking of the various individuals files from their homes in the repos, to the expected locations in our home directory.
 Even if we're not using the thoughtbot dotfiles, rcm is a great tool for managing our own dotfile setup.

 ##Distributed DotFile Convention

 One approach is to break apart the otherwise very large config files into smaller, more manageable config files:
 
