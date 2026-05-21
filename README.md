# 🎁 Lojinha da Keila

> Uma plataforma de e-commerce interna para o pessoal de CR com sistema de recompensas em **CRCoins** - moedas virtuais.

---

## 📋 Sobre o Projeto

A **Lojinha da Keila** é uma plataforma de marketplace interno que permite aos colaboradores da CR:

✨ **Funcionalidades Principais:**
- 🛍️ **Catálogo de Produtos** - Browse produtos e promoções
- 💳 **Carrinho de Compras** - Adicionar/remover itens
- 💰 **Sistema de Moedas Virtuais** - CRCoins como forma de pagamento
- 📦 **Histórico de Pedidos** - Acompanhar compras realizadas
- 🎯 **Links de Recompensas** - Ganhar coins completando ações
- 👨‍💼 **Painel Admin** - Gerenciar produtos, pedidos, usuários e moedas
- 🔐 **Autenticação Segura** - Login com validação de email
- 📱 **Interface Responsiva** - Acesso via web e mobile

---

## 🚀 Quick Start

### Pré-requisitos
- Node.js 16+
- NPM ou Yarn
- Conta Supabase

### Instalação

```bash
# Clonar repositório
git clone <seu-repo>
cd Lojinha-da-Keila

# Instalar dependências
npm install

# Configurar variáveis de ambiente
cp .env.example .env
# Editar .env com suas credenciais

# Iniciar servidor local
npm start
```

### Deploy (Vercel)

```bash
# Deploy automático via Vercel
npm run deploy

# Ou fazer push para main branch
git push origin main
```

---

## 📁 Estrutura do Projeto

```
Lojinha-da-Keila/
├── index.html              # Página principal
├── package.json            # Dependências
├── vercel.json             # Configuração Vercel
├── README.md               # Este arquivo
│
├── /api                    # Endpoints REST
│   ├── auth.js            # Autenticação
│   ├── admin.js           # Gerenciamento admin
│   ├── products.js        # Catálogo de produtos
│   └── orders.js          # Gestão de pedidos
│
├── /src                    # Código-fonte
│   ├── style.css          # Estilos globais
│   └── /js
│       ├── app.js         # Aplicação principal
│       ├── router.js      # Roteamento SPA
│       ├── supabase.js    # Configuração Supabase
│       ├── auth.js        # Lógica de autenticação
│       ├── loja.js        # Funcionalidades da loja
│       ├── admin.js       # Painel administrativo
│       ├── components.js  # Componentes reutilizáveis
│       └── utils.js       # Funções utilitárias
│
├── /public                # Arquivos estáticos
│   ├── /images           # Imagens de produtos/banners
│   ├── /icons            # Ícones SVG
│   └── /sounds           # Efeitos sonoros
│
└── /supabase             # Backend Supabase
    ├── /functions        # Cloud Functions
    │   ├── /purchase-item       # Processar compra
    │   ├── /give-coins          # Adicionar moedas
    │   ├── /import-users        # Importar usuários em lote
    │   ├── /redeem-link         # Resgatar link de recompensa
    │   └── /update-stock        # Atualizar estoque
    │
    └── /migrations       # Schemas do banco
        └── 001_init.sql  # Tabelas iniciais
```

---

## 🔑 Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
# Supabase
VITE_SUPABASE_URL=https://sua-instancia.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anonima

# API
VITE_API_URL=http://localhost:3000

# Configurações
VITE_APP_NAME=Lojinha da Keila
VITE_APP_VERSION=1.0.0
```

---

## 💻 Desenvolvimento

### Scripts Disponíveis

```bash
# Iniciar dev server
npm start

# Build para produção
npm run build

# Deploy para Vercel
npm run deploy

# Executar testes
npm test

