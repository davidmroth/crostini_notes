### # crostini_notes - Adapted from https://github.com/lstoll/cros-crostini


##### No need to put Chrome OS into developers mode!! (as of Chrome OS 67.0.3383.0)

##### Setup container
**Start a container** - `vmc start <container name>` (pick a container name)<br>

#### To login as a user
**Run a container as a user** - `run_container.sh --container_name=<container name> --user=<any username> --shell`<br>


#### To login as root
**Run a container as root** - `run_container.sh --container_name=<container name> --user=root --shell`<br>

#### Install atom
`apt update`<br>
`apt install curl`<br>
`curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -`<br>
`apt update`<br>

`curl -sL https://atom.io/download/deb > atom.deb`<br>
`dpkg -i atom.deb`<br>
`apt install --fix-broken`<br>
