# Ubuntu NAS Setup

A basic guide on setting up different file sharing solutions on Ubuntu as a basic NAS server.

## Headless Mode(No GUI)

Edit the file `/etc/default/grub`:

`sudo nano /etc/default/grub`


Change the `"quiet splash"` on the following line to `"text"`(use `ctrl+x` to save and exit):

`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`


Update the boot configuration with:

`sudo update-grub`


Set `systemd` to the multi-user run level:

```
sudo systemctl enable multi-user.target --force
sudo systemctl set-default multi-user.target
```

The GUI can be started at any time by running `startx` when logged in.


## SFTP

An encrypted file transfer protocol that runs on top of SSH.

Pros:
 - Standard support in most FTP clients
 - Secure SSH encryption
 - Works over internet
 - Very easy setup
 - Password-less access using pubkey

Cons:
 - Not that fast



Install an SSH service:

`sudo apt install openssh-server`

That's it. You should now be able to use SFTP. It is the same username and password as your account on the server.

Enable password-less connections by generating a pubkey(the way is different on 
different programs) and adding it to the `~/.ssh/id_rsa.pub` file for the user 
you are logging in as.


## NFS

More direct access to the filesystem on the server.

Pros:
 - Extremely fast
 - Mostly easy setup
 - Local IP white listing

Cons:
 - Does not work over internet(by design)
 - Less standard support on non-unix-like OSes


On the server install `nfs-kernel-server`:

`sudo apt install nfs-kernel-server`


The add a folder you want to share in `/etc/exports`:

`sudo nano /etc/exports`


You could add user directories with very permissive access with(replace * with ip to white list):

`/home    *(rw,sync,no_root_squash)`


When done update exports with:

`sudo exportfs -ra`

Windows Clients are available:

Built-in: 

https://www.ibm.com/support/knowledgecenter/en/ST5Q4U/com.ibm.storwize.v7000.unified.141.doc/usgr_cnnctng_via_nfs_frm_wndws.html

https://graspingtech.com/mount-nfs-share-windows-10/

