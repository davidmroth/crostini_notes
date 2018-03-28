# crostini_notes - Adapted from https://github.com/davidmroth/cros-crostini


#https://www.chromium.org/developers/how-tos/run-chromium-with-flags
Setting Flags for Chrome OS
- Put the device into dev mode, disable rootfs verification, and bring up a command prompt
- Modify /etc/chrome_dev.conf (read the comments in the file for more details)
- Restart the UI via:
  * sudo restart ui

#https://sites.google.com/site/cr48ite/getting-technical/remove-rootfs-verification-make-read-write
/usr/share/vboot/bin/make_dev_ssd.sh --remove_rootfs_verification --partitions 4
mount -o remount,rw /


#https://github.com/lstoll/cros-crostini
edit /etc/chrome_dev.conf , add --enable-features=Crostini

vmc start dev
curl -Lo /tmp/stretch.tgz http://github.com/lstoll/cros-crostini/releases/download/0.1/stretch.tgz
lxc image import /tmp/stretch.tgz --alias stretch

lxc launch stretch stretch
lxc exec stretch -- useradd -u 1000 \
    -s "/bin/bash" \
    -m "buser"
groups="audio cdrom dialout floppy plugdev sudo users video"
for group in ${groups}; do
    lxc exec stretch -- usermod -aG "${group}" buser
done

lxc exec stretch --  loginctl enable-linger buser
lxc exec stretch -- /bin/login -f buser

# to login as root
lxc exec stretch -- /bin/bash


# install atom
apt update
apt install curl
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
apt update
apt install nodejs clang
apt install libxss1 libasound2

curl -sL https://atom.io/download/deb > atom.deb
dpkg -i atom.deb
apt install --fix-broken
