# Ubuntu NAS Setup

A basic guide on setting up different file sharing solutions on Ubuntu as a basic NAS server.

## Headless Mode(No GUI)

Edit the file `/etc/default/grub`:
`sudo nano /etc/default/grub`

Change the `"quiet splash"` on the following line to `"text"`:
`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`

Update the boot configuration with:
`sudo update-grub`

Set `systemd` to the multi-user run level:

```
sudo systemctl enable multi-user.target --force
sudo systemctl set-default multi-user.target
```
