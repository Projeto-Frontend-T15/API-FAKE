# MEU CONDOMINIO

Essa é uma aplicação MEU CONDOMINIO com objetivo de cadastrar moradores e sindicos dos condominios para facilitar a comunicação dentro do condominio. 

## Endpoints
A API possue endpoints para cadastrar seu usuario (moradar e sindico), realizar login, cadastrar condominio, realizar postagens das informações para os moradores e informações sobre melhorias e caixa do condominio.


### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.


### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"
