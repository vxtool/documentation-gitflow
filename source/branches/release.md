# Release 

- Criação a partir de: `dev` 
- Deve ser mesclada em: `dev` e `master` 
- Nomenclatura: `release/*`

A branch `release` apoia a preparação de uma nova versão de produção. Ela permite pequenas correções de bugs e a preparação para um `release`(número de versão). Os novos recursos estando em uma branch `release`, a branch `dev` é liberada para receber novos recursos para o próximo grande lançamento.

O momento chave para criar uma nova branch `release` de `dev` é quando o ambiente (quase) reflete o estado desejado da nova versão. Todos os recursos que são direcionados para a contrução do `release` devem ser mesclados para `dev` neste momento. Todos os recursos destinados a futuros lançamentos terão que esperar a criação da branch `release`.

É exatamente no início de uma branch `release` que é atribuído um número de versão para o lançamento. Até aquele momento, a branch `dev` refletiu mudanças para a "próxima versão", mas não está claro se essa "próxima versão" será 0.3 ou 1.0, até a branch `release` ser criada. Essa decisão do número da versão é feita sobre a criação da branch `release` e é realizado pelas regras do projeto.

## Criando uma branch

A branch `release` é criada a partir da branch `dev`. Digamos que a versão 1.1.5 é a versão atual de produção e nós temos um grande lançamento chegando. O estado de `dev` está pronto para a "próxima versão" e decidimos que isso vai se tornar a versão 1.2 (em vez de 1.1.6 ou 2.0). Portanto, será criada e dada a branch `release` um nome que reflete o novo número de versão:

```
$ git checkout -b release/1.2 dev
// Criou a nova branch "release-1.2"
$ 1.2 ./bump-version.sh
// Arquivos modificados com sucesso, versão alterada para 1.2.
$ git commit -am "Alterando o número de versão para 1.2"
// [release-1.2 74d9424] Alterando o número de versão para 1.2
// 1 arquivos alterados, 1 inserções (+), 1 exclusões (-)
```

Depois de criar uma nova branch e mudar para ela, nós mudamos o número da versão. No exemplo, bump-version.sh é um script shell fictício que muda alguns arquivos para refletir a nova versão. (Isto pode ser, obviamente, uma mudança manual.) Em seguida, criamos um `commit` com essa alteração.

A nova branch pode existir por um tempo, até que o `release` possa ser implementado definitivamente. Durante esse tempo, correções de bugs podem ser aplicadas nesta branch (em vez de ser na branch `dev`). É estritamente proibido adicionar grandes novos recursos aqui. Eles devem ser mesclados em `dev`, e portanto, esperar pelo próximo grande lançamento.

## Finalizando uma branch

Quando a branch `release` estiver pronta para se tornar um lançamento real, algumas ações precisam ser realizadas. Primeiro, a branch `release` é mesclada em `master` (uma vez que cada commit no `master` é um novo lançamento, por definição). Em seguida, os commits no `master` devem ser marcados para futura referência fácil para essa versão histórica. Finalmente, as alterações feitas na branch `release` precisam ser mescladas em `dev`, de modo que as versões futuras também contenham estas correções de bugs.

Os dois primeiros passos no git: 

```
$ git checkout master
// Entra para a branch 'master'
$ git merge --no-ff release/1.2
// Faz a junção do release com master.
$ git tag -a 1.2
// cria a tag da versão
```

O lançamento é feito e marcado para referência futura. 
Para manter as alterações feitas na branch `release`, precisamos mesclar em `dev`. 

```
$ git checkout dev
// Entra na branch "dev"
$ git merge --no-ff release-1.2
// Faz a junção do release com dev
```

Este passo pode muito bem levar a um conflito de mesclagem (provavelmente até mesmo, uma vez que nós mudamos o número da versão). Sendo assim, é só corrigir e fazer o commit.

Agora sim, a branch `release` pode ser finalizada, uma vez que não é mais necessária: 

```
$ git branch -d release/1.2
// Release/1.2 branch finalizado
```

[&#65513; Auxiliares](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/branches/supporting.md)

[&#65513; Readme](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)