1º - Criar conta de usuário root:

`sudo smbpasswd -a root`

2º - editar o arquivo /etc/samba/smb.conf e adicionar na seção [GLOBAL] os seguintes parâmetros:

add user script = /usr/sbin/useradd -M -c "Account User Samba" -s /bin/false -g Users %u

delete user script = /usr/sbin/userdel %u

`sudo groupadd Users`

3º - Aplicar as alterações usando o comando "smbcontrol":

`sudo smbcontrol smbd reload-config`

4º - Criar duas contas de usuários:

`sudo pdbedit -a aluno -f "Aluno Samba"`

`sudo pdbedit -a aluno2 -f "Aluno2 Samba"`

5º - Criar diretório "/mnt/samba/public" e o compartilhamento:

`sudo mkdir -v /mnt/samba/public`

`sudo vim /etc/samba/smb.conf`

Para exemplo adicione no final do arquivo smb.conf:

[publico]
    path = /mnt/samba/public
    read only = No

6º - Salvar as alterações e atribuir as permissões para a conta de usuário "Silvia Barreto":

`sudo chown -v aluno /mnt/samba/public`

7º - Desabilitar a conta "aluno" com o comando:

`sudo smbpasswd -d aluno`

8º - Habilitar a conta "aluno" com o comando:

`sudo smbpasswd -e aluno`

9º - Remover a conta "aluno2":

`sudo smbpasswd -x aluno2`
