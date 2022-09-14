# Ubuntu on Android

Termux exit problem (Android 12) solution with LADB app

```bash
1. Install LADB

2. Connect to a WiFi network

3. Run LADB

4. Allow debugging via WiFi
```

Now execute in LADB to allow more phantom process:

```bash
/system/bin/device_config put activity_manager max_phantom_processes 2147483647
```

update termux:

```bash
pkg update
```

## Installing Ubuntu:

Install proot-distro:

```bash
pkg install proot-distro
```

check available distros:

```bash
proot-distro list
```

Install ubuntu distro:

```bash
proot-distro install ubuntu
```

Login to ubuntu:

```bash
proot-distro login ubuntu
```

Check installed distro details:

```bash
cat /etc/os-release
```

Update ubuntu:

```bash
apt-get update -y && apt-get upgrade -y
```

Install sudo nano

```bash
apt install sudo nano
```

Creating new user

```bash
adduser spidey
```

Open sudoers with nano:

```bash
nano /etc/sudoers
```

give permission by adding  below line under root

```bash
spidey  ALL=(ALL:ALL) ALL
```

Login to new created user

```bash
su spidey
```

Go back to root user

```bash
exit
```

## Setup VNC:

```bash
sudo apt install udisks2
```

```bash
sudo rm /var/lib/dpkg/info/udisks2.postinst
```

```bash
echo "" >> /var/lib/dpkg/info/udisks2.postinst
```

```bash
sudo apt-mark hold udisks2
```

```bash
sudo apt purge gvfs-daemons gvfs-libs gvfs-common
```

```bash
sudo apt install xfce4 xfce4-terminal xfce4-whiskermenu-plugin
```

```bash
sudo apt install firefox gedit vlc dbus-x11 tigervnc-standalone-server
```

exit to root

```bash
exit
```

exit to termux 

```bash
exit
```

### Editing login to Ubuntu command

```bash
echo "proot-distro login --user spidey" >> $PREFIX/bin/ubuntu
```

```bash
nano $PREFIX/bin/ubuntu #add ubuntu after username and save
```

```bash
chmod +x $PREFIX/bin/ubuntu
```

login to ubuntu again just by typing ubuntu

```bash
ubuntu
```

Now bellow command

```bash
echo "vncserver -geometry 1600x900 -xstartup /usr/bin/startxfce4" >> /bin/vncstart
```

```bash
echo "vncserver -kill :1" >> /bin/vncstop
```

```bash
chmod +x /bin/vncstart
```

```bash
chmod +x /bin/vncstop
```

Start VNC

```bash
vncstart
```

Stop VNC

```bash
vncstop
```