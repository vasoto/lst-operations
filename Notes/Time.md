# Time

## Set time

[Link 1](https://codingbee.net/rhcsa/ntp-keeping-system-time-in-sync-on-centos-rhel-7)
[Link2](https://www.tecmint.com/synchronize-time-with-ntp-in-linux/)

```bash
systemctl status chronyd
systemctl disable chronyd
systemctl stop ntpd
timedatectl
ntpd -gq
hwclock --systohc
timedatectl set-ntp yes
systemctl start ntpd.service
systemctl enable ntpd.service
timedatectl
```

# NTPD Configuration

`/etc/ntp.conf`

```conf
# For more information about this file, see the man pages
# ntp.conf(5), ntp_acc(5), ntp_auth(5), ntp_clock(5), ntp_misc(5), ntp_mon(5).
driftfile /var/lib/ntp/drift

# Permit time synchronization with our time source, but do not
# permit the source to query or modify the service on this system.
# restrict default nomodify notrap nopeer noquery

# Permit all access over the loopback interface.  This could
# be tightened as well, but to do so would effect some of
# the administrative functions.
restrict 127.0.0.1

# cnt1
server 10.200.100.113

# cnt2
#server 10.200.100.112

disable auth
```
