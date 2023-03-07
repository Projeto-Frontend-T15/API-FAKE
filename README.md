<h1 align ='center'>MEU CONDOMINIO</h1>

Essa é uma aplicação MEU CONDOMINIO com objetivo de facilitar a comunicação dentro do seu condominio. 

## Endpoints
A API possue endpoints para cadastrar seu usuario (moradar e sindico), realizar login, cadastrar condominio, realizar postagens das informações para os moradores e informações sobre melhorias e caixa do condominio.

<a href="https://insomnia.rest/run/?label=MEU%20CONDOMINIO&uri=https%3A%2F%2Fgithub.com%2FProjeto-Frontend-T15%2FAPI-FAKE%2Fblob%2Fmain%2FInsomnia_meucondominio.json" target="_blank"><img src="https://insomnia.rest/images/run.svg" alt="Run in Insomnia"></a>

<blockquote> Para importar o JSON no Insomnia é só clicar no botão "Run in Insomnia". Depois é só seguir os passos que ele irá importar todos os endpoints em seu insomnia.
</blockquote>
<br>
<h2 align ='center'>Criação de usuário</h2>
POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.


### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"
