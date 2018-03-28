##### # crostini_notes - Adapted from https://github.com/davidmroth/cros-crostini


#### Setting flags for Chrome OS
##### (https://www.chromium.org/developers/how-tos/run-chromium-with-flags)

- Put the device into dev mode, disable rootfs verification, and bring up a command prompt
- Modify /etc/chrome_dev.conf (read the comments in the file for more details)
- Restart the UI via:
  * `sudo restart ui`<br>

##### #https://sites.google.com/site/cr48ite/getting-technical/remove-rootfs-verification-make-read-write
`/usr/share/vboot/bin/make_dev_ssd.sh --remove_rootfs_verification --partitions 4`<br>
`mount -o remount,rw /`<br>

`vi /etc/chrome_dev.conf`, then append --enable-features=Crostini<br>

##### Setup container
`vmc start dev`<br>
`curl -Lo /tmp/stretch.tgz http://github.com/lstoll/cros-crostini/releases/download/0.1/stretch.tgz`<br>
`lxc image import /tmp/stretch.tgz --alias stretch`

`lxc launch stretch stretch`<br>
`lxc exec stretch -- useradd -u 1000 \`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`-s "/bin/bash" \`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`-m "buser"`<br>
`groups="audio cdrom dialout floppy plugdev sudo users video"`<br>
`for group in ${groups}; do`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`lxc exec stretch -- usermod -aG "${group}" buser`<br>
`done`<br>

`lxc exec stretch --  loginctl enable-linger buser`<br>
`lxc exec stretch -- /bin/login -f buser`<br>
<br>

#### To login as root
`lxc exec stretch -- /bin/bash`<br>

#### Install atom
`apt update`<br>
`apt install curl`<br>
`curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -`<br>
`apt update`<br>
`apt install nodejs`<br>
`apt install libxss1 libasound2`<br>

`curl -sL https://atom.io/download/deb > atom.deb`<br>
`dpkg -i atom.deb`<br>
`apt install --fix-broken`<br>
