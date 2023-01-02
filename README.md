# EazyHome API

Esta é a API da EazyHome. O objetivo da aplicação é conectar clientes e prestadores de serviço domiciliares, de modo a agilizar a procura de prestadores especializados.

## Endpoints

A API tem 3 Endpoints, podendo cadastrar usuários, realizar login, e acessar o perfil do usuário, seja ele cliente ou prestador.

### Cadastro

POST /register - FORMATO DA REQUISIÇÃO

{
"email": "exemplo@mail.com",
"password": "exemplo",
"name": "Exemplo",
"age": 18,
"type": "cliente",
"activeServices": [],
"doneServices": []
}

A chave "type" será preenchida de acordo com o formulário de registro utilizado na página (cliente ou prestador), enquanto as chaves "activeServices" e "doneServices" devem ser sempre inicializadas como arrays vazios.

RESPOSTA DA API - STATUS 201

{
"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZlbGlwcGVAbWFpbC5jb20iLCJpYXQiOjE2NzI2OTc3MjAsImV4cCI6MTY3MjcwMTMyMCwic3ViIjoiMiJ9.9oQnDT5eN4Ib5rHqxz0BCbMRHYCYyc3euvuI28lb0WQ",
"user": {
"email": "exemplo@mail.com",
"name": "Exemplo",
"age": 18,
"type": "cliente",
"activeServices": [],
"doneServices": [],
"id": 1
}
}

ERRO - STATUS 400 - E-MAIL JÁ CADASTRADO

"Email already exists"

### Login

POST /login - FORMATO DA REQUISIÇÃO

{
"email": "exemplo@mail.com",
"password": "exemplo"
}

RESPOSTA DA API - STATUS 200

{
"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZlbGlwcGVAbWFpbC5jb20iLCJpYXQiOjE2NzI2OTc3MjAsImV4cCI6MTY3MjcwMTMyMCwic3ViIjoiMiJ9.9oQnDT5eN4Ib5rHqxz0BCbMRHYCYyc3euvuI28lb0WQ",
"user": {
"email": "exemplo@mail.com",
"name": "Exemplo",
"age": 18,
"type": "cliente",
"activeServices": [],
"doneServices": [],
"id": 1
}
}

ERRO - STATUS 400 - SENHA INCORRETA

"Incorrect Password"

ERRO - STATUS 400 - USUÁRIO NÃO CADASTRADO

"Cannot find user"

### Profile

GET /users/"id do usuário" - SEM CORPO DE REQUISIÇÃO - NECESSÁRIA AUTENTICAÇÃO

RESPOSTA DA API - STATUS 200

{
"email": "exemplo@mail.com",
"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
"name": "Exemplo",
"age": 18,
"id": 1,
"type": "cliente",
"activeServices": [],
"doneServices": []
}

ERRO - STATUS 401 - SEM TOKEN DE ACESSO

"Missing Token"
