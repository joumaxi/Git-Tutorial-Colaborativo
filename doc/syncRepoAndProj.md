# Sincronizando Repo e Projeto 

## Na Primeira Vez

Este passo é realizado entre um repositório vazio e a pasta de projeto com os arquivos que se  deseja enviar para o controle de versão:
```bash
$ git init
$ git add arquivos_do_projeto
$ git status #use para ver o que foi adicionado
$ git commit -m "Primeiro commit"
$ git remote add origin /caminho_do_repo
$ git remote -v #use para ver se foi incluído 
$ git push origin master
```
> **Nota**: o comando `remote add` adiciona um caminho marcado como `origin`. Essa definição simplifica a chamada do endereço do _Repo_ e também permite que outros endereços de _Repos_ possam ser cadastrados e utilizados.

Para testar se a inclusão foi feita com sucesso, volte para a pasta do ambiente de trabalho e execute um [clone](#copiando-de-repo-existente). Caso tenha adicionado o caminho errado, pode removê-lo usando `git remote rm origin`.

Caso sua pasta ainda não tenha arquivos de projeto e o repositório vazio já tiver sido criado, faça um [clone](#copiando-de-repo-existente), adicione os arquivos na pasta e depois [atualize](#atualizando-o-repo).

## Durante o Desenvolvimento

Durante a construção do _Projeto_, pode haver mais de um usuário produzindo alterações e atualizando o mesmo _Repo_, desta forma, além de periodicamente verificar se alguém gerou alguma revisão é necessário sincronizar com o _Repo_.

Caso deseje sincronizar apenas o índice, use:

```bash
$ git fetch origin
```

 Se o _Projeto_ não possui nenhuma alteração em andamento e você deseje buscar a última versão, use:

```bash
$ git pull origin master
```

Caso o projeto possua alterações em andamento e você deseje pausá-las para buscar a última versão, então você precisa:

```bash
$ git add arquivo #adicione o que está incompleto
$ git stash 	#irá salvar e ocultar os arquivos adicionados
$ git reset --hard origin/master	#volta ao padrão do repo
$ git stash pop #volta o trabalho incompleto
$ git commit -m "Corrigidos bugs"
$ git push origin master
```

Desta forma o trabalho não é perdido e pode ser retomado  depois.

## Sincronizando Ramo do Projeto com o Repo

Durante a construção do _projeto_, [ramificações](#criando-ramificações) são criadas e apagadas, seja para realizar correção de _bugs_ seja para lançar novas funcionalidades ao _projeto_. Normalmente esses _ramos_ permanecem apenas na pasta do _projeto_ contudo podem ser enviados para o _repo_ também. Para tanto faça:

```bash
$ git push -u origin ramo1
```

[Voltar](main.md)
