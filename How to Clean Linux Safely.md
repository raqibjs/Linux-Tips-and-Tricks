# Easy tips for Linux Mint and Ubuntu, both for beginners and for advanced users.

As the Victorians used to say: cleanliness is next to godliness. So here are some tips to make your Linux even more divine.

First of all two warnings:

I. Never use cleaning applications like BleachBit! Those software wrecking balls are very risky and may damage your system beyond repair. There are a few safe cleaning actions, which I'll describe below.

II. Another cleaning pitfall is this: by default, there are two microcode packages installed in your system: one for Intel CPU's and one for AMD CPU's. Don't remove the one you don't need!

Both microcode packages are installed as dependencies of the kernel metapackage, so removing one or the other will also remove that metapackage. The other microcode will become a candidate for auto-removal, and future kernel updates will not be offered correctly.

OK, now that's out of the way, let's get started:

Linux Mint doesn't get polluted much over time. It doesn't even need defragmentation. The only cleansing actions you might want to do in Linux Mint, are the following:

Preliminary emergency cleaning
0. If you can't even boot normally because your disk is too full, you'll need to do some preliminary emergency cleaning before you can apply the cleaning methods described on this page. For this, proceed as follows:

In the Grub bootloader menu, select Advanced options and then a line that contains the words (recovery mode). There might be multiple of those; in that case it doesn't matter which one of those you select.

One of the options you get to see then, should be a clean option. Set it to work and hopefully this'll give you the leeway you need to reboot normally. Then apply the other cleaning methods described on this page.

If you never get to see the Grub menu: you can make the Grub menu visible when you turn on your computer, by hitting the Esc key just once, immediately after the BIOS screen disappears.

However, hitting the Esc key just once at the exact right moment can be difficult. In that case, hit the Esc key repeatedly, immediately after the BIOS screen disappears. That increases your chances of success, but it'll give you a Grub command prompt without the menu.

No worries, however: at the Grub prompt, type normal and hit Enter. Then immediately start tapping the Esc key again repeatedly, until the menu is displayed after all. This time, don't worry about hitting Esc too many times: tapping Esc more than once at this point, won't drop you to the Grub command prompt anymore.

Empty the trash bin
1. Maybe too obvious to mention, but still: don't forget to empty the trash bin from time to time. Launch your file manager and right-click on the Trash folder - Empty trash. Repeat this in each user account.

Clear the updates cache
2. From the main menu, launch Synaptic Package Manager.

Panel of Synaptic: Settings - Preferences - Files

Select: Delete downloaded packages after installation

Press the button: Delete Cached Package Files

Clear the thumbnail cache
3. For each displayed picture, Mint automatically creates a thumbnail, for viewing in the file manager. It stores those thumbnails in a hidden directory in your user account (names of hidden directories and hidden files start with a dot, like .cache or .bash_history. The dot makes them hidden).

Over time, the number of thumbnails can increase a lot, up to 512 MB. Moreover, the thumbnail cache will eventually contain many superfluous thumbnails of pictures that don't exist anymore. By default, only thumbnails older than six months will be deleted.

The quickest way to get rid of all the thumbnails is to use the terminal for deleting the folder in which they reside. No worries: the system will re-create that folder and its subfolders automatically, the next time that thumbnails will be generated. Proceed like this:

Launch a terminal window.
(You can launch a terminal window like this: *Click*)

Copy/paste the following command line into the terminal, in order to avoid typing errors:

rm -rfv ~/.cache/thumbnails

Press Enter.

Note: This will probably affect the thumbnails on your desktop as well; in that case it should suffice to simply log out and in again (or reboot your computer), which will create them anew.

Repeat the above in each user account.

Do you wish to change the settings for thumbnails, so that their maximum size and age are reduced? Then proceed like this (only tested in Cinnamon yet):

First install dconf-editor. In the terminal:

sudo apt-get install dconf-editor

Press Enter. Type your password when prompted. In Ubuntu this remains entirely invisible, not even dots will show when you type it, that's normal. In Mint this has changed: you'll see asterisks when you type. Press Enter again.

Then in the terminal:

dconf-editor

Press Enter.

