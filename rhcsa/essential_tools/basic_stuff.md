1. Use input-output redirection (>, >>, |, 2>, etc.)
	* essentially change the output/input from monitor/keyboard

    * The default locations for input, output, and error are referred to as standard input (stdin), standard output (stdout), and standard error (stderr). 
		* These are known as streams and streams are treated like files (like almost everything on linux)
		* The file descriptors for the streams are:
			* file descriptor 0: stdin -> default is keyboard
			* file descriptor 1: stdout -> default is monitor
			* file descriptor 2: stderr
		* Redirection symbols:
			* < or 0<
			* > or 1>
			* 2>
    
    * Standard input redirection can be done to have a command read the required information from an alternative source, such as a file, instead of the keyboard. For example:
        ```shell
        cat < /etc/cron.allow 
        ```

    * Standard output redirection sends the output generated by a command to an alternative destination, such as a file. For example:
        ```shell
        ll > ll.out
        ```

    * Standard error redirection sends the output generated by a command to an alternative destination, such as a file. For example: 
        ```shell
        echo test 2> outerr.out
        ```

    * Instead of > to create or overwrite, >> can be used to append to a file.

    * To redirect both stdout and stderror to the same file:
        ```shell
        echo test >> result.txt 2>&1
        ```

	* This command will direct stdout to a file called capture.txt and stderr to a file called error.txt:
		```shell
		/error.sh 1> capture.txt 2> error.txt
        		```




* Everything in linux is a file (or at least trys to be)
    * can be accessed with read() and write()
    * hardware can be accessed via device files in /dev
    * streams are files
    * network sockets are files
* Pipes
    * redirect output of one command to another command
* History: gives command history
    * cntr + r
    * -c clears current history, -w clears ALL history(can also delete ~/.bash_profile)
    * located in ~/.bash_history (all commands kept in memory until shell closed then history is written)
* Bash cmpletion
    * Can hit tab twice on incomplete commands or filenames and cli will autocmplete ghe command or file
* Environment files
    * login shells:
        * When ssh'ing into systems, when logging in the FIRST TIME to system
        * /etc/profile: used to configure ALL login shells
        * ~/.profile, /.bash_profile, /etc/zprofile, ~/.zprofile
    * non-login shells:
        * a subshell, terminal app, script
        * a terminal typically creates a subshell when it opens
            * the terminal program decides though whether to be login shell or not
            * mac osx is login shell though
        * /etc/bashrc, ~/.bashrc, ~/.zshrc 
    * interactive vs non-interactive
        * interactive: you will input commands
        * non-interactive: a script or command passed which opens a new shell environment
        * interactive login shells: standard SSH cnxxn
        * non interactive login shell: running a local script on remote computer via ssh
    * identify if in login shell
        ```shell
            prompt> echo $0
            -bash # "-" is the first character. Therefore, this is a login shell.

            prompt> echo $0
            bash # "-" is NOT the first character. This is NOT a login shell.
        ```
* login files:
    * /etc/motd: after login
    * /etc/issues: before login, good for specifying login issues or security concerns


1. Log in and switch users in multiuser targets

    * A user can switch to another user using the *su* command. The *-i* option ensures that the target users login scripts are run:
        ```shell
        sudo -i -u targetUser
        ``` 

    * To run a command as root without switching:
        ```shell
        sudo -c
        ``` 

    * The configuration for which users can run which commands using sudo is defined in the `/etc/sudoers` file. The visudo command is used to edit the sudoers file. The sudo command logs successful authentication and command data to `/var/log/secure`.

    * su -
        * 

* chvt 
    * switches between virtual terminals


* if a command is aliased can use a forward slash to ignore the alias
    * ie if ls is aliased to ls -la use \ls to use the original command



* Power off
    * shutdown [flags] [now | {time format}] [any message string]
        * like poweroff but gracefully shuts off machine
        * -r  will reboot after shutdown
        * allows a delay string
            * time format can be: +20 to shutdown in 20 min or actual time 05:00
        * message string notifys all users on the system
        * sudo shutdown -r +10 "System upgrade"
        * cancel a scheduled shutdown
            * sudo shutdown -c "Cancelling reboot"
    * commands:
        * systemctl reboot, 
        * reboot, 
        * systemctl halt, 
        * halt, 
        * systemctl poweroff, 
        * poweroff
        * shutdown -r now
        * init 6
        * sudo systemctl start reboot.target
    * poweroff talks to power management on the machine to shutoff power, sends ACPI command
    * halt shuts down system without powering off, does not shutoff power
    * echo b > /proc/sysrq-trigger
