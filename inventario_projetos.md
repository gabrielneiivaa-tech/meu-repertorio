# Inventário dos Projetos de Automação

Todos os projetos abaixo estão versionados como repositórios privados na conta do GitHub: **[gabrielneiivaa-tech](https://github.com/gabrielneiivaa-tech)**.

---

### 1. `contrato-d4`
- **Repositório:** [https://github.com/gabrielneiivaa-tech/contrato-d4](https://github.com/gabrielneiivaa-tech/contrato-d4)
- **Objetivo:** Robô em Python + Playwright que automatiza o envio de contratos em lote para a plataforma D4Sign.
- **Funcionalidades:**
  - Leitura da planilha mestre de pagamentos/contratos (`Pagtos_Contratos_2026.xlsx`).
  - Associação automática do e-mail do fornecedor e dos signatários fixos (Coordenação, Diretoria, Aprovação).
  - Upload automatizado do PDF, configuração da ordem de assinaturas e disparo.
  - Atualização do status de envio na planilha.

---

### 2. `prestacao-de-contas`
- **Repositório:** [https://github.com/gabrielneiivaa-tech/prestacao-de-contas](https://github.com/gabrielneiivaa-tech/prestacao-de-contas)
- **Objetivo:** Plataforma completa com dashboard Streamlit e múltiplos robôs de validação e lançamento.
- **Funcionalidades:**
  - Consulta automática de autenticidade fiscal (DANFE nacional, NF Paulistana SP e emissor nacional).
  - Automação de lançamentos no portal de gestão Bússola.
  - Gestão de deslocamento, conferência de despesas e geração de relatórios de prestação.

---

### 3. `automacao-notas-fiscais`
- **Repositório:** [https://github.com/gabrielneiivaa-tech/automacao-notas-fiscais](https://github.com/gabrielneiivaa-tech/automacao-notas-fiscais)
- **Objetivo:** Pipeline de processamento, carimbo e organização de notas fiscais em PDF.
- **Funcionalidades:**
  - Workflows automatizados com n8n (configurado localmente com Docker Compose).
  - Scripts PowerShell para leitura e categorização de notas.
  - Carimbo digital de PDFs usando bibliotecas `iTextSharp` e `BouncyCastle`.

---

### 4. `tabela-notas-fiscais`
- **Repositório:** [https://github.com/gabrielneiivaa-tech/tabela-notas-fiscais](https://github.com/gabrielneiivaa-tech/tabela-notas-fiscais)
- **Objetivo:** Consolidação e auditoria dos dados de notas fiscais recebidas.
- **Funcionalidades:**
  - Cruzamento de dados fiscais com relatórios de pagamentos.
  - Tratamento de inconsistências cadastrais e valores divergentes.

---

### 5. `reembolso`
- **Repositório:** [https://github.com/gabrielneiivaa-tech/reembolso](https://github.com/gabrielneiivaa-tech/reembolso)
- **Objetivo:** Organizador e processador de pedidos de reembolso de despesas operacionais.
- **Funcionalidades:**
  - Classificação de comprovantes e recibos.
  - Geração de resumos financeiros e controle de aprovações.