Expanding the subitems can be done by clicking on the little triangle before an item. In Cinnamon, click your way to: org - cinnamon - desktop - thumbnail-cache
(in MATE: org - mate - desktop - thumbnail-cache)

Click once on maximum-age and then once on 180, and change it to 90 (for example, if you want 90 days as maximum age).

Then click once on maximum-size and then once on 512, and change it to 128 (for example, if you want 128 MB as maximum size). Repeat this in each user account. That way, you won't have to pay attention to the disk space of the thumbnails anymore.

The registry
4. There's no need to clean the registry of Linux, as it can't get polluted in the first place. For the following reasons:

- Only the operating system itself has a central registry. The configurations of the applications aren't in there, because they don't have access to it. So they can't mess it up. They place their own default settings in their own folders in the system.

- Applications place upon installation a hidden settings file in the personal folder of each user. That's the only settings file that a user has access to. More or less like MS-DOS did, when each application only created its own .ini file with its settings.

- Each user has his own hidden copy of the central registry in his personal folder. That copy is the only thing that he can mess up, not the registry of another user account.

Make Firefox cleanse itself automatically upon quitting
5. Improve your privacy: you can configure Firefox to cleanse itself automatically, upon quitting. All cookies and history are being deleted then. Furthermore, you can limit the tracking that some websites do to follow you.

The price you pay is a small decrease in user friendliness, but it's not much. The privacy gain is huge, and outweighs this price by far.

You can do it like this:

Firefox menu button (with the three horizontal dashes on it) - Settings - tab Privacy & Security

a. Item Enhanced Tracking Protection: leave those settings at their defaults, because otherwise some websites might function less well.

You're going to set all cookies to be thrown away automatically upon closing Firefox (in the steps hereafter), so this tracking doesn't impact your privacy by much anyway!

b. Item Website Privacy Preferences: tick (enable):

Tell websites not to sell or share my data

Send websites a "Do Not Track" request

c. Item Cookies and Site Data: Tick the setting:

Delete cookies and site data when Firefox is closed

d. Item History: change the setting to:

Firefox will: Use custom settings for history

e. Now tick the following setting:

Clear history when Firefox closes

f. Then, click the button Settings... (on the right of "Clear history when Firefox closes") and tick everything, except for Site Preferences. Click OK.

g. Item Firefox Data Collection and Use: disable (untick) everything you see there.

h. Close the Settings tab and you're done with optimizing the settings for privacy.

Tip: sometimes it may come in handy to force a cleansing during your web browsing. Simply by closing Firefox and launching it anew.

Dealing with Flatpaks and the Flatpak infrastructure
6. Flatpak is an interesting way of always having the latest stable version of certain applications. But it also has disadvantages: Flatpaks take up much more disk space than ordinary applications from the normal software sources. That's because each Flatpak contains most of its supporting files and shares much less with the system.

This use of disk space can also increase quickly, because many Flatpaks are being updated very regularly. This frequent updating also causes a lot of data traffic.

This is how to limit the amount disk space that's being used by Flatpaks:

a. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. Copy/paste the following command line into the terminal, in order to avoid typing errors:

du -sh /var/lib/flatpak

Press Enter.

This should tell you how much disk space is consumed by Flatpaks now. Proceed like this to reduce it, by removing unused old Flatpaks:

c. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

d. Copy/paste the following command line into the terminal, in order to avoid typing errors:

flatpak uninstall --unused

Press Enter.

e. If you don't have much disk space or have to limit your data traffic, you might want to remove all installed Flatpaks and even the Flatpak infrastructure. Like this:

f. First launch Software Manager. Then click the Flatpak button (bottom right) and see which applications have a green circle with a white checkmark in it, after their name. Those are the installed Flatpaks. Remove them all.

g. After you've removed all installed Flatpaks, close Software Manager.

h. It's possible to remove the Flatpak infrastructure as well, in order to prevent installing new Flatpaks by accident. For removing the Flatpak plumbing you can proceed as follows:

i. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

j. Copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo apt-get purge "*flatpak*"

Press Enter. Type your password when prompted. Press Enter again.

