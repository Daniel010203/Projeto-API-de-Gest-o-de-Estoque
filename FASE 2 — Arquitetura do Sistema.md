FASE 2 — Arquitetura do Sistema


# 🚀 StockFlow API

## FASE 2 — Arquitetura do Sistema

Na etapa anterior definimos **o que o sistema deve fazer**.

Agora vamos definir **como ele será estruturado tecnicamente**.

A Fase 2 será dividida em:

```text
FASE 2 — ARQUITETURA
│
├── 2.1 Princípios arquiteturais
├── 2.2 Estilo arquitetural
├── 2.3 Arquitetura em camadas
├── 2.4 Responsabilidade das camadas
├── 2.5 Fluxo de uma requisição
├── 2.6 Domínio da aplicação
├── 2.7 Entidades
├── 2.8 Relacionamentos
├── 2.9 Arquitetura lógica
├── 2.10 Arquitetura física
└── 2.11 Decisões arquiteturais
```

---

# 2.1 Princípios arquiteturais

Para o StockFlow, vamos adotar os seguintes princípios:

### 1. Separação de responsabilidades

Cada componente terá uma responsabilidade específica.

```text
Router       → HTTP
Schema       → Validação
Service      → Negócio
Repository   → Persistência
Model        → Banco
```

---

### 2. Baixo acoplamento

Queremos evitar que uma camada dependa diretamente dos detalhes internos de outra.

Por exemplo:

```text
Router
  ↓
Service
  ↓
Repository
```

e não:

```text
Router
  ↓
SQL diretamente
```

---

### 3. Alta coesão

Cada módulo deve concentrar funcionalidades relacionadas.

Por exemplo:

```text
products.py
```

deve cuidar das rotas relacionadas a produtos, não de estoque, usuários e autenticação simultaneamente.

---

### 4. Testabilidade

Precisamos conseguir testar:

```text
Router
Service
Repository
```

de forma controlada.

Principalmente as regras críticas:

```text
entrada de estoque
saída de estoque
estoque insuficiente
SKU duplicado
estoque mínimo
```

---

# 2.2 Estilo arquitetural

Adotaremos inicialmente:

> **Arquitetura em camadas + API REST + separação de domínio, aplicação e infraestrutura.**

Não vamos implementar Clean Architecture de forma excessivamente rígida neste primeiro projeto.

Porém, vamos organizar o código de forma que posteriormente possamos evoluir para princípios mais próximos de:

```text
Clean Architecture
Hexagonal Architecture
Domain-Driven Design
```

sem precisar reconstruir o projeto inteiro.

---

# 2.3 Arquitetura em camadas

A arquitetura principal será:

```text
┌───────────────────────────────┐
│          CLIENTES             │
│                               │
│ Web | Mobile | BI | ERP      │
└───────────────┬───────────────┘
                │
                │ HTTP
                ▼
┌───────────────────────────────┐
│          API LAYER            │
│                               │
│ FastAPI                       │
│ Routers / Endpoints           │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│        SCHEMA LAYER           │
│                               │
│ Pydantic                      │
│ Request / Response            │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│        SERVICE LAYER          │
│                               │
│ Regras de negócio             │
│ Casos de uso                  │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      REPOSITORY LAYER         │
│                               │
│ SQLAlchemy                    │
│ Persistência                  │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│           DATABASE            │
│                               │
│ PostgreSQL                    │
└───────────────────────────────┘
```

---

# 2.4 Responsabilidade de cada camada

## API Layer

Localização:

```text
app/api/
```

Responsável por:

* endpoints;
* HTTP methods;
* parâmetros;
* status codes;
* dependências do FastAPI;
* encaminhamento para Services.

Exemplo:

```text
POST /api/v1/products
```

O endpoint **não deverá conter toda a regra de negócio**.

---

# Schema Layer

Localização:

```text
app/schemas/
```

Responsável pela representação dos dados.

Teremos, por exemplo:

```text
ProductCreate
ProductUpdate
ProductResponse
```

Imagine:

```python
ProductCreate(
    sku="TEC-001",
    name="Teclado",
    price=120.00,
    minimum_stock=10
)
```

O Pydantic fará a validação antes de chegarmos à regra de negócio.

---

# Service Layer

Localização:

```text
app/services/
```

Aqui estará o **coração da aplicação**.

Por exemplo:

```text
StockService
```

poderá executar:

```text
registrar_entrada()
registrar_saida()
consultar_saldo()
verificar_estoque_baixo()
```

A regra:

> Não permitir saída maior que o estoque disponível.

deverá estar aqui.

---

# Repository Layer

Localização:

```text
app/repositories/
```

Responsável pela persistência.

Exemplo:

```text
ProductRepository
```

poderá possuir:

```text
create()
get_by_id()
get_by_sku()
get_all()
update()
delete()
```

O Service não precisa conhecer detalhes de SQL.

---

# Model Layer

Localização:

```text
app/models/
```

Representa as entidades persistidas no banco.

Teremos:

```text
Category
Product
Stock
StockMovement
```

---

# 2.5 Fluxo de uma requisição

Vamos utilizar um exemplo real.

O usuário solicita:

```http
POST /api/v1/movements
```

para registrar uma entrada.

O fluxo será:

```text
Cliente
   │
   ▼
FastAPI
   │
   ▼
Router
   │
   ▼
Pydantic
   │
   ▼
Stock Service
   │
   ├── verifica produto
   ├── valida quantidade
   ├── cria movimentação
   └── atualiza estoque
   │
   ▼
Repository
   │
   ▼
SQLAlchemy
   │
   ▼
PostgreSQL
```

