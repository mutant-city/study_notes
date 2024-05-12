### SSH

1. Access remote systems using SSH

    * Secure Shell (SSH) provides a secure mechanism for data transmission between source and destination systems over IP networks.
    
    * SSH uses encryption and performs data integrity checks on transmitted data.
    
    * The version of SSH used is defined in `/etc/ssh/sshd_config`.
    
    * The most common authentication methods are Password-Based Authentication and Public/Private Key-Based Authentication.
    
    * The command *ssh-keygen* is used to generate keys and place them in the .ssh directory, and the command *ssh-copy-id* is used to copy the public key file to your account on the remote server.
    
    * TCP Wrappers is a host-based mechanism that is used to limit access to wrappers-aware TCP services on the system by inbound clients. 2 files `/etc/hosts.allow` and `/etc/hosts.deny` are used to control access. The .allow file is referenced before the .deny file. The format of the files is \<name of service process>:\<user@source>.
    
    * All messages related to TCP Wrappers are logged to the `/var/log/secure` file.
    


### Hardening SSH server


* Disable root login
    * SSH servers by default have root login enabled
    * modify the PermitRootLogin parameter in /etc/ssh/sshd_config and reload or restart the service.
* Disable password login
* Configure a nondefault port for SSH to listen on
    * /etc/ssh/sshd_config change port line
    * Active sessions will not be disconnected after restarting the SSH server (unless you fail to restart the SSH server successfully).
    * Network ports are labeled with SELinux security labels to prevent services from accessing ports where they should not go.
    * To allow a service to connect to a nondefault port, you need to use semanage port to change the label on the target port.
    * Before doing so, it is a good idea to check whether the port already has a label. You can do this by using the semanage port -l command.
    * If the port does not have a security label set yet, use -a to add a label to the port. If a security label has been set already, use -m to modify the current security label.
* Allow specific users only to log in on SSH
    * in /etc/ssh/sshd_config file
    * AllowUsers. This option takes a space-separated list of all users that will be allowed login through SSH.


### Cache SSH passphrase
1. Type ssh-agent /bin/bash to start the agent for the current (Bash) shell.
2. Type ssh-add to add the passphrase for the current user’s private key. The key is now cached.
3. Connect to the remote server. Notice that there is no longer a need to enter the passphrase.
* This procedure needs to be repeated for all new sessions that are created.