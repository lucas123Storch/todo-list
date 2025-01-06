# To-Do List App

Este é um aplicativo simples de lista de tarefas. O projeto permite que os usuários adicionem, atualizem e excluam tarefas com sincronização em tempo real.


## Pré-requisitos

- **Node.js**: Certifique-se de ter a versão **19.x** ou superior instalada. Você pode verificar a versão instalada executando:

  ```bash
  node -v
  ```

- **Gerenciador de Pacotes (npm)**: Utilize **npm** (instalado junto com o Node.js) para gerenciar as dependências.


## Configuração do Ambiente

1. **Copie o arquivo de exemplo do ambiente**:
   No diretório do projeto, copie o arquivo `.env.example` e renomeie-o para `.env`:

   ```bash
   cp .env.example .env
   ```

2. **Adicione as credenciais do Firebase**:
   Preencha o arquivo `.env` com as credenciais do Firebase, substituindo os placeholders pelos valores reais do seu projeto Firebase.

   ```env
   FIREBASE_API_KEY=your_firebase_api_key
   FIREBASE_AUTH_DOMAIN=your_firebase_auth_domain
   FIREBASE_PROJECT_ID=your_firebase_project_id
   FIREBASE_STORAGE_BUCKET=your_firebase_storage_bucket
   FIREBASE_MESSAGING_SENDER_ID=your_firebase_messaging_sender_id
   FIREBASE_APP_ID=your_firebase_app_id
   ```

---

## Instalação

1. **Instale as dependências**:
   Execute o seguinte comando para instalar todas as dependências do projeto:

   ```bash
   npm install
   ```

---

## Como Rodar o Projeto

1. **Iniciar o servidor de desenvolvimento**:
   Para rodar o projeto em modo de desenvolvimento, execute:

   ```bash
   npm run dev
   ```

2. **Acessar o aplicativo**:
   O projeto estará disponível no navegador no endereço:

   ```
   http://localhost:3000
   ```

---

## Tecnologias Utilizadas

- **Nuxt.js**: Framework para Vue.js.
- **Tailwind CSS**: Framework de CSS utilitário.
- **Firebase**: Para persistência no banco de dados em tempo real.

---

## Observações

- Certifique-se de que as credenciais do Firebase no arquivo `.env` estão corretas.
- Use a versão recomendada do Node.js para evitar problemas de compatibilidade.
