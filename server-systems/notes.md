# Lab 1

- DNS records are saved locally in the hosts file
- $ before prompt = signed in as a regular user
- to see your current username: whoami
- you can see information about any command by using the `man` command
- paginate trough files: ls / | less or ls / | more
- pause command: Ctrl+z
- resume it: fg
- find the process: ps aux | grep <command>
- kill it: kill <PID>
- find where executable is stored: which <exe>
- show file content: cat
- show first two lines of file: cat <file> | head -n 2
- show last line of file: cat <file> | tail -n 1
- grep with line number: grep -n <expr>
- create hard link (sets to same inode): ln <src> <target>
- create a symbolic link (contains path): ln -s <src> <target>
- only show the permissions of a file: ls -l <file> | cut -d ' ' -f 1
- permission format: owner group other, 4 = r, 2 = w, 1 = x
- only allow root to read a file: chown root <file> & chmod 400 <file>
- change the owner of a folder recursivly: chown -R <dir>
- see supported shells: cat /etc/shells
- open dash shell: dash
- exit to previous shell: Ctrl+d or exit
- make variables persistent: export variable-name
- see how much disk space you have free: df -k
- see processes a user started: ps -u <user>
- see memory usage: free 
- see cpu usage: top
- get passwd line of current user: grep $(whoami) /etc/passwd
- power down: shutdown now


## Tmux comamnds

