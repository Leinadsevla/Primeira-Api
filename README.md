# Task API

Esta API oferece funcionalidades para gerenciar tarefas vinculadas aos usuários. Cada usuário pode possuir múltiplas tarefas e a API disponibiliza operações para listagem, consulta, criação, atualização e remoção dessas tarefas.

##  Tecnologias Utilizadas

- **Node.js** - Runtime JavaScript
- **Express.js** - Framework web
- **PostgreSQL** - Banco de dados
- **pg** - Driver PostgreSQL para Node.js
- **dotenv** - Gerenciamento de variáveis de ambiente

##  Pré-requisitos

- Node.js (versão 14 ou superior)
- PostgreSQL instalado e configurado
- npm ou yarn

## 🔧 Instalação

1. Clone o repositório:
```bash
git clone <url-do-repositorio>
cd task-api
```

2. Instale as dependências:
```bash
npm install
```

3. Configure as variáveis de ambiente:
Crie um arquivo `.env` na raiz do projeto com as seguintes variáveis:

```env
DB_USER=seu_usuario
DB_HOST=localhost
DB_NAME=nome_do_banco
DB_PASSWORD=sua_senha
DB_PORT=5432
DB_SSL=false
DB_ENDPOINT_ID=seu_endpoint_id
PORT=3000
```

4. Configure o banco de dados:
Crie uma tabela `tarefas` no PostgreSQL:

```sql
CREATE TABLE tarefas (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    descricao TEXT,
    status VARCHAR(50) NOT NULL,
    usuario_id INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

5. Execute a aplicação:
```bash
npm start
```

A API estará disponível em `http://localhost:3000`

##  Endpoints da API

### Base URL: `/api`

#### 1. Listar todas as tarefas
- **GET** `/items`
- **Descrição**: Retorna todas as tarefas cadastradas
- **Resposta**: Array de objetos com as tarefas

#### 2. Buscar tarefa por ID
- **GET** `/items/:id`
- **Descrição**: Retorna uma tarefa específica pelo ID
- **Parâmetros**: `id` (ID da tarefa)
- **Resposta**: Objeto com os dados da tarefa

#### 3. Criar nova tarefa
- **POST** `/items`
- **Descrição**: Cria uma nova tarefa
- **Body**:
```json
{
    "titulo": "Título da tarefa",
    "descricao": "Descrição da tarefa",
    "status": "pendente",
    "usuario_id": 1
}
```
- **Campos obrigatórios**: `titulo`, `status`
- **Resposta**: Objeto com os dados da tarefa criada

#### 4. Atualizar tarefa
- **PUT** `/items/:id`
- **Descrição**: Atualiza uma tarefa existente
- **Parâmetros**: `id` (ID da tarefa)
- **Body**:
```json
{
    "titulo": "Novo título",
    "descricao": "Nova descrição",
    "status": "concluida"
}
```
- **Resposta**: Objeto com os dados da tarefa atualizada

#### 5. Deletar tarefa
- **DELETE** `/items/:id`
- **Descrição**: Remove uma tarefa
- **Parâmetros**: `id` (ID da tarefa)
- **Resposta**: Status 204 (sem conteúdo)

#### 6. Filtrar tarefas por status
- **GET** `/items/status?status=pendente`
- **Descrição**: Retorna tarefas filtradas por status
- **Parâmetros**: `status` (status para filtrar)
- **Resposta**: Array de objetos com as tarefas filtradas

##  Exemplos de Uso

### Criar uma nova tarefa
```bash
curl -X POST http://localhost:3000/api/items \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Estudar Node.js",
    "descricao": "Revisar conceitos de Express e PostgreSQL",
    "status": "pendente",
    "usuario_id": 1
  }'
```

### Listar todas as tarefas
```bash
curl http://localhost:3000/api/items
```

### Buscar tarefa por ID
```bash
curl http://localhost:3000/api/items/1
```

### Atualizar uma tarefa
```bash
curl -X PUT http://localhost:3000/api/items/1 \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Estudar Node.js - Atualizado",
    "descricao": "Concluído o estudo de Express",
    "status": "concluida"
  }'
```

### Filtrar tarefas por status
```bash
curl http://localhost:3000/api/items/status?status=pendente
```

##  Estrutura do Projeto

```
task-api/
├── cmr/
│   ├── app.js              # Arquivo principal da aplicação
│   ├── controllers/
│   │   └── tasksController.js  # Controladores das tarefas
│   └── routes/
│       └── taskRoutes.js      # Rotas da API
├── package.json
├── package-lock.json
└── README.md
```

##  Tratamento de Erros

A API retorna códigos de status HTTP apropriados:

- **200**: Sucesso
- **201**: Criado com sucesso
- **204**: Deletado com sucesso
- **400**: Dados inválidos
- **404**: Recurso não encontrado
- **500**: Erro interno do servidor


##  Autor

Desenvolvido para gerenciamento de tarefas com integração PostgreSQL.
