1. Setting up android phone

- Install Termux
https://f-droid.org/pt/packages/com.termux/

- Install Termux:Boot
https://f-droid.org/pt/packages/com.termux.boot/

Go to Android Settings and diable battery optimization for both.

2. Setting up termux enviroment

- [SSH Server](https://wiki.termux.com/wiki/Remote_Access#Starting_and_stopping_OpenSSH_server)

Install SSH Server
```
pkg upgrade
pkg install openssh
```

Define a password and star service
```
passwd
sshd
```

Discover your IP
```
ifconfig
```

Connect from computer on the same Wifi network.
```
ssh [IP] -p 8022 -l user
```

Avoid password by copying the content of your private key (~/id_rsa.pub) to the device into the file $HOME/.ssh/authorized_keys

- Utils

Instalar o vi:
```
pkg install x11-repo
pkg install vim-gtk
```

- [Termux Services](https://wiki.termux.com/wiki/Termux-services)
```
pkg install termux-services -y
```

Create the ~/.termux/boot/ directory.
Create the file ~/.termux/boot/start-sshd:
```
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
. $PREFIX/etc/profile
```

Enable SSHD service
```
sv-enable sshd
```

- [MariaDB](https://wiki.termux.com/wiki/MariaDB)
```
pkg install mariadb -y
```

Start MariaDB
```
sv up mysqld
```

Test
```
mysql -u $(whoami)
```

Enable service
```
sv-enable mysqld
```

- Nginx

```
pkg install nginx -y
sv up nginx
sv-enable nginx
```

Test page will be live on the address: http://[IP ADDRESS]:8080/

- PHP

```
pkg install php -y
```

- [Nodejs](https://wiki.termux.com/wiki/Node.js)

```
pkg install nodejs -y
pkg install yarn -y
pkg install binutils -y
```

- N8N

```
mkdir ~/.gyp && echo "{'variables':{'android_ndk_path':''}}" > ~/.gyp/include.gypi
pkg install clang libsqlite pkg-config -y
pkg install sqlite -y
npm install pnpm -g
pnpm install n8n -g
```