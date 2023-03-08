<h1 align ='center'>MEU CONDOMINIO</h1>

Essa é uma aplicação MEU CONDOMINIO com objetivo de facilitar a comunicação dentro do seu condominio. 

## Endpoints
A API possue endpoints para cadastrar seu usuario (moradar e sindico), realizar login, cadastrar condominio, realizar postagens das informações para os moradores e informações sobre melhorias e caixa do condominio.

<a href="https://insomnia.rest/run/?label=API%20MEU%20CONDOMINIO&uri=https%3A%2F%2Fgithub.com%2FProjeto-Frontend-T15%2FAPI-FAKE%2Fblob%2Fmain%2FInsomnia_meucondominio.json" target="_blank"><img src="https://insomnia.rest/images/run.svg" alt="Run in Insomnia"></a>

<blockquote> Para importar o JSON no Insomnia é só clicar no botão "Run in Insomnia". Depois é só seguir os passos que ele irá importar todos os endpoints em seu insomnia.
</blockquote>
<br>

A url base da API é https://api-meucondominio.onrender.com/

<h2 align ='center'>Criação de usuário</h2>
POST /register - FORMATO DA REQUISIÇÃO
<br>
USER - MORADOR

```json
{
        "is_admin": "false",
        "name": "ana",
        "email": "ana@mail.com",
        "password": "123456",
        "condId": 1
}
```


Caso dê tudo certo, a resposta será assim:
POST /register - FORMATO DA RESPOSTA - STATUS 201
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFuYUBtYWlsLmNvbSIsImlhdCI6MTY3ODE5NDg1MSwiZXhwIjoxNjc4MTk4NDUxLCJzdWIiOiIyIn0.o3-0RxCkaVzCd9xj_mW7Lo1gy9MLwNFzo7ZhLcpR71E",
	"user": {
		"email": "ana@mail.com",
		"is_admin": "false",
		"name": "ana",
		"condId": 1,
		"id": 2
	}
}
```
<br>

USER - SINDICO
```json
    {
        "is_admin": "true",
        "name": "sindico",
        "email": "sindico@mail.com",
        "password": "123456"
    }
```

Caso dê tudo certo, a resposta será assim:
POST /register - FORMATO DA RESPOSTA - STATUS 201
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InNpbmRpY29AbWFpbC5jb20iLCJpYXQiOjE2NzgxOTQ4MjIsImV4cCI6MTY3ODE5ODQyMiwic3ViIjoiMSJ9.EOwGfJkqkjFqEhT2odC5BhjJlQBJfdilBEe8QOoSfT8",
	"user": {
		"email": "sindico@mail.com",
		"is_admin": "true",
		"name": "sindico",
		"id": 1
	}
}
```
<h2 align ='center'>Possíveis erros</h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

Email já cadastrado:
<br>
POST /users -   FORMATO DA RESPOSTA - STATUS 400
<br>
"Email already exists"


Não preencher campos de email e senha:
<br>
POST /users -   FORMATO DA RESPOSTA - STATUS 400
<br>
"Email and password are required"

<h2 align ='center'>Login</h2>

POST /login - FORMATO DA REQUISIÇÃO
```json
{
	"email": "sindico@mail.com",
	"password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

POST /login - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InNpbmRpY29AbWFpbC5jb20iLCJpYXQiOjE2NzgxOTkwMTUsImV4cCI6MTY3ODIwMjYxNSwic3ViIjoiMSJ9.8bJrf4fGgkVn4ylh3ryBLgyE11WjS-CG5ESvBTHc_yk",
	"user": {
		"email": "sindico@mail.com",
		"is_admin": "true",
		"name": "sindico",
		"id": 1
	}
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token no localStorage para fazer a gestão do usuário no seu frontend.

<h2>Rotas que não necessitam de autorização</h2>

GET /conds - FORMATO DA REQUISIÇÃO
<br>
Rota do tipo GET para buscar condominios cadastrados 
<br>
##
Caso dê tudo certo, a resposta será assim:

GET  /conds - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"name": "Condominio Kenzie",
		"userId": 1,
		"id": 1
	},
	{
		"name": "Condominio Baden",
		"userId": 1,
		"id": 2
	}
]
```
<h2>Rotas que necessitam de autorização</h2>
<h3 align ='center'>SINDICO</h3>

