## Trabalhando com Etiquetas
Etiquetas são úteis para marcar pontos específicos do desenvolvimento. Podem ser do tipo de _Leve_ ou _Anotada_.
Para buscar Etiquetas do _Repo_ use:
```bash
$ git fetch origin 
```
> **Nota**: Certifique-se que nas configurações a opção `push.followtags` está em `true`, caso não esteja use: `git config --global push.followTags true`.

### Etiqueta Leve
Serve para identificar uma revisão de produto através  de um texto e não um número longo.
Para criar uma use:
```bash
$ git tag 0025.003.1279-01
```
> **Nota:** Não use espaços para nomear a etiqueta. Use etiquetas leves apenas para revisões locais.

### Etiqueta Anotada
Além do nome, também pode conter uma mensagem para explicar algo referente. Além de copiar todos os dados do autor, permite a verificação posterior. Para criar uma use:
```bash
$ git tag -a 0025.003.1279-01 -m "Lote de Produção"
```
### Consultando Etiquetas
Para consultar etiquetas existentes use:
```bash
$ git tag
```
Para consultar as informações de uma Etiqueta (_tag_) Anotada use:
```bash
$ git tag -v 0025.003.1279-01
```
### Etiqueta Retroativa
Para adicionar etiquetas retroativas, você precisa consultar o valor das revisões e atribuir a etiqueta ao valor desejado. Assim, faça:
```bash
$ git log --pretty=oneline #exibe commit e message.
$ git tag -a v1.0 9fceb02 #cria retroativo.
$ git tag #consulta se a tag foi criada.
```
### Apagando Etiquetas
Para apagar uma Etiqueta use:
```bash
$ git tag -d v1.0  
```
> **Nota**: Caso tenha criado uma Etiqueta e enviado para o _Repo_, será necessário realizar o mesmo comando no _Repo_ para remover a Etiqueta de lá também. 

[Voltar](main.md)
