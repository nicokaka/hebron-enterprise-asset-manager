O conteúdo está muito bom em termos de escrita e tom profissional. O que você escreveu passa exatamente a mensagem de maturidade e responsabilidade que empresas da Nova Zelândia buscam.

No entanto, notei que a formatação (Markdown) quebrou na segunda metade do texto que você mandou (especialmente na parte em Português e na lista de Features em inglês). Se você colar do jeito que me mandou, vai ficar tudo como um "blocão de texto" sem tópicos.

Abaixo, fiz a correção técnica da formatação (coloquei as bolinhas, negritos e títulos certos) e adicionei o rodapé que estava faltando.

Pode copiar este bloco inteiro abaixo que está pronto para publicar:

Markdown
<div align="center">

# Enterprise IT Asset Manager
### IT Asset Management & Inventory System

[🇺🇸 English](#-english) | [🇧🇷 Português](#-português)

</div>

---

> [!IMPORTANT]
> **🔒 Proprietary Software Notice / Aviso de Software Proprietário**
>
> **English:** This repository serves as a **showcase/portfolio entry**. The source code was developed exclusively for **Hebron (Pharmaceutical/Chemical Industry)** and cannot be shared publicly due to Non-Disclosure Agreements (NDA) and security policies. However, the **architecture**, **UI design**, and **logic documentation** are presented here to demonstrate technical capabilities.
>
> **Português:** Este repositório serve como uma **vitrine de portfólio**. O código-fonte foi desenvolvido exclusivamente para a **Hebron (Indústria Farmacêutica/Química)** e não pode ser compartilhado publicamente devido a acordos de confidencialidade (NDA). No entanto, a **arquitetura**, o **design** e a **documentação** são apresentados aqui para demonstrar capacidades técnicas.

---

<div id="-english"></div>

## 🇺🇸 English

> **Concept:** A robust **Java** application designed for comprehensive IT asset management, featuring a modern **Swing** interface and real-time synchronization with a **PostgreSQL** cloud database (Supabase).

### 🚀 Overview
This project serves as a central hub for managing IT infrastructure inventory. **It is currently deployed in production at Hebron's IT Infrastructure**, managing assets across multiple departments.

Unlike simple spreadsheets, this is a **dedicated desktop application** that ensures data integrity, multi-user access control, and detailed history tracking. It streamlines the lifecycle management of computers and equipment: from registration and status tracking to maintenance logs and asset retirement (Soft Delete), all wrapped in a sleek interface powered by **FlatLaf**.

### 📂 Project Structure & Architecture
Although the source code is private, the project follows a strict **MVC (Model-View-Controller)** architecture to ensure scalability. Here is the actual file structure used in production:

```text
hebron-enterprise-asset-manager/
├── lib/                        # External Dependencies (FlatLaf UI, PostgreSQL Driver)
├── src/
│   ├── controller/             # Business Logic Layer (Bridges View and Model)
│   │   ├── ComputerController.java
│   │   ├── HistoryController.java
│   │   ├── SyncController.java
│   │   └── UserController.java
│   │
│   ├── database/               # Singleton Connection Logic
│   │   └── DatabaseConnection.java
│   │
│   ├── model/                  # Data Layer
│   │   ├── dao/                # Data Access Objects (SQL Operations)
│   │   │   ├── ComputerDAO.java
│   │   │   ├── HistoryDAO.java
│   │   │   └── UserDAO.java
│   │   └── vo/                 # Value Objects (Entities)
│   │       ├── Computer.java
│   │       ├── HistoryLog.java
│   │       └── User.java
│   │
│   ├── view/                   # Presentation Layer (Swing UI)
│   │   ├── DashboardPanel.java
│   │   ├── InventoryPanel.java
│   │   ├── LoginFrame.java
│   │   ├── MainFrame.java
│   │   └── [Dialogs & Components]...
│   │
│   └── util/                   # Utilities & Security
│       ├── SessionManager.java # User Session Handling
│       ├── ThemeManager.java   # FlatLaf Theme Toggle
│       └── RoundedBorder.java  # Custom UI Components
└── README.md
⚙️ Key Features
Modern UI: Built with Java Swing and FlatLaf for a clean, responsive user experience similar to modern web apps.

Asset Lifecycle Management:

CRUD Operations: Complete Create, Read, Update, and Delete capabilities for IT assets.

Soft Delete: Safely remove items to a "Trash" bin with restoration capabilities, preventing accidental data loss.

Advanced Tracking:

History Logs: Automatically records all user actions (creations, updates, deletions) for full auditability.

Dashboard: Visual metrics for quick insights into asset status (Total, Active, Inactive).

Cloud Integration: Direct connection to Supabase (PostgreSQL) ensuring data is accessible and secure.

💻 Tech Stack
Language: Java

GUI Framework: Swing (with FlatLaf Light Theme)

Database: PostgreSQL (via Supabase)

Connectivity: JDBC with Singleton connection pattern

Architecture: MVC (Model-View-Controller) designed for scalability

Security: SQL Injection Prevention using Prepared Statements

📸 Screenshots
<div align="center"> </div>

<div id="-português"></div>

🇧🇷 Português
Conceito: Uma aplicação Java robusta projetada para o gerenciamento abrangente de ativos de TI, apresentando uma interface Swing moderna e sincronização em tempo real com um banco de dados PostgreSQL na nuvem (Supabase).

🚀 Resumo
Este projeto serve como um hub central para o gerenciamento do inventário de infraestrutura de TI. Atualmente está implantado em produção na Infraestrutura de TI da Hebron, gerenciando ativos em múltiplos departamentos.

Diferente de planilhas simples, esta é uma aplicação desktop dedicada que garante a integridade dos dados, controle de acesso multiusuário e rastreamento detalhado do histórico. Ele otimiza o gerenciamento do ciclo de vida de computadores e equipamentos: desde o registro e rastreamento de status até logs de manutenção e baixa de ativos (Soft Delete).

📂 Estrutura do Projeto e Arquitetura
Embora o código-fonte seja privado, o projeto segue uma rigorosa arquitetura MVC (Model-View-Controller). Veja a estrutura de arquivos real utilizada:

(Veja o diagrama na seção em inglês acima)

⚙️ Funcionalidades Principais
UI Moderna: Construída com Java Swing e FlatLaf para uma experiência de usuário limpa e responsiva.

Gerenciamento do Ciclo de Vida do Ativo:

Operações CRUD: Capacidades completas de Criação, Leitura, Atualização e Exclusão para ativos de TI.

Soft Delete: Remove itens com segurança para uma "Lixeira" com capacidade de restauração, prevenindo perda acidental de dados.

Rastreamento Avançado:

Logs de Histórico: Registra automaticamente todas as ações dos usuários para auditoria completa.

Dashboard: Métricas visuais para insights rápidos sobre o status dos ativos.

Integração em Nuvem: Conexão direta com Supabase (PostgreSQL) garantindo que os dados estejam acessíveis e seguros.

💻 Tecnologias
Linguagem: Java

Framework GUI: Swing (com Tema FlatLaf Light)

Banco de Dados: PostgreSQL (via Supabase)

Conectividade: JDBC com padrão de conexão Singleton

Arquitetura: MVC (Model-View-Controller) projetada para escalabilidade

Segurança: Prevenção contra SQL Injection usando Prepared Statements

<div align="center">

Developed by Nícolas Oliveira de Araújo (nicokaka)


IT Infrastructure Professional & Developer


LinkedIn Profile

</div>
