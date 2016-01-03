# Principais

- [master](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/master.md)
- [dev](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/dev.md)

O código do `HEAD` da branch principal `origin/master`, sempre representará o que está pronto para produção.

Na branch `origin/dev`, o código sempre refletirá um estado com as alterações de desenvolvimento mais recente entregues para o próximo `release`. Alguns chamariam isso de "branch de integração". Todos os outras branches, serão criados a partir deste. 
Quando o código na branch `dev` chega a um ponto estável e está pronto para ser lançado, todas as alterações devem ser mescladas de volta para `master`, marcado com um número de versão.

Portanto, cada vez que as alterações são mescladas de volta para master, esta é uma nova versão de produção.

[&#65513; Voltar](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)