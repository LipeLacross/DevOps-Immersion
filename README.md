## 🌐 [English Version of README](README_EN.md)

# DevOps-Immersion

Este repositório é dedicado ao **Alura & Google Cloud DevOps Immersion**. Aprenda DevOps na prática com projetos reais, cobrindo tecnologias essenciais como **Docker** (containers), pipelines de **CI/CD** e **Google Cloud Run** para deploy.

Acesse o guia completo: [alura.tv/guiademergulhodevops](https://alura.tv/guiademergulhodevops)

## 🔨 Funcionalidades do Projeto

- API REST para gestão escolar, permitindo:
  - Cadastro, consulta, atualização e remoção de **alunos**
  - Gerenciamento de **cursos**
  - Matrícula de alunos em cursos
- Deploy containerizado com Docker
- Pronto para integração contínua (CI/CD) e deploy no Google Cloud Run

### 📸 Exemplo Visual do Projeto

<div align="center">
  <img src="https://github.com/user-attachments/assets/584d9aee-57bb-4d24-b948-056467ff4e68" alt="Screenshot 2025-07-03 132707" width="350" style="margin: 8px; border-radius: 8px;">
  <img src="https://github.com/user-attachments/assets/ed764f6c-c4e5-45d0-9efc-b92dce5bd036" alt="Screenshot 2025-07-03 130932" width="350" style="margin: 8px; border-radius: 8px;">
</div>

> A API expõe endpoints documentados via Swagger em `/docs` após inicialização local ou em nuvem.

## ✔️ Técnicas e Tecnologias Utilizadas

- **Python** (FastAPI)
- **Docker** & Docker Compose
- **SQLAlchemy** (ORM)
- **SQLite** (banco de dados local)
- **Pydantic** (validação de dados)
- **Google Cloud Run** (deploy)
- **CI/CD** (integração contínua)

## 📁 Estrutura do Projeto

- **app.py**: Inicialização da aplicação FastAPI e inclusão das rotas principais.
- **database.py**: Configuração do banco de dados SQLite e sessão ORM.
- **models.py**: Definição das tabelas e relacionamentos (Alunos, Cursos, Matrículas).
- **schemas.py**: Schemas Pydantic para validação e serialização de dados.
- **requirements.txt**: Lista de dependências do projeto.
- **Dockerfile**: Instruções para construir a imagem Docker da aplicação.
- **docker-compose.yml**: Orquestração de containers para ambiente local.
- **escola.db**: Banco de dados SQLite utilizado pela aplicação.
- **README.md**: Documentação principal (este arquivo).
- **README_EN.md**: Versão em inglês da documentação.
- **LICENSE**: Licença do projeto.

## 🛠️ Abrir e rodar o projeto

Para iniciar o projeto localmente, siga os passos abaixo:

1. **Certifique-se de que o Docker está instalado**:
   - Baixe e instale o [Docker](https://www.docker.com/).

2. **Clone o Repositório**:
   ```
   git clone 
   cd DevOps-Immersion
   ```

3. **Suba a aplicação com Docker Compose**:
   ```
   docker-compose up --build
   ```

4. **Acesse a API**:
   - Acesse `http://localhost:8000/docs` para visualizar e testar os endpoints via Swagger.

## 🌐 Deploy

Para realizar o **deploy na nuvem usando o Google Cloud Run**, siga este passo a passo detalhado:

### 1. Pré-requisitos

- **Conta Google Cloud** ativa.
- **Projeto** criado no Google Cloud.
- **Google Cloud SDK** instalado na sua máquina (ou use o Cloud Shell no console).
- **APIs necessárias habilitadas**:
  ```
  gcloud services enable run.googleapis.com
  gcloud services enable cloudbuild.googleapis.com
  ```
- **Autentique-se**:
  ```
  gcloud auth login
  ```
- **Configure o projeto**:
  ```
  gcloud config set project SEU_PROJECT_ID
  ```

**Exemplo de tela de instalação do Google Cloud SDK:**

![Exemplo de instalação do Google Cloud SDK](https://pplx-res.cloudinary.com/image/private/user_uploads/55317053/d32b6db6-ce42-4950-8426-f30919db9d8e/image.jpg)

> Marque:
> - Google Cloud CLI Core Libraries and Tools (obrigatório)
> - Bundled Python (recomendado)
> - Cloud Tools for PowerShell (opcional)
> - Beta Commands (opcional)

### 2. Construa e envie a imagem Docker para o Container Registry

No diretório raiz do projeto (onde está o Dockerfile), execute:

```
gcloud builds submit --tag gcr.io/SEU_PROJECT_ID/devops-immersion
```
- Substitua `SEU_PROJECT_ID` pelo ID do seu projeto no Google Cloud.
- Esse comando irá construir a imagem Docker e enviá-la ao Container Registry do seu projeto.

### 3. Faça o deploy no Cloud Run

Execute o comando abaixo para criar (ou atualizar) o serviço no Cloud Run:

```
gcloud run deploy devops-immersion \
  --image gcr.io/SEU_PROJECT_ID/devops-immersion \
  --platform managed \
  --region SUA_REGIAO \
  --allow-unauthenticated
```
- Substitua `SEU_PROJECT_ID` pelo seu projeto.
- Substitua `SUA_REGIAO` pela região desejada (exemplo: `us-central1`, `southamerica-east1`).
- O parâmetro `--allow-unauthenticated` permite acesso público à API (remova se quiser acesso restrito).

Durante o deploy, você pode ser solicitado a confirmar o nome do serviço e a região.

### 4. Acesse sua aplicação

Após a conclusão, o terminal exibirá a URL pública do serviço Cloud Run. Basta acessar essa URL no navegador para consumir a API.

**Dicas adicionais:**

- Você pode acompanhar e gerenciar seus serviços pelo console web do Google Cloud, na seção **Cloud Run**.
- Para configurar variáveis de ambiente, memória, limites de requisição e outras opções, consulte a documentação oficial do Cloud Run.
- Caso queira automatizar o deploy via CI/CD, utilize um arquivo `cloudbuild.yaml` com as etapas de build e deploy.
