# Criando um Repo Vazio

Pode ser criado em uma conta do Bitbucket ou do Github, mas também pode ser gerado localmente e salvo em uma pasta do próprio computador ou de um servidor de arquivos.

## Repo em pasta local

```bash
$ mkdir repoTeste.git 
$ cd repoTeste.git
$ git init --bare 
```
Note que este tipo de repositório não possui seus arquivos acessíveis, mas pode ser consultado seus _commits_ através de:
```bash
$ cd repoTeste.git
$ git log
```

