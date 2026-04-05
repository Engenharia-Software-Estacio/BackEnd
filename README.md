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

# Trabalho em equipe com Git

## Estratégia de branches

Fluxo recomendado:

main → produção  
develop → integração das features  
feature branches → desenvolvimento isolado

### Regras

### Main

- sempre estável
- apenas código pronto para produção
- nunca fazer commit direto
- merge apenas vindo da develop

---

### Develop

- branch de integração
- recebe PR das features
- ambiente de validação
- pode ser deploy de staging

---

### Padrão de nomes para branchs:

feat/nome-da-feature <br>
fix/nome-do-bug <br>
refactor/nome-da-melhoria <br>
chore/nome-da-tarefa <br>
test/nome-do-teste <br>
docs/nome-da-doc <br>

exemplos:

feat/create-user-form <br>
feat/dashboard-metrics <br>
fix/login-validation <br>
refactor/api-pattern <br>
chore/update-eslint <br>
docs/project-architecture <br>

OBS: 2 pessoas não devem trabalhar na mesma branch, não ao mesmo tempo pelo menos.

---

# Conventional Commits

padrão:

tipo(escopo): descrição curta

exemplos:

feat(auth): add login form <br>
feat(users): create user CRUD <br>
fix(auth): correct token validation <br>
refactor(api): centralize error handler <br>
docs(readme): update setup instructions <br>
test(users): add unit tests <br>
chore(deps): update dependencies <br>

---

## Tipos mais comuns

| tipo | quando usar |
|------|-------------|
| feat | nova funcionalidade |
| fix | correção de bug |
| refactor | melhoria interna sem alterar comportamento |
| chore | tarefa técnica |
| docs | documentação |
| test | testes |
| style | formatação |
| perf | performance |
| build | build ou dependências |
| ci | configuração de CI |

---

## Boas mensagens de commit


feat(users): add pagination to users table <br>
fix(auth): prevent login with expired token <br>
refactor(api): standardize response format <br>
docs: update architecture section <br>

---

## Checklist antes de abrir PR

- código compila
- tipagem correta
- sem any desnecessário
- sem console.log
- sem código comentado
- lint passou
- testes passaram
- sem arquivos desnecessários

---

## Template de descrição de PR

implementa criação de usuário

mudanças: <br>

formulário de usuário <br>
validação com zod <br>
integração com API <br>

como testar: <br>