<h2>CRIAR CONDOMINIO</h2>

POST /conds - FORMATO DA REQUISIÇÃO
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o condominio.
```json
{
	"name": "Condominio Kenzie",
	"userId": 1
}
```

Caso dê tudo certo, a resposta será assim:

POST /messages - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"name": "Condominio Kenzie",
	"userId": 1,
	"id": 1
}
```

<h2>RECADOS</h2>
<h3 align ='center'>CRIAR RECADO</h3>

POST /messages - FORMATO DA REQUISIÇÃO
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o recado e o id do con dominio.
```json
{
	"userId": 1,
	"condId": 1,
	"title": "Informação sobre limpeza caixa d'água ",
	"descripiton": "Informo a todos os moradores que ocorrerá manutenção das caixas d'água do condominio e pode ocorrer falta de água em seu apartamento no dia 08-03 das 10h as 12h. Agradeço compreensão de todos"
}
```

Caso dê tudo certo, a resposta será assim:

POST /messages/ID - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"userId": 1,
	"condId": 1,
	"title": "Informação sobre limpeza caixa d'água ",
	"descripiton": "Informo a todos os moradores que ocorrerá manutenção das caixas d'água do condominio e pode ocorrer falta de água em seu apartamento no dia 08-03 das 10h as 12h. Agradeço compreensão de todos",
	"id": 1
}
```

<h3 align ='center'>EDITAR RECADO</h3>

PUT /messages/ID - FORMATO DA REQUISIÇÃO
<br>
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o recado e o id do con dominio.
```json
{
	"userId": 1,
  	"condId": 1,
	"title": "Info limpeza caixas d'água",
	"descripiton": "Informo a todos os moradores que ocorrerá manutenção das caixas d'água do condominio e pode ocorrer falta de água em seu apartamento no dia 20-03 das 10h as 12h. Agradeço compreensão de todos"
}
```

Caso dê tudo certo, a resposta será assim:

PUT /messages/ID - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"userId": 1,
	"condId": 1,
	"title": "Info limpeza caixas d'água",
	"descripiton": "Informo a todos os moradores que ocorrerá manutenção das caixas d'água do condominio e pode ocorrer falta de água em seu apartamento no dia 20-03 das 10h as 12h. Agradeço compreensão de todos",
	"id": 1
}
```

<h3 align ='center'>DELETAR RECADO</h3>
DELETE /messages/ID - FORMATO DA REQUISIÇÃO
<br>
Não tem corpo da requisição
<br>
Caso dê tudo certo, a resposta será assim:

DELETE /messages/ID - FORMATO DA RESPOSTA - STATUS 200
<br>
{}

<h2>CAIXA CONDOMINIO</h2>
POST /cachs - FORMATO DA REQUISIÇÃO
<br>
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o recado e o id do con dominio

```json
{
	"userId": 1,
	"cond_id": 1,
	"title": "Pagamento taxa condominio",
	"price": 1200,
	"type" : "Entrada"
}
```

Caso dê tudo certo, a resposta será assim:

POST /cachs - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"userId": 1,
	"cond_id": 1,
	"title": "Pagamento taxa condominio",
	"price": 1200,
	"type": "Entrada",
	"id": 1
}
```

<h2>MANUTENÇÃO CONDOMINIO</h2>

POST /maintenance - FORMATO DA REQUISIÇÃO
<br>
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o recado e o id do con dominio.
```json
{
	"userId": 1,
	"cond_id": 1,
	"name": "Fred",
	"service": "Eletricista",
	"contact": "99 99999-9999"
}
```

Caso dê tudo certo, a resposta será assim:

POST /maintenance - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"userId": 1,
	"cond_id": 1,
	"name": "Fred",
	"service": "Eletricista",
	"contact": "99 99999-9999",
	"id": 1
}
```

<h2>MELHORIAS CONDOMINIO</h2>
POST /improvements - FORMATO DA REQUISIÇÃO
<br>
No corpo da requisição é obrigatório encaminhar o id do sindico que esta criando o recado e o id do con dominio

```json
{
	"userId": 1,
	"condId": 1,
	"title": "Portão Eletrico",
	"description": "Foi realizada uma implantação do portão automatico para uma maior segurança dos moradores"
}
```

Caso dê tudo certo, a resposta será assim:

POST /improvements - FORMATO DA RESPOSTA - STATUS 200
```json
{
	"userId": 1,
	"condId": 1,
	"title": "Portão Eletrico",
	"description": "Foi realizada uma implantação do portão automatico para uma maior segurança dos moradores",
	"id": 1
}
```

<h2>COMENTÁRIOS DE CADA RECADO</h2>
<p>Realizar a busca dos comentários de cada morador sobre cada recado</p>
GET /comments?messageId=1 - FORMATO DA REQUISIÇÃO
<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /comments?messageId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"userId": 2,
		"messageId": 1,
		"comment": "Qual horario será realizado?",
		"id": 1
	}
]
```



<h2>MORADORES CONDOMINIO</h2>
<p>Buscar por todos os moradores do condominio</p>
GET /users?condId=1 - FORMATO DA REQUISIÇÃO

<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /users?condId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"email": "ana@mail.com",
		"password": "$2a$10$wY8bjsHMf/hlWZVfuyGqpO6pPIQA8YPNNGsJQFM0GuB3CJ0AOPKlu",
		"is_admin": "false",
		"name": "ana",
		"condId": 1,
		"id": 1
	}
]
```

<h3 align ='center'>MORADORES</h3>
O morador poderar realizar a leitura dos recados e realizar comentários em cada recado, leitua manutenção, leitura melhorias e leitura do fluxo de caixa.


<h2>ADICIONAR COMENTÁRIO NO RECADO</h2>
POST /comments - FORMATO DA REQUISIÇÃO

<br>
No corpo da requisição é obrigatório encaminhar o id do morador que esta criando o recado e o id do recado.
<br>

```json
{
	"userId": 2,
	"messageId" : 1,
	"comment": "Essa manutenção deveria ocorrer durante a semana em horarios que a maioria dos moradores estaria trabalhando!"
}
```

Caso dê tudo certo, a resposta será assim:

GET /messages?condId=1 - FORMATO DA RESPOSTA - STATUS 200

```json
{
	"userId": 2,
	"messageId": 1,
	"comment": "Essa manutenção deveria ocorrer durante a semana em horarios que a maioria dos moradores estaria trabalhando!",
	"id": 1
}
```


<h2>LEITURA RECADOS</h2>
GET /messages?condId=1 - FORMATO DA REQUISIÇÃO

<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /messages?condId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"userId": 1,
		"condId": 1,
		"title": "Informação sobre limpeza caixa d'água ",
		"descripiton": "Informo a todos os moradores que ocorrerá manutenção das caixas d'água do condominio e pode ocorrer falta de água em seu apartamento no dia 08-03 das 10h as 12h. Agradeço compreensão de todos",
		"id": 1
	}
]
```
<h2>LEITURA MANUTENÇÃO</h2>
GET /maintenance?condId=1 - FORMATO DA REQUISIÇÃO

<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /maintenance?condId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"userId": 1,
		"cond_id": 1,
		"name": "Fred",
		"service": "Eletricista",
		"contact": "99 99999-9999",
		"id": 1
	}
]
```
<h2>LEITURA MELHORIAS</h2>
GET /improvements?condId=1 - FORMATO DA REQUISIÇÃO

<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /improvements?condId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"userId": 1,
		"condId": 1,
		"title": "Portão Eletrico",
		"description": "Foi realizada uma implantação do portão automatico para uma maior segurança dos moradores",
		"id": 1
	}
]
```
<h2>LEITURA CAIXA</h2>
GET /cashs?condId=1 - FORMATO DA REQUISIÇÃO

<br>
Não tem corpo da requisição.
<br>
Caso dê tudo certo, a resposta será assim:

GET /cashs?condId=1 - FORMATO DA RESPOSTA - STATUS 200
```json
[
	{
		"userId": 1,
		"cond_id": 1,
		"title": "Pagamento taxa condominio",
		"price": 1200,
		"type": "Entrada",
		"id": 1
	}
]
```
