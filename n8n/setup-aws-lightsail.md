### Instalando o N8N no AWS Lightsail

Atualmente esta é a minha prnincipal opção para rodar um servidor N8N. O [AWS Lightsail](https://aws.amazon.com/pt/lightsail/pricing/) oferece opções de instâncias muito econômicas e fáceis de gerir.

O N8N é uma aplicação muito leve, sendo possível tirar bastante proveito do sistema com servidores simples. Tenho conseguido ótimos resultados com servidores de 1GB RAM e 1vCPU, modelo que trará um custo mensal de USD 10,00. Muito mais barato do que soluções similares como Zapier, Pluga e Make (ex-Integromat).

## Passo-a-passo

Crie uma instância Linux Ubuntu e siga os passos abaixo para instalar o N8N.

**1 - Instale o Node Js (versões pares acima da 18):**
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
nvm install 18.17.1
```

**2 - Instale o pnpm:**
```bash
npm install pnpm -g
```

**3 - Instale o n8n:**
```bash
pnpm install n8n -g
```

**4 - Instale o pm2:**
```bash
pnpm install pm2 -g
```

**5 - Crie um script de inicialização:**

Crie um script de inicialização chamado `n8n_start.sh` com o seguinte conteúdo:
```bash
#!/bin/bash
cd /home/ubuntu
pnpm n8n
```

**6 - Configure o PM2 para iniciar o N8N:**
```bash
pm2 start n8n_start.sh
pm2 startup
```
Copie e rode o código gerado, será algo como o seguinte:
```bash
sudo env PATH=$PATH:/home/ubuntu/.nvm/versions/node/v18.17.1/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```

**7 - Arquivo de configurações:**

Crie o arquivo inicial de configurações:
```bash
pm2 init simple
```

Edite-o e substitua pelo seguinte:
```javascript
module.exports = {
    apps : [{
      name   : "n8n",
      script: “/home/ubuntu/n8n_start.sh”,
      env: {
        "WEBHOOK_URL": "https://n8n.[seu dominio]",
        "GENERIC_TIMEZONE":"America/Sao_Paulo",
        "EXECUTIONS_DATA_SAVE_ON_SUCCESS": "none",
      } 
    }]
}
```
Salve, pause o pm2 e inicie novamente:
```bash
pm2 stop
pm2 start ecosystem.config.js
```

**8 - Configure o Lightsail:**

Abra a porta 5678 para testar se o N8N está rodando corretamente.
No painel da instância, na aba Networking adicione uma rule em IPv4 Firewall:

- Application: Custom
- Protocol: TCP
- Port: 5678

Pegue o Public IP e acesse `xxx:5678`.

Faça o setup inicial, criando a senha de acesso.

**9 - Instale e configure o Nginx:**
```bash
sudo apt install nginx
```

Instale e ative o certbot para gerar o certificado SSL:
```bash
sudo apt install software-properties-common
sudo apt update
sudo add-apt-repository ppa:certbot/certbot
sudo apt install python3-certbot-nginx
```

Tudo instalado, agora aponte o sudominio para o servidor. Se usar cloudflare, deixe o proxy inativo por enquanto.
```bash
sudo certbot --nginx -d n8n.[seu dominio]
Informe o email: [seu email]
```

**10 - Direcione o Nginx para o N8N:**

Edite o arquivo de configuração:
```bash
sudo vi /etc/nginx/sites-enabled/default
```

Procure pelo bloco abaixo:
```
server_name n8n.[seu dominio]; # managed by Certbot

location / {
# First attempt to serve request as file, then
# as directory, then fall back to displaying a 404.
 try_files $uri $uri/ =404;
```

Comente a linha `try_files` e acrescente as informações em `location /`. O resultado será este:
```
location / {
  proxy_pass http://localhost:5678;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "Upgrade";
  proxy_set_header Host $host;
  chunked_transfer_encoding off;
  proxy_buffering off;
  proxy_cache off;
}
```

Reinicie o nginx:
```bash
sudo systemctl restart nginx
```

Volte ao painel do Lightsail e exclua a porta 5678 do ipv4 e ipv6 - por segurança.

Pronto, o N8N está rodando.

## Otimização de memória

Com o uso intenso e nos momentos de upgrade e instalação, usando um servidor Lightsail com pouca memória, adicionar um arquivo SWAP melhora bastante a estabilidade e capacidade do ambiente.

# Crie e habilite um swap file:

```
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
