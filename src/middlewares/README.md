# middlewares/

Essa pasta contém as **funções intermediárias** que são executadas entre a requisição chegar e o controller ser chamado.

---

## Como funciona

```
Requisição HTTP → Route → Middleware → Controller → Service → Banco de dados → Resposta HTTP
```

Um middleware é uma função que tem acesso ao `req`, ao `res`, e a um terceiro argumento chamado `next`. Ele pode:

- Deixar a requisição continuar chamando `next()`
- Barrar a requisição devolvendo uma resposta diretamente

---

## O que você precisa criar aqui

### `auth.js`

O middleware de autenticação. Ele deve ser usado em todas as rotas que exigem que o usuário esteja logado.

**O que ele deve fazer:**
1. Ler o token JWT que vem no header da requisição
2. Verificar se o token é válido
3. Se for válido, deixar a requisição continuar com `next()`
4. Se não for, barrar com um erro `401`

O token normalmente vem no header `Authorization` nesse formato:
```
Authorization: Bearer <token>
```

Depois de verificar o token, é uma boa prática adicionar os dados do usuário ao `req` para que o controller consiga acessá-los:

```js
req.user = dadosDoToken; // ex: { id: 1, email: 'joao@email.com' }
next();
```

---

## Como usar nas rotas

O middleware é passado como argumento entre a rota e o controller:

```js
const authMiddleware = require('../middlewares/auth');

// Rota pública — qualquer um pode acessar
router.post('/login', authController.login);

// Rota privada — só usuários logados
router.get('/perfil', authMiddleware, userController.getPerfil);
```

---

## Dica

Você vai precisar do pacote `jsonwebtoken` para verificar o token. Instale com:

```bash
npm install jsonwebtoken
```

E não esqueça de definir uma variável `JWT_SECRET` no seu `.env` — ela é usada tanto para assinar o token no login quanto para verificá-lo aqui.