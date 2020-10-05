# Padronização de Commits utilizando Git Conventional Commits, Husky, lint-staged, standard JS.
----

## Como funciona?
Em suma, utilizaremos o Husky, lint-staged e standard para criar um script que será executado antes da realização de um commit, este script verificará o formato do código que está para ser "comitado". O formato do código seguirá o standard JS,


Além disso, utilizaremos o padrão de commit conhecido como Conventional Commits. Para isso, utilizaremos o módulo Git Conventional Commits, que verificará se algum dos commits fogem do padrão Conventional Commits.

## Antes de Começar

- Husky: é um módulo que permite a configuraçãp de hooks no github, no caso deste tutorial utilizaremos o pre-commit. O pre-commit é um script que será executado antes de executar um commit;

- lint-staged: é um módulo que permite configurar um script, geralmente de linting, para os arquivos que estão na staging-area. Assim, executará scripts somente nos arquivos que estão para ser commitados, eliminando o inconveniente de sempre verificar o projeto inteiro a cada commit.

- standard JS: é o nosso style guide. O lint-staged será configurado para chamar o módulo standard. Assim, qualquer arquivo que foge do padrão standard JS fará com que o commit não prossiga.

- Conventional Commits: Padrão de commits bastante utilizado que se baseia em cima do Angular Commit Guidelines.

## Setup  Husky, lint-staged, standard

#### Instalando Dependências

```
npm i standard -D
npm i lint-staged -D
npm i husky -D
```

#### Configurando o lint-staged com o standard JS

```
"lint-staged": {
    "*.js": [
      "standard --fix",
      "git add"
    ]
  },
```
Então, temos:

- *.js: configurando somente para executar em arquivos ".js";

- standard: executa o script standard caso algum arquivo esteja fora do padrão o commit não será executado

- --fix: Pede para o script standard concertar automaticamente arquivos que estejam fora do padrão do standard JS. Caso o script não consiga colocar o arquivo no padrão, então o commit não passará e será retornado uma menssagem de erro.

- git add: Se algum arquivo for concertado pelo comando standard --fix, então este será adicionado ao commit.


#### Configurando o Husjy com o lint-staged

```
 "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
```

Então temos:

- hooks: scripts que podem ser executados antes ou depois de algum commando importante do git;
- pre-commit: um dos hooks possíveis, executa scripts antes de executar o commando commit.


#### Exemplo de configuração do package.json
```
{
  "name": "padronizacao-commits-conventional",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "lint-staged": {
    "*.js": [
      "standard --fix",
      "git add"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "git-commit-msg-linter": "^3.0.0",
    "husky": "^4.3.0",
    "lint-staged": "^10.4.0",
    "standard": "^14.3.4"
  }
}
```

## Setup Conventional Commits

#### Instalando Dependências
```
npm i git-commit-msg-linter -D
```
#### Configurando

É possível configurar o git-commit-msg-linter como quiser, embora não seja necessário. Para isso, é necessário criar um arquivo com o nome commitlinterrc.json no root do projeto.

commitlinterrc.json
```
{
  "types": {
    "fix": false,
    "deps": "Novo tipo"
  },
  "max-len": 80,
  "debug": true
}
```

É possível criar novos tipos e também mudar a descrição de tipos já existentes. Além disso, é possível desabilitar alguns tipos.


#### Formato

De forma simplicada, podemos utilizar o seguinte formato:

```
<type>: <description>
```

Onde:

- type: é uma tag que especifica a natureza de seu commit: Algumas das tags utilizadas são: ```fix:```, ```feat```. ```build:```, ```chore:```, ```ci:```, ```docs:```, ```style:```, ```refactor:```, ```perf:```, ```test:```. Para entender seu uso e significados recomendo olhar as seguintes referências:
 [Conventional Commits Guideline](https://www.conventionalcommits.org/pt-br/v1.0.0-beta.4/), [Guia de GitWorkflow por ventq](
 https://gist.github.com/vtenq/7a93687108cb876f884c3ce75a8a8023);

 - description: a descrição do seu commit.

## Referências

- [Conventional Commits Guideline](https://www.conventionalcommits.org/pt-br/v1.0.0-beta.4/),
- [Guia de GitWorkflow por ventq](
 https://gist.github.com/vtenq/7a93687108cb876f884c3ce75a8a8023);
- [Husky - Github](https://github.com/typicode/husky#readme)
- [lint-staged - Github](https://github.com/okonet/lint-staged)
- [git-commit-msg-linter](https://github.com/legend80s/commit-msg-linter)
- [Git Hooks - Documentação do Git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
- [Tutorial de Git Hooks pela Hostinger](https://www.hostinger.com.br/tutoriais/como-usar-git-hooks/)
- [Gitflow Workflow - Atlassian](https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow)


## Agredecimentos Especiais

 Meus agradecimentos especiais vão para [Rmanguinho](https://github.com/rmanguinho), seu cursos gratuitos de [NodeJs, TDD e Clean Architecture](https://www.youtube.com/watch?v=vV1wQ6GFH0A&list=PL9aKtVrF05DyEwK5kdvzrYXFdpZfj1dsG) e [Dominando o Git](https://www.youtube.com/watch?v=oj1EAWwiojM&list=PL9aKtVrF05DzbNiE7jcm7s6z6Lg-u72Rq) ajudaram bastante. Para este tutorial, usei de referência especificamente as seguintes aulas:

 - [#1 API em NodeJS com Clean Architecture e TDD - Project Setup](https://youtu.be/zCZG9sNec98)
 - [#3 Git - Conventional Commits, Log e Tag](https://youtu.be/vV1wQ6GFH0A)




