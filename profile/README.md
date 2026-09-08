<div align="center">

  <img src="https://raw.githubusercontent.com/fiori-spineli/.github/main/logo.png" alt="Fiori & Spineli Logo" width="220" />

  <h1>FIORI & SPINELI</h1>
  <p><strong>Engenharia de Software, Arquitetura de Dados e Desenvolvimento de Produtos Digitais.</strong></p>

  <p>
    <a href="https://github.com/fiori-spineli"><img src="https://img.shields.io/badge/Organização-GitHub-18181B?style=flat-square&logo=github&logoColor=white" alt="GitHub Org" /></a>
    <img src="https://img.shields.io/badge/Foco-Engenharia%20%26%20Dados-4D3A99?style=flat-square" alt="Foco" />
    <img src="https://img.shields.io/badge/Status-Desenvolvimento%20Ativo-3F6B4D?style=flat-square" alt="Status" />
  </p>

</div>

---

### Visão Geral

A **Fiori & Spineli** é uma organização independente dedicada à concepção, modelagem e construção de software resiliente. Fundada por **Lucas Fiori** e **Samuel Spineli**, a iniciativa opera na interseção entre rigor de engenharia de software, arquitetura de dados e usabilidade centrada em problemas reais de mercado.

Nossa operação baseia-se na premissa de que a tecnologia é uma consequência do domínio do problema. Projetamos sistemas que priorizam consistência transacional, baixo atrito para o usuário final, contenção de privilégios e eficiência operacional.

---

### Linhas de Atuação

<table width="100%">
  <tr>
    <td width="50%" valign="top">
      <h4>Engenharia de Aplicações</h4>
      <ul>
        <li>Desenvolvimento full-stack de alta performance (Web e Mobile)</li>
        <li>Arquitetura orientada a serviços e Serverless / Edge Computing</li>
        <li>Projetos Offline-First e interfaces com fricção reduzida</li>
        <li>Design de APIs RESTful e contratos de integração seguros</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h4>Inteligência e Dados</h4>
      <ul>
        <li>Modelagem relacional, indexação e integridade transacional</li>
        <li>Pipelines de processamento, análise e Ciência de Dados</li>
        <li>Integração de modelos de Machine Learning e Inteligência Artificial</li>
        <li>Automação analítica voltada a tomada de decisão</li>
      </ul>
    </td>
  </tr>
</table>

---

### Fundadores e Liderança Técnica

<table width="100%">
  <tr>
    <td width="50%" valign="top">
      <h3>Lucas Fiori</h3>
      <p><strong>Dados, Inteligência Artificial & Engenharia de Aplicações</strong></p>
      <p>Atuação focada na estruturação analítica, modelagem de dados, algoritmos de Machine Learning e desenvolvimento de software orientado a dados. Experiência na concepção de soluções inteligentes, integração de modelos estatísticos e engenharia de pipelines de dados sustentáveis.</p>
      <p>
        <a href="https://github.com/fiori007"><img src="https://img.shields.io/badge/GitHub-fiori007-18181B?style=flat-square&logo=github&logoColor=white" alt="GitHub Lucas Fiori" /></a>
        <a href="https://www.linkedin.com/in/lucas-fiori/"><img src="https://img.shields.io/badge/LinkedIn-Lucas%20Fiori-4D3A99?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn Lucas Fiori" /></a>
      </p>
    </td>
    <td width="50%" valign="top">
      <h3>Samuel Spineli</h3>
      <p><strong>Engenharia de Software, Arquitetura de Sistemas & Performance</strong></p>
      <p>Cientista da Computação com foco em engenharia de sistemas escaláveis, arquitetura de aplicações web/mobile, infraestrutura, modelagem de banco de dados e computação de alta concorrência. Experiência na definição de padrões de projeto e governança técnica de ponta a ponta.</p>
      <p>
        <a href="https://github.com/samuelspineli34"><img src="https://img.shields.io/badge/GitHub-samuelspineli34-18181B?style=flat-square&logo=github&logoColor=white" alt="GitHub Samuel Spineli" /></a>
        <a href="https://www.linkedin.com/in/samuel-spineli/"><img src="https://img.shields.io/badge/LinkedIn-Samuel%20Spineli-4D3A99?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn Samuel Spineli" /></a>
      </p>
    </td>
  </tr>
</table>

---

### Portfólio em Destaque

#### Buteco