Tame your Timeshift
7. Your hard disk can fill up rapidly, if you use Timeshift for making snapshots of your system. Timeshift is notorious for gobbling up free space: it eats gigabytes like they're nothing. So keep the number of its snapshots down. Below, I'll describe the best way to set it up, how to use it and how to remove old snapshots.

The best way to set up Timeshift
7.1. First the number of snapshots to keep. I recommend to keep only two snapshots.

Why two? Well, it's an advantage to have one extra snapshot that's at least a month old. Namely in case the system damage you wish to repair by restoring a snapshot, was inflicted before the latest snapshot (which would mean that the latest snapshot contains that damage as well).

In case of automatic snapshots, limit the number of kept snapshots to two. Make them for example with a monthly interval; more frequent than that is usually nonsensical. But it's probably optimal to have no automation at all, and to simply make snapshots by hand. That's what I do.

Barring the rare exception, nobody needs to have more than two snapshots. Even if the snapshot you restore is quite old: simply run Update Manager after the restoration and your system will be up to date in almost no time at all.

Also, make sure that Timeshift stores its snapshots on a dedicated storage partition on your hard drive or even on an external hard drive. That way, your system won't ever run out of disk space because of Timeshift making a snapshot.

For that, proceed as follows:

From the menu, launch Timeshift. In the panel of Timeshift: Settings - Location
Select the dedicated storage partition you wish to use for this.

Note: The partition you select needs to be formatted as a Linux partition, so FAT32 or NTFS won't do. A partition formatted as EXT4 is the best option.

Removing Timeshift snapshots
7.2. To be on the safe side, only remove redundant snapshots within the Timeshift application itself. Don't use your file manager for that job! Then you can always be absolutely sure that the remaining snapshots stay consistent.

Removing old snapshots is guaranteed to be safe when you use Timeshift itself for the removal job. This will take a while to process though. That's because Timeshift needs to make sure that the files that have not been altered and are still needed, are preserved during the removal of the old snapshots.

As said: practically nobody needs to keep more than two snapshots for repairing a broken system. If you wish to automate the creation of snapshots, select a monthly interval with a retention of 2. No more.

There's no need to worry about which Timeshift snapshots you delete or in what order. Not even the very first snapshot needs to be kept; removing it won't affect the remaining snapshots.

The technical explanation is: although Timeshift snapshots are incremental in order to save storage space, each individual snapshot is still fully complete and independent from the other snapshots.

That looks like a contradiction, but it's not: Timeshift achieves this by using an advanced feature of the Linux file system (hard links, to be exact). The consequence is that snapshots can always safely be removed in any order.

To use an imperfect but helpful analogy, think of it like this: Timeshift's snapshot system behaves as if it consists of two components. Namely (1) a virtual "local software repository" with a copy of all your system files and (2) lists of those system files at particular points in time (namely the times at which the snapshots were made).

Important to know: each file is copied only once. So, your first snapshot will be roughly the same size as the entire system, which means that it's pretty big....

The next snapshot requires space only for its new file list (which is technically a series of hard links) and any additional new files (including updated versions of existing files). Because Timeshift's virtual "local software repository" belongs to all snapshots, you can delete the snapshots in any order. Without ever impairing the integrity of the remaining snapshots.

A file is only removed from Timeshift's virtual "local software repository", when all snapshots with that particular file on their lists are deleted. Which means of course, that only deleting all snapshots will also delete all contents of the virtual "local software repository".

And it also means that no more than one single snapshot, no matter which one it is, no matter how old or how recent it is, is enough for restoring the system.
(based on the fine explanation given by forum members slipstick, pbear, rene and gm10 on forums.linuxmint.com)

Note: The above explanation of the workings of Timeshift is only valid for the normal default EXT4 filesystem. If you have selected BTRFS instead, then that's quite a different cup of tea which falls outside the scope of my website.

How to restore a Timeshift snapshot from within the live session of Linux Mint
7.3. It can drive a grown man crazy: finding out how to restore a Timeshift snapshot residing on the hard disk, after booting into the live session of Linux Mint (using the Mint USB stick or DVD, which may become necessary after a disaster). Because you won't be able to select a snapshot by using the Browse button in the Timeshift toolbar....

