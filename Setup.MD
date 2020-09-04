## Deploying custom jitsi-meet on a AWS Ubuntu server

# Clone the github repository

Run `git clone https://github.com/recoveryrecord/jitsi-meet-1.git`

# Setup the build environment

## Get the correct version of npm

We need a version Node.js >= 10 and npm >= 6.  Since the current version from apt-get is too old, install nvm.

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash`

Follow the instructions to update your bash enviroment (or log out and back in).

Now that nvm is available, run

`nvm install node`

## Install node modules

In the jitsi-meet directory, run

`npm install`

Building at this point leads to an "Error: ENOSPC: System limit for number of file watchers reached".  To fix, run

`echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

This increases the number of file watchers.

# Build jitsi-meet

In the jitsi-meet directory, run

`make`

It should build the code, create a backup, and deploy it to /usr/share/jitsi-meet.