# Lint de código
npm run lint
```

### Fluxo de Desenvolvimento

1. **Clonar** e instalar dependências
2. **Criar branch** para sua feature: `git checkout -b feature/minha-feature`
3. **Desenvolver** e testar localmente
4. **Commit** com mensagens descritivas
5. **Push** e abrir Pull Request
6. **Deploy** automático após merge para `main`

---

## 🗄️ Banco de Dados (Supabase)

### Tabelas Principais

#### `users`
```sql
- id (UUID) - Chave primária
- email (VARCHAR) - Email único
- name (VARCHAR) - Nome completo
- avatar_url (VARCHAR) - URL do avatar
- coins_balance (INT) - Saldo de CRCoins
- role (ENUM) - user | admin
- created_at (TIMESTAMP)
```

#### `products`
```sql
- id (UUID) - Chave primária
- name (VARCHAR) - Nome do produto
- description (TEXT) - Descrição
- price (DECIMAL) - Preço em moedas
- image_url (VARCHAR) - URL da imagem
- stock (INT) - Quantidade em estoque
- category (VARCHAR) - Categoria
- created_at (TIMESTAMP)
```

#### `orders`
```sql
- id (UUID) - Chave primária
- user_id (UUID) - FK para users
- total_price (DECIMAL) - Valor total
- status (ENUM) - pending | completed | cancelled
- created_at (TIMESTAMP)
```

#### `reward_links`
```sql
- id (UUID) - Chave primária
- code (VARCHAR) - Código único
- coins_value (INT) - CRCoins a ganhar
- used_by (UUID) - FK para users que resgataram
- is_active (BOOLEAN)
- created_at (TIMESTAMP)
```

---

## 🔐 Autenticação & Autorização

### Fluxo de Login
1. Usuário insere email
2. Sistema valida se é colaborador de CR
3. Magic Link enviado via email
4. Clique no link + criação de sessão
5. Acesso à loja

### Papéis e Permissões

| Ação | User | Admin |
|------|:----:|:-----:|
| Visualizar loja | ✅ | ✅ |
| Comprar produtos | ✅ | ✅ |
| Ver pedidos próprios | ✅ | ✅ |
| Resgatar links | ✅ | ✅ |
| Gerenciar produtos | ❌ | ✅ |
| Gerenciar usuários | ❌ | ✅ |
| Distribuir moedas | ❌ | ✅ |
| Ver relatórios | ❌ | ✅ |

---

## 🎮 Como Usar

### Para Usuários Normais

1. **Login** com seu email de CR
2. **Explorar** catálogo de produtos
3. **Adicionar** itens ao carrinho
4. **Checkout** e confirmar compra com CRCoins
5. **Resgatar Links** de recompensa para ganhar moedas
6. **Acompanhar** pedidos no histórico

### Para Administradores

1. Acessar **Painel Admin** (ícone de engrenagem)
2. **Gerenciar Produtos** - Adicionar/editar/deletar
3. **Gerenciar Pedidos** - Aprovar e marcar como entregue
4. **Distribuir Moedas** - Dar coins para usuários
5. **Criar Links** - Gerar links de recompensa
6. **Importar Usuários** - Upload em lote (CSV)
7. **Ver Relatórios** - Análises de vendas e uso

---

## 🛠️ Tecnologias Utilizadas

### Frontend
- **Vanilla JavaScript** - Sem frameworks pesados
- **CSS3** - Styles responsivos
- **HTML5** - Markup semântico

### Backend
- **Supabase** - PostgreSQL + Auth + Real-time
- **Cloud Functions** - TypeScript/Node.js
- **Vercel** - Hosting e serverless

### Bibliotecas
- `supabase-js` - Cliente Supabase
- `date-fns` - Manipulação de datas
- Sem dependências desnecessárias!

---

## 📊 API Endpoints

### Autenticação
```
POST   /api/auth/login          - Enviar magic link
POST   /api/auth/verify         - Verificar token
POST   /api/auth/logout         - Fazer logout
GET    /api/auth/me             - Dados do usuário logado
```

### Produtos
```
GET    /api/products            - Listar todos
GET    /api/products/:id        - Detalhes de um produto
POST   /api/products            - Criar (admin)
PATCH  /api/products/:id        - Atualizar (admin)
DELETE /api/products/:id        - Deletar (admin)
```

### Pedidos
```
GET    /api/orders              - Listar meus pedidos
POST   /api/orders              - Criar pedido
GET    /api/orders/:id          - Detalhes do pedido
PATCH  /api/orders/:id          - Atualizar status (admin)
```

### Admin
```
GET    /api/admin/users         - Listar usuários
GET    /api/admin/stats         - Estatísticas
POST   /api/admin/give-coins    - Distribuir moedas
POST   /api/admin/import-users  - Importar em lote
```

---

## 🚨 Troubleshooting

### Erro: "Email não autorizado"
- Certifique-se de usar seu email de CR (@cr.com)
- Contate o administrador para ser adicionado

### Erro: "Conexão recusada ao Supabase"
- Verifique as credenciais em `.env`
- Confirme que a instância Supabase está online
- Teste a conexão: `npm run test:db`

### Moedas não aparecem após resgate
- Recarregue a página (F5)
- Aguarde alguns segundos (Real-time pode ter delay)
- Verifique logs no console (F12)

---

## 📞 Suporte

- 💬 **Dúvidas?** Abra uma issue no GitHub
- 🐛 **Bug encontrado?** Reporte com screenshot
- 💡 **Sugestão?** Discussion ou Pull Request

---

## 📄 Licença

Propriedade da CR. Uso restrito aos colaboradores.

---

## 👥 Contribuidores

Criado por **Keila** com ❤️ para o time de CR.

**Última atualização:** 21 de maio de 2026
