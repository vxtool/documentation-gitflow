# Documentação de fluxo no GIT

# Branches principais

- master
- dev

O código fonte do `HEAD` do branch principal `origin/master`, sempre representará que está pronto para produção.

No branch `origin/dev`, o código fonte sempre reflete um estado com as alterações de desenvolvimento mais recente entregues para o próximo `release`. Alguns chamariam isso de "ramo de integração". Qualquer outro branch será criado a partir deste.

Quando o código-fonte no branch dev chega a um ponto estável e está pronto para ser lançado, todas as alterações devem ser mescladas de volta para master de alguma forma e, em seguida, marcado com um número de versão.

Portanto, cada vez que as alterações são mescladas de volta para master, esta é uma nova versão de produção por definição.


# Branches auxiliares

Ao lado do branches principais master e dev, o nosso modelo de desenvolvimento utiliza uma variedade de branches de apoio para auxiliar o desenvolvimento paralelo entre os membros da equipe, facilidade de rastreamento de recursos, preparação para lançamentos de produção e para auxiliar na fixação rapidamente problemas de produção ao vivo. Ao contrário dos principais branches, estes branches sempre tem um tempo de vida limitado, uma vez que eles serão removidos eventualmente.

Os diferentes tipos de branches que podem utilizar são:

- feature
- release 
- hotfix 

Cada um desses branches têm um propósito específico e estão vinculados a regras estritas quanto à qual as sucursais podem ser seu ramo de origem e que ramos devem ser os seus destinos de mesclagem.

De maneira nenhuma esses branches são "especiais" de uma perspectiva técnica. Os tipos de filiais são classificados pela forma como os usamos. 

## Feature

Pode se ramificam a partir de: dev
Deve mesclar volta para: dev 
Filial convenção de nomenclatura: qualquer coisa, exceto master dev release-* ou hotfix-* 

os Branches features (ou às vezes chamados de branch topic) são usados ​​para desenvolver novas funcionalidades para o próximo ou um lançamento futuro distante. Ao iniciar o desenvolvimento de um recurso, a versão alvo em que esse recurso será incorporado pode muito bem ser desconhecida nesse ponto. A essência de um branch de recurso é que ele existe enquanto o recurso está em desenvolvimento, mas acabará por ser mescladas de volta para dev (definitivamente adicionar o novo recurso para o lançamento) ou descartados (no caso de uma experiência decepcionante).

Os branches features normalmente existem em repositórios do desenvolvedor apenas, não em origin.

### Criando um branch feature

Quando começar a trabalhar em um novo recurso, se ramificam a partir do branch dev. 

	$ git checkout -b myfeature dev


Incorporando uma característica finalizada em dev

Recursos acabados podem ser mescladas no branch dev definitivamente para serem adiciondos à próxima versão: 

	$ git checkout dev
	$ git merge --no-ff MyFeature
	$ git branch -d MyFeature
	$ git push origin dev

O --no-ff flag faz com que a impressão em série para criar sempre um novo objeto commit, mesmo que a fusão poderia ser realizada com um fast-forward. Isso evita a perda de informações sobre a existência histórica de um ramo de funcionalidade e reúne todos os commits que juntos adicionaram o recurso. Comparar:

Neste último caso, é impossível ver a história Git qual dos objetos cometem juntos têm implementado um recurso de que você teria que ler manualmente todas as mensagens de log. Reverter uma característica totalmente (ou seja, um grupo de commit), é uma verdadeira dor de cabeça na última situação, enquanto ele é feito facilmente se o --no-ff foi usada bandeira.

Sim, ele vai criar um pouco mais (Vazio) cometer objetos, mas o ganho é muito maior do que o custo. 


## Release 

Pode se ramificam a partir de: dev 
Deve mesclar volta para: dev e master 
Filial convenção de nomenclatura: release-* 

O branch release apoia a preparação de uma nova versão de produção. Eles permitem pequenas correções de bugs e preparar os meta-dados para um release (número da versão, construir datas, etc.). Ao fazer todo esse trabalho em um branch release, o branch dev é liberado para receber recursos para o próximo grande lançamento.

O momento-chave para ramificar um novo branch release de dev é quando desenvolver (quase) reflete o estado desejado da nova versão. Pelo menos todos os recursos que são direcionados para o release-to-be-construído deve ser fundidos para develop neste momento no tempo. Todos os recursos destinados aos futuros lançamentos não-poderão deve esperar até depois do ramo release é ramificado.

É exatamente no início de um ramo release que o lançamento é atribuído um número de versão-não mais cedo. Até aquele momento, a develop ramo refletiu mudanças para a "próxima versão", mas não está claro se essa "próxima versão" acabará por se tornar 0.3 ou 1.0, até o ramo release é iniciado. Essa decisão é feita sobre o início do ramo release e é realizado pelas regras do projeto no número da versão colisão.


### Criando um branch release

Branches de libertação são criados a partir do branch dev. Por exemplo, digamos versão 1.1.5 é a versão de produção atual e nós temos um grande lançamento chegando. O estado de dev está pronto para a "próxima versão" e decidimos que isso vai se tornar a versão 1.2 (em vez de 1.1.6 ou 2.0). Portanto, se ramificam e dar o branch release um nome que reflete o novo número de versão:

	$ git checkout -b release-1.2 dev
	Mudou para um novo branch "release-1.2"
	$ 1.2 ./bump-version.sh
	Arquivos modificados com sucesso, versão adiado para 1,2.
	$ git commit -a -m "Bumped número de versão para 1.2"
	[release-1.2 74d9424] Bumped número de versão para 1.2
	1 arquivos alterados, 1 inserções (+), 1 deleções (-)


