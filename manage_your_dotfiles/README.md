# Manage Your Dotfiles

## Install to a new computer

###### Step 1: install my customized `YADR`

```sh
> sh -c "`curl -fsSL https://raw.github.com/netalpha/dotfiles/master/install.sh`"
```

###### Step 2: pull updates from the [official](1) repository

```sh
> git remote add upstream https://github.com/skwp/dotfiles
> git pull upstream master
```

### Reinstall

###### Step 1: remove all about `zsh` and change the shell to `bash`

``` sh
> rake uninstall
# Attention: this will remove many of your configuration files. Please read the rake code before do it!
```


###### Step 2: install `YADR` as the installation to a new computer



