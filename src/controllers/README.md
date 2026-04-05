# controllers/

Essa pasta é responsável por **receber as requisições HTTP e devolver as respostas**. Nada mais do que isso.

O controller não deve conter lógica de negócio — ele é só o intermediário entre a rota e o service.

---

## Como funciona

Quando uma requisição chega na API, ela passa por esse caminho:

```
Requisição HTTP → Route → Middleware → Controller → Service → Banco de dados → Resposta HTTP
```

O controller:
1. Lê os dados que vieram na requisição (`req.body`, `req.params`, etc.)
2. Chama o service passando esses dados
3. Devolve a resposta com o resultado

---

## O que você precisa criar aqui

Um arquivo por contexto da aplicação. Exemplos:

- `authController.js` — cadastro e login
- `userController.js` — ações do perfil do usuário
- `productController.js` — se o projeto tiver produtos, e por aí vai

---

## Anatomia de um controller

```js
const meuService = require('../services/meuService');

async function minhaFuncao(req, res) {
  try {
    const { dado } = req.body;
    const resultado = await meuService.fazAlgo(dado); // delega pro service
    res.json(resultado);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: 'Erro interno no servidor.' });
  }
}

module.exports = { minhaFuncao };
```

Perceba que o controller **não sabe como o service funciona** — ele só chama e repassa o resultado.

---

## Boas práticas

**Mantenha os controllers pequenos.** Se uma função está ficando grande, é sinal de que tem lógica de negócio escapando para cá — mova para o service.

**Trate os erros aqui.** Use try/catch e retorne os status HTTP adequados:

| Status | Significado           | Quando usar                          |
|--------|-----------------------|--------------------------------------|
| 200    | OK                    | Requisição bem-sucedida              |
| 201    | Created               | Recurso criado com sucesso           |
| 400    | Bad Request           | Dados inválidos ou faltando          |
| 401    | Unauthorized          | Usuário não autenticado              |
| 404    | Not Found             | Recurso não encontrado               |
| 409    | Conflict              | Ex: e-mail já cadastrado             |
| 500    | Internal Server Error | Erro inesperado no servidor          |