# Primeiros Passos

Existem muitos tutoriais sobre **git**, contudo, existem algumas considerações:
1. Consulte primeiro a documentação oficial: o mantenedor é responsável por criar, editar e documentar a ferramenta.

Antes de mais nada:

1. Instale o [git](https://git-scm.com/) no seu computador.
2. Após a instalação, abra o [git-bash](c:\git\git-bash.exe) através do atalho disponível no computador e consulte a versão:
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

[Voltar](main.md)
