# Documentação do Fluxo de Trabalho com o GIT

[![licence mit](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/doc-solutions/documentation-gitflow/blob/master/LICENSE.md)
[![issues](https://img.shields.io/github/issues/doc-solutions/documentation-gitflow.svg)](https://github.com/doc-solutions/documentation-gitflow/issues)

## Introdução

É muito importante para um projeto, ter o versionamento do seu código. Principalmente, quando se tem mais de um desenvolvedor na equipe. Crie um cenário, onde um projeto tem 10 desenvolvedores e uma linha de código que você desenvolveu, não está como a deixou. E agora, como saber quem mexeu, se não tem o código versionado? Única solução é parar os outros 9 desenvolvedores e saber o que houve. Nem é preciso dizer que esse processo afetará muito a produtividade da equipe. Portanto, não há desculpas, para não versionar o código. E podemos estar fazendo isso com o [GIT](https://git-scm.com/book/pt-br/v1/). 

## Fluxo de trabalho

Apenas versionar o código, não evita todos os problemas que possam surgir durante o projeto. É necessário que se tenha um fluxo de trabalho e a equipe esteja alinhada. Logo abaixo, está descrita as funções das branches principais e auxiliares.

Veja o gráfico do [Fluxo completo](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/images/flow.jpg).

## Branches

- [Principais](source/branches/main.md)
	- [Master](source/branches/master.md)
	- [Dev](source/branches/dev.md)
- [Auxiliares](source/branches/supporting.md)
	- [Feature](source/branches/feature.md)
	- [Release](source/branches/release.md)
	- [Hotfix](source/branches/hotfix.md)

## Sugestão de nomeação

### Branches auxiliares

Sugestão de nomeação para as branches auxiliares: 

- release/[versão]
- feature/[data(formato americano)]_[nome da feature]
- hotfix/[data(formato americano)]_[nome do hotfix]

Assim, garante mais distinção entre as branches do mesmo segmento.

### Gerenciador de tarefas  e Issues(problemas)

A nomeação pode se extender para o seu gerenciador de tarefas(ex: Jira, Trello...) e a seção de `issues` do seu serviço de controle de versão GIT(ex: github, bitbucket...).

Podemos nos colocar em um cenário:

	- Tarefa: #1
	- Branch: feature/20160103_login

	Na descrição da tarefa, informando a branch que está sendo utilizada, deixará todos os envolvidos cientes sobre a branch. 
	Com a tarefa finalizada, será enviado o _Pull Request_ para a branch `dev` e será criado uma identificação do mesmo. Vamos supor que foi gerado a identificação #34, para o _Pull Request_ . O mesmo deverá ser informado na tarefa, para tenhamos um controle maior dos `commits`, após a finalização da branch. 

Dependendo do nível da tarefa e do alinhamento da equipe, pode ser criado uma `issue`, onde no título se pode constar o identificador do gerenciador de tarefas. Ou simplemente, existe uma `issue` e precisa ser associado a uma tarefa. Isso seria apenas uma sugestão de processo, dependendo do cenário da equipe. Podendo haver desenvolvedores, que estarão acostumados com o ambiente do serviço de controle de versão e os integrantes(designers, analistas e etc), que só terão acesso ao gerenciador de tarefa. Por esse motivo, é muito importante uma boa ligação entre os 2.

Querendo ir ao máximo da organização, podemos estar inserindo `flags`, para identificar os `commits`. O mesmo pode ser inserido no início da mensagem do `commit`, como pode ser visto no exemplo visual abaixo.

Uma boa prática para a padronização das mensagens dos `commits`, dos títulos e descrições das `issues`, é os mesmos serem escritos em inglês.

Dê uma olhada no [Exemplo visual de nomeação(branches, commits e issues)](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/images/branches.jpg).

Cada equipe tem que alinhar os processos para identificação e associação. E para isso é muito importante a nomeação de branches, commits e issues. Fica a sugestão e tendo ideias para contribuir, não perca tempo. :) 

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