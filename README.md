# ED Frios — Controle de Caixa

Aplicativo web de controle de receitas e despesas do ED Frios (Massapé - CE).

## Estrutura do projeto

```
.
├── index.html   # aplicativo completo (HTML, CSS e JS em um único arquivo)
├── assets/      # imagens e outros recursos estáticos
└── docs/        # documentação e anotações do projeto
```

## Funcionalidades

- Registro de receitas e despesas por sócio
- Filtros por período, categoria e forma de pagamento
- Resumo de saldo por sócio
- Gráfico de despesas/receitas por categoria
- Gerenciamento de categorias personalizadas

## Como usar

Basta abrir o arquivo `index.html` em um navegador (ou acessar a página publicada via GitHub Pages).

## Dados compartilhados entre aparelhos

O app usa o Firebase Realtime Database para que os dois sócios vejam os mesmos dados em aparelhos diferentes:

- A URL do banco fica na constante `FIREBASE_URL`, no início do `<script>` do `index.html`.
- Enquanto `FIREBASE_URL` estiver vazia, os dados ficam salvos apenas no aparelho (via `localStorage`).
- Com a URL configurada, o app salva no Firebase e sincroniza automaticamente a cada 15 segundos e ao reabrir o app. Sem internet, os dados ficam no aparelho e são enviados quando a conexão voltar.

Para criar o banco (gratuito): acesse [console.firebase.google.com](https://console.firebase.google.com), crie um projeto, crie um **Realtime Database** e, na aba **Regras**, publique:

```json
{
  "rules": {
    "edfrios": {
      ".read": true,
      ".write": true
    }
  }
}
```

Depois copie a URL do banco (ex: `https://seu-projeto-default-rtdb.firebaseio.com`) e cole na constante `FIREBASE_URL`.

> Atenção: com essas regras, qualquer pessoa que descobrir a URL do banco consegue ler e alterar os dados. Para este uso (controle interno entre dois sócios), é uma troca aceitável entre simplicidade e segurança — mas não guarde dados sensíveis além do necessário.
