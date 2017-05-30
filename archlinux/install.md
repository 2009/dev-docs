# My Archlinux Install
#### TODO

- [ ] Add a section on checking for errors!!!!

## Install non-GUI packages

```
pacman -S git openssh termite networkmanager ranger atool highlight /
          mediainfo file htop scrot fasd
```

## Install main GUI packages

```
pacman -S git xorg xorg-utils xorg-apps xterm xorg-xinit awesome
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

## Install Yaourt

```
mkdir ~/build
cd ~/build
git clone https://aur.archlinux.org/package-query.git
cd package-query
makepkg -si
cd ..
git clone https://aur.archlinux.org/yaourt.git
cd yaourt
makepkg -si
cd ..
```

## Install AUR packages

```
yaourt -S tamzen-font-git blockify spotify bitlbee-steam-git tasksh
```

## Enable NetworkManager

```
systemctl enable NetworkManager
systemctl start NetworkManager
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

## Setup Weechat and Bitlbee

Start and enable bitlbee daemon `systemctl start bitlbee`. This will
make it show up in weechat.

See this link http://zanshin.net/2015/01/10/a-guide-for-setting-up-weechat-and-bitlbee/  
See help for weechat and bitlbee.  
See https://github.com/bitlbee/bitlbee-steam for adding steam account  

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
