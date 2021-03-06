Here is a simple shell extension to simplify access to your Crostini container: 
- https://github.com/davidmroth/chrome-secure-shell/tree/crostini
- Reddit discussion: https://www.reddit.com/r/Crostini/comments/8bet6j/crostini_shell_access_your_container_with_one/


### # crostini_notes - Adapted from https://github.com/lstoll/cros-crostini
<br>

### No need to put Chrome OS into developers mode!! (as of Chrome OS 67.0.3383.0)
<br>

### Setup container
**Start a container** - `vmc start <container name>` (pick a container name)<br>
<br>

### To login as a user
**Run a container as a user** - `run_container.sh --container_name=<container name> --user=<any username> --shell`<br>
<br>

### To login as root
**Run a container as root** - `run_container.sh --container_name=<container name> --user=root --shell`<br>
<br>
<br>

### Install atom
`apt update`<br>
`apt install curl gnupg libxss1 libasound2`<br>
`curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -`<br>
`apt update`<br>

`curl -sL https://atom.io/download/deb > atom.deb`<br>
`dpkg -i atom.deb`<br>
`apt install --fix-broken`<br>
