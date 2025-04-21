# Checkpoint 5 DOMAIN DRIVEN DESIGN USING JAVA 
Aluno: Gabriel Gomes Cardoso  
RM:559597
### 1. Introdução
O objetivo dessa atividade é criar uma documentação de uma api de cartas de Magic The Gathering (MTG). Simulando suas rotas e seus retornos

### 2. Rotas da API 
| Método | Rota                          | Descrição                                           | Status Codes         |
|--------|-------------------------------|----------------------------------------------------|----------------------|
| GET    | /decks                        | Listar todos os decks                              | 200, 500             |
| GET    | /decks/{id}                   | Buscar deck por ID                                 | 200, 404, 500        |
| POST   | /decks                        | Criar novo deck                                    | 201, 400, 500        |
| PUT    | /decks/{id}                   | Atualizar deck existente                           | 200, 400, 404, 500   |
| PATCH  | /decks/{id}/removed           | Marcar deck como removido (remoção lógica)         | 200, 404, 500        |
| DELETE | /decks/{id}                   | Excluir um deck (remoção física)                   | 204, 404, 500        |
| GET    | /decks/{id}/cards             | Listar cartas de um deck                           | 200, 404, 500        |
| POST   | /decks/{id}/cards             | Adicionar carta ao deck                            | 201, 400, 404, 500   |
| DELETE | /decks/{id}/cards/{idCard}    | Remover carta do deck                              | 204, 404, 500        |
| GET    | /cards                        | Listar todas as cartas                             | 200, 500             |
| GET    | /cards/{id}                   | Buscar carta por ID                                | 200, 404, 500        |
| POST   | /cards                        | Criar nova carta                                   | 201, 400, 500        |
| PUT    | /cards/{id}                   | Atualizar carta existente                          | 200, 400, 404, 500   |
| PATCH  | /cards/{id}/removed           | Marcar carta como removida (remoção lógica)        | 200, 404, 500        |
| DELETE | /cards/{id}                   | Excluir carta do banco (remoção física)            | 204, 404, 500        |
| GET    | /artist                       | Listar todos os artistas                           | 200, 500             |
| GET    | /artist/{id}/cards            | Listar todas as cartas de um artist                | 200, 204, 400, 500   |
| GET    | /artist/{id}                  | Buscar artista por ID                              | 200, 404, 500        |
| POST   | /artist                       | Cadastrar novo artista                             | 201, 400, 500        |
| PUT    | /artist/{id}                  | Atualizar artista                                  | 200, 400, 404, 500   |
| GET    | /cards/{id}/artist            | Retornar artista responsável pela carta            | 200, 404, 500        |
| PATCH  | /artist/{id}/removed          | Marcar artista como removida (remoção lógica)      | 200, 404, 500        |
| DELETE | /artist/{id}                  | Excluir artista do banco (remoção física)          | 204, 404, 500        |

##### Status code
200 OK: Requisição foi bem-sucedida.  
201 Created: Novo objeto foi criado com sucesso.  
204 No Content: Ação foi executada com sucesso, mas não há conteúdo a retornar.  
400 Bad Request: A requisição está malformada ou possui dados inválidos.  
404 Not Found: O recurso solicitado não foi encontrado.   
500 Internal Server Error: Erro inesperado no servidor (ex: exceção não tratada, falha no banco).  

### 3. DTOs e Modelos de Dados
#####DTOs de requisição:
- PostDeckDTO
```json
{
  "nome": "string obrigatório",
  "formato": "string obrigatório",
  "descricao": "string opcional"
  "dataCriacao": "string obrigatório"
}
```

- PutDeckDTO
```json
{
  "nome": "string obrigatório",
  "formato": "string obrigatório",
  "descricao": "string opcional"
  "dataCriacao": "string obrigatório"
}
```
- PostCardDTO
```json
{
  "nome": "string obrigatório",
  "tipo": "string obrigatório",
  "cor": "string obrigatório",
  "custoMana": "string obrigatório"
}
```

- PutCardDTO
```json
{
  "nome": "string obrigatório",
  "tipo": "string obrigatório",
  "cor": "string obrigatório",
  "custoMana": "string obrigatório"
}
```

- PostCardnoDeckDTO
```json
{
  "idCarta": "integer obrigatório",
  "quantidade": "integer obrigatório"
}
```

- PostArtistDTO
```json
{
  "nome": "string obrigatório",
  "pais": "string obrigatório"
}
```

- PutArtistDTO
```json
{
  "nome": "string obrigatório",
  "pais": "string obrigatório"
}
```
- patchRemocaoLogicaDTO
```json
{
  "removido": "boolean obrigatório"
}
```

#####DTOs de resposta:
- DeckDTO
```json
{
  "id": "integer obrigatório", 
  "nome": "string obrigatório",
  "formato": "string obrigatório",
  "descricao": "string opicional",
  "cartas": [
    {
      "id": "integer obrigatório" ,
      "nome": "string obrigatório",
      "tipo": "string obrigatório",
      "cor": "string obrigatório",
      "custoMana": "string obrigatório",
      "quantidade": "integer obrigatório",
    }
  ],
  "dataCriacao": "string obrigatório",
}
```
- CardDTO
```json
{
  "id": "integer obrigatório",
  "nome": "string obrigatório",
  "tipo": "string obrigatório",
  "cor": "string obrigatório",
  "custoMana": "string obrigatório",
  "artista": {
    "id": "integer obrigatório",
    "nome": "string obrigatório"
  },
  "dataCriacao": "string obrigatório"
}
```
- ArtistDTO
```json
{
  "id": "integer obrigatório",
  "nome": "string obrigatório",
  "pais": "string obrigatório",
  "cartas": [
    {
      "id": "integer obrigatório",
      "nome": "string obrigatório",
      "tipo": "string obrigatório",
      "cor": "string obrigatório",
      "custoMana": "string obrigatório"
    }
  ]
}
```