Depois:

```text
PostgreSQL
    ↓
Repository
    ↓
Service
    ↓
Schema
    ↓
FastAPI
    ↓
JSON
```

---

# 2.6 Domínio da aplicação

Agora vamos definir o **domínio do StockFlow**.

O domínio principal é:

> **Gestão e controle de estoque.**

Dentro dele temos quatro conceitos principais:

```text
                    ESTOQUE
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
      Categoria      Produto     Movimentação
                         │
                         ▼
                       Saldo
```

---

# 2.7 Entidades

Nossa primeira versão terá quatro entidades principais.

## Category

Representa uma categoria de produtos.

```text
Category
──────────────
id
name
description
is_active
created_at
updated_at
```

---

## Product

Representa o produto.

```text
Product
────────────────
id
category_id
sku
name
description
price
minimum_stock
is_active
created_at
updated_at
```

---

## Stock

Representa o saldo atual.

```text
Stock
────────────
id
product_id
quantity
updated_at
```

---

## StockMovement

Representa uma alteração no estoque.

```text
StockMovement
────────────────────
id
product_id
movement_type
quantity
reason
created_at
```

---

# 2.8 Relacionamentos

Agora chegamos a uma parte fundamental da arquitetura.

## Categoria → Produto

Uma categoria pode possuir vários produtos.

```text
CATEGORY 1 ───────── N PRODUCT
```

Exemplo:

```text
Informática
│
├── Teclado
├── Mouse
├── Monitor
└── Webcam
```

---

## Produto → Estoque

Cada produto terá um registro de estoque.

```text
PRODUCT 1 ───────── 1 STOCK
```

Exemplo:

```text
Teclado
   │
   └── Estoque: 150
```

---

## Produto → Movimentações

Um produto poderá possuir várias movimentações.

```text
PRODUCT 1 ───────── N STOCK_MOVEMENT
```

Exemplo:

```text
Teclado
│
├── Entrada +100
├── Saída -20
├── Entrada +50
└── Saída -10
```

---

# 2.9 Arquitetura lógica

Nossa aplicação ficará organizada conceitualmente assim:

```text
                         STOCKFLOW
                             │
       ┌─────────────────────┼─────────────────────┐
       │                     │                     │
       ▼                     ▼                     ▼
   PRODUCTS              CATEGORIES             STOCK
       │                                           │
       │                                           │
       └────────────────────┬──────────────────────┘
                            │
                            ▼
                     MOVEMENTS
```

E tecnicamente:

```text
app/
│
├── api/
│
├── schemas/
│
├── services/
│
├── repositories/
│
├── models/
│
└── core/
```

---

# 2.10 Arquitetura física

Agora pensemos no ambiente onde tudo será executado.

Vamos utilizar Docker.

Teremos inicialmente dois containers:

```text
┌─────────────────────────────┐
│        Docker Network       │
│                             │
│  ┌───────────────────────┐  │
│  │     stockflow-api     │  │
│  │                       │  │
│  │ Python + FastAPI      │  │
│  └───────────┬───────────┘  │
│              │              │
│              │ PostgreSQL   │
│              ▼              │
│  ┌───────────────────────┐  │
│  │     stockflow-db      │  │
│  │                       │  │
│  │ PostgreSQL             │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

Posteriormente poderemos adicionar:

```text
Redis
Celery
Nginx
Prometheus
Grafana
```

se o projeto evoluir para necessidades que justifiquem esses componentes.

---

# 2.11 Decisões arquiteturais

Vamos registrar nossas decisões.

## ADR-001 — Framework

**Decisão:** FastAPI.

**Motivo:**

* Python;
* excelente suporte a APIs REST;
* validação com Pydantic;
* documentação OpenAPI;
* suporte a programação assíncrona;
* boa integração com bancos e ferramentas Python.

---

## ADR-002 — Banco

**Decisão:** PostgreSQL.

**Motivo:**

* banco relacional robusto;
* excelente suporte a SQL;
* integridade referencial;
* adequado para aplicações corporativas;
* integração com SQLAlchemy;
* facilidade de execução via Docker.

---

## ADR-003 — ORM

**Decisão:** SQLAlchemy.

**Motivo:**

Permite trabalhar com o banco utilizando uma camada de abstração Python, mantendo flexibilidade para consultas SQL quando necessário.

---

## ADR-004 — Validação

**Decisão:** Pydantic.

Será utilizado para:

```text
Request validation
Response serialization
Data validation
```

---

## ADR-005 — Migrações

**Decisão:** Alembic.

Não vamos depender de comandos manuais para criar e alterar tabelas.

O histórico da estrutura do banco será versionado.

---

## ADR-006 — Testes

**Decisão:** Pytest.

Os testes serão organizados por funcionalidade:

```text
tests/
├── test_categories.py
├── test_products.py
├── test_stock.py
└── test_movements.py
```

---

# 📌 Resultado da FASE 2

Chegamos a uma arquitetura bem definida:

```text
                  CLIENTE
                     │
                     ▼
                  FASTAPI
                     │
                     ▼
                  ROUTER
                     │
                     ▼
                 PYDANTIC
                     │
                     ▼
                  SERVICE
                     │
                     ▼
                REPOSITORY
                     │
                     ▼
                SQLALCHEMY
                     │
                     ▼
                POSTGRESQL
```

Com o domínio:

```text
Category
    │
    └── Product
           │
           ├── Stock
           │
           └── StockMovement
```

E a infraestrutura:

```text
Docker
 ├── API
 └── PostgreSQL
```

---
