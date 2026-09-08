# Fiori & Spineli

**Software, dados e ideias transformadas em produtos.**

A **Fiori & Spineli** é uma organização independente criada por **Lucas Fiori** e **Samuel Spineli** para desenvolver software, experimentar tecnologias e transformar problemas reais em produtos digitais.

Nosso foco está na interseção entre **engenharia de software, desenvolvimento de aplicações, dados e experiência de usuário** — construindo soluções que sejam tecnicamente sólidas, simples de utilizar e capazes de resolver problemas concretos.

> **Construir coisas úteis. Entender o problema. Fazer direito.**

---

## O que fazemos

A Fiori & Spineli funciona como um espaço para transformar ideias em software.

Trabalhamos principalmente com:

* Desenvolvimento de aplicações web e mobile
* Engenharia e arquitetura de software
* Modelagem e gerenciamento de dados
* APIs e integrações
* Automação de processos
* Data Science e aplicações orientadas a dados
* Prototipação e validação de produtos
* Experimentação com novas tecnologias

Nem todo projeto nasce para virar produto.

Alguns existem para aprender, testar uma hipótese ou explorar uma tecnologia. Outros começam pequenos e evoluem até se tornarem sistemas completos.

A organização existe para dar um lugar comum a todos eles.

---

## Projetos

### 🍻 Buteco

**O caderninho de contas do buteco, no celular.**

O **Buteco** é o primeiro produto desenvolvido pela Fiori & Spineli.

A ideia é simples: substituir o tradicional caderninho de contas por uma experiência digital que não complique a vida de ninguém.

O dono do estabelecimento lança o consumo e o cliente acompanha sua própria conta através de um **link ou QR Code**, sem precisar instalar aplicativo ou criar uma conta.

#### Principais características

* Comandas digitais
* Cadastro de produtos
* Lançamento de consumo
* Acompanhamento da conta pelo cliente
* Acesso através de QR Code
* Acesso público sem criação de conta
* Divisão de conta
* Gestão de produtos e imagens
* Autenticação do proprietário por Magic Link
* Controle de acesso utilizando Row Level Security
* Interface responsiva para celular

#### Stack

| Camada                   | Tecnologia                              |
| ------------------------ | --------------------------------------- |
| Frontend                 | Next.js 16 + React 19                   |
| Runtime / Bundler        | Turbopack                               |
| Estilo                   | Tailwind CSS v4                         |
| Backend                  | Next.js Server Actions / Route Handlers |
| Banco de dados           | PostgreSQL                              |
| Plataforma               | Supabase                                |
| Autenticação             | Supabase Auth                           |
| Autorização              | PostgreSQL RLS                          |
| QR Code                  | `qrcode.react`                          |
| Compressão de imagens    | `browser-image-compression`             |
| Processamento de imagens | `sharp`                                 |
| Linguagem                | TypeScript                              |

### Arquitetura

O Buteco foi projetado como uma aplicação web full-stack, mantendo o máximo possível da lógica próxima ao domínio da aplicação e utilizando o PostgreSQL como camada central de persistência e controle de acesso.

```text
┌─────────────────────────────────────────────────────┐
│                    BUTECO APP                       │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Proprietário                 Cliente               │
│       │                          │                  │
│       │ Dashboard                │ QR / Link        │
│       ▼                          ▼                  │
│  ┌───────────┐             ┌──────────────┐        │
│  │ Next.js   │             │ Página       │        │
│  │ App       │             │ Pública      │        │
│  └─────┬─────┘             └──────┬───────┘        │
│        │                            │                │
│        └────────────┬───────────────┘                │
│                     ▼                                │
│              ┌─────────────┐                        │
│              │   Supabase  │                        │
│              ├─────────────┤                        │
│              │ PostgreSQL  │                        │
│              │ Auth        │                        │
│              │ Storage     │                        │
│              │ RLS         │                        │
│              └─────────────┘                        │
│                                                     │
└─────────────────────────────────────────────────────┘
```

