<h1 align ='center'>MEU CONDOMINIO</h1>

Essa é uma aplicação MEU CONDOMINIO com objetivo de facilitar a comunicação dentro do seu condominio. 

## Endpoints
A API possue endpoints para cadastrar seu usuario (moradar e sindico), realizar login, cadastrar condominio, realizar postagens das informações para os moradores e informações sobre melhorias e caixa do condominio.

<a href="https://insomnia.rest/run/?label=MEU%20CONDOMINIO&uri=https%3A%2F%2Fgithub.com%2FProjeto-Frontend-T15%2FAPI-FAKE%2Fblob%2Fmain%2FInsomnia_meucondominio.json" target="_blank"><img src="https://insomnia.rest/images/run.svg" alt="Run in Insomnia"></a>

<blockquote> Para importar o JSON no Insomnia é só clicar no botão "Run in Insomnia". Depois é só seguir os passos que ele irá importar todos os endpoints em seu insomnia.
</blockquote>
<br>

A url base da API é https://api-fake-meusindico.onrender.com/

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