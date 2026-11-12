# Perfil Técnico do Desenvolvedor

## 👤 Informações Gerais
- **Nome:** Gabriel Neiva
- **E-mail:** gabriel.neiivaa@gmail.com
- **GitHub:** [gabrielneiivaa-tech](https://github.com/gabrielneiivaa-tech)
- **Foco de Atuação:** Automação de Processos de Negócio (RPA), Engenharia de Dados Operacionais, Dashboards de Produtividade e Integrações de Sistemas Administrativos/Financeiros.

---

## 🛠️ Stack Tecnológica Dominada

### 1. Linguagens & Scripts
- **Python (3.10 - 3.12):** Linguagem principal para regras de negócio, raspagem de dados, RPA e automações.
- **PowerShell & Batch (.bat):** Scripts de inicialização rápida, orquestração de rotinas e empacotamento para usuários finais.
- **JavaScript / DOM:** Injeção de scripts no navegador para manipular elementos web complexos ou frameworks legados (jQuery).

### 2. Frameworks & Bibliotecas
- **Playwright (Python):** Escolha número 1 para automação de navegadores modernos (Chromium, Chrome).
- **Pandas / OpenPyXL:** Manipulação de planilhas complexas (.xlsx, .csv), cruzamento de bases, filtros dinâmicos e geração de relatórios.
- **Streamlit:** Construção rápida de dashboards e interfaces visuais para usuários corporativos.
- **iTextSharp / BouncyCastle / PyMuPDF:** Manipulação, carimbo e leitura de documentos em formato PDF.
- **n8n (Workflow Automation):** Orquestração de fluxos de dados, webhooks e integrações automatizadas.

### 3. Ferramentas & Controle de Versão
- **Git & GitHub CLI (`gh`):** Versionamento de código, controle de branches e backup em nuvem de repositórios privados.
- **Docker / Docker Compose:** Execução de serviços locais conteinerizados (ex: instâncias locais de n8n).

---

## 📐 Padrões de Arquitetura e Engenharia Adotados

1. **Separação de Responsabilidades (SoC):**
   - `config.py`: Centraliza todas as URLs, caminhos de rede, listas fixas de emails, seletores e credenciais em variáveis de ambiente.
   - `*_service.py`: Contém a regra de negócio pura (leitura de Excel, filtragem, validação de regras fiscais).
   - `*_browser.py`: Responsável exclusivamente pelas ações do navegador (cliques, inputs, upload, espera de rede).
   - `executar_*.py`: Orquestrador principal que liga os serviços e lida com o ciclo de vida do processo.

2. **Facilidade para o Usuário Final:**
   - Criação de arquivos `.bat` com pausamento final (`pause`), menus interativos e saídas coloridas no terminal.
   - O usuário não precisa saber comandos de terminal: um duplo clique executa toda a rotina.

3. **Tolerância a Falhas e Resiliência em Lote:**
   - Se um contrato ou nota fiscal falhar no processamento, o script grava o erro em log e continua com o próximo item sem travar a fila inteira.
   - Verificação prévia de pré-requisitos (arquivos existem? planilha está aberta no Excel travando a escrita?).

4. **Persistência de Sessão (Browser Context):**
   - Utilização de `user_data_dir` persistente para que o operador só precise fazer login com 2FA uma única vez.
