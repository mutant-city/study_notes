### General info
* if a command is aliased can use a forward slash to ignore the alias
    * ie if ls is aliased to ls -la use \ls to use the original command


* Programmable completion for bash is provided in the bash-completion module. To install this module:
    ```shell
    sudo dnf install bash-completion
    ```

### Types of commands
* internal commands: part of shell itself
* external commands: a file on the path
* use `type` to see if command is internal or external and if an alias or not

```
$ type ls
ls is aliased to `ls --color=auto'

$ type cd
cd is a shell builtin

$ type type
type is a shell builtin

$ type /bin/ls
/bin/ls is /bin/ls
```


### General commands
* env
    * Print all environmental variables

* time
    * Time taken to run a command

* uptime
    * Show system uptime

* uname
    * -a (details)
    * System information

* clear
    * Clear the screen

* which
    * Show path to a command file as if that command was being typed in at the prompt

* type
    * If the command is an alias, the output will show the alias definition.
    * If the command is a shell built-in, the output will indicate that.
    * If the command is a shell function, the output will show the function definition.
    * If the command is an external executable, the output will show the path to the executable.

* tty
    * Display terminal name

* `chvt `
    * switches between virtual terminals



### Command redirection

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

    * Standard error redirection sends the error output generated by a command to an alternative destination, such as a file. For example: 
        ```shell
        echo test 2> outerr.out
        ```

    * Instead of > to create or overwrite, >> can be used to append to a file.

	* This command will direct stdout to a file called capture.txt and stderr to a file called error.txt:
		```shell
		/error.sh 1> capture.txt 2> error.txt
        		```

    * To redirect both stdout and stderror to the same file:
        ```shell
        echo test >> result.txt 2>&1
        ```

    * Pipes
        * redirect output of one command to another command
        * `cat somefile.txt | grep someword`


### Shell types
* login shells:
    * When ssh'ing into systems, when logging in the FIRST TIME to system, when using `su <username>`
    * /etc/profile: used to configure ALL login shells
    * ~/.profile, /.bash_profile, /etc/zprofile, ~/.zprofile
        * for just a specific user

* non-login shells:
    * a subshell, terminal app, script
    * a terminal typically creates a subshell when it opens
        * the terminal program decides though whether to be login shell or not
        * mac osx is login shell though
    * /etc/bashrc, ~/.bashrc, ~/.zshrc 
        * runs for non-login shells

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

### History
* `history`: gives command history
    * cntr + r
    * -c clears current history, -w clears ALL history(can also delete ~/.bash_history)
    * located in ~/.bash_history (all commands kept in memory until shell closed then history is written)


### Login files
* login files:
    * /etc/motd: after login
    * /etc/issues: before login, good for specifying login issues or security concerns



### Everything in linux is a file (or at least trys to be)
    * can be accessed with read() and write() system calls
    * hardware can be accessed via device files in /dev
    * streams are files
    * network sockets are files


### Bash cmpletion
    * Can hit tab twice on incomplete commands or filenames and cli will autocmplete ghe command or file


