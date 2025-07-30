# Setting up Remote Server For VS Code

1. In `/etc/fstab`, remove the noexec option from `/home`&#x20;
2. Persist the changes by running `mount -o remount /home`
3. In `/etc/ssh/sshd_config` allow agent forwardeing
4. `systemctl restart sshd`
