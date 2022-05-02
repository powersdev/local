# Lando Boilerplate

## Quick Start

### Site Configuration
1. Clone this repo and rename it `git clone git@github.com:powersdev/local site-name`
2. Change your terminal directory to the new `site-name` folder
3. Configure the `.lando.yml` file
4. Run `lando start`

### Importing Data: ###

#### WPEngine ####
- Run `lando pull` to import plugins and data 

#### VIP ####
- Move any gzipped VaultPress export files into the site folder
- Run `lando vip-import filename1 filename2`

## Configuration
    
Input ssh url of the `repo` and the `multisite` status. 
If the site is on wpengine, add the `wpengine_name` (for pulling data).

Everything else is inferred from the repository or the imported database.

## Using Lando

The following commands are built-in

```bash
lando start     # starts the server
lando stop      # stops the server
lando rebuild   # run after modifying landofile 
lando destroy   # delete containers and all data
lando poweroff  # stop all running lando containers
lando ssh       # access the running container
```

The following commands are custom

```bash
lando setup         # installs wordpress and sets up the theme
lando pull          # pulls data/plugins/uploads from wpengine
lando vip-import    # imports a vaultpress export (used by VIP sites)
lando xdebug-on     # enable xdebug
lando xdebug-off    # disable xdebug
lando wpdebug       # run the wp-cli in xdebug mode
lando phpcs         # run phpcs with the custom ruleset
lando phpcbf        # run phpcbf with the custom ruleset
lando phpcs-compat  # run phpcs with the php 8 compatibility ruleset
```

The setup command allows you to download fresh files and run the WordPress install again. 
If you want fresh data, you must run `lando destroy` first to wipe the database. 

The pull command has to be run manually whenever you want fresh data.

The vip-import command allows you to specify one or more gzipped vaultpress exports.

## Requirements

[**Lando**](https://docs.lando.dev)

I recommend downloading the latest version directly from the GitHub releases page and installing it that way. 
I've had better results with manual installations than with package managers.

### MacOS

[MacOS Installation](https://docs.lando.dev/basics/installation.html#macos)

Make sure you download the ARM version from GitHub if you're running on an M1 mac.

### Windows

[Windows Installation](https://docs.lando.dev/basics/installation.html#windows)

I'd recommend using WSL2 over Hyper-V for Windows.

### Linux

[Linux Installation](https://docs.lando.dev/basics/installation.html#linux)

Install docker and then download the latest GitHub release. 

It's on the AUR and in the apt repositories, but I've had problems with both.

## TODO
- Infer `wpengine_name` from bitbucket-pipelines.yml