SaaS operacional concebido para modernizar a gestão e acompanhamento de contas de consumo de pequeno e médio porte, substituindo controles manuais por um fluxo digital sem atrito de cadastro para o cliente.

* **Acesso Zero-Friction:** Acesso público instantâneo por tokenização e QR Code, sem obrigatoriedade de instalação de software ou autenticação pelo consumidor final.
* **Segurança na Camada de Dados:** Autenticação via Magic Link e isolamento estrito entre locatários suportado por *PostgreSQL Row Level Security (RLS)*.
* **Encapsulamento por RPC:** O cliente anônimo consome os dados exclusivamente através de uma Remote Procedure Call (`comanda_publica(token)`), mitigando varredura e enumeração de dados públicos.
* **Precisão Aritmética:** Tratamento de valores financeiros como inteiros representados em centavos, eliminando desvios de arredondamento de ponto flutuante (*floating point roundoff error*).

```text
+-----------------------------------------------------------------------+
|                              BUTECO APP                               |
+-----------------------------------------------------------------------+
|                                                                       |
|  Estabelecimento (Proprietario)            Cliente Final (Consumidor) |
|         |                                              |              |
|         | Next.js App / Server Actions                 | QR Code / URL|
|         v                                              v              |
|  [ Dashboard Administrativo ]                [ Visao Publica / c/[token] ]
|         |                                              |              |
|         | RLS Policies                                 | RPC Execution|
|         +----------------------+-----------------------+              |
|                                |                                      |
|                                v                                      |
|                   [ PostgreSQL / Supabase Core ]                      |
|                   - Schema Relacional                                 |
|                   - RLS Enforcement                                   |
|                   - Storage com Processamento Sharp                   |
+-----------------------------------------------------------------------+
```

* **Repositório do Produto:** [github.com/fiori-spineli/buteco](https://github.com/fiori-spineli)

---

### Princípios de Engenharia

1. **Rigor Transacional e Domínio do Dado:** 
   O banco de dados é tratado como componente ativo de integridade e segurança, e não como um repositório passivo. Regras fundamentais de autorização são executadas diretamente via banco de dados (Row Level Security e RPCs com restrições explícitas de privilégio).

2. **Eliminação de Atrito Funcional:** 
   Se uma funcionalidade impõe barreiras excessivas para o usuário (instalação compulsória, criação de credenciais para tarefas efêmeras ou passos redundantes), a arquitetura do produto é reformulada.

3. **Modelagem Orientada à Precisão:** 
   Tipagens estritas e manipulação determinística de dados. Decisões técnicas são justificadas por restrições operacionais e eficiência de execução, evitando sobrecarga desnecessária de dependências.

---

### Matriz Tecnológica

<div align="center">

| Domínio | Ferramental e Tecnologias |
| :--- | :--- |
| **Linguagens** | TypeScript, Python, Dart, SQL, C/C++ |
| **Frontend & UI** | Next.js (App Router), React, Vite, Tailwind CSS, Flutter |
| **Backend & APIs** | Server Actions, Node.js, FastAPI, REST Architectures |
| **Bancos de Dados & Storage** | PostgreSQL, Supabase, SQLite, Redis |
| **Dados & Machine Learning** | Pandas, NumPy, Scikit-learn, Modelagem Relacional |
| **Infraestrutura & DevOps** | Git, GitHub Actions, Docker, Linux Systems |

</div>

---

### Estrutura Organizacional

```text
fiori-spineli/
├── Produtos/
│   └── Buteco/                  # Gestao digital de consumo para estabelecimentos
├── Inteligencia-e-Dados/        # Pipelines, modelos de predicao e analise estatistica
├── Componentes-Core/            # Modulos utilitarios, seguranca e bibliotecas base
└── Pesquisa-e-Prototipacao/     # Validacao de hipoteses tecnicas e novos conceitos
```

---

<div align="center">

  <sub>Fiori & Spineli &bull; Organização de Tecnologia e Inovação Independente</sub>

</div>

### Dicas de Configuração no GitHub

1. Para que essa página seja renderizada como a página oficial da organização no GitHub, crie um repositório público chamado exatamente **`.github`** dentro da organização `fiori-spineli`.
2. Salve o conteúdo acima no caminho:
   ```text
   .github/profile/README.md
   ```
3. Crie a pasta `.github/assets/` e adicione o arquivo da sua logo com o nome `logo.png` para que o cabeçalho seja carregado automaticamente sem links quebrados.
