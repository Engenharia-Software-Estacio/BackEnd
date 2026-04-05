# services/

Essa pasta contém a **lógica de negócio** da aplicação. É aqui que as coisas de fato acontecem: validações, regras do sistema, consultas ao banco de dados.

---

## Como funciona

```
Requisição HTTP → Route → Middleware → Controller → Service → Banco de dados → Resposta HTTP
```

O service não sabe nada sobre HTTP — ele não conhece `req` nem `res`. Ele só recebe dados, processa e retorna um resultado. Isso o torna mais fácil de testar e de reutilizar.

---

## O que você precisa criar aqui

Um arquivo por contexto da aplicação, espelhando os controllers:

- `authService.js` — lógica de cadastro e login
- `userService.js` — lógica de perfil do usuário
- `productService.js` — lógica de produtos, e por aí vai

---

## Anatomia de um service

```js
const db = require('../config/db');

async function fazAlgo(dado) {
  // 1. Valida os dados recebidos
  if (!dado) {
    throw new Error('Dado obrigatório não informado.');
  }

  // 2. Consulta ou salva no banco
  const resultado = await db.query('SELECT * FROM tabela WHERE coluna = $1', [dado]);

  // 3. Retorna o resultado para o controller
  return resultado.rows[0];
}

module.exports = { fazAlgo };
```

---

## Boas práticas

**Jogue erros ao invés de retornar respostas HTTP.** O service não deve usar `res.json()` ou `res.status()` — isso é responsabilidade do controller. Quando algo der errado, lance um erro com `throw new Error(...)` e deixe o controller tratá-lo.

**Nunca salve senhas em texto puro.** Antes de salvar a senha de um usuário no banco, sempre criptografe com uma biblioteca como o `bcryptjs`.

**Centralize as regras aqui.** Se a mesma regra de negócio aparece em mais de um lugar da aplicação, ela pertence ao service — não ao controller.