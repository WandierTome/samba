LISTAR CONTAS DE USUÁRIOS NA LINHA DE COMANDO:

```
sudo samba-tool user list
```

CRIAR CONTAS DE USUÁRIOS NA LINHA DE COMANDO:

	samba-tool user create --must-change-at-next-login aluno
	samba-tool user create --given-name="Aluno2 Amaral" --must-change-at-next login aluno2
	samba-tool user create --given-name="Aluna Oliveira" --surname="Oliveira" -  must-change-at-next-login Aluna

CRIAR VÁRIAS CONTAS DE USUÁRIOS USANDO O LAÇO DE REPETIÇÃO FOR:

    for users in suzane mauricio mariane edson solange; samba-tool user create --must-change-at-next-login

REDEFINIR UMA SENHA NA LINHA DE COMANDO:

    samba-tool user setpassword aluno

DESABILITAR/HABILITAR CONTA DE USUÁRIO:

    samba-tool user disable aluno
    samba-tool user enable aluno

REMOVER UMA CONTA DE USUÁRIO:

    samba-tool user delete aluno