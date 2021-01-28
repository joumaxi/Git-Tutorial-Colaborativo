## Consulta Histórico do Repo
O histórico de versões pode ser consultado com:
```bash
$ git fetch origin
$ git log
```
Note que o `fetch` serve para sincronizar o índice do _Repo_ com o do _Projeto_. Isso é muito útil quando alguém, que também tenha acesso ao _Repo_, tenha gerado alguma revisão.

Para uma consulta simplificada do histórico, pode-se utilizar:
- Consulta apenas das mensagens de revisão:
```bash
$ git shortlog
```
- Consulta do número simplificado da revisão e mensagem em uma linha:
```bash
$ git log --oneline
```
- Consulta do número total da revisão e mensagem em uma linha:
```bash
$ git --pretty=online
```

## Adicionando Arquivo Retroativo
O *git* permite que se adicione arquivos retroativamente ao projeto sem que se crie uma revisão nova.
```bash
$ git add file
$ git commit --amend
$ git push -f origin master
```
Note que a opção `-f` serve para forçar a atualização do repositório.

Após o `commit`, o arquivo de mensagem da última revisão será aberto para edição. Não esqueça de acrescentar o que foi modificado.
> **Nota**: só faça alterações retroativas apenas quando realmente precisar corrigir a última versão gerada. Lembre-se que na unificação, só será visível a versão corrigida.

### Revertendo Alteração Retroativa
Em alguns casos, pode ser necessário cancelar uma alteração retroativa,  principalmente se for preciso executar uma mesclagem, para proceder, você deve cancelar a alteração retroativa (neste caso é a última realizada), então faça:
```bash
$ git reset --soft HEAD@{1} #cancela mas não deleta.
$ git commit -C HEAD@{1} #separa os commits.
```

## Consulta Alterações no Projeto
Para verificar se o repositório local apresenta alterações, use:
```bash
$ git status
```

## Ignorando Arquivos
Pode-se tornar _invisível_ arquivos e pastas Para o controle de versão. Para fazer isso crie um arquivo chamado `.gitignore` e acrescente a ele, em cada linha, o nome dos tipos de arquivos qur deseja que o controle de versão ignore.
Este processo poderá ser efetuado diretamente no terminal:
``` bash
$ vim .gitignore
#preencha com os nomes que deseja excluir
$ git add .gitignore #inclua ao controle de versão 
```

## Copiando de Repo Existente
A ação de copiar os arquivos do repositório existente para o projeto é:
```bash
$ git clone endereco_do_repo
```
> **Nota**: Lembre-se que será criado uma pasta com o mesmo nome da pasta do repositório.

## Atualizando o Repo
Quando desejar atualizar os arquivos do _Repo_ com as alterações que você fez, use:
```bash
$ git status
$ git add *  #também pode ser específico
$ git status #veja se adicionou tudo que deseja
$ git commit -m "Descreva a alteração"
$ git push origin master
```
> **Nota**: Para apenas atualizar arquivos modificados e que já estão no _Repo_, use: `git add -u`.

Caso tenha adicionado algum arquivo indesejado, você pode removê-lo da lista ou até mesmo da pasta.

Para removê-lo apenas da lista:
```bash
$ git reset -- nome_do_arquivo
```
Para além da lista, também removê-lo da pasta do projeto:
```bash
$ git rm nome_do_arquivo
```
> **Nota**: Caso deseje configurar os arquivos ou pastas que não devem ser acrescentados ao repositório, use o [`.gitignore`](#ignorando-arquivos)

### Definindo caminho de Repo
Para adicionar um endereço de um _Repo_ ao _Projeto_, use:
```bash
$ git remote add origin /p/#ENGENHARIA\ -\ SOLUTRON/Repositorios/ihm16x2_sorvete.git
```
Observe que o `origin` é o nome usado para identificar o local onde se encontra o _Repo_.
> **Nota**: para representar caminhos com espaço nos nomes, use `\` antes do espaço, pois o espaço é considerando um caracter especial para o **bash**.

Para apagar um caminho de _Repo_ chamei de `origin`, use:
```bash
$ git remote remove origin
```

Para consultar quais caminhos de _Repo_ estão definidos use:
```bash
$ git remote -v
```
