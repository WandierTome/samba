# Ingressar Cliente Linux no domínio

1º Etapa - instalar dependências:sh

`sudo apt install realmd sssd sssd-tools libnss-sss libpam-sss adcli samba-common-bin systemd-timesyncd -y`

2º Etapa - sicrinizar a data e hora com o sercidor DC01:

`sudo editor /etc/systemd/timesyncd.conf` (exp. editor nano, vim, gedit e outros...).

Descomentando NTP e configurando para NTP=IP do Servidor (exp. 10.0.0.10).

2.1 Resete o serviço systemd-timesyn.service:

`sudo systemd restart systemd-timesyncd.serviço`

3º Etapa - editar arquivo /etc/nsswitch.conf e substituir a linha:

> editor /etc/nsswitch.conf

**hosts: &ensp; files mdns4_minimal [NOTFOUND=return] dns**

**por:**

**hosts: files dns**

4º Etapa - Ingressar no domínio:

`realm join empresa.local --user=administrator --client-software=sssd --os-name="Linux Desktop" -v`

5º Etapa - Editar arquivo /etc/sssd/sssd.conf e incluir no fim do arquivo a linha

> **override_homedir=/home/%d/%u**

6º Etapa - Salvar as alterações e reiniciar o sssd.service:

`systemctl restart sssd.service`

7º - Alterar o arquivo do gerenciador de boot lightdm:
> **/usr/share/lightdm/lightdm.conf.d/50-ubuntu-mate.conf, incluindo as seguintes linhas:**

> **greeter-show-manual-login=true**
> **greeter-hide-users=true**

> **OBS: Em outras versões do ubuntu é necessário alterar o arquivo de configuração do gerenciador de login correspondente, a versão principal do Ubuntu Desktop usa o GDM, então é necessário alterar o arquivo de configuração do GDM para ter os mesmos resultados.**

8º - Reinicie o computador:
