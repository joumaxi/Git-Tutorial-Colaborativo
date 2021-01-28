# Regras Básicas do Git
Para poder usufruir desses recursos você precisa entender algumas regras:

1. O controle de versão possui duas pastas principais: uma chamada Repositório ou _Repo_ e outra chamada de _Projeto_.
2. A pasta do _Repo_ é onde os arquivos do projeto são empurrados ou puxados. Não deve ser modificada manualmente e seu conteúdo não pode ser visualizado pois converte os arquivos para um formato que só o controle de versão entende.
3. A pasta do _Projeto_ é onde os arquivos são criados e atualizados e só poderá ter controle de versão caso seja iniciado um: após isso, será criado automaticamente uma pasta de informações que possibilita a comunicação com o _Repo_.
4. O controle de versão só funciona se o usuário se comprometer a  utilizar os comandos do controle de versão. Toda alteração importante deve ser comentada e enviada para o repositório.
5. Um projeto pode apresentar ramificações durante seu desenvolvimento. Essas divisões facilitam as alterações em propostas diferentes e quando mescladas com o _Projeto_, identificam mudanças importantes no desenvolvimento.
6. As alterações do _Projeto_ podem ser rotuladas para orientar a evolução do trabalho.

## Entendendo o conceito dos Índices de Versão

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

[Voltar](main.md)
