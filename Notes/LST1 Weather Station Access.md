# Problem

Dear Vassil

I am still struggling with the NFS mounting of the FEFS.
It seems to work OK on operator1.
Please check:
/fefs-test
and
/fefs/LST1/DrivePositioning

But on safetycollector (10.1.12.1)
I am having troubles even though it should be identical case.
Can you please check the safetycollector machine?

Some info:
1. I decided to use user control, which is available on fefs and now also on operator1 and safetycollector. uid=10002

2. I am exporting FEFS from tcs07:
```
[root@tcs07 ~]# cat /etc/exports
/fefs/onsite/monitoring/evb-test operator1(rw) operatorSpare(rw)
/fefs/onsite/monitoring/weather 10.1.12.1(rw)
/fefs/onsite/monitoring/driveLST1/DrivePositioning 10.1.12.1(ro) operator1(ro)
```
Please let me know if you can have a look into it, I'll send you the pwd for user control
and if need root pwd for the safetycollector.

Best

# Observations
* `ping` from `tcs07` works fine:
```
64 bytes from 10.1.12.1: icmp_seq=60 ttl=63 time=0.226 ms
64 bytes from 10.1.12.1: icmp_seq=61 ttl=63 time=0.181 ms
64 bytes from 10.1.12.1: icmp_seq=62 ttl=63 time=0.195 ms
64 bytes from 10.1.12.1: icmp_seq=63 ttl=63 time=0.265 ms
64 bytes from 10.1.12.1: icmp_seq=64 ttl=63 time=0.221 ms
64 bytes from 10.1.12.1: icmp_seq=65 ttl=63 time=0.255 ms
64 bytes from 10.1.12.1: icmp_seq=66 ttl=63 time=0.218 ms
64 bytes from 10.1.12.1: icmp_seq=67 ttl=63 time=0.237 ms
64 bytes from 10.1.12.1: icmp_seq=68 ttl=63 time=0.231 ms
64 bytes from 10.1.12.1: icmp_seq=69 ttl=63 time=0.250 ms
64 bytes from 10.1.12.1: icmp_seq=70 ttl=63 time=0.237 ms
64 bytes from 10.1.12.1: icmp_seq=71 ttl=63 time=0.238 ms
```
* Every ~10 seconds connections from user `lst1` from `login2-int.ctan` (see `/var/log/messages`)

* Some of the NFS packages on safetycollector are older:
```dotnetcli
libnfsidmap.x86_64                      0.25-19.el7                    @anaconda
nfs-utils.x86_64                        1:1.3.0-0.61.el7               @anaconda
nfs4-acl-tools.x86_64                   0.3.3-19.el7                   @anaconda
```
* `traceroute operator1 --mtu` is getting stuck
* `scp /tmp/home.tgz operator1:/tmp` is getting stalled at exactly 2112Kb 
* NO errors in the network interfaces

# Trials

* from https://www.thegeekdiary.com/how-to-enable-nfs-debug-logging-using-rpcdebug/
* See https://stackoverflow.com/questions/11985008/sending-a-large-file-with-scp-to-a-certain-server-stalls-at-exactly-2112-kb


# Resolution
* Lower the MTU from 9000 to 1492 solved the issue `ip link set dev eth0 mtu 1492`
* Persisted in `/etc/sysconfig/network-scripts/ifcfg-eno1` -- `MTU=1492`


#