Depois de criar um novo branch e mudar para ele, nós bater o número da versão. Aqui, bump-version.sh é um script shell ficcional que muda alguns arquivos na cópia de trabalho para refletir a nova versão. (Isto pode ser, obviamente, uma mudança-o manual do ponto sendo que alguns arquivos mudar.) Em seguida, o número da versão colidido está comprometida.

Este novo branch pode existir lá por um tempo, até queo release pode ser implementado definitivamente. Durante esse tempo, correções de bugs pode ser aplicada neste ramo (em vez de sobre o branch dev). Adicionando grandes novos recursos aqui é estritamente proibida. Eles devem ser fundidas em develop e, portanto, esperar pelo próximo grande lançamento.

### Terminar um branch release

Quando o estado do branch release está pronto para se tornar um lançamento real, algumas ações precisam ser realizadas. Primeiro, o branch release é mesclado master (uma vez que cada commit no master é um novo lançamento, por definição, lembre-se). Em seguida, que cometem no master deve ser marcado para futura referência fácil para essa versão histórica. Finalmente, as alterações feitas no ramo release precisam ser mescladas de volta para dev de modo que as versões futuras também contêm estas correções de bugs.

Os dois primeiros passos na git: 

	$ git checkout master
	Comutado para ramificar 'master'
	$ git merge --no-ff release-1.2
	Fusão tomada pelos recursiva.
	(Resumo das alterações)
	$ git tag -a 1.2

O lançamento é feito agora, e marcou para referência futura.

    Edit: Você pode muito bem querer usar as -s ou -u <key> bandeiras para assinar seu tag cryptographically. 

Para manter as alterações feitas no ramo release, precisamos mesclar aqueles volta para develop no entanto. Em Git: 

	$ git checkout dev
	Comutado para o branch "dev"
	$ git merge --no-ff release-1.2
	Fusão tomada pelo recursivo.
	(Resumo das alterações)

Este passo pode muito bem levar a um conflito de mesclagem (provavelmente até mesmo, uma vez que nós mudamos o número da versão). Se assim for, corrigi-lo e cometer.

Agora estamos realmente feito eo ramo release pode ser afastado, uma vez que não é mais necessário: 

	$ git branch -d release-1.2
	Release-1.2 ramo eliminado (foi ff452fe).


## Hotfix

Pode se ramificam a partir de: master 
Deve mesclar volta para: dev e master 
Filial convenção de nomenclatura: hotfix-* 

Os branches hotfix são muito parecidos com branch release em que eles também são destinadas a preparar-se para uma nova versão de produção, embora não planejada. Eles surgem da necessidade de agir imediatamente após um estado indesejado de uma versão de produção ao vivo. Quando um bug crítico em uma versão de produção deve ser resolvido imediatamente, um ramo correcção poderá ser ramificou-se a partir da tag correspondente no branch master que marca a versão de produção.

A essência é que o trabalho dos membros da equipe (no develop ramo) pode continuar, enquanto outra pessoa está a preparar uma correção de produção rápida.

### Criando o branch hotfix

Os branches hotfix são criados a partir do branch master. Por exemplo, digamos que a versão 1.2 é a versão de produção atual em execução ao vivo e causando problemas devido a um erro grave. Mas as mudanças em dev ainda instável. Podemos, então, ramificar um branch hotfix e começar a corrigir o problema: 

	$ git checkout -b hotfix-1.2.1 master
	Mudou para um novo ramo "hotfix-1.2.1"
	$ ./bump-version.sh 1.2.1
	Arquivos modificados com sucesso, versão 1.2.1 batido.
	$ git commit -a -m "Bumped número de versão para 1.2.1"
	[hotfix-1.2.1 41e61bb] número da versão 1.2.1 para Batido
	1 arquivos alterados, 1 inserções (+), 1 deleções (-)

Não se esqueça de bater o número de versão depois ramificando-se!

Em seguida, corrigir o erro e se comprometer a correção em um ou mais submissões separadas. 

	$ git commit -m "Corrigido o problema de produção grave"
	[hotfix-1.2.1 abbe5d6] problema de produção fixo grave
	5 arquivos mudou, 32 inserções (+), 17 exclusões (-)


### Terminar um branch hotfix

Quando terminar, o bugfix precisa ser mescladas de volta para master mas também precisa ser mescladas de volta para dev a fim de salvaguardar que o bugfix está incluído na próxima versão também. Isto é completamente semelhante à forma como branches releases estão acabados.

Primeiro, atualizar master e marcar o lançamento. 

	$ git checkout master
	Comutado para ramificar 'master'
	$ git merge --no-ff hotfix-1.2.1
	Fusão tomada pelos recursiva.
	(Resumo das alterações)
	$ git tag -a 1.2.1

Edit: Você pode muito bem querer usar as -s ou -u <key> bandeiras para assinar seu tag cryptographically.

Em seguida, incluir a correção de bugs em dev também: 

	$ git checkout develop
	Comutado para ramo "desenvolver"
	$ git merge --no-ff hotfix-1.2.1
	Fusão tomada pelos recursiva.
	(Resumo das alterações)

A única exceção à regra aqui é que, quando um branch release existe atualmente, as mudanças de hotfix precisam ser fundidos em que branch release, em vez de dev. Back-fusão da correção no branch release acabará por resultar na bugfix sendo fundidos em dev também, quando o branch release está terminado. (Se o trabalho em dev imediatamente requer esta bugfix e não pode esperar para o branch release para ser concluída, você pode, seguramente, mesclar o bugfix em develop agora já bem.)

Por fim, remova o ramo temporário: 

	$ git branch -d hotfix-1.2.1
	Excluída ramo hotfix-1.2.1 (foi abbe5d6).