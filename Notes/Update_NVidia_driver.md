# 

## Download driver

```bash
wget https://us.download.nvidia.com/XFree86/Linux-x86_64/460.56/NVIDIA-Linux-x86_64-460.56.run
```

## Install CENTOS7 dev tools

Install all prerequisites for a successful Nvidia driver compilation and installation

```bash
yum groupinstall "Development Tools"
yum install kernel-devel epel-release
yum install dkms
```

The dkms package is optional. However, this package will ensure continuous Nvidia kernel module compilation and installation in the event of new kernel update.

## Disable noveau

Disable `nouveau` driver by changing the configuration `/etc/default/grub file`. Add the `nouveau.modeset=0` into line starting with `GRUB_CMDLINE_LINUX`. Below you can find example of grub configuration file reflecting the previously suggested change:

```txt
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto rd.lvm.lv=centos/root rd.lvm.lv=centos/swap rhgb quiet nouveau.modeset=0 rd.driver.blacklist=nouveau"
GRUB_DISABLE_RECOVERY="true"
```

The above __line 6__ ensures that the `nouveau` driver is disabled the next time you boot your CentOS 7 Linux system. Once ready execute the following command to apply the new GRUB configuration change:

* BIOS
```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```
* EFI
```
sudo grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
```

## Create blacklist for noveau
Create a file named like `/etc/modprobe.d/blacklist-nouveau.conf` and enter following:

```txt
blacklist nouveau
options nouveau modeset=0
```
and in `/etc/modprobe.d/blacklist.conf` :

```txt
blacklist nouveau

```
## Backup old kernel

```
mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img
dracut /boot/initramfs-$(uname -r).img $(uname -r)
```

## Reboot and check that nouveau is gone

Reboot your CentOS 7 Linux System. 
```
sudo dracut --force
```

Once the boot is finished confirm that the nouveau open source Nvidia driver is no longer in use:

```bash
lshw -numeric -C display
```

## Switch to text mode

The Nvidia drivers must be installed while Xorg server is stopped. Switch to text mode by:

```
systemctl isolate multi-user.target
```

## Install NVidia driver

Install the Nvidia driver by executing the following command:

```bash
bash NVIDIA-Linux-x86_64-460.56.run --dkms -s
```

If dkms build fails, try following:

```bash
cd /lib/modules/3.10.0-1062.9.1.el7.x86_64/
rm build
ln -s /usr/src/kernels/3.10.0-1160.15.2.el7.x86_64 build
```
and retry the installation.

## Reboot

```
rmmod nouveau
```
