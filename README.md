<div align="center">

# 🏭 Enterprise IT Asset Manager
### Sistema de Inventário de TI — Hebron Indústria Farmacêutica

[🇺🇸 English](#-english) | [🇧🇷 Português](#-português)

![Java](https://img.shields.io/badge/Java-17+-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Supabase-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-Local_Cache-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production-brightgreen?style=for-the-badge)

</div>

---

> [!IMPORTANT]
> **🔒 Proprietary Software Notice / Aviso de Software Proprietário**
>
> **English:** This repository serves as a **showcase/portfolio entry**. The source code was developed exclusively for **Hebron (Pharmaceutical/Chemical Industry)** and cannot be shared publicly due to Non-Disclosure Agreements (NDA) and security policies. However, the **architecture**, **UI design**, and **technical documentation** are presented here to demonstrate technical capabilities.
>
> **Português:** Este repositório serve como uma **vitrine de portfólio**. O código-fonte foi desenvolvido exclusivamente para a **Hebron (Indústria Farmacêutica/Química)** e não pode ser compartilhado publicamente devido a acordos de confidencialidade (NDA). No entanto, a **arquitetura**, o **design** e a **documentação técnica** são apresentados aqui para demonstrar capacidades técnicas.

---

<div id="-english"></div>

## 🇺🇸 English

> **A robust Java desktop application for comprehensive IT asset management, featuring an offline-first architecture, real-time cloud synchronization, and a modern Swing interface.**

### 🚀 Overview

This project serves as a central hub for managing IT infrastructure inventory. **It is currently deployed in production at Hebron's IT department**, managing assets across multiple departments and locations.

Unlike spreadsheets, this is a **dedicated desktop application** that ensures data integrity, multi-user access control, and full audit trails — all wrapped in a modern interface powered by **FlatLaf**.

### 🏗️ Architecture

The application follows an **Offline-First** design pattern with **MVC (Model-View-Controller)** architecture:

```
┌─────────────┐     ┌──────────────┐     ┌──────────────────────────┐
│   View      │────▶│  Controller  │────▶│        Model             │
│  (Swing UI) │◀────│              │◀────│  ┌─────────┐ ┌────────┐  │
│             │     │              │     │  │ SQLite  │ │Supabase│  │
│ • LoginPanel│     │• Inventory   │     │  │(Offline)│◀▶│(Cloud) │  │
│ • Dashboard │     │  Controller  │     │  └─────────┘ └────────┘  │
│ • Sidebar   │     │• Login       │     │                          │
│ • TopBar    │     │  Controller  │     │  DatabaseHelper          │
│ • Forms     │     │              │     │  (Singleton Connection)  │
└─────────────┘     └──────────────┘     └──────────────────────────┘
```

**Offline-First Strategy:**
- All operations write to **SQLite** (local) first, ensuring the app works without internet.
- A background **sync engine** pushes changes to **Supabase (PostgreSQL)** when connectivity is available.
- Data is pulled from the cloud on startup to keep local cache fresh.
- Restored backup data is kept **sync-blocked until manual reconciliation**, preventing accidental duplicate uploads to the cloud.

### 📂 Project Structure

```text
InventarioHB2/
├── config.properties               # 🔒 Database credentials (gitignored)
├── lib/                             # External dependencies
│   ├── flatlaf-3.7.jar              #    Modern UI theme
│   ├── postgresql-42.7.7.jar        #    PostgreSQL JDBC driver
│   ├── sqlite-jdbc-3.48.0.0.jar     #    SQLite JDBC driver
│   └── slf4j-*.jar                  #    Logging framework
│
├── src/
│   ├── controller/                  # Business Logic Layer
│   │   ├── InventoryController.java #    Asset CRUD, search, sync, CSV import/export
│   │   └── LoginController.java     #    Authentication, user registration
│   │
│   ├── model/                       # Data Layer
│   │   ├── DatabaseHelper.java      #    Dual-database manager (SQLite + PostgreSQL)
│   │   ├── Computer.java            #    Asset entity (16 fields including lifecycle)
│   │   ├── HistoryEntry.java        #    Audit log entry
│   │   └── User.java                #    User entity with hashed passwords
│   │
│   ├── view/                        # Presentation Layer (15 components)
│   │   ├── MainApp.java             #    Application entry point & frame manager
│   │   ├── LoginPanel.java          #    Login screen with branding
│   │   ├── InventoryPanel.java      #    Main inventory table with filters
│   │   ├── SidebarPanel.java        #    Navigation sidebar with action buttons
│   │   ├── TopBarPanel.java         #    Search bar, stats, location filter
│   │   ├── ComputerFormHandler.java #    Asset registration/edit form (16 fields)
│   │   ├── ComputerTableModel.java  #    JTable data model
│   │   ├── RecycleBinPanel.java     #    Soft-deleted assets management
│   │   ├── HistoryWindow.java       #    Audit history viewer
│   │   ├── UserManagementDialog.java#    User CRUD (admin only)
│   │   ├── RegisterDialog.java      #    New user registration
│   │   ├── ModernIcon.java          #    Custom vector icon system (13 icons)
│   │   └── ...                      #    Additional UI components
│   │
│   ├── util/                        # Utilities
│   │   ├── CSVExporter.java         #    CSV import/export + template generation
│   │   └── UpdateManager.java       #    Auto-update via GitHub Releases API
│   │
│   └── resources/
│       └── images/                  #    Logos, icons
│
├── data_cache/                      # 🔒 Local SQLite database (gitignored)
└── README.md
```

### ⚙️ Key Features

| Category | Feature | Description |
|----------|---------|-------------|
| **Asset Management** | CRUD Operations | Full create, read, update, and delete for IT assets (16 tracked fields) |
| | Soft Delete & Recycle Bin | Safe deletion with full restoration capability |
| | Activity Status | Track assets as Active/Inactive with visual indicators |
| **Data Import/Export** | CSV Export | Export full inventory or filtered results to CSV |
| | CSV Import (Bulk) | Professional import wizard: download template → fill in Excel → import |
| | Template Generation | Auto-generates CSV template with headers and example data |
| | Safe Restore Guard | Restored local backups require explicit reconciliation before cloud sync is allowed |
| **Sync & Connectivity** | Offline-First | Full functionality without internet — SQLite local cache |
| | Cloud Sync | Background sync to Supabase PostgreSQL when online |
| | Sync Status Indicators | Visual icons showing sync state per asset |
| **Security** | PBKDF2 Password Hashing | New passwords use PBKDF2 and legacy SHA-256/plain-text entries are migrated transparently |
| | Externalized Credentials | Database secrets in `config.properties`, not in code |
| | Role-Based Access | Admin vs regular user permissions |
| **Audit & History** | Action Logging | Every create, edit, delete is logged with user, timestamp, and description |
| | History Export | Export audit logs to CSV |
| **UI/UX** | Modern Interface | FlatLaf theme with custom vector icons |
| | Dashboard Stats | Real-time counters: Total, Active, Inactive assets |
| | Multi-Filter Search | Search + location filter + status filter, combinable |
| | Auto-Updates | Checks GitHub Releases for new versions on startup |

### 💻 Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Language** | Java 17+ | Core application |
| **GUI** | Swing + FlatLaf 3.7 | Modern desktop UI |
| **Local DB** | SQLite 3.48 | Offline cache & primary data store |
| **Cloud DB** | PostgreSQL (Supabase) | Cloud sync & multi-device support |
| **Connectivity** | JDBC (Singleton Pattern) | Database connections |
| **Security** | PBKDF2, SHA-256 legacy migration, java.security | Password hashing and migration |
| **Updates** | GitHub Releases API | Auto-update mechanism |
| **Architecture** | MVC + Offline-First | Scalability & resilience |

### 🔐 Security Measures
- **No hardcoded credentials** — database secrets loaded from external `config.properties`
- **PBKDF2 password hashing** for current passwords, with automatic migration from legacy SHA-256/plain-text
- **SQL injection prevention** using Prepared Statements throughout
- **Restore safety guard** — restored local backups block synchronization until manual reconciliation, reducing duplicate remote records
- **Sensitive files gitignored** — `config.properties`, `data_cache/` excluded from VCS

### 📸 Screenshots
<div align="center">

  <!-- Adicione screenshots aqui -->
  <!-- <img src="screenshots/login.png" alt="Login Screen" width="400"> -->
  <!-- <img src="screenshots/dashboard.png" alt="Dashboard" width="800"> -->
  <!-- <img src="screenshots/import_dialog.png" alt="CSV Import" width="400"> -->

</div>

---

<div id="-português"></div>

## 🇧🇷 Português

> **Uma aplicação desktop Java robusta para gerenciamento completo de ativos de TI, com arquitetura offline-first, sincronização em tempo real com a nuvem e interface Swing moderna.**

### 🚀 Resumo

Este projeto serve como hub central para o gerenciamento do inventário de infraestrutura de TI. **Atualmente está implantado em produção no departamento de TI da Hebron**, gerenciando ativos em múltiplos departamentos e locais.

Diferente de planilhas, esta é uma **aplicação desktop dedicada** que garante integridade dos dados, controle de acesso multiusuário e auditoria completa — tudo em uma interface moderna com **FlatLaf**.

### 🏗️ Arquitetura

A aplicação segue o padrão **Offline-First** com arquitetura **MVC (Model-View-Controller)**:

- **Offline-First:** Todas as operações gravam primeiro no **SQLite** (local), garantindo funcionamento sem internet.
- **Sync em Background:** Um motor de sincronização envia alterações ao **Supabase (PostgreSQL)** quando há conectividade.
- **Dados frescos:** O cache local é atualizado com dados da nuvem ao iniciar a aplicação.
- **Restore protegido:** bases restauradas a partir de backup ficam bloqueadas para sincronização até reconciliação manual, evitando duplicações na nuvem.

Consulte a [seção em inglês](#-project-structure) acima para a estrutura completa de arquivos.

### ⚙️ Funcionalidades Principais

| Categoria | Funcionalidade | Descrição |
|-----------|---------------|-----------|
| **Gestão de Ativos** | Operações CRUD | Criação, leitura, atualização e exclusão completa (16 campos rastreados) |
| | Soft Delete e Lixeira | Exclusão segura com restauração completa |
| | Status de Atividade | Rastreamento Ativo/Inativo com indicadores visuais |
| **Importação/Exportação** | Exportar CSV | Exporta inventário completo ou filtrado para CSV |
| | Importar CSV (em lote) | Wizard profissional: baixar modelo → preencher no Excel → importar |
| | Geração de Template | Gera modelo CSV com cabeçalhos e dados de exemplo |
| | Restore com Proteção | Backups restaurados exigem reconciliação explícita antes de sincronizar com a nuvem |
| **Sync e Conectividade** | Offline-First | Funcionalidade total sem internet — cache local SQLite |
| | Sync com Nuvem | Sincronização em background com Supabase PostgreSQL |
| **Segurança** | Hash PBKDF2 | Novas senhas usam PBKDF2 e credenciais legadas são migradas de forma transparente |
| | Credenciais Externalizadas | Segredos do banco em `config.properties`, não no código |
| | Controle de Acesso | Permissões diferenciadas: admin vs usuário comum |
| **Auditoria** | Log de Ações | Toda criação, edição e exclusão é registrada com usuário, data/hora e descrição |
| **UI/UX** | Interface Moderna | Tema FlatLaf com ícones vetoriais customizados |
| | Dashboard | Contadores em tempo real: Total, Ativos, Inativos |
| | Busca Multi-Filtro | Pesquisa + filtro de local + filtro de status, combináveis |
| | Auto-Atualização | Verifica novas versões via GitHub Releases API |

### 💻 Tecnologias

| Camada | Tecnologia | Finalidade |
|--------|-----------|------------|
| **Linguagem** | Java 17+ | Aplicação principal |
| **GUI** | Swing + FlatLaf 3.7 | Interface desktop moderna |
| **BD Local** | SQLite 3.48 | Cache offline e armazenamento primário |
| **BD Nuvem** | PostgreSQL (Supabase) | Sincronização e suporte multi-dispositivo |
| **Conectividade** | JDBC (Padrão Singleton) | Conexões de banco de dados |
| **Segurança** | PBKDF2, migração legada de SHA-256, java.security | Hashing e migração de senhas |
| **Atualizações** | GitHub Releases API | Mecanismo de auto-atualização |
| **Arquitetura** | MVC + Offline-First | Escalabilidade e resiliência |

---

<div align="center">

**Developed by Nícolas Oliveira de Araújo**
<br>
IT Infrastructure Professional & Developer @ Hebron
<br>
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/idogmal/)
[![GitHub](https://img.shields.io/badge/GitHub-idogmal-181717?style=flat-square&logo=github)](https://github.com/idogmal)

</div>
