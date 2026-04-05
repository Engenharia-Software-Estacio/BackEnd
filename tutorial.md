# src/

Essa é a pasta principal da aplicação. É aqui que fica todo o código do servidor.

---

## `index.js`

O ponto de entrada da aplicação. É o primeiro arquivo que roda quando você inicia o servidor.

**O que ele deve fazer:**

1. Carregar as variáveis de ambiente com `dotenv`
2. Criar a aplicação Express
3. Registrar os middlewares globais (como `cors` e `express.json()`)
4. Registrar as rotas
5. Iniciar o servidor em uma porta

---

## Middlewares globais importantes

**`cors`** — permite que o frontend (rodando em outro endereço) consiga fazer requisições para a API. Sem ele, o navegador vai bloquear as chamadas.

**`express.json()`** — permite que o Express leia o corpo (`body`) das requisições no formato JSON. Sem ele, `req.body` vai ser sempre `undefined`.

Instale com:
```bash
npm install express cors dotenv
```

---

## Estrutura de pastas

```
src/
├── config/       → conexão com o banco de dados
├── controllers/  → recebe a requisição e devolve a resposta
├── services/     → lógica de negócio
├── middlewares/  → funções que rodam antes dos controllers
├── routes/       → define as URLs da API
└── index.js      → ponto de entrada do servidor
```

Cada pasta tem seu próprio `README.md` explicando o que criar lá dentro.