The solution is simple, but not intuitive at all: in Timeshift, launch its Wizard and select Locations. Point it at the location on the hard disk where the snapshots reside. The rest is as easy as it should have been in the first place.

Remove most Asian fonts
8. If you're not a user of Asian fonts, you might remove most of those. That should free up some disk space, but more importantly: the font selection box in Libre Office will become much less cluttered. Linux Mint 22 contains a lot less of those Asian fonts than its predecessors, but there are still quite a lot of them.

Note: Sometimes, removing fonts may have unwanted side effects! I haven't experienced those on my machines after the removal of the Asian fonts described below, which is why I recommend removing them. But your mileage may vary, so proceed with caution: for example, if you have installed MythTV, this removal might also remove MythTV. It's especially something to keep in mind, when you wish to remove even more fonts....

This is how to remove most Asian fonts:

a. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. Copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo apt-get remove "fonts-noto*"

Press Enter. Type your password when prompted. In Ubuntu this remains entirely invisible, not even dots will show when you type it, that's normal. In Mint this has changed: you'll see asterisks when you type. Press Enter again.

c. You've just done away with each and every Noto font, which is a bit too drastic. The following terminal command should give you back some non-Asian Noto fonts which are more generally useful (copy/paste it and press Enter):

sudo apt-get install fonts-noto-mono fonts-noto-unhinted fonts-noto-color-emoji

d. Just to make sure, follow it up with this terminal command (use copy/paste to transfer it to the terminal):

sudo dpkg-reconfigure fontconfig

Press Enter.

e. Reboot your machine.

Finally: I strongly advise to leave it at that. Don't remove any other fonts, because of the aforementioned risk of negative side effects!

How to undo: re-installing removed Asian fonts
8.1. Regrets? If you want to re-install the Asian fonts that you've removed by applying the how-to in item 8, simply run the command sudo apt-get install fonts-noto in the terminal. Afterwards, run dpkg-reconfigure fontconfig again, reboot and all should be like it was before.

Remove old kernels
9. You probably have installed new kernels from time to time. If so, you may want to clean up a bit, after a while.

After a kernel update, the old kernel still shows in the Grub boot menu, under the header Advanced options for Linux Mint. Because you might want to start your machine with the old kernel, if the new kernel doesn't function well....

So far, so good. But having more than one redundant kernel is superfluous and a waste of disk space, because each kernel uses up more than 200 MB (headers included). Below I describe various ways how you can remove old kernels and thereby clean up the Grub boot loader menu as well.

Note: Don't use cleaning applications like Bleachbit or Computer Janitor for this job! They're dangerous software wrecking balls and are at best superfluous.

Now let's get started:

Many old redundant kernels? Remove them all in one stroke
9.1. Is the amount of old kernels huge? This is how you can remove all old redundant kernels quickly, in one stroke:

a. Launch Update Manager. In the toolbar of Update Manager: View - Linux kernels

This may take some time. Then a warning window pops up. Ignore it and click "Continue" in order to proceed.

b. Press the button Remove Kernels... You should then get to see a list of all removable old kernels.

Note: I strongly recommend not to throw away all of them: leave at least one spare kernel installed. You never know when such a spare kernel might come in handy, for example when your currently active newer kernel suddenly starts misbehaving....

Removal of specific redundant kernels
9.2. You can also remove a specific redundant kernel. Like this:

a. Launch Update Manager. In the toolbar of Update Manager: View - Linux kernels

This may take some time. Then a warning window pops up. Ignore it and click "Continue" in order to proceed.

b. Ignore the button labeled Remove Kernels... , because that button is meant for mass removal. Just click on the kernel that you want to throw away. Then click on the "Remove" button.

Note: I strongly recommend to leave the latest redundant old kernel in your system, just to be on the safe side! It never hurts to have a spare kernel that's known to work well....

c. Now reboot your computer.

Automatic removal of old redundant kernels
9.3. The easiest and recommended way to prevent an accumulation of old redundant kernels, is to enable the automatic feature for removing obsolete kernels in Update Manager.

It's a safe tool to use and smart as well, because it leaves the latest redundant old kernel in your system, just to be on the safe side. It's wise to have one spare kernel that's known to work well...

