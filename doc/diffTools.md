## Buscando todas as alterações da revisão 
Para mostrar todos os arquivos alterados, bem como o que foi alterado, use:
```bash
$ git show 9fceb02
```
> **Nota**: Pode-se também usar o nome de **tag**.

Caso queira uma visão gráfica do negócio, use:
```bash
$ gitk
```

## Comparando alterações entre arquivos
As alterações de arquivos entre versões podem ser consultadas em conjunto usando:
```bash
$ git diff tag1 tag2 --stat
```
Para consultar alterações específicas no conteúdo use:
```bash
$ git diff tag1 tag2 -- arquivo
```
Caso possua uma ferramenta gráfica de diferenciação, use:
```bash
$ git difftool tags/tag1 tags/tag2
```

## Buscando Versão Anterior de Arquivo
Para buscar a versão anterior do arquivo, basta retornar para a versão antes de sua modificação, para tanto faça:
```bash
$ git log pretty=oneline #exibe commit e message.
$ git checkout 9fceb02
```
> **Nota**: Caso haja **tags**, pode-se por o nome do **tag** no lugar do número do **commit**.

