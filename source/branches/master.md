# Master

Ao criar um novo repositório é necessário um primeiro commit para que seja criado a branch principal `master`. Podemos fazer isso diretamente no serviço de controle de versão ou localmente na nossa máquina: 

``` 
$ mkdir project-name
$ cd project-name
$ git init
$ git remote add origin https://github.com/[username]/[project-name].git
```

- Cria a pasta do projeto
- Entra na pasta
- Inicia um repositório local
- Adiciona a origrm remota

ou 

``` 
$ git clone https://github.com/[username]/[project-name].git
$ cd project-name
``` 

- Clona o projeto
- Entra na pasta


Depois, criamos um arquivo no projeto, adicionamos e depois fazemos o `commit`. 

Por intermédio da `flag` ***-u***(Upstream), na hora de fazer o `push`, será associada a branch com a branch `master` remota e gravar no seu .git/config, caso isso ainda não tenha sido feito.

```
$ git add README.md
$ git commit -m "first commit"
$ git push -u origin master
```


[&#65513; Principais](https://github.com/doc-solutions/documentation-gitflow/blob/master/source/branches/main.md)

[&#65513; Readme](https://github.com/doc-solutions/documentation-gitflow/blob/master/README.md)