You can enable this automatic feature as follows:

Update Manager - panel: Edit - Preferences

Tab Automation - section Automatic Maintenance - Remove obsolete kernels and dependencies: switch it on.

Important warning: Do NOT enable Apply updates automatically! Updates should never be installed automatically, because there's always a risk (however small) that they'll disrupt your work on the computer. That's why you should at all times install them yourself, at a time that suits you, when there's no risk of disruption of your computer jobs.

Finished! That's all you ever need to do. Doing more is risky and not advisable.

Set a reasonable maximum log size for systemd
10. The logs of systemd can sometimes grow too big. This is how to restrict their size to a sensible minimum:

a. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. First you're going to reduce their current size well below 100 MB, which should be more than enough in almost all circumstances. For that one-time action, copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo journalctl --vacuum-size=40M

Press Enter. Type your password when prompted. In Ubuntu this remains entirely invisible, not even dots will show when you type it, that's normal. In Mint this has changed: you'll see asterisks when you type. Press Enter again.

c. When that one-time job is done, you're going to put a permanent size cap of 100 MB on the logs. For setting that size cap, copy/paste the following command line into the terminal, in order to avoid typing errors. It's one big line:

sudo sed -i 's/#SystemMaxUse=/SystemMaxUse=100M/' /etc/systemd/journald.conf

Press Enter.

d. Now you're going to put a permanent number cap of seven log files on the logs. Which equals seven boot procedures.

For setting that number cap, copy/paste the following command line into the terminal, in order to avoid typing errors. It's one big line:

sudo sed -i 's/#SystemMaxFiles=100/SystemMaxFiles=7/g' /etc/systemd/journald.conf

Press Enter.

e. Then apply the new settings, with this terminal command (use copy/paste to transfer it into the terminal):

sudo journalctl --rotate

Press Enter.

You're done!

Optional: reduce other system logs
11. Besides taming the logs of systemd, as described in item 10 on this page, you can also reduce some other system logs. Under normal circumstances this won't free up nearly as much disk space as taming the systemd logs, but it's always fun to restrict the system log files to a sensible minimum....

Proceed as follows:

a. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. First you're going to delete current system logs. For that one-time action, copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo rm -v /var/log/*.log* /var/log/syslog*

Press Enter. Type your password when prompted. In Ubuntu this remains entirely invisible, not even dots will show when you type it, that's normal. In Mint this has changed: you'll see asterisks when you type. Press Enter again.

c. Now you're going to reduce the number of kept logs to 1, for two types of logs, in the settings file rsyslog. For the first log type, copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo sed -i 's/rotate 7/rotate 1/g' /etc/logrotate.d/rsyslog

Press Enter.

Then copy/paste this command into the terminal for the second log type:

sudo sed -i 's/rotate 4/rotate 1/g' /etc/logrotate.d/rsyslog

Press Enter.

d. Then you're going to set the log rotation for rsyslog to daily instead of weekly. Log rotation simply means starting afresh; you're going to configure your system to start each day with a new empty log, thus limiting its potential size. Proceed like this:

Copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo sed -i 's/weekly/daily/g' /etc/logrotate.d/rsyslog

Press Enter.

e. Now you're going to reduce the number of kept logs to 1, in another settings file named logrotate.conf. Copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo sed -i 's/rotate 4/rotate 1/g' /etc/logrotate.conf

Press Enter.

f. Then you're going to set the log rotation in logrotate.conf to daily instead of weekly. Copy/paste the following command line into the terminal, in order to avoid typing errors:

sudo sed -i 's/weekly/daily/g' /etc/logrotate.conf

Press Enter.

g. Finally, reboot your computer.

You're done!

Turn off the firewall log
12. Have you enabled the firewall ufw (which is recommended)? Then you'll probably never look at its logs, so it won't hurt to turn off all logging by the firewall. Especially because it can be rather spammy sometimes. Turning off its log can be done like this:

a. Launch a terminal window.
(You can launch a terminal window like this: *Click*)

b. Copy/paste this blue line into the terminal:

sudo ufw logging off

