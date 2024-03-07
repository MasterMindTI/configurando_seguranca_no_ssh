# Configurando_seguranca_no_ssh

# Modificando Configurações no Servidor SSH

## Vamos para o Procedimento ?
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg" width="40" height="40"/>
                
####################################################################
## 1. Pré-Requisitos
####################################################################
- 1.1. Servidor Debian 12x ou Slackware 15

####################################################################
## 2. Configuração
####################################################################

- 2.1. Edite o arquivo de configuração do SSH em /etc/ssh/sshd_config

```
sudo nano /etc/ssh/sshd_config
```

- 2.2. E faça as seguintes alterações:

```
Port 61122
# Primeiro caso do PermitRootLogin
# permite autenticação root somente via chaves - no caso de programa de
backup
PermitRootLogin prohibit-password
PermitRootLogin yes

# Segundo caso do PermitRootLogin
#PermitRootLogin prohibit-password
PermitRootLogin no

# Especificar o número de tentativas de conexões permitidas, o padrão é 6
MaxAuthTries 4

# Máximo de sessões conectadas, o padrão é 10
MaxSessions 6

# Autoriza autenticação via chaves
PubkeyAuthentication yes

# Procurar por chaves autenticadas, que vamos enviar ao servidor "Conexão
feita somente pelas chaves"
AuthorizedKeysFile .ssh/authorized_keys .ssh/authorized_keys2

# Bloqueia o acesso ssh ao ambiente gráfico
X11Forwarding no

# Tempo de Inatividade para desconexão automática (600 = 10m)
ClientAliveInterval 600

# Quantas solicitações vai enviar ao cliente, o padrão é 3
ClientAliveCountMax 3

# Permitir autenticação via senha (sim ou não)
PasswordAuthentication no

# Permitir senhas vazias
PermitEmptyPasswords no
```
*NOTA: Depois de fazer as configurações, não reinicie o SSH antes de testar.

- 2.3. Gere uma chave SSH no cliente:

```
$ ssh-keygen -t rsa -b 4096 -C "contato@mastermindti.com.br"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/lucas/.ssh/id_rsa):
/home/lucas/.ssh/slackware-vm_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/lucas/.ssh/slackware-vm_rsa
Your public key has been saved in /home/lucas/.ssh/slackware-vm_rsa.pub
```
A chave será salva em /home/lucas/.ssh/slackware-vm_rsa

- 2.4. Envie a chave pública para o servidor:

```
ssh-copy-id -i /home/lucas/.ssh/slackware-vm_rsa.pub lucas@192.168.196.245
```
Você será solicitado a inserir a senha do usuário no servidor.

- 2.5. Teste a conexão com o servidor:

```
ssh -i .ssh/slackware-vm_rsa 'lucas@192.168.196.245' -p 61122
```
Certifique-se de que a conexão seja bem-sucedida antes de prosseguir

- 2.6. Acesse o servidor e reinicie o serviço de SSH após o teste bem-sucedido:

- No slackware o comando é:
  
```
/etc/rc.d/rc.sshd restart
```

- No Debian 12 o comando é:

```
systemctl restart sshd.service
```

- 3. Configurando Acesso Simplificado

- 3.1. Edite o arquivo ~/.ssh/config:

```
nano ~/.ssh/config
```

- 3.2. E adicione o seguinte conteúdo:

```
Host slackware-vm
  HostName 192.168.196.245
  User lucas
  Port 61122
  IdentityFile ~/.ssh/slackware-vm_rsa
```
- Salve e saia

- 3.3. Agora, você pode acessar o servidor SSH usando:

```
ssh slackware-vm
```

- Conclusão

Agora você configurou com sucesso a segurança do SSH no seu servidor, garantindo uma
comunicação segura entre o cliente e o servidor.

<a href="https://www.youtube.com/watch?v=VX3phETfmZ8" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>

####################################################################
## Informações Adicionais:
#### MasterMindTI - Configurando a Seguranca ssh no Debian 12x ou Slackware 15 
#### Procedimento: Configurando_seguranca_no_ssh
#### @Responsável: Lucas Tavares Soares
#### @Data: 06/03/2024
#### @Versão: 1.0.0
#### @Homologado: Debian 12 x64 e Slackware 15 x64
####################################################################

### Qualquer dúvida, entre em contato.

e-mail: contato@mastermindti.com.br

## Contatos:

<div>
<a href="https://www.youtube.com/@mastermindti" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
<a href = "mailto:contato@mastermindti.com.br"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
<a href="https://www.linkedin.com/in/lucastavarestga/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a>
</div>

## Estatisticas

<div>
<a href="https://github.com/MasterMindTI">
<img height="180em" src="https://github-readme-stats.vercel.app/api?username=MasterMindTI&show_icons=true&theme=dracula&include_all_commits=true&count_private=true"/>
</div>
