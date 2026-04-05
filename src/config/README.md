# config/

Essa pasta guarda as **configurações globais** da aplicação — coisas que precisam ser inicializadas uma vez e reutilizadas em vários lugares.

---

## O que você precisa criar aqui

### `db.js`

Esse arquivo é responsável por criar e exportar a **conexão com o banco de dados**.

Independente da ferramenta que você escolher (Prisma, pg, Sequelize, etc.), o objetivo é o mesmo: inicializar a conexão em um lugar só e exportar para ser usada nos controllers.

**Exemplos de ferramentas comuns para PostgreSQL:**

- **`pg`** — driver direto, você escreve SQL na mão. Mais simples, mais controle.
- **`Prisma`** — ORM moderno, você define os modelos em um schema e ele gera as queries.
- **`Sequelize`** — ORM mais tradicional, popular em projetos Node.js.

Escolha uma, instale com `npm install`, e configure a conexão aqui.

```js
// Exemplo de como importar nos outros arquivos depois:
const db = require('../config/db');
```

---

## Por que centralizar aqui?

Se um dia você precisar trocar o banco ou ajustar as configurações de conexão, você muda em **um único lugar** — e todo o resto da aplicação continua funcionando normalmente.

---

## Dica: variáveis de ambiente

Nunca coloque usuário, senha ou URL do banco diretamente no código. Use variáveis de ambiente com o pacote `dotenv`:

```
DATABASE_URL=postgresql://usuario:senha@localhost:5432/nome_do_banco
```

E acesse no código com `process.env.DATABASE_URL`. Lembre de criar um arquivo `.env.example` documentando quais variáveis são necessárias — mas nunca suba o `.env` real pro Git.