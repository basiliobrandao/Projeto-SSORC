Projeto-SSORC

Instalação do Samba
Atualizar e instalar pacotes

sudo apt update && sudo apt upgrade
sudo apt install samba 

Criar o diretório para as músicas
sudo mkdir -p /srv/samba/musica

Criar outro usuario no linux 
Entre nas configurações, vá em “users” e crie um usuário de administrador 

Ajustar as permissões da pasta
sudo chmod -R 777 /srv/samba/musica

Criar o dono da pasta
Seu usuário administrador:seu usuário comum
sudo chown admin:teste /srv/samba/musica

Configurando o Samba 

Acessar o arquivo de configuração do Samba 
sudo vim /etc/samba/smb.conf
sudo nano /etc/samba/smb.conf

No final do arquivo adicione uma seção de compartilhamento
comment: 
path /
browseable = yes
guest ok = yes
writable = yes
create mask = 0777
directory mask = 0777
public = yes
veto files: 
veto oplock files = yes

Reiniciar o Samba para aplicar as configurações
sudo systemctl restart smbd

Verificar o status do Samba
sudo systemctl status smbd | Verificar se está ativo e funcionando.
sudo systemctl start smbd | Se o Samba não estiver ativo.

Configuração no VirtualBox
Acesse as configurações de rede no VirtualBox e mude o tipo de placa para “Placa em modo Bridge” para que o compartilhamento seja possível.
Além disso, os computadores precisam estar na mesma rede para funcionar.

Acessar o IP da máquina virtual
ip a

Acessar a pasta através de uma máquina Windows
Para acessar a pasta compartilhada através do windows pressione a teclas WIN + R e digite o IP da máquina virtual e depois o nome da seção de compartilhamento criada no Samba, dessa maneira:
\\IP-do-servidor\nome-da-seção
