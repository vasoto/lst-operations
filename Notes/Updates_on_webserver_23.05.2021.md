## Error: Terminating since out of inotify watches
Check /var/log/lsyncd/lsyncd.log:
```
Sun May 23 19:17:52 2021 Normal: --- Startup ---
Sun May 23 19:18:21 2021 Error: Terminating since out of inotify watches.
Consider increasing /proc/sys/fs/inotify/max_user_watches
```
See https://tt-inc.org/lsyncd-error-terminating-since-out-of-inotify-watches.html

Check allowed inotify watches:
```bash
cat /proc/sys/fs/inotify/max_user_watches
8192
```

### Solution
1. `sysctl fs.inotify.max_user_watches=65536`
2. `vi /etc/sysctl.conf`
    ```bash
    #fix lsyncd error terminating since out of inotify watches
    fs.inotify.max_user_watches=65536
    ```


## Add user auxmonit
1. Create user `useradd -m -G docker auxmonit`

## SSH only on 161.72.87.* network
Added to `/etc/ssh/sshd_confg`:
```
PermitRootLogin no
Match Address 161.72.87.*
  PermitRootLogin yes
```

## Fix lsyncd
See https://linoxide.com/setup-lsyncd-sync-directories/

## Set timzone to UTC in www-backup

```
timedatectl set-timezone UTC
```

## Set NTP server on www and www.backup to 161.72.87.61

```
driftfile /var/lib/ntp/drift

restrict 127.0.0.1

server 161.72.87.61
```

## Add users and groups to www-backup

```
groupadd -g 980 docker
usermod -aG docker lst1
usermod -aG wheel lst1
groupadd -g 1002 datacheck
useradd -g 1002 -G www datacheck
groupadd -g 1003 cacomonit
useradd -m -g 1003 -G docker cacomonit
groupadd -g 1004 auxmonit
useradd -m -g 1004 -G docker auxmonit
```