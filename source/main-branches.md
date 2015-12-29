# Branches principais

- master
- dev

O código fonte do `HEAD` do branch principal `origin/master`, sempre representará que está pronto para produção.

No branch `origin/dev`, o código fonte sempre reflete um estado com as alterações de desenvolvimento mais recente entregues para o próximo `release`. Alguns chamariam isso de "ramo de integração". Qualquer outro branch será criado a partir deste.

Quando o código-fonte no branch dev chega a um ponto estável e está pronto para ser lançado, todas as alterações devem ser mescladas de volta para master de alguma forma e, em seguida, marcado com um número de versão.

Portanto, cada vez que as alterações são mescladas de volta para master, esta é uma nova versão de produção por definição.

[< Voltar](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)