Reference:

https://github.com/archlinux/archinstall

https://archinstall.readthedocs.io/index.html

https://archinstall.readthedocs.io/installing/guided.html

The above are good, but they don't tell you how to simply create, edit and save these files for later use. That is the purpose of this text.

NOTE: I am not a coder, so there may be some mistakes or mistyping of a file name or path in here. This is the first time I have used json files, but I managed to feel my way through this somehow. I am typing this all out from memory of last night and I am old, so... if I can do this, you can do this. I just know that there are no YouTube videos showing people how to use this new installer for Arch.

These are the saved config files from a fresh install of Arch Linux on my desktop PC.
The user_credentials.json has been deleted. It saves the user name and password in  plain text and should not be used on a new install, or saved in a file anywhere, EVER.

Get the newest Arch ISO booted up and let's do this. You are root, so you do not need sudo. For your reference, you are in /root .

(1) On a new install, start by making sure your networking is up.
iwctl can be used for wi-fi connections

(2) get the pacman keys. If this fails, go back to step (1) You must have a connection.
This will get the keys and sync the pacman repo db

pacman -Syy

(3) I like micro, but you can use vi, vim, nano, etc. We can assume you are creating these for the first time.

pacman -S micro

(4) Optional + Note that these are Case Sensitive! These can also be done in /etc/pacman.conf on the new install after it is all completed.

micro /etc/pacman.conf

uncomment #Color

uncomment #VerbosePkgLists

uncomment #ParallelDownloads = 5

add a line just below it with ILoveCandy

uncomment #[multilib]

uncomment #Include = /etc/pacman.d/mirrorlist

save and exit

sudo pacman -Syy to get the new key and sync the new repo

(5) Lets do a dry run and get a copy of these config files to save and edit. This is really important if you want to do this with BTRFS and snapshots. The default settup is not like I would do mine. I prefer my settings for the subvolumes. Make sure you are still in /root .

archinstall --dry-run

(6) Go through each of the choices in the menu. Take your time and get them right. You want a good set of configs to start with.

(7) Once you have completed your input of all of the configs, go down to Save Configuration and then Save All. Save the files to /root and this will put them right into the directory you are working from. Now, we can stop the install and edit the config files to do a better job with our partitions and subvolumes.

(8) Run "archinstall --config user_configuration.json --disk_layouts user_disk_layout.json --creds user_credentials.json" and almost everything will be there except a password for root.

Once you have completed the install and exited back to the command line, simply copy them to the new install with the following two commands, so you will have them for later and can upload them to your git.

mkdir /mnt/archinstall/home/yourusername/archinstall

cp /root/*.json /mnt/archinstall/home/yourusername/archinstall/

To use these files later, simply run them from a git url as shown in the command below. You don't even have to clone them. That's awesome! The following should be one line. Just one long command. Edit it to your git url. You don't want to use mine. Make one. You can do this!

"archinstall --config https://github.com/wilsonephillips/archinstall/user_configuration.json --disk_layouts https://github.com/wilsonephillips/archinstall/user_disk_layout.json"

