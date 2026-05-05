# 💰 HL Tech Finance v1.00

<div align="center">
  <img src="src/assets/logo.png" alt="HL Tech Finance Logo" width="200"/>
  <p><em>Sistema de Gestão Financeira Multi-Loja</em></p>
</div>

## 📋 Sobre

O **HL Tech Finance** é um sistema de gestão financeira para pequenos negócios, desenvolvido em Python com Streamlit. Roda localmente como aplicativo Windows (.exe), sem depender de internet ou servidores externos.

Suporta múltiplas lojas, controle de fiados, gestão de produtos e backup automático de dados.

## ✨ Funcionalidades

| Módulo | O que faz |
|---|---|
| 📊 **Dashboard** | Métricas do dia e do mês, gráficos de desempenho |
| 💰 **Vendas** | Registro de vendas com múltiplas formas de pagamento |
| 💸 **Despesas** | Controle de gastos por categoria |
| 👥 **Clientes** | Cadastro e histórico de clientes |
| 💳 **Créditos (Fiados)** | Controle de fiados com vencimento e alertas |
| 📦 **Produtos** | Catálogo com estoque e precificação |
| 🏪 **Multi-loja** | Dados separados por loja, troca rápida na sidebar |
| 💾 **Backup** | Automático ao abrir e fechar, rotação de 30 dias |
| 🎨 **Temas** | Temas visuais configuráveis |

## 🚀 Instalação (Windows)

Baixe o instalador `HLTechFinance_Setup_v1.0.0.exe` e execute. O app será instalado sem necessidade de permissão de administrador.

Na primeira execução, o banco de dados é criado automaticamente em:
```
%APPDATA%\HLTechFinance\finance.db
```

## 🛠️ Desenvolvimento local

### Pré-requisitos
- Python 3.10+
- pip

### Setup

```bash
git clone https://github.com/LucasArlen/hltech-finance-v1.00.git
cd hltech-finance-v1.00
pip install -r requirements.txt
streamlit run app.py
```

### Build (Windows)

Pré-requisitos: Python 3.10+, PyInstaller e [Inno Setup 6](https://jrsoftware.org/isdl.php).

**Forma mais fácil — duplo clique em `build.bat`:**

```
build.bat
```

O script detecta automaticamente o Python, PyInstaller e o Inno Setup instalados na máquina, limpa builds anteriores, compila o EXE e gera o instalador. Funciona em qualquer PC — sem configuração de caminhos.

O instalador é gerado em:
```
HLBuild8installer\HLTechFinance_Setup_v1.0.0.exe
```

**Forma manual (avançado):**

```bash
# Gerar EXE
pyinstaller hl_finance.spec --distpath HLBuild8dist --workpath HLBuild8build --noconfirm

# Gerar instalador (Inno Setup detecta os caminhos automaticamente pelo installer.iss)
"C:\Program Files (x86)\Inno Setup 6\ISCC.exe" installer.iss
```

## 🔄 Migração do Mercatta App

Se você usava o Mercatta App anteriormente, o HL Tech Finance detecta automaticamente o banco de dados antigo e migra os dados na primeira execução. Também é possível rodar manualmente:

```bash
python scripts/migrate_from_mercatta.py "Nome da Loja"
```

## 💾 Backup

- **Automático ao abrir**: uma vez por dia
- **Automático ao fechar**: sempre que o app é encerrado
- **Retenção**: últimos 30 dias
- **Local**: `%APPDATA%\HLTechFinance\backups\`
- **Manual e download**: Configurações → Backup

## 📁 Estrutura do projeto

```
hltech-finance-v1.00/
├── app.py                        # Entrada principal
├── launcher.py                   # Launcher do EXE (abre navegador, backup ao fechar)
├── hl_finance.spec               # Config PyInstaller
├── installer.iss                 # Config Inno Setup
├── requirements.txt
├── src/
│   ├── components/               # Sidebar, topbar, layout
│   ├── config/                   # Temas e constantes
│   ├── core/
│   │   ├── database.py           # Engine SQLAlchemy + migrações automáticas
│   │   ├── license.py            # Validação de licença
│   │   ├── models/               # Sale, Expense, Customer, Credit, Produto, Store
│   │   ├── services/
│   │   │   └── data_service.py   # Camada única de acesso a dados
│   │   └── theme_manager.py
│   ├── pages/                    # Dashboard, Vendas, Despesas, Clientes, Créditos, Produtos, Configurações
│   └── utils/
├── scripts/
│   ├── backup_database.py        # Backup, rotação e restore
│   └── migrate_from_mercatta.py  # Migração do banco antigo
└── data/                         # finance.db (desenvolvimento local)
```

## 🛣️ Roadmap

- [x] Multi-loja
- [x] Controle de fiados com vencimento
- [x] Backup automático ao abrir e fechar
- [x] Migração do Mercatta App
- [x] Alertas de estoque baixo e fiados vencidos
- [x] Venda desconta estoque automaticamente
- [x] Exportação de relatórios para Excel
- [x] Autenticação multi-usuário

## 📄 Licença

Proprietário — todos os direitos reservados. Uso autorizado mediante licença HL Tech.
