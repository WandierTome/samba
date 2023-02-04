# Aula de Compilação e instalação do serviço samba
### 1º - Atualização do sistema e Instalação das dependências do samba 4.x
**apt-get update && apt-get upgrade -y**

**apt-get install wget acl attr autoconf bind9utils bison build-essential debhelper dnsutils docbook-xml docbook-xsl flex gdb libjansson-dev krb5-user libacl1-dev libaio-dev libarchive-dev libattr1-dev libblkid-dev libbsd-dev libcap-dev libcups2-dev libgnutls28-dev libgpgme-dev libjson-perl libldap2-dev libncurses5-dev libpam0g-dev libparse-yapp-perl libpopt-dev libreadline-dev nettle-dev perl pkg-config python-all-dev python-crypto python2-dbg python-dev python-dnspython python3-dnspython python3-gpg python-markdown python3-markdown python3-dev xsltproc zlib1g-dev liblmdb-dev lmdb-utils libsystemd-dev perl-modules-5.* libdbus-1-dev libtasn1-bin -y**

### 2º - Baixar o código fonte do samba e extrair o conteúdo do arquivo:

**cd /usr/src/ && wget -c https://download.samba.org/pub/samba/stable/samba-4.9.4.tar.gz tar -xf samba-4.9.4.tar.gz && cd samba-4.9.4**

### 3º - Configurando:
**./configure --with-systemd --prefix=/usr/local/samba --enable-fhs**

### 4º - Compilando e instalando o serviço samba:
**make && make install**