# Sugestão de nomeação

## Branches auxiliares

Sugestão de nomeação para as branches auxiliares: 

- `release/[versão]`
- `feature/[data(formato americano)]_[nome da feature]`
- `hotfix/[versão]`

Assim, garante mais distinção entre as branches do mesmo segmento.

## Gerenciador de tarefas  e Issues(problemas)

A nomeação pode se extender para o seu gerenciador de tarefas(ex: Jira, Trello...) e a seção de `issues` do seu serviço de controle de versão GIT(ex: github, bitbucket...).

Podemos nos colocar em um cenário:

>- Tarefa: #1
>- Branch: feature/20160103_login

>Na descrição da tarefa, informando a branch que está sendo utilizada, deixará todos os envolvidos cientes sobre a branch. 
>Com a tarefa finalizada, será enviado o _Pull Request_ para a branch `dev` e será criado uma identificação do mesmo. Vamos supor que foi gerado a identificação #34, para o _Pull Request_ . O mesmo deverá ser informado na tarefa, para tenhamos um controle maior dos `commits`, após a finalização da branch. 

Dependendo do nível da tarefa e do alinhamento da equipe, pode ser criado uma `issue`, onde no título se pode constar o identificador do gerenciador de tarefas. Ou simplemente, existe uma `issue` e precisa ser associado a uma tarefa. Isso seria apenas uma sugestão de processo, dependendo do cenário da equipe. Podendo haver desenvolvedores, que estarão acostumados com o ambiente do serviço de controle de versão e os integrantes(designers, analistas e etc), que só terão acesso ao gerenciador de tarefa. Por esse motivo, é muito importante uma boa ligação entre os 2.

Querendo ir ao máximo da organização, podemos estar inserindo `flags`, para identificar os `commits`. O mesmo pode ser inserido no início da mensagem do `commit`, como pode ser visto no exemplo visual abaixo.

Uma boa prática para a padronização das mensagens dos `commits`, dos títulos e descrições das `issues`, é os mesmos serem escritos em inglês.

![Exemplo visual de nomeação(branches, commits e issues)](images/branches.jpg)

Cada equipe tem que alinhar os processos para identificação e associação. E para isso é muito importante a nomeação de branches, commits e issues. Fica a sugestão e tendo ideias para contribuir, não perca tempo. :) 