Uma decisão importante do projeto é que o cliente **não recebe acesso direto às tabelas do banco**.

A consulta pública passa por uma função específica, `comanda_publica(token)`, evitando que um usuário anônimo consiga enumerar comandas ou dados de outros estabelecimentos apenas por possuir a chave pública da aplicação.

---

## Princípios técnicos

Algumas decisões são consideradas fundamentais nos nossos projetos.

### Precisão antes de conveniência

Valores monetários não são armazenados como ponto flutuante.

No Buteco, dinheiro é representado como **inteiro em centavos**, evitando problemas clássicos de precisão numérica.

```text
R$ 12,50
   ↓
1250 centavos
```

### Segurança no banco

Autenticação e autorização não são consideradas apenas responsabilidades do frontend.

Quando possível, as próprias regras de acesso são reforçadas no banco através de **Row Level Security (RLS)**.

### Menor privilégio

O fato de uma aplicação possuir uma chave pública não significa que ela deve possuir acesso irrestrito aos dados.

A arquitetura procura expor somente aquilo que cada fluxo realmente precisa.

### Simplicidade para o usuário

Tecnologia não deve aparecer onde não precisa.

No Buteco, o cliente não precisa:

* instalar aplicativo;
* criar conta;
* lembrar senha;
* procurar o estabelecimento;
* aprender uma interface complexa.

Ele simplesmente escaneia o QR Code e vê sua conta.

---

## Estrutura do Buteco

```text
app/
├── (auth)/
│   └── login/                  # Entrada por Magic Link
│
├── (dashboard)/
│   ├── dashboard/              # Resumo e comandas
│   ├── comanda/
│   │   ├── nova/               # Nova comanda
│   │   └── [id]/               # Gestão da comanda
│   └── produtos/               # Catálogo de produtos
│
├── c/
│   └── [token]/                # Página pública do cliente
│
├── api/
│   └── produtos/
│       └── imagem/             # Processamento de imagens
│
├── actions/                    # Server Actions
│
components/                     # Componentes compartilhados
lib/                            # Infraestrutura e utilidades
supabase/
└── migrations/                 # Schema versionado

proxy.ts                        # Renovação de sessão
```

---

## Documentação

O código é apenas uma parte dos projetos.

Para o Buteco, mantemos documentação de arquitetura, decisões técnicas, diagramas e wireframes.

* **Arquitetura técnica:** `ButecoApp - Arquitetura Tecnica.docx`
* **Diagramas e wireframes:** `docs/LINKS.md`

---

## Como executar o Buteco

### 1. Criar o projeto no Supabase

