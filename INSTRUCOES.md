# Atacadão do Sorvete · Instruções de Uso

## Links importantes
- **App:** https://matheusgasp.github.io/index.html/
- **Drive (dados):** arquivo `atacadao_financeiro.json` no seu Google Drive
- **Repositório:** https://github.com/matheusgasp/index.html

---

## Como iniciar cada tipo de conversa

### 📦 Lançar NF
> Use quando chegar uma nota fiscal de compra.

**O que falar:**
> "Aqui está a NF da [fornecedor]" + anexar o PDF

**O que acontece:**
1. Eu leio a NF, calculo GM% real com os preços do catálogo
2. Gero o JSON de importação
3. Você cola no app → aba 📦 NF → Importar
4. Se quiser deploy automático: cole o token do GitHub no início da conversa

**Para deploy automático, comece a conversa assim:**
> "Token: ghp_..." + "Aqui está a NF..."

---

### 📊 Ver DRE / Análise financeira
> Use para entender a situação financeira do mês.

**O que falar:**
> "Como está o DRE de [mês]?" ou "Qual fornecedor tem melhor margem?"

**O que acontece:**
- Eu leio os dados do Drive e faço a análise
- Não precisa de token nem de deploy

---

### 🛒 Lançar vendas
> Use para registrar o faturamento do dia ou da semana.

**O que falar:**
> "Vendi R$ X hoje em revenda" ou "Registra as vendas da semana"

**O que acontece:**
- Eu gero o JSON de venda
- Você cola no app → aba 🛒 Vendas

---

### 🔧 Ajustar o app
> Use quando quiser mudar algo no sistema (novo fornecedor, novo campo, nova tela).

**O que falar:**
> "Quero adicionar [funcionalidade]" ou "Tem um bug em [tela]"

**Para deploy automático, comece assim:**
> "Token: ghp_..." + descrição do ajuste

---

## Token do GitHub

O token é necessário apenas quando eu precisar fazer deploy (subir nova versão do app).

**Como gerar um novo token:**
1. Acesse: github.com/settings/tokens/new
2. Note: `claude-deploy`
3. Expiration: `No expiration`
4. Scope: ✅ `repo`
5. Clique em Generate token e cole no início da conversa

> ⚠️ Revogue o token depois de usar se preferir mais segurança.
> Gere um novo na próxima vez que precisar de deploy.

---

## Fornecedores e GM% calculadas

| Fornecedor | GM% Real | Base de cálculo |
|---|---|---|
| Gelateria Antártica | 33–43% (média 36,9%) | NF 000.170.710 · abril/2026 · com IPI+ICMS-ST |
| Los Los (PPPP) | 26–48% (média 31,0%) | NF 000.006.000 · abril/2026 · sem impostos adicionais |
| Cream Color | 30–45% | estimativa (sem NF real ainda) |
| Ice Tasty | 30–50% | estimativa (sem NF real ainda) |
| Icegustos | 38–47% | estimativa (sem NF real ainda) |
| Boa Chá | 19–31% | estimativa (sem NF real ainda) |
| DG Açaizinho | 43–58% | estimativa (sem NF real ainda) |

> À medida que novas NFs chegarem, as GM% serão recalculadas com dados reais.

---

## Observações técnicas

- **Impostos:** Gelateria Antártica cobra IPI + ICMS-ST à parte (CST 010) — sempre incluir no CMV. Los Los já embute o ICMS-ST no preço (CST 060) — não há adicional.
- **Preços de venda:** baseados no arquivo `Produtos__18_04_2026.xlsx` do projeto.
- **Storage:** dados salvos em `atacadao_financeiro.json` no Google Drive via Google Apps Script.
