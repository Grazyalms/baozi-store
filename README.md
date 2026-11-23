# Baozi Store - API REST

API REST simples (Java 17 + Spring Boot 3 + Spring Data JPA + H2/MySQL) para controle de clientes, produtos e pedidos da Baozi Store.

## Como rodar
1. Instale o JDK 17+.
2. Abra o projeto como projeto Maven na IDE (IntelliJ, Eclipse, STS ou VS Code) e execute `BaoziStoreApplication`,
   ou rode no terminal: `mvn spring-boot:run`
3. A API sobe em `http://localhost:8080`.

### Banco de dados
- **Padrão: H2** (não precisa instalar nada). Os dados ficam na pasta `data/`. Para ver as tabelas no navegador (bom para print do "banco configurado"):
  `http://localhost:8080/h2-console` com JDBC URL `jdbc:h2:file:./data/baozi_store`, usuário `sa` e senha vazia.
- **MySQL:** em `src/main/resources/application.properties`, comente o bloco do H2, descomente o bloco do MySQL e troque `SUA_SENHA`.
  O banco `baozi_store` é criado automaticamente.

## Endpoints
| Entidade | POST | GET (todos) | GET por ID | DELETE | PUT (opcional) |
|---|---|---|---|---|---|
| Cliente | /clientes | /clientes | /clientes/{id} | /clientes/{id} | /clientes/{id} |
| Produto | /produtos | /produtos | /produtos/{id} | /produtos/{id} | /produtos/{id} |
| Pedido  | /pedidos  | /pedidos  | /pedidos/{id}  | /pedidos/{id}  | /pedidos/{id}  |

## JSONs para testar no Postman (Body > raw > JSON)
Troque `SeuNome123456` pelo seu nome + RU e o nome do produto pelo que você usar na descrição do PDF.

POST /clientes
```json
{ "nome": "SeuNome123456", "clienteDesde": "2026-11-18" }
```

POST /produtos
```json
{ "nome": "Baozi de Carne", "preco": 6.50, "estoque": true }
```

POST /pedidos (use os ids retornados nos POSTs anteriores)
```json
{ "clienteId": 1, "produtoId": 1, "quantidade": 3 }
```

## Ordem sugerida dos prints
1. POST /clientes, POST /produtos, POST /pedidos
2. GET /clientes, GET /produtos, GET /pedidos
3. GET /clientes/1, GET /produtos/1, GET /pedidos/1
4. DELETE de um registro (de preferência crie um pedido extra só para apagar) e um GET depois mostrando que sumiu