Press Enter. Type your password when prompted. In Ubuntu this remains entirely invisible, not even dots will show when you type it, that's normal. In Mint this has changed: you'll see asterisks when you type. Press Enter again.

Regrets? Then turn firewall logging on again like this
12.1. Do you want to enable logging by the firewall again? Then use the following terminal command to turn firewall logging on again with the default amount of activity (low):

sudo ufw logging low

All should be then, as it was before.

Emergency measure: dumping the Xorg logs automatically
13. Only to be applied as emergency measure! It's thankfully a rare problem, but it might happen that your Xorg log gets spammed so much with errors, that it fills up the hard disk. In such a case it's of course best to fix the error, thus stopping the log spamming. But if that's not possible, this is a quick-and-dirty workaround:

a. First remove the current logs. Copy/paste into the terminal:

sudo rm -v /var/log/Xorg*

Press Enter.

b. Then make sure that they're dumped automatically into /dev/null in the future. Copy/paste the following blue lines into the terminal:

First command:
sudo ln -s -v /dev/null /var/log/Xorg.0.log

Press Enter.

Second command:
sudo ln -s -v /dev/null /var/log/Xorg.0.log.old

Press Enter.

Regrets? Restoring the Xorg logs
13.1. If you wish to re-enable the Xorg logging again, execute these two commands:

sudo unlink /var/log/Xorg.0.log

sudo unlink /var/log/Xorg.0.log.old

Emergency measure: dumping the xsession error log automatically
14. Only to be applied as emergency measure! Thankfully this issue is rare, but it might happen that your xsession error log gets spammed so much with errors, that it fills up the hard disk. In such a case it's of course best to fix the error, thus stopping the log spamming. But if that's not possible, this is a quick-and-dirty workaround:

a. First remove the current logs. Copy/paste into the terminal:

rm -v ~/.xsession-error*

Press Enter.

b. Then make sure that they're dumped automatically into /dev/null in the future. Copy/paste the following blue lines into the terminal:

First command:
ln -s -v /dev/null ~/.xsession-errors

Press Enter.

Second command:
ln -s -v /dev/null ~/.xsession-errors.old

Press Enter.

Regrets? Restoring the xsession error log
14.1. If you wish to re-enable the xsession error logging again, execute these two commands:

unlink ~/.xsession-errors

unlink ~/.xsession-errors.old

Want to get rid of polluted settings in your web browser?
15. Do you have polluted settings in Firefox or Chrome (sometimes caused by rotten, shady or rogue add-ons), and do you wish to start anew with a clean browser? Then proceed like this:

a. First make a backup of your current web browser settings (because you never know why you might need them sometime):

- Launch a terminal window (this is how to launch a terminal window: *Click*).

- Use copy/paste to transfer the following blue command line to the terminal:

For Firefox:
cp -r -v ~/.mozilla ~/.mozillabackup

Press Enter.

For Chrome:
cp -r -v ~/.config/google-chrome ~/.config/google-chromebackup

Press Enter.

b. Now export your bookmarks to a backup file:

For Firefox:
Click the "Library" button (the one with the four bars) - Bookmarks - Show All Bookmarks (down below)

Import and Backup - Backup...

Save the bookmarks-xxx.json file to the location you prefer.

Later on, you can import your bookmarks again in a clean Firefox.

For Chrome:
On the upper right in your browser window, click on the three dots - Bookmarks - Bookmark manager

Click on the three white dots - Export bookmarks to HTML file...

Later on, you can import them again in your clean Chrome.

c. You will also lose all of your stored login passwords for websites! Make sure you know them all.

d. Close the web browser you wish to clean.

e. Launch a terminal window.

f. Copy/paste the following blue command line into the terminal, in order to avoid typing errors:

For Firefox:
rm -r -v ~/.mozilla && rm -r -v ~/.cache/mozilla

Press Enter.

For Chrome:
rm -r -v ~/.config/google-chrome && rm -r -v ~/.cache/google-chrome

Press Enter.

g. Launch your web browser again. It should be clean.

h. Import your old bookmarks from the backup you've created. Importing can be done by means of the same feature as the one you've used for exporting.

You're done! From now on, avoid all shady add-ons and extensions, and install only those that you really need and trust.
