# fix_chrome_app_desktop_file
An on-demand Google Chrome .desktop app window class updater bash script.

This script works around an issue where KDE Plasma 5.1x (as of at least 2018-10-03) is unable to separate Google Chrome App windows from Google Chrome's general window class. A consequence of this would be Apps not using their intended icons, and also grouping under a single Chrome window. It's a minor usability issue.

Credit for the workaround is due here: https://superuser.com/a/1068709

I suspect this only helps users running X11. It's also quite possible that this is not inherently an issue on Wayland systems, but I have not tested this.


# Requirements
1. Your system will need the `xdotool` package.
2. For now, this has been written only for Arch/Manjaro systems, but I should be able to update the script for .deb/.rpm-based distros as well, quite soon.  
As a workaround for other distros (or where this is not currently working), you can modify the section involving `pacman` or omit the package install condition check entirely.

# Installation and Usage
1. Place the script in `~/.local/share/applications`, where your respective .desktop files are.
2. Set Execute permissions on the script. For example: `chmod 755 fix_chrome_app_desktop_file`
3. Determine which chrome-\*.desktop file you need to modify.  
You can check the `Name` value from each of the chrome-\*.desktop files to see what Chrome App it corresponds with.
4. Run the script with a chosen chrome-\*.desktop file for its argument.  
For example, `./fix_chrome_app_desktop_file chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop`  
The script will automatically prompt the installation of `xdotool`, if needed.

# Example
```
$ ./fix_chrome_app_desktop_file chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop
Checking if xdotool is installed...
xdotool is already installed - proceeding.
Modifying chrome-pjkljhegncpnkpknbcohdijeoejaedia-Default.desktop, Gmail, with class crx_pjkljhegncpnkpknbcohdijeoejaedia
Old Exec parameter: Exec=/opt/google/chrome/google-chrome --profile-directory=Default --app-id=pjkljhegncpnkpknbcohdijeoejaedia
New Exec parameter: Exec=/opt/google/chrome/google-chrome --profile-directory=Default --app-id=pjkljhegncpnkpknbcohdijeoejaedia &&xdotool search --sync --classname crx_pjkljhegncpnkpknbcohdijeoejaedia set_window --class crx_pjkljhegncpnkpknbcohdijeoejaedia
Done!
```
