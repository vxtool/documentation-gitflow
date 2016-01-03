# Documentação do Fluxo de Trabalho com o GIT

[![licence mit](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/doc-solutions/documentation-gitflow/blob/master/LICENSE.md)
[![issues](https://img.shields.io/github/issues/doc-solutions/documentation-gitflow.svg)](https://github.com/doc-solutions/documentation-gitflow/issues)

## Introdução

É muito importante para um projeto, ter o versionamento do seu código. Principalmente, quando se tem mais de um desenvolvedor na equipe. Crie um cenário, onde um projeto tem 10 desenvolvedores e uma linha de código que você desenvolveu, não está como a deixou. E agora, como saber quem mexeu, se não tem o código versionado? Única solução é parar os outros 9 desenvolvedores e saber o que houve. Nem é preciso dizer que esse processo afetará muito a produtividade da equipe. Portanto, não há desculpas, para não versionar o código. E podemos estar fazendo com o [GIT](https://git-scm.com/book/pt-br/v1/). 

## Fluxo de trabalho

Apenas versionar o código, não evita todos os problemas que possam surgir durante o projeto. É necessário que se tenha um fluxo de trabalho e a equipe esteja alinhada. Abaixo na parte de [Ilustração](#ilustracao), podemos ver o `fluxo completo`. E logo abaixo, está descrita as funções das branches principais e auxiliares.

## Branches

- [Principais](source/branches/main.md)
	- [Master](source/branches/master.md)
	- [Dev](source/branches/dev.md)
- [Auxiliares](source/branches/supporting.md)
	- [Feature](source/branches/feature.md)
	- [Release](source/branches/release.md)
	- [Hotfix](source/branches/hotfix.md)

## Ilustração

- [Fluxo completo](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/images/flow.jpg)
- [Nomeação](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/images/branches.jpg)

## Referências

- [Cheatsheet do git-flow](http://danielkummer.github.io/git-flow-cheatsheet/index.pt_BR.html)
- [Atlassian - Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

## Contribuindo

Veja o [Contributing](CONTRIBUTING.md) para mais detalhes.

## Log

Veja o [Changelog](CHANGELOG.md) para mais detalhes.

## Licença

[MIT license](LICENSE.md) © Copyright 2015 [Hemerson Vianna](http://hemersonvianna.io).