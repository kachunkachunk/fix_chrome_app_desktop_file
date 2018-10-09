# fix_chrome_app_desktop_file
An on-demand Google Chrome .desktop app window class updater bash script. Made by me, for me, but shared against better judgment. For now I don't maintain this and use Chromium instead, where the issue doesn't seem to occur.

This script attempts to work around an issue where KDE Plasma 5.1x (as of at least 2018-10-03) is unable to separate Google Chrome App windows from Google Chrome's general window, presumably from using the same class. A more meaningful consequence of this would be Apps not using their intended icons, and also grouping under a single Chrome window. It's a minor usability issue in the end, but it is (or was?) correctable.

Credit for the workaround is really due here: https://superuser.com/a/1068709

I suspect this only helps users running X11. It's also quite possible that this is not inherently an issue on Wayland systems, but I won't be testing this for a very long time, probably.


# Requirements
1. Your system will need the `xdotool` package.
2. At least for now, this has been written only for Arch-based systems, but I should be able to update the script for .deb and .rpm-based distributions as well, and quite soon.  
As a workaround for other distributions (or where this is not currently working), you can modify the section involving `pacman` or omit the package install condition check logic altogether.


# Installation and Usage
1. If necessary, set Execute permissions on the script. For example: `chmod 755 fix_chrome_app_desktop_file`
2. Determine which `~/.local/share/applications/chrome-\*.desktop` file you need to modify.  
You can check the `Name` value from each of the chrome-\*.desktop files to see what Chrome App it corresponds with. For instance: `grep "Name=" ~/.local/share/applications/chrome-*.desktop` to get a list of resulting files and their Name values.
4. Run the script with a chosen chrome-\*.desktop file for its argument.  
For example, `./fix_chrome_app_desktop_file ~/.local/share/applications/chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop`


The script will automatically prompt the installation of `xdotool`, if needed.  
Possible to-do: Make this work nicely for .deb and .rpm-based distributions.


# Example
```
$ ./fix_chrome_app_desktop_file ~/.local/share/applications/chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop
Checking if xdotool is installed...
xdotool is already installed - proceeding.
Modifying chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop, Gmail, with class crx_pjkljhegncpnkpknbcohdijeoejaedia
Old Exec parameter: Exec=/opt/google/chrome/google-chrome --profile-directory=Default --app-id=pjkljhegncpnkpknbcohdijeoejaedia
New Exec parameter: Exec=/opt/google/chrome/google-chrome --profile-directory=Default --app-id=pjkljhegncpnkpknbcohdijeoejaedia &&xdotool search --sync --classname crx_pjkljhegncpnkpknbcohdijeoejaedia set_window --class crx_pjkljhegncpnkpknbcohdijeoejaedia
Done!
```
