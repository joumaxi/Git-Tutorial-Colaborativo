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
