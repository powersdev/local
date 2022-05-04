# Introduction

The most important files and directories are listed below.

```shell
# Landofiles
.lando.base.yml
.lando.yml

# Binaries
bin/

# Configuration Files
config/

# Code Quality
composer.json
phpcs.xml
```

## Landofiles

There are two landofiles:

```shell
.lando.yml		
.lando.base.yml	
```

The files are split between a core config (which is common to all sites) and a site config (which contains details specific to this site). This is done to streamline the setup process.

### Core Configuration

A fairly standard WordPress configuration including phpmyadmin and mailhog. Additional config has been added to enable xdebug for use in your IDE among other things.

Custom tooling is detailed in the [readme](/#using-lando).

### Site Configuration

Here is where the site-specific work is done. 

```yml
name: local
proxy: # these have to match the name above
  appserver:
    - local.lndo.site
  pma:
    - pma.local.lndo.site
  mailhog:
    - mh.local.lndo.site
config:
  php: "8.0"
services:
  appserver:
    overrides:
      environment:
        # General site information
        wpengine_name: local
        repo: git@github.com:powersdev/scaffold
        multisite: no
        # SSH Keys
        repo_ssh_key: id_ed25519
        wpe_ssh_key: id_ed25519
```

The following steps need to be taken:

1. Rename the environment from `local` to something else (throughout the file).
2. Set the `wpengine_name`
2. Modify the repo to point at your site files.
	- This repo is expected to include the `wp-content` folder as required by [wpengine's .gitignore](https://wpengine.com/wp-content/uploads/2020/02/recommended-gitignore-wp.txt)
3. Modify the `multisite`, `php`, and ssh values as needed.

After configuring the site, all one has to do is run `lando start` to kick off the process. If the `wordpress` folder is not found in the project, it will automatically be downloaded and installed alongside the site repo.

## Binaries

The `bin` folder contains a collection of python and bash scripts. The original project was a couple of bash scripts, but it has since evolved. (I'm not terribly happy with the outcome of the python rewrite, so I'm now looking at [hush](https://hush-shell.github.io/) as a potential replacement.)

### Contents

Here is a list of the files in the `bin/` directory:

```
# Prepare the container and tooling
build
setup
run

# Set up WordPress and site files
core_install
theme_install

# Import production data
pull
vip_import

# Perform automatic domain replacement
search_replace
multisite_search_replace
```

### Overview

Here is a quick list of the things that these scripts are in charge of:

- Set up tooling inside the container, such as node and python
- Download and install the latest version of WordPress
- Pull files and data from the production environment via `ssh` and `rsync`
- Import Vaultpress data (for VIP sites)
- Set up themes by installing npm dependencies and running build tools
- Perform automatic search and replace on regular sites and multisite network

There are some clever details worked in there, like setting up a local user after `setup` and `pull`, or disabling plugins related to outgoing mail to avoid "email from dev" scenarios. [Suggestions are always welcome](mailto:jon@powers.dev).

# Summary

These tools allow the user to create a near duplicate of a production site in 10 minutes or less.

The process of building this tool has brought me great joy. There is nothing better than the excitement of others when it "just works". 

Pull requests are welcome.
