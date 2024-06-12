


### This process is needed if faced phn dependencies.
```
sudo nano /etc/apt/sources.list
```
Add the following lines to your `sources.list` file to include the main Debian repositories:
```
deb http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main contrib non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main contrib non-free non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
```
Update the package lists
```
sudo apt update
```
### Install missing dependencies: (If needed)
After updating the package lists, you should install the missing dependencies. Run the following commands one by one to install the dependencies:
```
sudo apt install libpango1.0-0 php php-cgi php-cli php-gd php-sqlite3 php-pear xinetd libfreeradius3
```
### Now try to Install Checkmk Raw Edition
```
sudo apt install ./check-mk-raw-2.2.0p25_0.bookworm_amd64.deb
```


```
gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C
```

```
root@AutomationTest:~# gpg --list-keys E5267A6C
pub   rsa1024 2009-01-26 [SC]
      14AA40EC0831756756D7F66C4F4EA0AAE5267A6C
uid           [ unknown] Launchpad PPA for Ondřej Surý

```

