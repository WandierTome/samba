# Ingressando servidor de arquivo ao domínio samba como membro

1º - Atualize o sistema e instale os pacotes:

    sudo apt-get update
    sudo apt-get install libnss-winbind krb5-user libwbclient0

2º - Configurar client NTP systemd-timesyncd.service para sincronizar data e hora com servidores domain controllers:

    sudo vim /etc/systemd/timesyncd.conf

**Alterar deixando assim:**

    [Time]  
    NTP=10.10.10.11 10.10.10.12

2.1º - Reiniciar unidade de serviço systemd-timesyncd.service

    sudo systemctl restart systemd-timesyncd.service

4º - Configurar arquivo /etc/krb5.conf:

    sudo vim /etc/krb5.conf

**Conteúdo do arquivo /etc/krb5.conf deve ficar como mostrado a seguir:**

    [libdefaults]  
    default_realm = EMPRESA.LOCAL  
    dns_lookup_realm = false  
    dns_lookup_kdc = true  

5º - Testar comunicação usando o KERBEROS:

    kinit administrator
    klist
    kdestroy

6º - Editar arquivo /etc/samba/smb.conf e deixar assim:

    [global]
    #==== Parâmetros usados para ingressar no domínio ====#
    workgroup = EMPRESA
    netbios name = fileserver
    realm = EMPRESA.LOCAL
    security = ads  
    #==================== LOGs ===========================#  
    log file = /var/log/samba/fileserver.log  
    max log size = 2048  
    log level = 2  

7º - Salvar as alterações e aplicar as configurações:

    testparm
    sudo systemctl restart smbd.service nmbd.service

8º - Ingressar computador no domínio:

    net ads join -U administrator

9º - Validar se o servidor ingressou no domínio com sucesso:

    net ads testjoin

10º - Configurar o sistema para usar Winbind:

    systemctl enable winbind.service
    systemctl start winbind.service
    vim /etc/samba/smb.conf
    idmap config *:backend = tdb
    idmap config *:range = 2000-2050
    idmap config EMPRESA:backend = rid
    idmap config EMPRESA:range = 3000-40000
    # Enumerar contas de usuários e Grupos de Usuários #
    winbind enum users = yes
    winbind enum groups = yes

11º - Reiniciar as unidades de serviço
 
    winbind.service e smbd.service:
    systemctl restart winbind.service smbd.service

12º - Alterar arquivo /etc/nsswitch.conf deixando os paramentos passwd e group:

    vim /etc/nsswitch.conf

    passwd:     files systemd winbind
    group:      files systemd winbind
