---
title: "Tutorial Git"
author: "Joumaxi"
date: 2019-09-06

---

# Tutorial Git para Repositórios
Este tutorial tem por objetivo facilitar o uso de recursos de repositório aplicados a projetos de Firmware, PCI e Documentos.

[TOC]

## Primeiros Passos
Antes de mais nada:
1. Instale o [**git**](https://gitforwindows.org/) no seu computador.
2. Após a instalação, abra o [**git-bash**](c:\git\git-bash.exe) através do atalho disponível no computador e consulte a versão:
```bash
$ git --version
```
3. Verifique suas credenciais:
```bash
$ git config --list
```

Observe os campos que informam o seu nome (`user.name`) e o seu email (`user.email`), caso não estejam claros para sua identificação, faça uma nova configuração (próximo passo).

4. Configure suas credenciais:

```bash
$ git config --global user.name "Meu nome"
$ git config --global user.email "meu_email@dominio.com"
```
Esta configuração é importante para identificar o usuário que realiza as alterações no repositório.

5. Tenha em mente o que você quer controlar e como funciona o controle de versão. 

Para informações mais completas, consulte o [site do git](https://git-scm.com/docs/). Ou digite:
```bash
$ git help <nome_do_comando>
```
## Regras Básicas do Git
Para poder usufruir desses recursos você precisa entender algumas regras:
1. O controle de versão possui duas pastas principais: uma chamada Repositório ou _Repo_ e outra chamada de _Projeto_.
2. A pasta do _Repo_ é onde os arquivos do projeto são empurrados ou puxados. Não deve ser modificada manualmente e seu conteúdo não pode ser visualizado pois converte os arquivos para um formato que só o controle de versão entende.
3. A pasta do _Projeto_ é onde os arquivos são criados e atualizados e só poderá ter controle de versão caso seja iniciado um: após isso, será criado automaticamente uma pasta de informações que possibilita a comunicação com o _Repo_.
4. O controle de versão só funciona se o usuário se comprometer a  utilizar os comandos do controle de versão. Toda alteração importante deve ser comentada e enviada para o repositório.
5. Um projeto pode apresentar ramificações durante seu desenvolvimento. Essas divisões facilitam as alterações em propostas diferentes e quando mescladas com o _Projeto_, identificam mudanças importantes no desenvolvimento.
6. As alterações do _Projeto_ podem ser rotuladas para orientar a evolução do trabalho.


## Criando um Repo Vazio

Pode ser criado em uma conta do Bitbucket ou do Github, mas também pode ser gerado localmente e salvo em uma pasta do próprio computador ou de um servidor de arquivos.
### Repo em pasta local
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

## Sincronizando Repo e Projeto 

### Na Primeira Vez

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

### Durante o Desenvolvimento

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
### Ignorando Arquivos
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

### Adicionando Arquivo Retroativo
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

### Entendendo o conceito dos Índices de Versão

É através da posição do índice que é possível saber se o _Projeto_ está atualizado em relação ao _Repo_.

Veja o exemplo a seguir:

```bash
$ git log
commit b2da6d5d809d50555663461314fef03183e90fae (HEAD -> master, origin/master)
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 16:08:42 2019 -0300

    Adicionado arquivo README

commit 594292f0c23dffedb1a9ad0791c054c8ea51ecc8
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 09:24:04 2019 -0300

    Primeiro, cpuFlap com driver importado e arquivos de saída.

```

Neste caso, temos um projeto com 2 revisões. Veja o texto entre parênteses no final da 2ª linha:

- `HEAD -> master`: este é a posição do índice de versão da pasta de _Projeto_.
- ` origin/master`: este é a posição do índice de versão  da pasta do _Repo_.

Analisando as versões é possível ver que o _Repo_ e o _Projeto_ estão na mesma posição, então estão atualizados.

Quando estes índices estão em posições diferentes ou um deles está oculto, então temos diz-se que estão sem sincronismo.

Por exemplo, observe este outro caso:

```bash
$ git log
commit 75846a84a7913f280028036abe8af7a48d28b852 (HEAD -> master)
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 17:39:00 2019 -0300

    Adicionado info sobre uC ao README.

commit b2da6d5d809d50555663461314fef03183e90fae (origin/master, origin/HEAD)
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 16:08:42 2019 -0300

    Adicionado arquivo README

commit 594292f0c23dffedb1a9ad0791c054c8ea51ecc8
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 09:24:04 2019 -0300

    Primeiro, cpuFlap com driver importado e arquivos de saída.

```

Observe que o _Repo_  está desatualizado em relação ao _Projeto_, ou seja, trata-se de uma revisão local que ainda não foi enviada ao _Repo_.

Mas se na consulta fosse exibido esse caso:

```bash
$ git log
commit b2da6d5d809d50555663461314fef03183e90fae (HEAD -> master)
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 16:08:42 2019 -0300

    Adicionado arquivo README

commit 594292f0c23dffedb1a9ad0791c054c8ea51ecc8
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 09:24:04 2019 -0300

    Primeiro, cpuFlap com driver importado e arquivos de saída.

```

Veja que provavelmente o _Projeto_ está desatualizado pois não mostra onde está o índice `origin/master`.

Para atualizar o _Projeto_, use:

```bash
$ git pull origin master
From C:/projetosKicad/repoKicad/cpuFlap
 * branch            master     -> FETCH_HEAD
Updating b2da6d5..75846a8
Fast-forward
 README.md | 6 ++++--
 1 file changed, 4 insertions(+), 2 deletions(-)
```

E se novamente for consultado os índices, pode-se notar que agora estão sincronizados.

```bash
$ git log
commit 75846a84a7913f280028036abe8af7a48d28b852 (HEAD -> master, origin/master)
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 17:39:00 2019 -0300

    Adicionado info sobre uC ao README.

commit b2da6d5d809d50555663461314fef03183e90fae
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 16:08:42 2019 -0300

    Adicionado arquivo README

commit 594292f0c23dffedb1a9ad0791c054c8ea51ecc8
Author: joumaxi <joumaxi@gmail.com>
Date:   Thu Sep 12 09:24:04 2019 -0300

    Primeiro, cpuFlap com driver importado e arquivos de saída.

```

## Criando Ramificações
As ramificações são divisões do projeto. Quando criadas, podem permanecer apenas na pasta do _projeto_ ou serem enviadas para o _repo_.
> **Nota**: Evite nomear ramos com caracteres especiais! Use nomes pequenos e fáceis de serem digitados. Caracteres especiais causam falhas na operação do **git**.

### Ramificando e Trocando 
Para realizar uma ramificação e troca do ramo master para o ramo criado use:
```bash 
$ git checkout -b ramo1
```
Note que a opção `-b` serve para criar a divisão e mudar para ela. Caso você esteja no ramo _master_ e executar esse comando, você criará e mudará para o ramo `ramo1`. Isso significa que todas as suas alterações serão gravadas no `ramo1` até que novamente você vá para outro ramo.
### Apagando Ramo Local
Caso tenha criado um ramo na pasta de projeto e ainda não tiver sincronizado este com o _repo_, use:
```bash
$ git branch -d ramo1 #use -D para forçar!
```
### Apagando o Ramo no Repo
Caso já tenha enviado o _ramo_ para o _repo_, para apagá-lo. Você deverá ir até a pasta do _Repo_ e executar o mesmo comando para apagá-lo [localmente](#apagando-ramo-local).

### Enviando Ramo para o Repo
Um ramo só é enviado para o _repo_ se o seguinte comando for executado.
```bash
$ git push origin ramo1
```

### Trocando para Ramo Existente 
Para simplesmente trocar de um ramo para o outro existente,  use:
```bash
$ git checkout ramo1
```
### Consultando Ramos Existentes
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
### Verificando Alterações entre Ramos
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
### Mesclando Ramos
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

## Desfazendo Alterações do Projeto
Para eliminar alterações locais ou buscar a última versão disponível no repositório, use:
```bash
$ git fetch origin
$ git reset --hard origin/master
```

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
$ git flag -d v1.0  
```
> **Nota**: Caso tenha criado uma Etiqueta e enviado para o _Repo_, será necessário realizar o mesmo comando no _Repo_ para remover a Etiqueta de lá também. 

## Ferramentas de Mesclagem Externas
Muitas vezes a visualização de diferenças na linha de comando são confusas. Para tanto,  existem ferramentas que usam recursos coloridos e intuitivos para facilitar esse trabalho.
### Meld
Para instalar o **Meld**, execute a seguinte seqüência:

1. Busque a última versão no [site oficial do Meld](https://meldmerge.org) e instale na raiz do sistema.
> **Nota**: Para ambiente _Windows_ utilize a versão **Meld-3.18.3-win32** para integrar com o **git-bash**.

2. Crie uma pasta `scripts` no caminho `C:/Git/scripts`.

3. Crie um _script_ em _python_, com o nome `diff.py` dentro do caminho criado no passo anterior e com o seguinte conteúdo:
```python
#!/c/Python27/python
import sys
import os
os.system('C/Meld/Meld.exe %s %s' % (sys.argv[2],sys.argv[5]))

```
4.Dê permissão ao `diff.py`:
```bash
$ chmod +x diff.py
```
5. Para integrar ao _git_ use:
```bash
$ git config --global diff.external 'C:/Git/scripts/diff.py'
$ git config --global merge.tool meld
```
6. Para usar essa ferramenta faça:
```bash
$ git diff tag1:arquivo tag2:arquivo
```

## Empacotando Projetos
 Serve para arquivar projetos e remover seu controle de versão. Também pode ser usado para utilizar como exemplo para outros projetos. Para executar use:
```bash
$ git archive -o projeto.zip HEAD
```
Note que o nome `HEAD` pode ser substituído por um _tag_ ou uma outra revisão do projeto.

## Extraindo informações do Repo
As informações sobre o _Ramo de Projeto_ ou Revisão podem ser extraídas através de _scripts_. Para tanto use:
```bash
$ git symbolic-ref HEAD #exibe o ramo
$ git rev-parse --short=7 HEAD #exibe a revisão
```
## Resolvendo Problemas
### Erro de Configuração no Windows XP
Caso apareça a mensagem de problemas no _SSL_ quando realizar qualquer comunicação, tipo um clone, adicione a _Variável de Ambiente_  `GIT_SSL_NO_VERIFY` e faça o valor igual a `1`.

## Automação de Tarefas

A automação de tarefas é fundamental para melhorar a produtividade dos trabalhos, além de estabelecer um padrão de construção e apresentação de informações. Junto com o _git_, podem ser utilizadas as seguintes aplicações:

- Python
- Todo.txt
- SQLite

### Configurando o Python no Windows 8.1

Em plataforma _Windows_ recomenda-se utilizar o `Python3`de 32 bits pois para aplicações gráficas, as bibliotecas `tk` e `pywin32`devem usar um _Python_ compilado em 32 bits. Adicione à _Variável de Ambiente_ chamada `Path`os caminhos de instalação do **Python**  e de execução de seus **Scripts** .

> **Nota**: Instale o Python em um caminho o menor possível, para que o texto adicionado ao `Path` não seja muito longo, por exemplo: `C:\Python38;C:\Python38\Scripts`.

### Instalando o PIP no Windows 8.1

O _pip_ é um gerenciador de pacotes para _python_ , para instalar no _Windows_ siga os seguintes passos:

1. Após instalar o _Python_, baixe o arquivo [get-pip.py](https://bootstrap.pypa.io/get-pip.py);

2. Execute o comando:

   ```bash
   $ python get-pip.py
   ```

3. Consulte se o _pip_ foi instalado com sucesso:

   ```bash
   $ pip --version
   ```

> **Nota**: O arquivo get-pip.py está disponível na pasta deste repositório em `\scripts\`.

