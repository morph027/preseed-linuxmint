# Preseed Linux Mint

*HINT*: Regard this thing as a template, please adjust to your needs (packages,localizations,...) 

As ubiquity does not allow as much customizations as preseed (e.g. local repos), we are bootstrapping a minimal ubuntu, add Linux Mint repos and then the packages. You might adjust things to your needs, like desktop environment (MATE/Cinnamon) and Login Manager (MDM/LightDM) and so on.

It will ask for:

* hostname

## PXE setup

In your PXE server setup, you need to add something like this:

```
label install
        menu label Preseed Cinnamon
        kernel ubuntu-installer/linux
        append preseed/url=http://some.host/preseed/crypto-trusty-cinnamon.seed initrd=ubuntu-installer/initrd.gz locale=de_DE.UTF-8 debian/priority=critical vga=normal debian-installer/keymap=de console-keymaps-at/keymap=de console-setup/layoutcode=de_DE netcfg/choose_interface=auto localechooser/translation/warn-light=true localechooser/translation/warn-severe=true console-setup/ask_detect=false --
```

## Extras

### apt-cacher-ng

As we are using an apt-cacher-ng host in our network, we'd like to use this for preseeding. Just look for the comments regarding apt-cacher-ng and adjust to your setup. Thats also the reason, why the sources list gets fetched in _late\_command_, cause preseeding will leave the "ugly" strings there. You could then switch to a setup using [apt-find-proxy](https://github.com/Tolaris/apt-find-proxy), which only uses the apt-cacher-ng proxy when reachable.

### LightDM Mint Theme

See section in _late-command-trusty_
