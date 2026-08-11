# 📦 StockFlow — API de Gestão de Estoque

> **Sistema de Gestão de Estoque desenvolvido com Python, com arquitetura orientada a API e foco em boas práticas de Engenharia de Software.**

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![Python](https://img.shields.io/badge/Python-3.x-blue)
![API](https://img.shields.io/badge/API-REST-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 📌 Sobre o Projeto

O **StockFlow** é uma aplicação voltada para **gestão e controle de estoque**, desenvolvida com o objetivo de aplicar, de forma prática, conceitos de **Engenharia de Software, desenvolvimento Backend, APIs REST, persistência de dados, testes automatizados e documentação técnica**.

O projeto está sendo desenvolvido de forma incremental, seguindo uma abordagem estruturada desde a definição dos requisitos até a implementação e evolução da solução.

A proposta é simular o desenvolvimento de um sistema que poderia ser utilizado por empresas para controlar produtos, movimentações e informações relacionadas ao estoque.

---

## 🎯 Objetivo

Desenvolver uma API robusta e escalável para gerenciamento de estoque, permitindo centralizar operações relacionadas a:

* Cadastro de produtos
* Controle de categorias
* Controle de estoque
* Entrada de produtos
* Saída de produtos
* Movimentações de estoque
* Consulta de disponibilidade
* Atualização de informações
* Monitoramento de indicadores
* Integração com outros sistemas

O projeto também tem como objetivo demonstrar competências técnicas relacionadas ao desenvolvimento de sistemas Backend com Python.

---

## 💼 Contexto de Negócio

Problemas comuns encontrados em processos de gestão de estoque:

* Controle manual de produtos;
* Falta de rastreabilidade das movimentações;
* Informações descentralizadas;
* Dificuldade para identificar estoque baixo;
* Falta de padronização dos processos;
* Erros no registro de entradas e saídas;
* Dificuldade para integração com outros sistemas;
* Baixa visibilidade sobre os indicadores de estoque.

O StockFlow busca solucionar esses problemas através de uma solução centralizada e baseada em API.

---

## 🏗️ Engenharia de Software

O desenvolvimento do projeto segue uma abordagem estruturada, contemplando diferentes etapas do ciclo de desenvolvimento de software.

### Fases do projeto

```text
FASE 1 — Engenharia de Software
        ↓
FASE 2 — Levantamento de Requisitos
        ↓
FASE 3 — Arquitetura da Solução
        ↓
FASE 4 — Modelagem de Dados
        ↓
FASE 5 — Desenvolvimento da API
        ↓
FASE 6 — Testes
        ↓
FASE 7 — Dockerização
        ↓
FASE 8 — Documentação
        ↓
FASE 9 — CI/CD
        ↓
FASE 10 — Evolução e Monitoramento
```

A documentação técnica do projeto está disponível no próprio repositório.

---

## 🧩 Principais Funcionalidades

### 📦 Produtos

* Cadastro de produtos;
* Consulta de produtos;
* Atualização de produtos;
* Exclusão de produtos;
* Consulta por identificador;
* Controle de informações do produto.

### 🏷️ Categorias

* Cadastro de categorias;
* Consulta de categorias;
* Associação entre produtos e categorias;
* Organização dos produtos.

### 📊 Controle de Estoque

* Consulta do estoque atual;
* Registro de entradas;
* Registro de saídas;
* Atualização de quantidades;
* Identificação de estoque mínimo;
* Controle da disponibilidade dos produtos.

### 🔄 Movimentações

O sistema deverá manter o histórico das movimentações realizadas no estoque.

Exemplo:

```text
Produto
   │
   ├── Entrada
   │      └── +100 unidades
   │
   ├── Saída
   │      └── -25 unidades
   │
   └── Saldo
          └── 75 unidades
```

---

## 🔌 API REST

A comunicação com o sistema será realizada através de uma **API REST**, permitindo que diferentes aplicações possam consumir os recursos disponibilizados pelo StockFlow.

Exemplo de estrutura:

```text
GET     /products
GET     /products/{id}
POST    /products
PUT     /products/{id}
DELETE  /products/{id}

GET     /categories
POST    /categories

GET     /stock
POST    /stock/entry
POST    /stock/exit

GET     /movements
GET     /movements/{id}
```

> Os endpoints podem sofrer alterações durante a evolução do projeto.

---

## 🏛️ Arquitetura

A arquitetura está sendo estruturada visando **separação de responsabilidades, manutenção, escalabilidade e facilidade de testes**.

Conceitualmente:

```text
                    CLIENTE
                       │
                       ▼
                 ┌───────────┐
                 │    API    │
                 └─────┬─────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Routers      │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Services     │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │   Repositories  │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    Database     │
              └─────────────────┘
```

Essa abordagem permite separar:

* Camada de apresentação;
* Regras de negócio;
* Persistência;
* Modelos;
* Validação;
* Configurações;
* Testes.

---

## 🗄️ Modelo de Dados

O domínio principal do sistema está baseado em entidades relacionadas à gestão de estoque.

Modelo conceitual:

```text
┌──────────────┐
│   Categoria  │
└──────┬───────┘
       │
       │ 1:N
       ▼
┌──────────────┐
│   Produto    │
└──────┬───────┘
       │
       │ 1:N
       ▼
┌──────────────┐
│ Movimentação │
└──────────────┘
```

A modelagem completa está documentada nos artefatos de Engenharia de Software do projeto.

---

## 🛠️ Tecnologias

As tecnologias utilizadas e previstas para o desenvolvimento incluem:

| Tecnologia        | Utilização                   |
| ----------------- | ---------------------------- |
| Python            | Linguagem principal          |
| FastAPI           | Desenvolvimento da API       |
| Pydantic          | Validação e serialização     |
| SQLAlchemy        | ORM / persistência           |
| PostgreSQL        | Banco de dados               |
| Pytest            | Testes automatizados         |
| Docker            | Containerização              |
| Git               | Controle de versão           |
| GitHub            | Versionamento e documentação |
| Swagger / OpenAPI | Documentação da API          |

---

## 📁 Estrutura do Projeto

A estrutura proposta segue uma organização orientada à separação de responsabilidades:

```text
StockFlow/
│
├── app/
│   ├── api/
│   │   ├── routes/
│   │   └── dependencies/
│   │
│   ├── core/
│   │   ├── config.py
│   │   └── security.py
│   │
│   ├── models/
│   │
│   ├── schemas/
│   │
│   ├── services/
│   │
│   ├── repositories/
│   │
│   └── main.py
│
├── tests/
│   ├── unit/
│   └── integration/
│
├── docs/
│
├── .env.example
├── .gitignore
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── LICENSE
└── README.md
```

> A estrutura poderá evoluir conforme novas funcionalidades forem implementadas.

---

## 🚀 Como Executar

### 1. Clonar o repositório

```bash
git clone https://github.com/Daniel010203/StockFlow.git
```

### 2. Acessar o projeto

```bash
cd StockFlow
```

### 3. Criar ambiente virtual

Windows:

```bash
python -m venv venv
```

Ativação:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 4. Instalar dependências

```bash
pip install -r requirements.txt
```

### 5. Configurar variáveis de ambiente

Criar um arquivo:

```text
.env
```

A configuração deve conter as variáveis necessárias para conexão com o banco de dados e demais serviços utilizados pela aplicação.

### 6. Executar a API

Exemplo utilizando Uvicorn:

```bash
uvicorn app.main:app --reload
```

A API ficará disponível localmente em:

```text
http://127.0.0.1:8000
```

---

## 📚 Documentação da API

Uma das vantagens do FastAPI é a geração automática da documentação baseada em OpenAPI.

Após executar a aplicação:

### Swagger UI

```text
http://127.0.0.1:8000/docs
```

### ReDoc

```text
http://127.0.0.1:8000/redoc
```

Essas interfaces permitem visualizar e testar os endpoints da API.

---

## 🧪 Testes

O projeto será desenvolvido considerando testes automatizados como parte do ciclo de desenvolvimento.

Estrutura:

```text
tests/
├── unit/
└── integration/
```

Execução:

```bash
pytest
```

Os testes deverão contemplar principalmente:

* Regras de negócio;
* Validação de dados;
* Endpoints;
* Operações de estoque;
* Persistência;
* Tratamento de erros;
* Integração com banco de dados.

---

## 🐳 Docker

O projeto possui como objetivo disponibilizar uma execução padronizada através de containers.

Exemplo:

```bash
docker compose up --build
```

Arquitetura prevista:

```text
┌─────────────────────┐
│      Cliente        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   StockFlow API     │
│      FastAPI        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│     PostgreSQL      │
└─────────────────────┘
```

---

## 🔐 Segurança

Entre as práticas previstas para evolução do projeto:

* Validação de entrada;
* Controle de acesso;
* Autenticação;
* Autorização;
* Proteção de credenciais;
* Variáveis de ambiente;
* Tratamento seguro de exceções;
* Não exposição de informações sensíveis;
* Controle de acesso aos recursos da API.

---

## 📈 Evolução Planejada

O StockFlow será evoluído progressivamente.

### Roadmap

* [x] Definição inicial do projeto
* [x] Engenharia de requisitos
* [x] Documento SRS
* [x] Documentação inicial
* [ ] Modelagem completa do banco
* [ ] Implementação da API
* [ ] CRUD de produtos
* [ ] CRUD de categorias
* [ ] Controle de entradas
* [ ] Controle de saídas
* [ ] Histórico de movimentações
* [ ] Validação de estoque mínimo
* [ ] Autenticação
* [ ] Autorização
* [ ] Testes unitários
* [ ] Testes de integração
* [ ] Docker
* [ ] CI/CD
* [ ] Monitoramento
* [ ] Deploy
* [ ] Dashboard
* [ ] Métricas e indicadores
* [ ] Integração com sistemas externos

---

## 📊 Indicadores Futuramente Disponíveis

Uma evolução natural do projeto será disponibilizar indicadores relacionados à operação de estoque.

Exemplos:

* Quantidade total de produtos;
* Produtos com estoque baixo;
* Produtos sem estoque;
* Entradas por período;
* Saídas por período;
* Produtos mais movimentados;
* Giro de estoque;
* Valor estimado do estoque;
* Histórico de movimentações.

---

## 🎓 Objetivo de Portfólio

O StockFlow faz parte de uma estratégia de desenvolvimento de projetos práticos voltados à consolidação de conhecimentos em:

**Python Backend + Engenharia de Software + APIs + Banco de Dados + Arquitetura + Testes + Docker.**

O projeto busca demonstrar não apenas capacidade de escrever código, mas também capacidade de participar de **todo o ciclo de desenvolvimento de uma solução de software**.

```text
REQUISITOS
    ↓
ARQUITETURA
    ↓
MODELAGEM
    ↓
DESENVOLVIMENTO
    ↓
TESTES
    ↓
CONTAINERIZAÇÃO
    ↓
DOCUMENTAÇÃO
    ↓
DEPLOY
```

---

## 📖 Documentação do Projeto

A documentação técnica e os artefatos de Engenharia de Software estão disponíveis no repositório.

Entre os documentos estão:

* Visão geral do sistema;
* Documento de requisitos;
* SRS — Software Requirements Specification;
* Documentação de Engenharia de Software;
* Modelo de dados;
* Arquitetura;
* Especificações técnicas.

---

## 👨‍💻 Autor

**Daniel Vieira**

Projeto desenvolvido para estudos e construção de portfólio profissional na área de Tecnologia da Informação, com foco em:

* Python Backend;
* Desenvolvimento de APIs;
* Engenharia de Software;
* Banco de Dados;
* Análise de Sistemas;
* Data & Analytics.

---

## 📄 Licença

Este projeto está disponível sob a licença **MIT**.

Consulte o arquivo `LICENSE` para obter mais informações.

---

## ⭐ Projeto em Desenvolvimento

O **StockFlow** encontra-se em desenvolvimento contínuo.

Novas funcionalidades, melhorias arquiteturais, testes, documentação e recursos de infraestrutura serão incorporados progressivamente ao projeto.

**Feedbacks, sugestões e contribuições são bem-vindos.**

