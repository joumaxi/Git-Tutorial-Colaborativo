
## Trabalhando com Sub-módulos

Um *Sub-módulo* é um *projeto adicional de outro repositório* e é usado quando se deseja incluir novas funcionalidades ao seu projeto. Como possuem controle de versão diferente, devem ser atualizados de maneira individual e garantem  que incompatibilidades com versões mais recentes do sub-módulo não afetem a construção do *projeto principal*.

### Adicionando sub-módulos ao projeto

### Clonando um projeto com sub-módulos

### Atualizando sub-módulos retroativamente

### Apagando um sub-módulo do projeto

Para remover um sub-módulo de seu projeto, são necessários alguns passos:

1. Acesse o arquivo `.gitmodules` e remova o sub-módulo desejado:

   ```bash
   [submodule "drv"]
           path = drv
           url = C:/Users/CIDRAL/IarStm8/repos/lib_drv_iar_stm8s.git/
   
   [submodule "api"]
           path = api
           url = C:/Users/CIDRAL/IarStm8/repos/lib_api.git/
   
   ```

   Neste caso, será removido o sub-módulo `drv`, então ao final da edição, tem-se:

   ```bash
   [submodule "api"]
           path = api
           url = C:/Users/CIDRAL/IarStm8/repos/lib_api.git/
           
   ```

2. Adicione as alterações para enviar para a revisão:

   ```bash
   $ git add .gitmodules
   ```

   

3. Acesse o arquivo `.git/config` e remova as informações do sub-módulo correspondente, neste caso, **remova** a informação:

   ```bash
   [submodule "drv"]
           url = C:/Users/CIDRAL/IarStm8/repos/lib_drv_iar_stm8s.git/
   
   ```

4. Remova o caminho do sub-módulo da revisão:

   ```bash
   $ git rm --cached drv
   ```

5. Remova a pasta do sub-módulo correspondente de dentro da pasta do `.git/modules`:

   ```bash
   $ rm -rf .git/modules/drv
   ```

6. Gere a revisão com a mensagem da exclusão do sub-módulo:

   ```bash
   $ git commit -m "Removido o submodulo drv."
   ```

7. Caso deseje apagar os arquivos da pasta use o comando:

   ```bash
   $ rm -rf drv
   ```