- start a named session: tmux new-session -s <name>
- split your tmux session window horizontally (create a new pane) while in a tmux session: Ctrl+b "
- split your tmux session window vertically (create a new pane) while in a tmux session: Ctrl+b %
- switch focus between panes while in a tmux session: Ctrl+b arrow_key
- detach from your named session: Ctrl+b d
- re-attach to your existing named session: tmux attach -t <name>
- list all tmux sessions in the terminal: tmux list-sessions
- destroy the named session: tmux kill-session -t <name>
- go into copy mode: Ctrl+b [


# Lab 2

- get all sources: grep '^deb ' /etc/apt/sources.list
- debian sources format: deb <options> <uri> <suite> <component1> <component2>
- list all packages that start with <x>: apt list "<x>\*"
- get package details: apt show <package>
- show maintainer of package and hide error stream: apt show <package> 2>/dev/null | grep '^Maintainer:'
- get from the second fragment of command with delimiter( ): cut -d ' ' -f 2-
- assign variable to output of command: <variable>=$(<command>)
- see what files are installed by a package: dpkg -L <package name>
- find package in dpkg index: dpkg -l <package name>
- see time vm was on: uptime
- find to which package a command belongs: dpkg -S $(which <command>)
- find and execute command on each file: find /etc/default -type f -exec dpkg -S {} \;


# Lab 3

- input and return number of lines: cat | tee <file> | wc -l
- gunzip uncompress file into stdout: gunzip -c <file> | less
- same as above but with zless: zless <file>
- download and unzip gzip: wget -O - <url> | gunzip -c | tar xf -
- create a named pipe: mkfifo <file>
- copy data: dd if=/dev/urandom of=/tmp/gibberish bs=1024k count=10
- file information: stat <filename>
- get file type: file <filename>
- unzip with gzip: gzip -dc <filename> > <target>
- disk free: df -h
- disk usage: du -h
- disk usage in bytes: du -b
- mounted file systems: mount or /proc/mounts or /etc/mtab
- file systems that get mounted on boot: /etc/fstab
- make FAT16 file system of a image: mkfs.fat -F 16 <image>
- read binary content (hex reader): xxd <file>
- read strings of binary file (uses binutils package): strings <file>
- mount loopback image: mount -o loop <image> /mnt
- unmount a fs: umount /mnt

# Lab 4

- find current user its id: id (look at uid field)
- see current user its groups: groups
- add a group to a user: adduser <user> <group>
- the /etc/group file stores the information about user groups on the system (can be managed by vigr)
- groups command is based on the login session, so when updated a refresh or re-login is requird
- edit sudoer's file: visudo
- grep sudoers groups: sudo cat /etc/sudoers | grep '^%'
- su execute command as root: su -c "<command>"
- difference between su and sudo: sudo requires your own password and su root password, su logs it as root who did that and sudo as your normal user, su runs all commands as super user and sudo can be fine-grained
- use sudo to obtain root shell: sudo su -
- open man page for passwd file: man 5 passwd
- find man page for application: find /usr/share/man -name '*<query>*' or man -k <query> (1 is for shell commands, 5 for file formats)
- edit passwd file: vipw
- you are always executing something on behalf of a group, not a user
- work on behalf of a group: newgrp <group>
- edit /etc/shadow file: vipw -s
- password expiry: chage
- recursivly set chmod: chmod -R <params>
- find files with certain permissions: find / -perm <permission>
- set default file execution as the file owner (even if you are another user): chmod +u+s <file>
- previous point can be prevent by setting the nosuid in mount option in /etc/fstab
- lock a user from logging in: passwd -l <username>
- unlock such a lock: passwd -u <username>
- if a user is locked from logging in a ! is prepended to the password in the /etc/shadow file
- find all files owned by the current user: find / -user $(whoami) 2>/dev/null
- find all files owned by a group: find / -group <group> 2>/dev/null
- set default permissions for new files that are created (filters out what permissions should not be set, eg 777 results in no permissions, the permission gets subtracted): umask <permission>
- a default umask can be set in the .bashrc file, which can be reloaded using `source .bashrc`
- a message of the day (motd) can be set in the /etc/motd file
- default files for a new user (its skeleton) can be found in /etc/skel
- add a user: useradd <user>
- delete a user: userdel <user>
- add user to group with usermod: usermod -aG <group> <user>

# Lab 5

- create new ssh credentials: ssh-keygen
- save credentials: ssh-copy-id <user@host>
- save credentials windows: put public key in .ssh/authorized_keys
- confirm sftp is enabled in /etc/ssh/sshd_config
- sftp user@ip
- upload file: put <file> <final_name>
- download file: get <file> <final_name>
- nfs file exports file: /etc/exports
- /etc/exports apply changes: exportfs -r
- /etc/exports format: <location> <ip>/<range>(<params>), for example /usr/share/doc 192.168.0.0/16(ro,sync,no_subtree_check)
- mount a nfs share: mount <ip>:<location> <mount point>, for example sudo mount 192.168.37.140:/usr/share/doc /mnt
- no_root_squash option: allows root users to write
- edit scheduled jobs: crontab -e
- see manual for crontab format: man 5 crontab
- crontab time fields: minute (0-59), hour (0-23, 0 = midnight), day (1-31), month (1-12), weekday (0-6, 0 = Sunday), an * can be used for when it should be run for every instance, a `,` can be used for or concatination, and a `-` can be used for defining a range
- display crontab to the stdout: crontab -l
- remove current crontab: crontab -r
- allowing/denying user-level cron: /etc/cron.allow or /etc/cron.deny list users who are able to do that action
- only allow root for cron: create empty cron.deny
- set preffered editor in .bashrc: export EDITOR=nvim
- run scripts as root within the cron folders: /etc/cron.hourly/, /etc/cron.daily/, /etc/cron.weekly/, and /etc/cron.monthly/ 
- to run a crontab as non root: minute(s) hour(s) day(s)-of-month month(s) day(s)-of-week user command
- schedule a task with `at`: at <time><AM|PM> (enter, type script and ctrl+D to exit)
- see scheduled at's: atq


## Special cron strings

```
string      meaning 
@reboot     Run once, at startup. 
@yearly     Run once a year, "0 0 1 1 *". 
@annually   (same as @yearly) 
@monthly    Run once a month, "0 0 1 * *". 
@weekly     Run once a week, "0 0 * * 0". 
@daily      Run once a day, "0 0 * * *". 
@midnight   (same as @daily) 
@hourly     Run once an hour, "0 * * * *". 
@reboot     /path/to/execuable1
```


# Lab 6

- apache disable events, and create a new process for each request: s2dismod mpm_event && a2enmod mpm_prefork
- restart apache: systemctl restart apache2
- list all port usage (net-tools): netstat -plnt
- download file: wget <uri>
- w3m browser: w3m <url>
- see processes: top (or use a variation like htop or btop++)
- see visual tree of running processes and their children (psmisc): pstree
- find all processes of a application: ps -ef | grep <application> or ps aux | grep <application>
- find all process id's of an application: pidof <application>
- see all signals: man 7 signal
- kill a process: kill <PID>
- kill a process by name: pkill <application>
- send signal to process: kill -<signal> <PID>
- manage apache with its build in tool: apache2ctl
- read environment variables from a process: cat /proc/<PID>/environ
- read default umask from a process: cat /proc/<PID>/status | grep Umask


## Signals

- SIGCHLD: one of your child processes died and you need to reap the zombie (so you know its exit status: 0 = success or something else = a (possibly minor) problem occurred)
- SIGINT: you  are  currently  working  but  the  user  wants  to  interrupt  whatever  you  are  doing  (for example, to go back to a prompt or menu) and they just pressed Ctrl-C
- SIGSEGV , SIGBUS: you had a segmentation fault (memory error); you should clean up, close open files, save some data and exit as soon as possible
- SIGHUP: you are still running, but the user just rudely closed their ssh window and there is no one reading what you write on the terminal anymore (hangup)
- SIGKILL: the kernel is forcibly killing you (no chance to override this)
- SIGTERM (terminate): the system or user want you to stop, and instead of using your Exit command (or q key), they chose to send you a signal Note When shutting down or rebooting your server, systemd will eventually send all processes the SIGTERM signal to stop them. For daemons (services running in the background) like apache, this is the only way to quit them, as there is no CLI or GUI visibly running; it's running in the background. Note 2 A process may be malfunctioning or behaving badly, or it may prefer not to obey your request (yet, or at all) because it wants to save some data first, ... If you really want it to stop and it is not responding to the SIGTERM signal for whatever reason, you can send the more drastic SIGKILL signal (point above) which will always work. When rebooting or shutting down, systemd will first try SIGTERM, and if the process takes too long to obey, it will eventually kill it off using SIGKILL. That’s what you sometimes see when shutting down your vm.
- SIGQUIT: the user really wants you to stop and insists, but wants to be nice and give you a chance to shut down gracefully.



# Lab 7

- requirements for man and info pages: info, bash-doc 
- top of file: head -n <lines>
- bottom of file: tail -n <lines>
- recursive force removal: rm -rf
- create file with argument name: touch -- <name>
- remove file with argument name: rm -- -rf
- get the word count of an output: wc -l
- read input into variables: read <var1> <var2> ... (example: read firstname lastname info
- command substitution (use a command in the call of another): $(...)
- write read to file: read <var1> <var2> < <myfile>
- get duplicate lines: sort <file> | uniq -d > <out-file>
- sort unique (no duplicates): sort -u <file>
- sort reverse: sort -r <file>





## Bash parsing schema

 make arguments into next command
┌────────────────────────────────┐
│                                ▼
│ ┌───────────────────────────────────────────────────────────┐
│ │                        split into                         ├──┬────────┐
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │        │
│ ┌───────────────────────────────────────────────────────────┐  │        │
│ │                      brace expansion                      │  │        │
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │ double │
│ ┌───────────────────────────────────────────────────────────┐  │ quotes │
│ │                      tilde expansion                      │  │        │
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │        │
│ ┌───────────────────────────────────────────────────────────┐  │        │
│ │                    parameter expansion                    │◄─┘        │
│ └───────────────────────────────────────────────────────────┘           │
│                                ▼                                        │
│ ┌───────────────────────────────────────────────────────────┐           │ single
│ │                   command substitution                    │           │ quotes
│ └───────────────────────────────────────────────────────────┘           │
│                                ▼                                        │
│ ┌───────────────────────────────────────────────────────────┐           │
│ │                  arithmetic substitution                  ├──┐        │
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │        │
│ ┌───────────────────────────────────────────────────────────┐  │        │
│ │                      word splittion                       │  │        │
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │ double │
│ ┌───────────────────────────────────────────────────────────┐  │ quotes │
│ │                    pathname expansion                     │  │        │
│ └───────────────────────────────────────────────────────────┘  │        │
│                                ▼                               │        │
│ ┌───────────────────────────────────────────────────────────┐  │        │
│ │command lookup: function, build-in command, executable file│◄─┘◄───────┘
│ └─────────────────────────────┬─────────────────────────────┘
│                               │
│                               ▼
│                       xxxxxxxxxxxxxxxxx
│                       x               x
└────────── eval ───────x  run command  x
                        x               x
                        xxxxxxxxxxxxxxxxx


## Bash execution order

1.	read input from file, string or terminal
2.	break up into tokens separated by meta-characters and obeying quoting rules
3.	parse tokens
4.	shell expansions
5.	redirect
6.	execute
7.	optionally wait and collect exit status


## Brace expansion

1. Pattern Matching: Use brace expansion to generate multiple strings based on a pattern. {red,green,blue}apple
    * Output: redapple greenapple blueapple
2. Numeric Range: Specify a range of numbers inside curly braces to generate a sequence of strings. Number{1..5}
    * Output: Number1 Number2 Number3 Number4 Number5
3. Character Range: Specify a range of characters inside curly braces to generate a sequence of strings. {A..D}
    * Output: A B C D
4. Combining Patterns: Combine multiple brace expressions to generate all possible combinations. {a,b}{1,2}
    * Output: a1 a2 b1 b2
5. Nested Brace Expansion: Nest brace expansions to create more complex combinations. {a,{1..3},{x,y}}
    * Output: a 1 2 3 x y


## Tilde expansion 

~ = home directory
~<username> = home directory of another user
~+ = current working directory
~- = previous working directory

> PRO TIP xoxo: if you moved from directory and would like to go back to your previous directory, you can just type `cd -`


## Bash operations

- VAR++ VAR-- variable post-increment and -decrement
- ++VAR –VAR	variable pre-increment and -decrement
- + -			unary plus/minus
- ~ !			logical/bitwise negation
- **			exponentiation
- * / %		multiplication, division, modulo
- + -			addition and subtraction
- << >>		left/right bitwise shift
- <= >= < >		comparison operators
- == !=		equality and inequality
- &			bitwise AND
- ^			bitwise exclusive OR
- |			bitwise OR
- &&			logical AND
- ||			logical OR
- expr?expr:expr	c-style conditional operator
- = *= /= %= +=
- -= <<= >>= &=
- ^= !=|		assignments
- ,			expression separator


## Filename expansion patterns

- *			          0 (inclusive!) or more characters
- ?			          exact 1 character
- [abcd]		      exact 1 character, but only those that are listed (here: a, b, c or d)
- [a-d]			      exact 1 character, but only those that are listed (here: a till d)
- [^ab]  [!ab]	  exact 1 character, but not those that are listed (here: not a nor b)
- \	              preserve literal value of the next character
- "…"	            preserves the literal value of all characters within the quotes, with the exception of $, ` and \
- '…'	            preserves the literal value of each character (incl backslash!) within the quotes


## File descriptors

- 0	STDIN
- 1	STDOUT
- 2	STDERR


## Redirections:

- >	write
- >>	append
- >|	overwrite


## Conditionals


1. Equal (==): Checks if two strings are equal. if [ "$var" == "value" ]
    * Example: if [ "$name" == "John" ]
2. Not Equal (!=): Checks if two strings are not equal. if [ "$var" != "value" ]
    * Example: if [ "$status" != "active" ]
3. Less Than (-lt): Checks if a numeric value is less than another. if [ "$num" -lt 10 ]
    * Example: if [ "$count" -lt 5 ]
4. Greater Than (-gt): Checks if a numeric value is greater than another. if [ "$num" -gt 20 ]
    * Example: if [ "$score" -gt 90 ]
5. Less Than or Equal To (-le): Checks if a numeric value is less than or equal to another. if [ "$num" -le 5 ]
    * Example: if [ "$age" -le 18 ]
6. Greater Than or Equal To (-ge): Checks if a numeric value is greater than or equal to another. if [ "$num" -ge 10 ]
    * Example: if [ "$temperature" -ge 25 ]


## Loops

1. For Loop: Executes a set of commands for a specified number of times or for each item in a list.
    ```bash
    for variable in list
    do
        # commands
    done

    #Example:
    for i in {1..5}
    do
        echo "Iteration: $i"
    done
    ```

2. While Loop: Executes a set of commands as long as a specified condition is true.
    ```bash
    while condition
    do
        # commands
    done

    # Example:
    count=1
    while [ $count -le 5 ]
    do
        echo "Count: $count"
        ((count++))
    done
    ```

3. Until Loop: Executes a set of commands until a specified condition becomes true.
    ```bash
    until condition
    do
        # commands
    done

    #Example:
    count=1
    until [ $count -gt 5 ]
    do
        echo "Count: $count"
        ((count++))
    done
    ```


## Arguments


### Positional Parameters: The arguments passed to the script or function are stored in positional parameters.

- $0: Name of the script or function itself.
- $1, $2, $3, ...: Value of the 1st, 2nd, 3rd, ... argument, respectively.
- $@: All the arguments passed as an array.
- $#: Number of arguments passed.


### Special Variables:

- $?: Exit status of the last executed command.
- $$: Process ID (PID) of the current script or shell.
- $!: PID of the last background command.
- $RANDOM: Random number between 0 and 32767.
- $LINENO: Current line number in the script.


## Functions scope example

function hello {
    local LOCAL="local"
    INNER="non-local"
    SCOPE="inner scope"
    echo "inside hello:"
    echo -e "\tSCOPE: $SCOPE"
    echo -e "\tINNER: $INNER"
    echo -e "\tLOCAL: $LOCAL"
}
echo -e ''$_{1..80}'\b_'
echo ''; echo "before hello:"
echo -e "\tSCOPE: $SCOPE"
echo -e "\tINNER: $INNER"
echo -e "\tLOCAL: $LOCAL"
echo -e ''$_{1..80}'\b_' ; echo ''
hello
echo -e ''$_{1..80}'\b_'
echo ''; echo "after hello:"
echo -e "\tSCOPE: $SCOPE"
echo -e "\tINNER: $INNER"
echo -e "\tLOCAL: $LOCAL"
echo -e ''$_{1..80}'\b_' ; echo ''

________________________________________________________________________________

before hello:
        SCOPE:
        INNER:
        LOCAL:
________________________________________________________________________________

inside hello:
        SCOPE: inner scope
        INNER: non-local
        LOCAL: local
________________________________________________________________________________

after hello:
        SCOPE: inner scope
        INNER: non-local
        LOCAL:
________________________________________________________________________________


## Advanced shell features

1. Grouping commands in bash using parentheses (… ; … ; …) creates a subshell, while curly braces {… ; … ; …} do not. Commands within parentheses are executed in a subshell, which means changes to the shell environment are not propagated to the main shell. Commands within curly braces are executed in the current shell.

2. Invoking a script in bash can be done in different ways:
    * ./<some-script> executes the script in a subshell, using the current shell environment.
    * .<some-script> or source <some-script> executes the script in the current shell, without creating a subshell. It allows modifications to the shell environment.

Running ./<some-script> runs the script as an executable file, while .<some-script> and source <some-script> execute the script within the current shell, allowing for environment changes to persist.


# Lab 8

- network interfaces for ifup and ifdown are stored in /etc/network/interfaces
- add a static interface example:
	iface eth0 inet static
	    address 192.168.1.100
	    netmask 255.255.255.0
	    broadcast 192.168.1.255
	    (gateway 192.168.1.255)
- allow autmatic statup of interface (boot): auto <interface>
- allow startup when event: allow-hotplug <interface>
- dhcp interface: iface <inteface> inet dhcp
- change state of interface: ifup/ifdown <interface>
- change with ifconfig: sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
- change dns information: /etc/resolv.conf
- show the default router: ip a
- flush ip (removes entries): ip a flush dev <interface>
- flush route entries: ip route flush table all
- flush neighbour cache: ip neigh flush all
- get route table: netstat -r
- get route table with numeric addresses (net-tools): route -n
- get route table with ip: ip route show
- change default gateway: route del default gw 192.168.X.2 && route add default gw 10.10.X.2
- dummy name serve (hosts file): /etc/hosts
- check if DHCP daemon is running: ps -ef | grep dhclient
- installing dnsmasq: apt install dnsmasq
- dnsmasq config file: /etc/dnsmasq.conf
- dnsmasq uses the /etc/resolv.conf file to find out to which nameserver it should forward its queries
- test dnsmasq config for validity: dnsmasq --test
- dnsmasq set dhcp lease range and time (/etc/dnsmasq.conf): dhcp-range=<from>,<to>,<time> for example dhcp-range=10.10.37.100,10.10.37.110,12h
- folder which stores the dhcp leases: /var/lib/dhcp/
- lease ip to mac address with name: dhcp-host=<mac>,<name>,<ip>,<time> for example dhcp-host=00:0c:29:55:ac:ea,boris,10.10.37.113,24h
- change nameserver: server=8.8.8.8


# Lab 9

- dnsmasq pxelinux.0 bootloader specification: dhcp-boot
- enable tftp auth (only server files owned by the dnsmasq user): tftp-secure
- tar unzip file verbosely to directory: tar -xzvf <file>.tar.gz -C <target folder>
- NOTE FOR NFS: make sure the no_root_squash option is present
- use debootstrap to create a debian fs in a directory: sudo debootstrap --arch=amd64 stable /srv/clientrootfs http://deb.debian.org/debian/
- install the linux kernel: apt install linux-image-amd64
- use directory as root fs: chroot <dir>
- the /boot files from the fs need to be copied to the tftp nfs, make sure to remove the version suffixes
- also copy the pxelinux.0 net bootloader
- contents of the pxelinux.cfg/default file example:
	DEFAULT netboot
	SAY Netbooting my familyname-firstname-Pixie
	TIMEOUT 0
	PROMPT 0
	LABEL netboot
	KERNEL vmlinuz
	APPEND initrd=initrd.img ip=dhcp root=/dev/nfs nfsroot=yourprime’s10.10.XX.YY_address:/srv/clientrootfs rw --
- the host of the fs can see and edit all files that are done on the fs (even if it was changed from another computer through the network boot), this is because all changes are saved to the host disk fs
- booting without a nfs root system means that it will use the ram as a fs
- you can mount a iso as a cdrom as a loop device, here is an example: mount -o loop -t iso9660 dsl-4.4.10-initrd.iso /mnt
- networkboot pxelinux.cfg/default example file:
	DEFAULT dsl
	SAY Netbooting my familyname-firstname-Pixie via MAC-address recognition
	TIMEOUT 0
	PROMPT 0
	LABEL dsl
	KERNEL linux24
	APPEND initrd=minirt24.gz ip=dhcp ramdisk_size=100000 init=/etc/init BOOT_IMAGE=knoppix --


# Final note

Good luck everone, I really had a great refresher by creating this refference. 
Greetings, Artur De Witte

~ publicly available at https://github.com/Arthurdw/expertise 
