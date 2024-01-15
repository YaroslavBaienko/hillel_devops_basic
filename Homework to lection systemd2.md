## Task 
1. Attach output in txt format of all commands within the lecture and provide comments
2. Create an ubuntu container with Debootstrap

** SOME STDOUT DONE WITH "tail && head" or only "tail" or only "head" for reducing space (screenshots are attached)
## Solutions
### 1 Attach output in txt format of all commands within the lecture and provide comments
### px xawf
#### STDIN
```bash
ps xawf
```
#### STDOUT 
```less
citizenseven@proxmox-ubuntu-warmachine:~$ ps xawf | tail && head
   2042 ?        Ssl    0:00 /usr/sbin/ModemManager
   2172 ?        Ss     0:00 /lib/systemd/systemd-machined
  13417 ?        Ss     0:00 systemd-nspawn --quiet --keep-unit --boot --link-journal=try-guest --network-veth -U --settings=override --machine=bullseye1
  13420 ?        Ss     0:00  \_ /usr/lib/systemd/systemd
  13445 ?        Ss     0:00      \_ /lib/systemd/systemd-journald
  13468 ?        Ss     0:00      \_ /usr/sbin/cron -f
  13469 ?        Ssl    0:00      \_ /usr/sbin/rsyslogd -n -iNONE
  13474 pts/0    Ss+    0:00      \_ /sbin/agetty -o -p -- \u --noclear --keep-baud console 115200,38400,9600 vt220
  13775 ?        Ss     0:00 /lib/systemd/systemd --user
  13776 ?        S      0:00  \_ (sd-pam)

```
#### Explanation
This command helps understand what processes are running, their states, and how they're related. Useful for checking system activity.
### systemd-analyze
#### STDIN
```bash
systemd-analyze
```
#### STDOUT
```less
citizenseven@proxmox-ubuntu-warmachine:~$ systemd-analyze
Startup finished in 2.850s (kernel) + 28.637s (userspace) = 31.488s
graphical.target reached after 28.047s in userspace
citizenseven@proxmox-ubuntu-warmachine:~$
```
#### Explanation
The `systemd-analyze` command provides information about the system's boot-up performance.
### systemd-analyze blame
#### STDIN
```bash
systemd-analyze blame
```
#### STDOUT
```less
citizenseven@proxmox-ubuntu-warmachine:~$ systemd-analyze blame | tail && head
   12ms snap-lxd-24322.mount
   12ms snapd.socket
   11ms grub-initrd-fallback.service
    7ms systemd-update-utmp-runlevel.service
    6ms polkit.service
    6ms modprobe@tun.service
    6ms user-runtime-dir@1000.service
    5ms modprobe@dm-mod.service
    4ms modprobe@loop.service
   36us blk-availability.service
```
#### Explanation
The `systemd-analyze blame` command lists system services and how long they took to start during boot, helping to identify which services are slowing down the boot process.
### 


sudo debootstrap --arch=amd64 jammy /var/lib/machines/jammy1

