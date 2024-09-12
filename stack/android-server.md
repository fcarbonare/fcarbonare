# Usando celular antigo como servidor

## 1. Configurando o android

- Install Termux
https://f-droid.org/pt/packages/com.termux/

- Install Termux:Boot
https://f-droid.org/pt/packages/com.termux.boot/

- Vá nas configurações do celular e desabilite a otimização de bateria para os dois aplicativos.

## 2. Configurando o termux

- [SSH Server](https://wiki.termux.com/wiki/Remote_Access#Starting_and_stopping_OpenSSH_server)

Instalando o servidor SSH
```
pkg upgrade
pkg install openssh
```

Defina uma senha e inicie o serviço
```
passwd
sshd
```

Descubra o IP da sua rede local para se conectar via SSH
```
ifconfig
```

Conecte de um computador que estiver na mesma rede WiFi
```
ssh [IP] -p 8022 -l user
```

Evite digitar a senha toda vez que for se conectar copiando o conteúdo da sua chave privada local (~/id_rsa.pub) para o arquivo de chaves autorizadas do celular: $HOME/.ssh/authorized_keys

- Utils

Instale o vi:
```
pkg install x11-repo
pkg install vim-gtk
```

Instale o git
```
pkg update && pkg upgrade && pkg install git -y
```

- [Termux Services](https://wiki.termux.com/wiki/Termux-services)
```
pkg install termux-services -y
```

Crie o diretório ~/.termux/boot
Crie o arquivo ~/.termux/boot/start-sshd
```
#!/data/data/com.termux/files/usr/bin/sh
termux-wake-lock
. $PREFIX/etc/profile
```

Ative o serviço do SSHD
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

Você vai poder acessar a página de teste no endereço: http://[IP ADDRESS]:8080/
O Chrome vai apresentar erro, pois não possui certificado SSL.

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

## Deixando o nginx público via [cloudflared](https://github.com/rajbhx/cloudflared-termux)

```
git clone https://github.com/rajbhx/cloudflared-termux
cd cloudflared-termux
chmod +x Cloudflared-termux_@rajbhx.sh
bash Cloudflared-termux_@rajbhx.sh
```

- Siga as instruções para configurar o tunnel:
https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/create-local-tunnel/

Crie o arquivo ~/.termux/boot/start-cloudflared:
```
#!/data/data/com.termux/files/usr/bin/sh
cloudflared tunnel run [ID]
```
