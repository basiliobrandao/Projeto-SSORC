# Configuração do Samba para Compartilhamento de Músicas

Este documento fornece um guia passo a passo para instalar e configurar o Samba em um ambiente Linux para compartilhamento de arquivos de música.

---

## 1. Atualizar e Instalar o Samba

Execute os seguintes comandos para atualizar o sistema e instalar o Samba:

```bash
sudo apt update && sudo apt upgrade
sudo apt install samba
```

---

## 2. Criar o Diretório para as Músicas

Crie o diretório onde as músicas serão armazenadas:

```bash
sudo mkdir -p /srv/samba/musica
```

---

## 3. Criar um Novo Usuário no Linux

1. Acesse as configurações do sistema.
2. Vá para "Usuários".
3. Crie um novo usuário administrador.

---

## 4. Ajustar as Permissões da Pasta

Dê permissão total à pasta de compartilhamento:

```bash
sudo chmod -R 777 /srv/samba/musica
```

Defina o dono da pasta usando o usuário administrador e usuário comum:

```bash
sudo chown admin:teste /srv/samba/musica
```

---

## 5. Configurar o Samba

Edite o arquivo de configuração do Samba:

```bash
sudo nano /etc/samba/smb.conf
```

No final do arquivo, adicione a seguinte configuração:

```ini
[musicas]
    comment = Compartilhamento de Músicas
    path = /srv/samba/musica
    browseable = yes
    guest ok = yes
    writable = yes
    create mask = 0777
    directory mask = 0777
    public = yes
    veto files = /*.mp4/
    veto oplock files = yes
```
Se quiser bloquear outros tipos de arquivos, adicione a extensão do arquivo no formato /*.extensão

Salve o arquivo e saia do editor.

---

## 6. Reiniciar o Samba

Para aplicar as configurações, reinicie o serviço do Samba:

```bash
sudo systemctl restart smbd
```

Verifique o status do serviço para garantir que ele está rodando:

```bash
sudo systemctl status smbd
```

Caso o serviço não esteja ativo, inicie-o manualmente:

```bash
sudo systemctl start smbd
```

---

## 7. Configuração no VirtualBox

Se estiver utilizando o Samba em uma máquina virtual no VirtualBox, configure a rede para "Placa em modo Bridge" para que o compartilhamento funcione corretamente.

Certifique-se de que os computadores estejam na mesma rede para acessar o compartilhamento.

---

## 8. Descobrir o Endereço IP da Máquina Virtual

Para acessar o compartilhamento de outra máquina, primeiro descubra o IP da máquina virtual:

```bash
ip a
```

---

## 9. Acessar a Pasta Compartilhada no Windows

Para acessar a pasta compartilhada a partir do Windows:

1. Pressione `WIN + R`.
2. Digite o seguinte comando e pressione `Enter`:

```
\\IP-do-servidor\musicas
```

Agora, a pasta compartilhada estará acessível no Windows.

---

Agora seu compartilhamento de músicas via Samba está pronto para uso! 🎵


