# Portal Contabilidade — LBC Solicitadora

Portal de consulta read-only para a contabilista (Rosália) e Liliana.

## Ficheiros

- `index.html` — o portal completo (tudo num único ficheiro)
- `logo.png` — logo da LBC Solicitadora (já incluído)

## Como testar localmente (antes de publicar)

1. Abrir uma janela de comandos (cmd ou PowerShell)
2. Navegar para a pasta deste portal:
   ```
   cd C:\caminho\para\portal-contabilidade
   ```
3. Iniciar um servidor web local (necessário para o login Microsoft funcionar):
   ```
   python -m http.server 8080
   ```
   (Se não tiver Python: instalar do Microsoft Store ou usar `npx serve -p 8080` se tiver Node.js)
4. Abrir no browser: <http://localhost:8080>
5. Clicar em "Entrar com Microsoft" e usar a sua conta Liliana

## Como publicar no GitHub Pages

1. No GitHub, criar repositório novo: `portal-contabilidade`
   - Visibilidade: pode ser pública (não há segredos no código — o login é feito pelo Azure)
2. Fazer upload deste `index.html` e do `logo.png` para o repositório
3. No GitHub do repositório: **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: **main** / **(root)**
   - Save
4. Aguardar 1-2 minutos. URL será algo como:
   `https://<utilizador>.github.io/portal-contabilidade/`
5. **IMPORTANTE**: depois de saber a URL, voltar ao Azure (Microsoft Entra ID → App registrations → Portal Contabilidade LBC → Authentication) e adicionar essa URL aos **Redirect URIs** (tipo SPA).

## Quem pode entrar

A lista de emails autorizados está no código (constante `EMAILS_AUTORIZADOS`):
- `liliana.cardoso@lbc-solicitadora.pt`
- `rosaliamarques@contasecompanhia.eu`

Para adicionar mais utilizadores, editar essa constante e atualizar o ficheiro no GitHub.
**Atenção:** o utilizador também tem de estar convidado como Guest no Azure AD da LBC para conseguir fazer login.

## Funcionalidades

- 5 cards de métricas (Despesas, Cliente, IVA, Sem fatura, Por conciliar)
- Filtros: mês, ano, tipo, fatura, conta, conciliação
- Lista de movimentos com agrupamentos e tags
- Botão "Ver" para abrir PDFs das faturas
- Exportação Excel: 6 opções (Mês/Ano × Principal/Secundária/Todas)
- Login Microsoft (MSAL.js)
- Tradução automática de links das faturas (do site principal para o site contabilidade)

## O que NÃO tem (intencional)

- Sem botão "+ Novo movimento"
- Sem edição
- Sem conciliação manual
- Sem upload de extratos
- Sem ferramentas admin
- Sem outras tabs (só Contabilidade)
