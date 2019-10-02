<h1 align="center">
  Recursos Web Avançado
  <br>
  <br>
  Com este tutorial você sera capaz de: Rodar seu backend na DigitalOcean. Enviar seu frontend ReactJs online. Integração contínua no backend com Buddy.works e Netlify no frontend, apenas dando commit no github.
  <br>
  <br>
</h1>



## **Tabela de conteudo**

- [**Tabela de conteudo**](#tabela-de-conteudo)
- [**Criar droplet na DigitalOcean**](#criar-droplet-na-digitalocean)
  - [**Configuração inicial depois de instalar o ubuntu**](#configura%c3%a7%c3%a3o-inicial-depois-de-instalar-o-ubuntu)

<hr/>

## **Criar droplet na DigitalOcean**

Passo a passo de como criar o droplet:

**1.** Vai em create e depois seleciona droplet
<p align="center">
  <img src="https://i.imgur.com/ZQ0Yz6R.png" alt="Create">
</p>

**2.** Após entrar na tela de criação, você seleciona o sistema operacional a seu gosto, mas aqui irei utilizar o **Ubuntu 18.04.3 (LTS ) x64**.

**3.** Selecionar qual será o plano de hospedagem. Para uma aplicação basica, o plano de $5/mês resolve bem, então estarei utilizando-o.
<p align="center">
  <img src="https://i.imgur.com/ioVrrCM.png" alt="Choose plan">
</p>

**4.** Selecionar onde vai ficar a região do datacenter:
<p align="center">
  <img src="https://i.imgur.com/ng1yiaI.png" alt="Choose datacenter region">
</p>

**5.** Nessa parte é preferivel usar o SSH Keys:
<p align="center">
  <img src="https://i.imgur.com/nmF2aoY.png" alt="SSH">
</p>

**6.** Aperte em 'New SSH Key' para adicionar uma nova chave na DigitalOcean, se você já tem gerado uma ssh key no seu pc, copie-a e cole no campo que apareceu (caminho para a chave: `~/.ssh/id_rsa.pub` ). Se você não tiver, siga o tutorial que aparece no canto direito da tela de adicionar chave. Depois de adicionar, verifique de selecionar o checkbox.
<p align="center">
  <img src="https://i.imgur.com/yOIq8lE.png" alt="SSH">
</p>

**7.** Depois basta escolher o nome para sua host e apertar em criar droplet.

### **Configuração inicial depois de instalar o ubuntu**

* Logando como root e criando novo usuario
  
  **1.**`ssh root@server_ip`
  
  **2.** Não é ideal ficar fazendo alterações com a conta root, então vamos criar um novo user, como exemplo irei usar meu nome, mas lembre de mudar para o seu nome de usuario:
  ```sh
  adduser victor
  ```
  **3.** Daremos acesso de administrador a esse usuario: 
   ```sh
   usermod -aG sudo victor
   ```
  **4.** Ligando o firewall e permitindo conexões ssh: 
  ```sh
  ufw allow OpenSSH
  ufw enable
  ```
  **5.** Se você optou por usar o SSH key ao inves da senha, você ira precisar copiar a sua chave ssh para o `~/.ssh/authorized_keys`, para isso use o seguinte comando:
  ```sh
  rsync --archive --chown=victor:victor ~/.ssh /home/victor
  ```
  **6.** Agora de `logout` e entre com a conta:
  ```sh
  ssh victor@server_ip
  ```
* Instalando Node.js e yarn
  **1.** A seguir irei passar o comando necessario para instalar o Node.js 12
  ```sh
  sudo apt-get install curl
  curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
  sudo apt-get install nodejs
  ```
  Se preferir a versão __LTS__:
  ```sh
  sudo apt-get install curl
  curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
  sudo apt-get install nodejs
  ```
  **2.** Instalando yarn:
  ```sh
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
  sudo apt-get update && sudo apt-get install yarn
  ```
