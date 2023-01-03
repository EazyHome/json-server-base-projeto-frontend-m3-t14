# EazyHome API

Esta é a API da EazyHome. O objetivo da aplicação é conectar clientes e prestadores de serviço domiciliares, de modo a agilizar a procura de prestadores especializados.

## Endpoints

A API tem 3 Endpoints, podendo cadastrar usuários, realizar login, e acessar o perfil do usuário, seja ele cliente ou prestador.

### Cadastro

POST /register - FORMATO DA REQUISIÇÃO

<pre>

{
    "email": "exemplo@mail.com",
    "password": "exemplo",
    "name": "Exemplo",
    "age": 18,
    "type": "cliente"
}
</pre>

A chave "type" será preenchida de acordo com o formulário de registro utilizado na página (cliente ou prestador).

RESPOSTA DA API - STATUS 201

<pre>

{
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZlbGlwcGVAbWFpbC5jb20iLCJpYXQiOjE2NzI2OTc3MjAsImV4cCI6MTY3MjcwMTMyMCwic3ViIjoiMiJ9. 9oQnDT5eN4Ib5rHqxz0BCbMRHYCYyc3euvuI28lb0WQ",
    "user": {
        "email": "exemplo@mail.com",
        "name": "Exemplo",
        "age": 18,
        "type": "cliente",
        "id": 1
    }
}
</pre>

ERRO - STATUS 400 - E-MAIL JÁ CADASTRADO

<pre>
"Email already exists"
</pre>

### Login

POST /login - FORMATO DA REQUISIÇÃO

<pre>
{
    "email": "exemplo@mail.com",
    "password": "exemplo"
}
</pre>

RESPOSTA DA API - STATUS 200

<pre>
{
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZlbGlwcGVAbWFpbC5jb20iLCJpYXQiOjE2NzI2OTc3MjAsImV4cCI6MTY3MjcwMTMyMCwic3ViIjoiMiJ9.9oQnDT5eN4Ib5rHqxz0BCbMRHYCYyc3euvuI28lb0WQ",
    "user": {
        "email": "exemplo@mail.com",
        "name": "Exemplo",
        "age": 18,
        "type": "cliente",
        "id": 1
    }
}
</pre>

ERRO - STATUS 400 - SENHA INCORRETA

<pre>
"Incorrect Password"
</pre>

ERRO - STATUS 400 - USUÁRIO NÃO CADASTRADO

<pre>
"Cannot find user"
</pre>

### Profile

GET /users/"id do usuário" - SEM CORPO DE REQUISIÇÃO - NECESSÁRIA AUTENTICAÇÃO

RESPOSTA DA API - STATUS 200

<pre>
{
    "email": "exemplo@mail.com",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "name": "Exemplo",
    "age": 18,
    "id": 1,
    "type": "cliente"
}
</pre>

ERRO - STATUS 401 - SEM TOKEN DE ACESSO

<pre>
"Missing token"
</pre>

### Serviços Finalizados

GET /doneServices - SEM CORPO DE REQUISIÇÃO - NECESSÁRIA AUTENTICAÇÃO

RESPOSTA DA API - STATUS 200

<pre>
[
	{
		"id": 1,
		"name": "Troca de caixa de fusíveis",
		"type": "Elétrica",
		"description": "Substituição da caixa e fiação dos fusíveis da casa",
		"userId": 1,
		"providerId": 2
	}
]
</pre>

ERRO - STATUS 401 - SEM TOKEN DE ACESSO

<pre>
"Missing token"
</pre>

### Serviços Ativos

GET /activeServices - SEM CORPO DE REQUISIÇÃO - NECESSÁRIA AUTENTICAÇÃO

RESPOSTA DA API - STATUS 200

<pre>
[
	{
		"id": 2,
		"name": "Conserto de Telhado",
		"type": "Estrutural",
		"description": "Substituição de telhas quebradas",
		"userId": 1,
		"providerId": 2
	}
]
</pre>

ERRO - STATUS 401 - SEM TOKEN DE ACESSO

<pre>
"Missing token"
</pre>
