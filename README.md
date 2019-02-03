# ubuntu-motd-login-warning
A bash script display a Message of the Day (motd) warning when a user successfully connects over Secure Shell (SSH).

## Background

If you want something to be printed as a message of the day or motd in Ubuntu, the proper way is to add a shell script to the `/etc/update-motd.d/` directory.

Here's the default content of that directory:

```
00-header             50-motd-news   80-livepatch          95-hwe-eol         98-reboot-required
10-help-text          51-cloudguest  90-updates-available  97-overlayroot     
50-landscape-sysinfo  80-esm         91-release-upgrade    98-fsck-at-reboot
```
The files are just shell scripts that are, with few exceptions, processed in order by name. If you want your script to be run and the output displayed before `10-help-text`, just name your `script 09-my-script`. 

A few caveats:

* The script should do what it does and display output to standard output.
* The script must be executable, as with any script. `sudo chmod + x your-script-name`
* The script should display a blank line at the beginning of its output. `echo`
* The script should have a end with a newline character. 
* The script should run quickly or cache its output. 
* The script filename should be preceded by a two digit number.
* The file name should not have any file extension.

See the man page entry for `update-motd` for details. `man update-motd`

## [Project Goal](#project-goal)

Demonstrate how to add a file to present your own motd message and provide a sample file for you to use.

## Who This Is For

Any Ubuntu users who want to customize their motd messages.

This can be useful for a legal warning telling would-be bad guys the system is not open access and they should leave if they are unauthorized, or for presenting any information about your system you like to see at login.

## What It Does

If you follow the instructions provided and copy the file `96-access-warning` to the `/etc/update-motd.d/` directory, the following message will be displayed, along with the other default messages, when a user logs in to your server:

```

-------------------------------------------------------------------------------
    ___         __  __               _                __
   /   | __  __/ /_/ /_  ____  _____(_)___  ___  ____/ /
  / /| |/ / / / __/ __ \/ __ \/ ___/ /_  / / _ \/ __  /
 / ___ / /_/ / /_/ / / / /_/ / /  / / / /_/  __/ /_/ /
/_/ _||\__,_/\__/_/ /_/\____/_/  /_/ /___/\___/\__,_/
   /   | _____________  __________
  / /| |/ ___/ ___/ _ \/ ___/ ___/
 / ___ / /__/ /__/  __(__  |__  )
/_/__||\___/\__||\___/_||_/____/
  / __ \____  / /_  __/ /
 / / / / __ \/ / / / / /
/ /_/ / / / / / /_/ /_/
\____/_/ /_/_/\__, (_)
             /____/

ALERT! You are logging into a secured device! Your IP Address, Login Time, and
Username have been noted and have been sent to the server administrator!

 This service is restricted to authorized users only. All activities on this
system are logged.

 Unauthorized access will be fully investigated and reported to the
appropriate law enforcement agencies.

--------------------------------------------------------------------------------

```

## Prerequisites

There are no prerequisites to achieve before adding this warning banner to your motd files.

It is helpful if you understand how to use a text editor such as `vim` or `nano`.

It is helpful if you understand how `sudo` permissions work.

## Installing

Read and understand the content of the `96-access-warning` file. Once you're satisfied that it won't cause harm, copy it into your /etc/update-motd.d directory. You can either download it directly to your server or just type `sudo vim 96-access-warning` (substitute vim with nano if you prefer) from within the `/etc/update-motd.d/` directory hit `i` for insert if using vim, and paste the content into the file.

Once the file is in your `/etc/update-motd.d/` directory, make it executable by typing `sudo chmod +x 96-access-warning`.

## Usage

Just log in using SSH and see your new banner. If you prefer it be earlier or later in your list of displayed content, just change the leading two digit number so it appears before or after the others as appropriate.

## Updates

Just do a `git pull` to update to the latest version if you're using this in your own git repository, or update the content in the `96-access-warning` file. 

You can change the content to anything you'd like to see at login, but I encourage you to change the file name to something that makes sense for what is displayed should you choose to do this.


## Author

* **Ted LeRoy** - *Initial Work* - `96-access-warning`

## License

This project is licensed under the GNU General Public License - see the [LICENSE.md](https://github.com/TedLeRoy/docksec/blob/master/LICENSE) file for details.

## Acknowledgements

* Thanks to the open source community for keeping the information flowing freely!
* I did find the warning message contained in the script that said it was OK to use, but sadly don't remember where I found it. Thanks to whoever wrote it!

## Built With

sh on Ubuntu 18.04.1 LTS Server 

## Shellcheck

This script has been tested on [ShellCheck](https://www.shellcheck.net/) and runs clean. Try out ShellCheck for your scripts!

## Future Goals

Nothing really. This is a super small project.

## Run Results

Here's a screenshot of the warning displayed when the script is run on login:

![login-script-run-results](https://i.ibb.co/rHNM3mB/script-run-screenshot.png)
