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