Crie um projeto no [Supabase](https://supabase.com/).

O plano gratuito é suficiente para desenvolvimento e testes iniciais.

Depois, abra o **SQL Editor** e execute:

```text
supabase/migrations/0001_init.sql
```

O `0001_init.sql` representa o schema completo e idempotente do projeto, incluindo:

* tabelas;
* relacionamentos;
* índices;
* políticas RLS;
* função de acesso público;
* bucket de imagens;
* grants necessários.

As migrations `0002`, `0003` e `0004` são correções históricas destinadas a instalações antigas.

Em uma instalação nova, o `0001_init.sql` já representa o estado final esperado.

---

### 2. Configurar as variáveis de ambiente

Copie o arquivo de exemplo:

```bash
cp .env.example .env.local
```

Preencha as credenciais do projeto Supabase.

Depois:

```bash
npm install
npm run dev
```

A aplicação estará disponível em:

```text
http://localhost:3000
```

---

### 3. Configurar autenticação

No Supabase:

```text
Authentication
└── URL Configuration
```

Adicione a URL de callback:

```text
http://localhost:3000/auth/callback
```

Também deve ser cadastrada a URL correspondente ao ambiente de produção.

---

## Desenvolvimento

Scripts principais:

```bash
npm run dev       # Desenvolvimento
npm run build     # Build de produção
npm start         # Executa o build
npx eslint .      # Lint
```

---

## Ecossistema

A Fiori & Spineli não é definida por uma única tecnologia.

Os projetos individuais podem utilizar stacks diferentes conforme o problema.

Entre as tecnologias e áreas que fazem parte do nosso ecossistema estão:

```text
Frontend
├── TypeScript
├── React
├── Next.js
├── Vite
├── Tailwind CSS
└── Flutter

Backend
├── Python
├── APIs REST
├── Server Actions
└── Integrações

Dados
├── PostgreSQL
├── SQL
├── Data Modeling
├── Data Science
└── Machine Learning

Infraestrutura
├── Git
├── GitHub
├── CI/CD
├── Linux
└── Cloud Services
```

A escolha da tecnologia é consequência do problema, não o contrário.

---

## Quem está por trás

### Lucas Fiori

Atuação entre **dados e desenvolvimento de software**, com interesse em Data Science, Machine Learning, desenvolvimento de aplicações e bancos de dados.

Projetos pessoais incluem aplicações em Python e Dart, análise de dados e projetos acadêmicos envolvendo dados e machine learning.

**GitHub:** [@fiori007](https://github.com/fiori007)
**Linkedin:** [Lucas Fiori](https://www.linkedin.com/in/lucas-fiori/)

---

### Samuel Spineli

**Software Developer** com formação em Ciência da Computação e experiência em engenharia de software, arquitetura de aplicações, desenvolvimento web, APIs, bancos de dados e infraestrutura.

Entre seus projetos estão aplicações web e mobile, sistemas de gerenciamento, ferramentas musicais, projetos de machine learning e aplicações desktop.

**GitHub:** [@samuelspineli34](https://github.com/samuelspineli34)
**Linkedin:** [Samuel Spineli](https://www.linkedin.com/in/samuel-spineli/)

---

## Filosofia

A Fiori & Spineli nasceu de uma ideia simples:

> **Boas soluções começam entendendo o problema, não escolhendo a tecnologia.**

Por isso, nossos projetos procuram equilibrar três coisas:

```text
              ┌───────────────┐
              │    PROBLEMA   │
              └───────┬───────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
   ┌─────────────┐         ┌─────────────┐
   │   PRODUTO   │◄────────│ TECNOLOGIA  │
   └──────┬──────┘         └─────────────┘
          │
          ▼
   ┌─────────────┐
   │   PESSOAS   │
   └─────────────┘
```

Não queremos apenas escrever código.

Queremos entender o contexto, modelar o problema, construir a solução e descobrir o que acontece quando ela encontra usuários reais.

---

## Roadmap

O Buteco é apenas o começo.

Nossa intenção é continuar desenvolvendo produtos e experimentos dentro da organização, explorando diferentes problemas, tecnologias e modelos de software.

```text
                    Fiori & Spineli
                          │
          ┌───────────────┼───────────────┐
          │               │               │
       Produtos        Experimentos       Dados
          │               │               │
          ▼               ▼               ▼
       Buteco        Protótipos       Analytics
          │               │               │
          └───────────────┼───────────────┘
                          │
                          ▼
                     Novos produtos
```

Projetos futuros podem envolver:

* aplicações SaaS;
* ferramentas para pequenos negócios;
* automação;
* análise de dados;
* aplicações inteligentes;
* ferramentas para desenvolvedores;
* experimentos com novas tecnologias.

---

## Repositórios

Os projetos públicos da organização ficam disponíveis no GitHub:

**[github.com/fiori-spineli](https://github.com/fiori-spineli)**

Cada repositório possui sua própria documentação, stack e decisões arquiteturais.

---

## Licença

A licença de cada projeto é definida individualmente em seu respectivo repositório.

---

<div align="center">

**Fiori & Spineli**

*Software, dados e ideias transformadas em produtos.*

</div>
