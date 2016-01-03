# Hotfix

- Criação a partir de: `master`
- Deve ser mesclada em: `dev` e `master`
- Nomenclatura: `hotfix-*` 

Os branches `hotfix` são muito parecidos com os branches `release`, eles também são destinados a preparar-se para uma nova versão de produção, embora não planejada. Eles surgem da necessidade de agir imediatamente após um estado indesejado de uma versão de produção ao vivo. Quando um `bug` crítico em uma versão de produção deve ser resolvido imediatamente, um branch de correção será ramificado a partir da tag correspondente no branch master que marca a versão de produção.

A essência é que o trabalho dos membros da equipe (branch dev) possam continuar, enquanto outra pessoa está a preparar uma correção de produção rápida.

## Criando o branch hotfix

Os branches `hotfix` são criados a partir do branch `master`. Por exemplo, digamos que a versão 1.2 é a versão de produção atual em execução ao vivo e causando problemas devido a um erro grave. Mas as mudanças em `dev` ainda instável. Podemos, então, ramificar um branch `hotfix` e começar a corrigir o problema: 

```
$ git checkout -b hotfix-1.2.1 master
// Mudou para um novo ramo "hotfix-1.2.1"
$ ./bump-version.sh 1.2.1
// Arquivos modificados com sucesso, versão 1.2.1.
$ git commit -a -m "Trocado o número de versão para 1.2.1"
// [hotfix-1.2.1 41e61bb] número da versão 1.2.1
// 1 arquivos alterados, 1 inserções (+), 1 deleções (-)
```

Não se esqueça de mudar o número de versão depois ramificar!

Em seguida, corrigir o erro e se comprometer a correção em um ou mais submissões separadas. 

```
$ git commit -m "Corrigido o problema de produção grave"
//[hotfix-1.2.1 abbe5d6] problema de produção fixo grave
//5 arquivos mudou, 32 inserções (+), 17 exclusões (-)
```

### Finalizar um branch hotfix

Quando terminar, o `hotfix` precisa ser mesclado de volta para `master`, mas também precisa ser mesclado em `dev` a fim de salvar que o `hotfix` que está incluído na próxima versão. Isto é completamente semelhante à forma como branches `releases` são finalizados.

Primeiro, atualizar `master` e marcar o lançamento. 

```
$ git checkout master
// Para ramificar 'master'
$ git merge --no-ff hotfix-1.2.1
// Fusão tomada pelos recursiva.
// (Resumo das alterações)
$ git tag -a 1.2.1
```

Você pode muito bem querer usar as `flags` -s ou -u <key> para assinar seu tag cryptografica.

Em seguida, incluir a correção de bugs em `dev` também: 

```
$ git checkout develop
// Para ramo "dev"
$ git merge --no-ff hotfix-1.2.1
// Fusão tomada pelos recursiva.
// (Resumo das alterações)
```

A única exceção a regra, é quando um `branch` release existe atualmente, as mudanças de `hotfix` precisam ser mesclados no branch `release`, em vez de `dev`. A mesclagem da correção no branch `release` acabará por resultar na `hotfix` sendo mesclado em `dev` também, quando o branch `release` estiver finalizado. (Se o trabalho em `dev` imediatamente requer este `hotfix` e não pode esperar para o branch `release` para ser concluída, você pode, seguramente, mesclar o `hotfix` em `dev`.)

Por fim, remova o branch temporário: 

```
$ git branch -d hotfix-1.2.1
// Excluído o branch hotfix-1.2.1.
```

[< Voltar](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)