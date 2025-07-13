# 📚 Blog Backend – Tech Challenge Fase 2

## 💡 Descrição do Projeto

Esta aplicação entrega o backend de uma plataforma de **blog** para uso de professores da rede pública, onde é possível criar, editar, excluir, listar e buscar postagens via API RESTful.  
O objetivo foi refatorar o backend de OutSystems para **Node.js**, usando persistência em **MongoDB**, seguindo boas práticas de API moderna e com deploy simplificado via Docker.

---

## 🏗️ Arquitetura da Solução

- **Backend:** Node.js + Express
- **Banco de Dados:** MongoDB (container)
- **ORM:** Mongoose
- **API:** RESTful
- **Testes:** Jest + Supertest
- **CI/CD:** GitHub Actions
- **Containerização:** Docker + Docker Compose

### Estrutura de Pastas
blog-backend-buuu/
├── src/
│ ├── models/ # Modelos Mongoose
│ ├── routes/ # Rotas REST (posts)
│ ├── app.js # App Express
│ └── server.js # Inicialização e conexão com MongoDB
├── tests/ # Testes automatizados
├── Dockerfile # Imagem do backend
├── docker-compose.yml# Orquestração de backend + MongoDB
├── .github/
│ └── workflows/
│ └── ci.yml # Pipeline de CI/CD
├── package.json
└── README.md

yaml
Copiar
Editar


---

## 🚀 Guia de Uso

### 1. Requisitos

- Docker e Docker Compose instalados  
**ou**  
- Node.js 20+ e MongoDB rodando localmente

### 2. Como Rodar

#### **Com Docker (recomendado):**
```bash
docker-compose up --build

A API fica disponível em: http://localhost:3000

Sem Docker:

Instale dependências:
npm install
Rode o MongoDB na porta 27017
Inicie o backend:
npm start

| Método | Endpoint                   | Descrição                                   |
| ------ | -------------------------- | ------------------------------------------- |
| GET    | /posts                     | Lista todos os posts                        |
| GET    | /posts/\:id                | Retorna post pelo ID                        |
| POST   | /posts                     | Cria novo post                              |
| PUT    | /posts/\:id                | Edita post existente                        |
| DELETE | /posts/\:id                | Exclui post                                 |
| GET    | /posts/search?term=palavra | Busca posts por termo no título ou conteúdo |


Exemplos com curl
Listar todos:

bash
Copiar
Editar
curl http://localhost:3000/posts
Buscar por termo:

bash
Copiar
Editar
curl http://localhost:3000/posts/search?term=professor
Criar post:

bash
Copiar
Editar
curl -X POST http://localhost:3000/posts \
-H "Content-Type: application/json" \
-d '{"title":"Título", "content":"Conteúdo", "author":"Buuu"}'
Editar post:

bash
Copiar
Editar
curl -X PUT http://localhost:3000/posts/<ID> \
-H "Content-Type: application/json" \
-d '{"title":"Novo título", "content":"Novo conteúdo", "author":"Buuu"}'
Excluir post:

bash
Copiar
Editar
curl -X DELETE http://localhost:3000/posts/<ID>

✅ Testes
Para rodar testes automatizados:

bash
Copiar
Editar
npm test
Cobertura mínima: 20% (Jest coverage incluído)

🛠️ Pipeline CI/CD
Pipeline automático usando GitHub Actions:

Build, lint e teste a cada push na branch main

Serviço MongoDB disponível no ambiente de teste

🧩 Principais Complexidades e Desafios Enfrentados
🔥 Configuração de Ambiente
Primeira vez utilizando Docker em projeto real: apanhamos para entender a lógica de containers, network e volumes. Quebramos a cabeça até entender que o backend só “enxergava” o Mongo se estivesse tudo no mesmo docker-compose. 

Problemas de permissão no Docker Desktop no Windows, especialmente com WSL2.

Dependências do Node (versões de bibliotecas como supertest) causaram build quebrado e obrigaram a revisar package.json algumas vezes.

Descoberta de que a configuração do Docker Compose muda conforme a versão instalada (avisos sobre version obsoleta).

Dificuldade inicial para rodar comandos de teste e conectar com banco de dados “limpo” durante a pipeline do CI.

💀 Primeiro Contato Real com Docker
Complexo entender como subir múltiplos serviços e como as redes internas do Docker funcionam.

Gerenciar persistência do banco usando volumes foi um aprendizado importante pra evitar perder dados a cada build.

Debugging de erros do tipo “Cannot connect to MongoDB” e “Connection refused” foram frequentes até entender a ordem de inicialização dos containers.

Performance prejudicada, sendo necessário a reinicialização periódica do windows.

👀 Outras Pedras no Caminho
Build do Node travando com dependência errada ou cache de pacote corrompido.

Lidar com logs do Docker e do MongoDB em paralelo (nunca subestimem a verborragia do Mongo no terminal).

Adaptar a estrutura de código para separar responsabilidades (rotas, modelos, controllers), visando clareza para futuras expansões.

🦾 Como superamos
Uso intensivo de documentação oficial do Docker, Stack Overflow e ChatGPT para debugging rápido.

Testes de endpoints com insomnia a cada alteração, ajudaram a validar integração.

Pares revisando PRs e incentivando a commit contínuo, para evitar perder trabalho.

Cada erro foi registrado, pesquisado e documentado para facilitar manutenções futuras.

👥 Equipe & Créditos
Desenvolvido por: [Bruna Moura, rm362412] - [Carolina M, rm] - [Fernanda Magalhães, rm]

Tech Challenge Fase 2 - FIAP/Outros

🚀 Lições Aprendidas
Docker é um superpoder, mas exige paciência para domar.

Testar integração cedo evita surpresas na entrega.

APIs REST, mesmo simples, merecem código limpo e bem separado.

Documentar os erros e soluções salvou horas de retrabalho.
