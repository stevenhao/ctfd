# ctfd

## Usage
Use `ctfd` to jump to the most recently `cd`'d to directory.

This is useful if you need to open multiple shells (e.g. ssh) and work in a hard to find directory. If you only have one shell open, the behavior should be the same as `cd -`.

## Installation
Add these lines to your `~/.bashrc`, `~/.profile`, or `~/.zshrc` file to have it automatically sourced upon login:

```sh
function cd { # change the default behavior of cd
  builtin cd "$@" && [ -d ~/.ctfd ] && pwd > ~/.ctfd/lastdir
}

function ctfd {
  [ -d ~/.ctfd ] || echo '~/.ctfd does not exist'
  [ -f ~/.ctfd/lastdir ] && cd $(cat ~/.ctfd/lastdir)
}
```

Create the `~/.ctfd` directory. `ctfd` will read and write to `~/.ctfd/lastdir` to track your working directory.

```sh
mkdir ~/.ctfd
```

Done!

To test your installation, open two shells (if you already have two open shells, don't forget to `source ~/.bashrc`) and navigate to some directory in the first one. Type `ctfd` in the second shell and you should be taken to the same directory.
