## Release 

Será ramificado a partir de: `dev` 
Deve ser mesclado de volta para: `dev` e `master` 
Convenção de nomenclatura: release-* 

O branch `release` apoia a preparação de uma nova versão de produção. Eles permitem pequenas correções de bugs e preparar os meta-dados para um `release` (número da versão, construção de datas, etc.). Ao fazer todo esse trabalho em um branch `release`, o branch `dev` é liberado para receber recursos para o próximo grande lançamento.

O momento chave para ramificar um novo branch `release` de `dev` é quando o ambiente (quase) reflete o estado desejado da nova versão. Pelo menos todos os recursos que são direcionados para a contrução do `release` deve ser mesclado para `dev` neste momento. Todos os recursos destinados aos futuros lançamentos não poderãoesperar até depois do branch `release` é ramificado.

É exatamente no início de um branch `release` que o lançamento é atribuído um número de versão. Até aquele momento, o branch `dev` refletiu mudanças para a "próxima versão", mas não está claro se essa "próxima versão" acabará por se tornar 0.3 ou 1.0, até o branch release é iniciado. Essa decisão é feita sobre o início do branch `release` e é realizado pelas regras do projeto no número da versão.


### Criando um branch release

Os branches `release` são criados a partir do branch `dev`. Por exemplo, digamos que a versão 1.1.5 é a versão de produção atual e nós temos um grande lançamento chegando. O estado de `dev` está pronto para a "próxima versão" e decidimos que isso vai se tornar a versão 1.2 (em vez de 1.1.6 ou 2.0). Portanto, se ramificar e dar o branch `release` um nome que reflete o novo número de versão:

```
$ git checkout -b release-1.2 dev
// Mudou para um novo branch "release-1.2"
$ 1.2 ./bump-version.sh
// Arquivos modificados com sucesso, versão adiado para 1,2.
$ git commit -a -m "Mudando o número de versão para 1.2"
// [release-1.2 74d9424] Mudando o número de versão para 1.2
// 1 arquivos alterados, 1 inserções (+), 1 deleções (-)
```

Depois de criar um novo branch e mudar para ele, nós mudamos o número da versão. Aqui, bump-version.sh é um script shell fictício que muda alguns arquivos na cópia de trabalho para refletir a nova versão. (Isto pode ser, obviamente, uma mudança manual.) Em seguida, o número da versão alterada está comprometida.

Este novo branch pode existir lá por um tempo, até que o `release` possa ser implementado definitivamente. Durante esse tempo, correções de bugs pode ser aplicada neste branch (em vez de ser no branch `dev`). Adicionando grandes novos recursos aqui é estritamente proibido. Eles devem ser mesclados em dev, e portanto, esperar pelo próximo grande lançamento.

### Finalizar um branch release

Quando o estado do branch `release` está pronto para se tornar um lançamento real, algumas ações precisam ser realizadas. Primeiro, o branch `release` é mesclado em `master` (uma vez que cada commit no `master` é um novo lançamento, por definição). Em seguida, que os commits no `master` devem ser marcados para futura referência fácil para essa versão histórica. Finalmente, as alterações feitas no branch `release` precisam ser mescladas de volta para `dev` de modo que as versões futuras também contêm estas correções de bugs.

Os dois primeiros passos no git: 

```
$ git checkout master
// Para ramificar 'master'
$ git merge --no-ff release-1.2
// Fusão tomada pelos recursiva.
// (Resumo das alterações)
$ git tag -a 1.2
```

O lançamento é feito agora, e marcou para referência futura.

Você pode muito bem querer usar as bandeiras -s ou -u <key>  para assinar seu tag cryptografica. 
 
Para manter as alterações feitas no branch release, precisamos mesclar aqueles volta para `dev`. 

```
$ git checkout dev
// Para o branch "dev"
$ git merge --no-ff release-1.2
// Fusão tomada pelo recursivo.
// (Resumo das alterações)
```

Este passo pode muito bem levar a um conflito de mesclagem (provavelmente até mesmo, uma vez que nós mudamos o número da versão). Se assim for, corrigí-lo e fazer o commit.

Agora estamos realmente feito e o branch `release` pode ser finalizado, uma vez que não é mais necessário: 

```
$ git branch -d release-1.2
// Release-1.2 branch finalizado
```

[< Voltar](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)