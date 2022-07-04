# Desafio 01 - Database Queries

Este desafio faz parte da lista de desafios que compõem o curso de NodeJS.

Visite à [Rockseat](https://rocketseat.com.br/) para saber mais sobre o curso.

<p align="center">
  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/code36u4r60/ignite-desafio-conceitos-do-nodejs?style=flat">

  <a href="https://rocketseat.com.br">
    <img alt="Made by Eduardo Queirós" src="https://img.shields.io/badge/made%20by-Eduardo%20Queirós-red">
  </a>

  <img alt="License" src="https://img.shields.io/badge/license-MIT-%2304D361">
  
</p>

<p align="center">
  <a href="#rocket-sobre-o-desafio">Sobre o desafio</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#keyboard-instalação-e-execução-do-projeto">Instalação e Execução do Projeto</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#template-da-aplicação">Template da aplicação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#instruções">Instruções</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-licença">Licença</a>
</p>

## :rocket: Sobre o desafio

Nesse desafio, foram realizadas consultas no banco de dados com o TypeORM de três maneiras:

- Usando o ORM
- Usando Query Builder
- Usando Raw Query

No template, você irá encontrar uma aplicação já estruturada (apenas as entidades e repositórios) onde você deverá completar o que falta nas consultas dos dois repositórios.

A aplicação possui dois módulos: `users` e `games`. Um **usuário** pode ter vários jogos e um mesmo **jogo** pode estar associado a vários usuários.

### :keyboard: Instalação e Execução do Projeto

- Clone o repositório

```
https://github.com/code36u4r60/ignite-desafio-database-queries.git
```

ou

```
git@github.com:code36u4r60/ignite-desafio-database-queries.git
```

ou

```
gh repo clone code36u4r60/ignite-desafio-database-queries
```

- Entrar na pasta do projeto

```
cd ignite-desafio-componentizando-a-aplicacao
```

- Instale as dependências com o Yarn

```
yarn
```

- Crie uma database no banco Postgres com o nome `queries_challenge`. <br>
  Ou, substitua os dados de autenticação (caso os seus não sejam os mesmos) no arquivo `ormconfig.json`

- Executar as `migrations`

```
yarn typeorm migration:run
```

- Para executar os testes

```
yarn test
```

### Template da aplicação

Foi utilizado um modelo de template que possui o esqueleto do projeto.

O template está disponível na seguinte URL:

[rocketseat-education/ignite-template-database-queries](https://github.com/rocketseat-education/ignite-template-database-queries)

**Dica**: Caso não saiba utilizar repositórios do GitHub como template, temos um guia em **[nosso FAQ](https://www.notion.so/FAQ-Desafios-ddd8fcdf2339436a816a0d9e45767664).**

## Instruções

## Repositórios da aplicação

Com o repositório criado a partir do template e clonado na sua máquina, navegue até os arquivos **src/modules/users/repositories/implementations/UsersRepository.ts** e **src/modules/games/repositories/implementations/GamesRepository.ts**.
Esses deverão ser completados para que os testes sejam satisfeitos.

### UsersRepository

- Método **findUserWithGamesById**

  Esse método deve receber o **Id** de um usuário e retornar os dados do usuário encontrado juntamente com os dados de todos os **games** que esse usuário possui.

  Exemplo de retorno:

  ```jsx
  {
  	id: '81482ac4-29bd-497f-b71a-8ae3b20eca9b',
  	first_name: 'John',
  	last_name: 'Doe',
  	email: 'mail@example.com',
  	created_at: '2021-03-19 19:35:09.877037',
  	updated_at: '2021-03-19 19:35:09.877037',
  	games: [
  		{
  			id: '63a6c35a-ac97-4773-9021-fb93973c8139',
  			title: 'GTA V',
  			created_at: '2021-03-19 19:35:09.877037',
  			updated_at: '2021-03-19 19:35:09.877037',
  		},
  		{
  			id: '74e4fc3b-434d-4452-94eb-27a85dce8d1a',
  			title: 'Among Us',
  			created_at: '2021-03-19 19:35:09.877037',
  			updated_at: '2021-03-19 19:35:09.877037',
  		}
  	]
  }
  ```

- Método **findAllUsersOrderedByFirstName**

  Esse método deve retornar a listagem de usuários cadastrados em ordem alfabética (**ASC**).

  Lembre-se que aqui deve ser usado **raw query** para a consulta.

- Método **findUserByFullName**

  Esse método deve receber `first_name` e `last_name` e retornar um usuário que possua os mesmos `first_name` e `last_name`. Aqui você deve encontrar o usuário ignorando se o argumento passado está em caixa alta ou não.

  Por exemplo, suponhamos que existe um usuário onde o `first_name` é `Danilo` e o `last_name` é `Vieira`. O método deve retornar o usuário mesmo que os argumentos passados sejam `daNiLo` para `first_name` e `vIeiRA` para `last_name`. Essa consulta deve ser realizada utilizando **raw query** e você pode buscar pelo uso do **LOWER** no Postgres para resolver esse problema.

### GamesRepository

- Método **findByTitleContaining**

  Esse método deve receber parte do título de um jogo ou o título inteiro e retornar um ou mais jogos que derem match com a consulta.

  Se o método for chamado com o argumento `"or S"` e existir algum jogo com essa sequência de letras no título, o retorno deve ser feito, como por exemplo o seguinte retorno:

  ```jsx
  [
    {
      id: "63a6c35a-ac97-4773-9021-fb93973c8139",
      title: "Need F**or S**peed: Payback",
      created_at: "2021-03-19 19:35:09.877037",
      updated_at: "2021-03-19 19:35:09.877037",
    },
    {
      id: "74e4fc3b-434d-4452-94eb-27a85dce8d1a",
      title: "Need F**or S**peed: Underground",
      created_at: "2021-03-19 19:35:09.877037",
      updated_at: "2021-03-19 19:35:09.877037",
    },
  ];
  ```

  A consulta também deve ser feita de forma case insensitive, ignorando caixa alta onde no banco não existe. Para exemplo, considerando a busca exemplificada acima, o retorno deve ser o mesmo caso o parâmetro passado seja uma string `"nEEd"`.

  Você pode buscar pelo uso do **ILIKE** no Postgres para resolver esse problema. Lembre-se que aqui deve ser usado **query builder** para realizar a consulta.

- Método **countAllGames**

  Esse método deve retornar uma contagem do total de games existentes no banco. Deve ser usada **raw query** para essa consulta.

- Método **findUsersByGameId**

  Esse método deve receber o `Id` de um game e retornar uma lista de todos os usuários que possuem o game do `Id` informado.

  Exemplo de retorno:

  ```jsx
  [
    {
      id: "81482ac4-29bd-497f-b71a-8ae3b20eca9b",
      first_name: "John",
      last_name: "Doe",
      email: "mail@example.com",
      created_at: "2021-03-19 19:35:09.877037",
      updated_at: "2021-03-19 19:35:09.877037",
    },
    {
      id: "75920ac4-32ed-497f-b71a-8ae3c19eca9b",
      first_name: "Usuário",
      last_name: "Qualquer",
      email: "usuarioqualquer@example.com",
      created_at: "2021-03-19 19:35:09.877037",
      updated_at: "2021-03-19 19:35:09.877037",
    },
  ];
  ```

### Específicação dos testes

Para esse desafio, temos os seguintes testes:

- **[UsersRepository] should be able to find user with games list by user's ID**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no método `findByTitleContaining`.

- **[UsersRepository] should be able to list users ordered by first name**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é no método `findAllUsersOrderedByFirstName`. 

- **[UsersRepository] should be able to find user by full name**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é no método `findUserByFullName`. 

- **[GamesRepository] should be able find a game by entire or partial given title**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é no método `findByTitleContaining`.

- **[GamesRepository] should be able to get the total count of games**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é no método `countAllGames`.

- **[GamesRepository] should be able to list users who have given game id**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é no método `findUsersByGameId`.
  

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](https://github.com/git/git-scm.com/blob/master/MIT-LICENSE.txt) para mais detalhes.

---

Created with 💜 by <a href="https://www.linkedin.com/in/eduardoqueiros/">Eduardo Queirós</a> :wave: