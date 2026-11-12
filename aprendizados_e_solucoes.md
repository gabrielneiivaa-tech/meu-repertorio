# Aprendizados Práticos e Soluções de Engenharia

Este documento reúne soluções para problemas reais enfrentados e superados durante o desenvolvimento das automações.

---

## 1. Ambientes Corporativos Sem Privilégios de Administrador (Windows)

### Problema:
Instaladores padrão (`.msi`, `winget install`) costumam exigir elevação UAC (`Exit code: 1602` ou bloqueio de TI).

### Solução Consolidada:
- **Git para Windows:** Utilizar o instalador de escopo de usuário ou pacote zip portátil extraído em:
  `C:\Users\<usuario>\AppData\Local\Programs\Git\`
- **GitHub CLI (`gh`):** Baixar o arquivo zip oficial dos releases (`gh_*_windows_amd64.zip`), descompactar em:
  `C:\Users\<usuario>\AppData\Local\Programs\gh\bin`
- **Variáveis de Ambiente:** Adicionar os diretórios ao `Path` do usuário (registro de usuário, sem precisar de permissão de máquina):
  ```powershell
  $userPath = [System.Environment]::GetEnvironmentVariable("Path", "User")
  [System.Environment]::SetEnvironmentVariable("Path", "$userPath;C:\caminho\bin", "User")
  ```

---

## 2. Automação Web Avançada com Playwright

### Caso A: Input de Upload Transparente Sobreposto a Botão
- **Sintoma:** O teste tenta clicar em `<button>Escolher documento</button>`, mas recebe erro `element intercepts pointer events: <input type="file" id="fileupload">`.
- **Solução:** Nunca clicar no botão visual quando houver um `<input type="file">`. Usar diretamente:
  ```python
  page.locator("#fileupload").set_input_files(caminho_arquivo)
  ```

### Caso B: Formulários que usam jQuery FileUpload / Plugins JS Legados
- **Sintoma:** O arquivo é anexado ao `<input>`, mas a barra de progresso ou evento de envio da página não inicia.
- **Causa:** O plugin da página aguarda o evento `.on('change')` do jQuery e não reconhece a atribuição direta do DOM.
- **Solução:** Forçar o disparo do evento através do contexto de execução da página:
  ```python
  page.evaluate("""() => {
      const el = document.querySelector('#fileupload');
      if (window.jQuery) {
          window.jQuery(el).trigger('change');
      } else {
          el.dispatchEvent(new Event('change', { bubbles: true }));
      }
  }""")
  ```

### Caso C: Persistência de Login Sem Expor Senhas
- Em portais com verificação em duas etapas (2FA) ou reCAPTCHA, nunca automatizar a digitação de senha e código.
- Abrir o navegador com perfil persistente (`user_data_dir="./browser_profile"`), pausar o script para o usuário logar manualmente no primeiro uso, e nas próximas execuções a sessão estará salva.

---

## 3. Manipulação de Planilhas e Arquivos Fiscais

### Cuidados com Excel (`openpyxl` / `pandas`):
- Se uma planilha estiver aberta no Excel pelo usuário, o Windows bloqueia a escrita (`PermissionError: [Errno 13] Permission denied`).
- **Padrão:** Sempre encapsular gravações com `try/except` avisando especificamente para o usuário fechar o arquivo Excel antes de tentar novamente.
- Colunas com fórmulas devem ser lidas com `data_only=True` no `openpyxl` para obter os valores calculados e não o texto da fórmula.

---

## 4. Orquestração e Integração (n8n & Scripts)
- O uso de n8n local via Docker Compose permite construir rotinas assíncronas com gatilhos de webhook e pastas monitoradas (*file watchers*).
- Empacotar comandos repetitivos em arquivos `.bat` na raiz dos projetos garante que qualquer pessoa da equipe consiga operar os robôs sem instalar ambientes de desenvolvimento complexos.
