# Backend — API REST com Express

## Pré-requisitos

- Node.js 18+
- PostgreSQL instalado e rodando
- Conta no GitHub

---

## Configurando o Git e a chave SSH

Antes de clonar o projeto, você precisa configurar o Git e criar uma chave SSH para autenticar com o GitHub sem precisar digitar senha toda vez.

### 1. Instale o Git

Baixe e instale o Git em https://git-scm.com/download/win. Deixe todas as opções padrão durante a instalação.

Depois, abra o **Git Bash** e configure seu nome e e-mail:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

Use o mesmo e-mail da sua conta no GitHub.

### 2. Gere uma chave SSH

Ainda no Git Bash:

```bash
ssh-keygen -t ed25519 -C "seu@email.com"
```

Vai aparecer uma pergunta sobre onde salvar — só pressione `Enter` para usar o local padrão. Depois vai pedir uma senha — pode deixar em branco e pressionar `Enter` duas vezes.

### 3. Adicione a chave SSH ao GitHub

Copie a chave pública com o comando:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copie tudo que aparecer. Depois:

1. Acesse https://github.com/settings/keys
2. Clique em **New SSH key**
3. Dê um nome (ex: "Meu notebook") e cole a chave
4. Clique em **Add SSH key**

### 4. Teste a conexão

```bash
ssh -T git@github.com
```

Se aparecer `Hi seu-usuario! You've successfully authenticated`, está tudo certo.

---

## Clonando o projeto

Com a chave SSH configurada, clone o repositório:

```bash
git clone git@github.com:usuario/nome-do-repositorio.git
```

Entre na pasta do backend:

```bash
cd nome-do-repositorio/backend
```

---

## Como rodar

### 1. Instale as dependências

```bash
npm install
```

### 2. Configure as variáveis de ambiente

```bash
cp .env.example .env
```

Abra o arquivo `.env` e preencha com os dados do seu banco:

```env
DATABASE_URL="sua-string-de-conexao-aqui"
JWT_SECRET="uma-chave-secreta-longa-e-aleatoria"
JWT_EXPIRES_IN="7d"
PORT=3001
```

### 3. Rode o servidor em modo desenvolvimento

```bash
npm run dev
```

O servidor vai iniciar em **http://localhost:3001**. Se aparecer `Servidor rodando em http://localhost:3001` no terminal, está funcionando.

---

## Estrutura do projeto

```
src/
├── config/       → conexão com o banco de dados
├── controllers/  → recebe a requisição e devolve a resposta
├── services/     → lógica de negócio
├── middlewares/  → funções que rodam antes dos controllers
├── routes/       → define as URLs da API
└── index.js      → ponto de entrada do servidor
```

Cada pasta tem um `README.md` explicando o que criar lá dentro.

---

## Como adicionar uma nova funcionalidade

1. Crie o service em `src/services/`
2. Crie o controller em `src/controllers/`
3. Crie as rotas em `src/routes/`
4. Registre a rota no `src/index.js`

---

## Comandos úteis

```bash
npm run dev    # Sobe o servidor com hot-reload
npm start      # Sobe o servidor sem hot-reload
```