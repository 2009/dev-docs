# My Archlinux Install

[Installation Guide][3]

## Issues with installation from USB (UEFI)

A few times I've encounted issue with boot using UEFI, using the
legacy usb boot option or setting the kernal parameter `nomodeset`
usally works.

Other kernal parameters to try: `i915.modeset=0` `radeon.modeset=0`
`nouveau.modeset=0` `nvidia.modeset=0` `acpi=0`

Another option is to boot into another existing distro (or liveCD),
then install arch from there, using something like [arch-bootstrap][2].

[Install arch from an Existing System][1]  

## Install non-GUI packages

```
pacman -S git openssh termite networkmanager pkgfile /
          ranger atool highlight mediainfo file /
          htop scrot bind-tools /
          fasd thefuck zsh
```

## Install main GUI packages

```
pacman -S git xorg xorg-apps xterm xorg-xinit awesome
```

## Create .xinitrc and add `exec awesome`

```
cp /etc/X11/xinit/xinitrc ~/.xinitrc
```

## Install additional GUI packages

```
pacman -S git ttf-dejavu tamsyn-font firefox chromium gimp inkscape mpv /
          pulseaudio pulsaudio-alsa pavucontrol playerctl weechat bitlbee /
          zathura zathura-pdf-poppler task ntp firewalld
```

## Update pkgfile for command not found suggestions with zsh

```
pkgfile --update
```

## Install `yay`
[Instruction on installation - jguer/yay][4]

```sh
mkdir ~/build
cd ~/build
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
```

## Install AUR packages

```
yay -S tamzen-font-git blockify spotify bitlbee-steam-git tasksh
```

## Enable NetworkManager

```
systemctl enable NetworkManager
systemctl start NetworkManager
```
## Generate SSH keys

[SSH keys - Arch Wiki][5]

```sh
ssh-keygen -C "$(whoami)@$(hostname)-$(date -I)" -G "$HOME/.ssh/id_rsa.$(hostname)"
```

Add ssh config to use the new key as our default:
```sh
cat <<EOF | tee $HOME/.ssh/config
Host *
  IdentityFile ~/.ssh/id_rsa.$(hostname)
EOF
```

## Setup SSH server

#### Change the default port
Change `ListenStream` to port 4395 (or any random unused port)

```
systemctl edit sshd.socket
```

#### Force public key authentication

Edit `sshd_config`
```
PasswordAuthentication no
ChallengeResponseAuthentication no
```

#### Enable sshd

```
systemctl enable sshd.socket
systemctl start sshd.socket
```

#### Allow ssh port in firewalld
https://fedoraproject.org/wiki/Firewalld?rd=FirewallD

```
firewall-cmd --permanent --zone=public --add-port=4395/tcp
firewall-cmd --permanent --zone=public --remove-service=ssh
```

## Start firewalld

```
systemctl start firewalld
systemctl enable firewalld
```

## Setup Wireless

Just use the networkmanager command `nmtui`

## Setup Bluetooth

[Bluetooth - Arch Wiki][6]  

```sh
pacman -S bluez bluez-utils

# Start and/or enable bluetooth
systemctl start bluetooth.service
systemctl enable bluetooth.service
```

## Setup Weechat and Bitlbee

Start and enable bitlbee daemon `systemctl start bitlbee`. This will
make it show up in weechat.

See this link http://zanshin.net/2015/01/10/a-guide-for-setting-up-weechat-and-bitlbee/  
See help for weechat and bitlbee.  
See https://github.com/bitlbee/bitlbee-steam for adding steam account  
See https://wiki.bitlbee.org/HowtoMigrate on migrating setting from computers

Start the service
```
systemctl enable bitlbee
systemctl start bitlbee
```

Automatically identify and connect to accounts
```
# Add autoconnect to bitlbee server
/server add gtalk localhost/6667 -autoconnect
/connect gtalk

# Register you nick with the bitlbee server
register
/oper anything <password>

# Add gtalk account
account add jabber <email> <password>
account gtalk on
set nick_format %full_name

# Add auto identification
/set irc.server.<server-name>.command "/msg &bitlbee identify; /oper &bitlbee <password>"
/save

# With different nick for each server
/set irc.server.<server-name>.command "/nick <nick>; /msg &bitlbee identify; /oper &bitlbee <password>"
/save

# Ex: /set irc.server.gtalk.command "/msg &bitlbee identify; /oper &bitlbee this is my cool pass"
```

Oper command syntax (could not find this anywhere)
```
/oper <any-random-string> <password>
```
Remember to `/save` after adding an account.

## Setup blockify with spotify

With blockify you can mute commercials. It is available in the AUR as blockify.

To have this start and run in the background every time Spotify starts you will
need to automate this yourself:

```shell
#!/bin/sh

spotify=/usr/bin/spotify

if [[ -x $spotify && -x /usr/bin/blockify ]];
then
  blockify &
  block_pid=$!
  $spotify
  trap "kill -9 $block_pid" SIGINT SIGTERM EXIT
fi
```

By placing this script at `/usr/local/bin/spotify`, it gets preferred to
`/usr/bin/spotify` everytime you start Spotify, so there's nothing else to
change and updates won't break it.

## Setup hibernation with Grub and systemd

[Power Management: Suspend and Hibernate](https://wiki.archlinux.org/index.php/Power_management/Suspend_and_hibernate)

Append `resume` to the following line in `/etc/default/grub.cfg`:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash _resume=UUID=4209c845-f495-4c43-8a03-5363dd433153_"
```

Regenerate the grub.cfg:

```
grub-mkconfig -o /boot/grub/grub.cfg
```

Update initramfs (`/etc/mkinitcpio.config`) and add the `resume` hook after `udev`:

```
HOOKS="base udev _resume_ autodetect modconf block filesystems keyboard fsck"
```

Rebuild the image:

```
mkinitcpio -p linux
```

## Setup screensaver and lock screen

> TODO: Lock on suspend and hibernate

### Setup

```
yay -S xscreensaver-arch-logo
```

Start the xscreensaver daemon when X start by putting hte following in .xinitrc
```
xscreensaver -no-splash &
```

### Configuration

Running `xscreensaver-demo` will allow you to configure the screensaver and
settings, this will write to to `~/.xscreensaver`.

### Running

To start the screensaver run `xscreensaver-comman --lock`

## Checking for errors

[System maintenance (check for errors) - Arch Wiki][7]

```sh
# errors in log files
journalctl -p 3 -xb

# errors with services
systemctl --failed

# Xorg errors
grep -e \(EE\) -e \(WW\) /var/log/Xorg.0.log
```

[1]: https://wiki.archlinux.org/index.php/Install_from_Existing_Linux
[2]: https://github.com/tokland/arch-bootstrap
[3]: https://wiki.archlinux.org/index.php/Installation_guide
[4]: https://github.com/Jguer/yay
[5]: https://wiki.archlinux.org/index.php/SSH_keys#Generating_an_SSH_key_pair
[6]: https://wiki.archlinux.org/index.php/Bluetooth
[7]: https://wiki.archlinux.org/index.php/System_maintenance#Check_for_errors
