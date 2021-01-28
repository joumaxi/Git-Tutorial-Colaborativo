## Criando Ramificações
As ramificações são divisões do projeto. Quando criadas, podem permanecer apenas na pasta do _projeto_ ou serem enviadas para o _repo_.
> **Nota**: Evite nomear ramos com caracteres especiais! Use nomes pequenos e fáceis de serem digitados. Caracteres especiais causam falhas na operação do **git**.

## Ramificando e Trocando 
Para realizar uma ramificação e troca do ramo master para o ramo criado use:
```bash 
$ git checkout -b ramo1
```
Note que a opção `-b` serve para criar a divisão e mudar para ela. Caso você esteja no ramo _master_ e executar esse comando, você criará e mudará para o ramo `ramo1`. Isso significa que todas as suas alterações serão gravadas no `ramo1` até que novamente você vá para outro ramo.
## Apagando Ramo Local
Caso tenha criado um ramo na pasta de projeto e ainda não tiver sincronizado este com o _repo_, use:
```bash
$ git branch -d ramo1 #use -D para forçar!
```
## Apagando o Ramo no Repo
Caso já tenha enviado o _ramo_ para o _repo_, para apagá-lo. Você deverá ir até a pasta do _Repo_ e executar o mesmo comando para apagá-lo [localmente](#apagando-ramo-local).

## Enviando Ramo para o Repo
Um ramo só é enviado para o _repo_ se o seguinte comando for executado.
```bash
$ git push origin ramo1
```

## Trocando para Ramo Existente 
Para simplesmente trocar de um ramo para o outro existente,  use:
```bash
$ git checkout ramo1
```
## Consultando Ramos Existentes
Para consultar os ramos criados dentro de sua pasta de projeto, use:
```bash
$ git branch
```
Mas caso queira consultar se foram criados ramos no _Repo_, use:
```bash
$ git fetch origin
$ git branch -r  #lista os ramos do repo.
```
Se quiser consultar se algum ramo foi apagado, use:
```bash
$ git fetch -p
$ git branch -a  #lista os locais e os do repo.
```
## Verificando Alterações entre Ramos
Para consultar quais os arquivos modificados, use:
```bash
$ git checkout master
$ git diff --name-status  ramo1
```
Mas caso deseje ver o conteúdo das alterações, use:
```bash
$ git checkout master
$ git diff ramo1
```
## Mesclando Ramos
Para atualizar o ramo `master` com as alterações do `ramo1` use:
```bash
$ git checkout master
$ git merge ramo1 #mescla histórico do ramo também. 
```
Para mesclar os arquivos mas preservar o histórico do ramo, use:
```bash
$ git checkout master
$ git merge --no-ff ramo1 #mescla e preserva histórico do ramo. 
```

[Voltar](main.md)
