# Hotfix

- Criação a partir de: `master`
- Deve ser mesclada em: `dev` e `master`
- Nomenclatura: `hotfix/*` 

A branch `hotfix` é muito parecida com a branch `release`, ela também é destinada para uma nova versão de produção, embora não planejada. Ela é criada da necessidade de agir imediatamente após um estado indesejado de uma versão de produção. Quando um `bug` crítico em uma versão de produção deve ser resolvido imediatamente, uma branch `hotfix` será criada a partir da tag correspondente na branch `master` que marca a versão atual de produção.

É fundamental que o trabalho dos membros da equipe(branch dev) possa continuar, enquanto outra pessoa está preparando uma correção rápida para produção.

## Criando uma branch

A branch `hotfix` é criada a partir da branch `master`. Digamos que a versão 1.2 é a versão atual de produção e está causando problemas devido a um erro grave. Mas há mudanças em `dev` ainda instável. Podemos, criar uma branch `hotfix` e começar a corrigir o problema: 

```
$ git checkout -b hotfix/1.2.1 master
// Criou uma nova branch "hotfix/1.2.1"
$ ./bump-version.sh 1.2.1
// Arquivos modificados com sucesso, versão 1.2.1.
$ git commit -am "Alterando o número de versão para 1.2.1"
// [hotfix-1.2.1 41e61bb] Alterando o número da versão 1.2.1
// 1 arquivos alterados, 1 inserções (+), 1 exclusões (-)
```

Em seguida, se corrige o erro, fazendo os `commits` para a correção. 

```
$ git commit -m "Corrigido o problema de produção grave"
//[hotfix/1.2.1 abbe5d6] Corrigido o problema de produção grave
//5 arquivos alterados, 32 inserções (+), 17 exclusões (-)
```

## Finalizando uma branch

Quando terminar, a branch `hotfix` precisa ser mesclada de volta para `master`, mas também precisa ser mesclada em `dev`, a fim de salvar o que está na branch `hotfix`, na próxima versão. É semelhante com a finalização de uma branch `release`.

Primeiro, atualizar a branch `master` e marcar o lançamento. 

```
$ git checkout master
// Entra na branch 'master'
$ git merge --no-ff hotfix/1.2.1
// Faz a junção do hotfix com master
$ git tag -a 1.2.1
// cria a tag da versão
```

Em seguida, incluir a correção de bugs em `dev` também: 

```
$ git checkout dev
// Entra na branch "dev"
$ git merge --no-ff hotfix/1.2.1
// Faz a junção do hotfix com dev
```

A única exceção a regra, é quando uma branch `release` existe e as mudanças da branch `hotfix`, precisam ser mescladas na branch `release`, ao invés de `dev`. A mesclagem da correção na branch `release` acabará por resultar na branch `hotfix` ser mesclada em `dev` também, quando a branch `release` estiver finalizada. (Se o trabalho em `dev` requer imediatamente este `hotfix` e não pode esperar para a branch `release` para ser concluída, você pode, seguramente, mesclar a branch `hotfix` em `dev`.)

Por fim, remova a branch temporário: 

```
$ git branch -d hotfix/1.2.1
// Excluída a branch hotfix/1.2.1.
```

[&#65513; Auxiliares](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/branches/supporting.md)

[&#65513; Readme](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)