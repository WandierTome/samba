Gerênciando Grupos de usuários pela linha de comando

1 - LISTAR GRUPOS DE USUÁRIOS DO DOMÍNIO:

```
samba-tool group list
```

2 - ADICIONAR GRUPO DE USUÁRIOS:

```
samba-tool group add --description="Grupo que contém contas de usuários dos Instrutores" --groupou=OU=instrutores instrutores

samba-tool group add --description="Grupo que contém contas de usuários dos funcionários do departamento de ti" --group-scope=Domain ti
```

​	2.1 - ADICIOMANDO VARIOS GROUPUS AO MESMO TEMP

```
for groups in diretoria rh financeiro; do samba-tool group add $groups; done
```

3 - ADICIONAR MEMBROS AO GRUPO DE USUÁRIOS:

```
samba-tool group addmembers instrutor carlos,gilberto
samba-tool group addmembers recepcao thais,suzane
samba-tool group addmembers admin mauricio,mariane
```

4 - LISTAR OS MEMBROS DO GRUPO DE USUÁRIOS:

```
samba-tool group listmembers instrutor
samba-tool group listmembers recepcao
samba-tool group listmembers admin
samba-tool group listmembers aulas
```

5 - REMOVER MEMBROS DO GRUPO DE USUÁRIOS:

```
samba-tool group add grupo1
samba-tool group addmembers ti grupo1
samba-tool group removemembers ti grupo1
```

6 - REMOVER UM GRUPO DE USUÁRIOS:

```
samba-tool group delete grupo1
```

7 - MOVER GRUPO DE USUÁRIOS PARA DENTRO DE UMA UNIDADE ORGANIZACIONAL:

```
samba-tool group move ti OU=ti
samba-tool group move diretoria "OU=Diretoria,DC=empresa
```

