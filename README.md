This docker image allows you to run the excellent `cat` command replacement `bat` within a container.  `bat` is a `cat` clone with wings! ...and Docker

See the __*excellent*__ `bat` project that this docker container wraps at [https://github.com/sharkdp/bat/](https://github.com/sharkdp/bat/)

![stars](https://img.shields.io/docker/stars/danlynn/bat.svg) ![pulls](https://img.shields.io/docker/pulls/danlynn/bat.svg) ![automated](https://img.shields.io/docker/automated/danlynn/bat.svg) ![automated](https://img.shields.io/docker/build/danlynn/bat.svg)

### Supported tags and respective `Dockerfile` links

+ [`0.6.1`,`latest` (0.6.1/Dockerfile)](https://github.com/danlynn/bat/blob/0.6.1/Dockerfile)

![bat logo](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/bat_logo_header.svg?sanitize=true)

## Usage

Note that these examples all use the shell alias described in the installation section below.

#### Syntax Highlighting

`bat` supports syntax highlighting for a large number of programming and markup languages:

![Syntax Highlighting Example](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/syntax_highlighting.png)

#### Git Integration

`bat` integrates with git to show modifications with respect to the index (see left side bar):

![Git Integration Example](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/git_integration.png)

Notice the `~`, `+`, `-` symbols in the left margin.  The wider `-` at the very top indicates that somewhere further down in the listing there are modifications.

#### Theme Selection

A number of different syntax highlighting themes are built-into `bat`.  To get a list of the available themes try `bat --list-themes`:

![List themes](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/list_themes.png)

Notice how `bat` gives a sample of each theme listed. Nice!

To use a theme other than the default, either pass the `--theme` option on the command line -or- set the `BAT_THEME` env var on your local machine:

![Select theme](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/select_theme1.png)

![Select theme](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/select_theme2.png)

Note that if you want to use a different theme as a default then you should probably just set the `BAT_THEME` env var in your ~/.bashrc file like:

```bash
export BAT_THEME=1337
```

## Installation

Basically, you don't install __*anything*__.  Instead, all you have to do is add the following bash alias definition to your ~/.bashrc file:

```bash
alias bat='docker run -it --rm -e BAT_THEME -v "$(pwd):/myapp" danlynn/bat'
```

This new alias will be available in any __*new*__ terminal tabs or windows that you open.

Then, upon your __*first*__ use of the `bat` command, docker will download this image and then continue on to run your `bat` command.  Every subsequent `bat` command will simply run as expected since the docker container will have already been created.

It is __*NOT*__ recommended, but if you really don't want to setup a bash alias then you can run the `bat` docker image as an executable container like:

```bash
docker run -it --rm -e BAT_THEME -v "$(pwd):/myapp" danlynn/bat myFile.js
```

### Docker-Specific Issues

Since all dependencies associated with running `bat` are included in the docker container, you don't need to install anything on your local machine - except maybe the bash alias.

This means that even though you might not have command-line git installed locally, the git support required to show the diffs still works because git is included in the docker container.

If you get a message like:

![Git Integration Example](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/no_such_file.png)

Then you have probably tried to `bat` a file outside of the current directory tree.  The `bat` bash alias is setup to share the __*current*__ directory with the docker container so that it can access the files that you pass as arguments.  If you want to successfully `bat` the file in that example, you would first need to `cd ..` up a directory and then use the `bat` command:

![Git Integration Example](https://raw.githubusercontent.com/danlynn/bat/master/README_assets/dir_tree.png)

Similarly, if you are trying to `bat` a file which is a soft link or is in a sub directory that is soft linked then it __*may*__ fail if those soft links are pointed at files which are not in the directory tree of the current directory.

Taking these "gotcha's" into account, 99.9% of normal `bat` use cases will work just fine.  So, don't sweat it and enjoy `bat`!
