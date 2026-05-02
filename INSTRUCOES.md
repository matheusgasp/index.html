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
> "Aqui está a NF da [fornecedor]" + anexar o PDF ou imagem

**O que acontece:**
1. Leio a NF e converto quantidades para UN (nunca CX)
2. Calculo GM% real com os preços do catálogo
3. Rateio impostos proporcionalmente nos itens (Ygloo, Cream Color)
4. Gero o JSON de importação
5. Você cola no app → aba 📦 NF → Importar

> ⚠️ **Regime de caixa:** a data de emissão no JSON deve ser a data do **pagamento**, não da NF.

---

### 💸 Lançar extrato bancário
> Use para registrar despesas, CMV e financeiros do mês.

**O que falar:**
> "Aqui está o extrato de [mês]" + anexar o PDF + enviar o backup mais recente do app

**O que acontece:**
1. Faço cross-check com o backup para não duplicar lançamentos
2. Identifico e pergunto sobre transações desconhecidas
3. Ignoro automaticamente: rendimentos MP, dinheiro reservado/retirado, transferências internas
4. Gero JSON de despesas + JSONs de NFs pendentes
5. Você importa no app

---

### 📊 Ver DRE / Análise financeira
> Use para entender a situação financeira do mês.

**O que falar:**
> "Como está o DRE de [mês]?" ou "Qual fornecedor tem melhor margem?"

**O que acontece:**
- Leio os dados do Drive e faço a análise
- Não precisa de token nem de deploy

---

### 🛒 Lançar vendas do PDV
> Use para registrar o faturamento do período.

**O que falar:**
> "Aqui estão as vendas de [período]" + dados extraídos do PDV

**O que acontece:**
- Gero o JSON de receitas por categoria (rev_propria, rev_revenda, rev_b2b)
- Você cola no app → aba 💸 Despesas → Importação em lote

---

### 🔧 Ajustar o app
> Use quando quiser mudar algo no sistema (nova funcionalidade, correção de bug).

**O que falar:**
> "Token: ghp_..." + descrição do ajuste + anexar o `index.html` atual se necessário

**O que acontece:**
1. Busco o código, aplico a alteração
2. Gero o `index.html` corrigido para download
3. Você faz upload manual no GitHub

---

## Token do GitHub

Necessário apenas para ajustes no app.

**Como gerar:**
1. Acesse: github.com/settings/tokens/new
2. Note: `claude-deploy`
3. Expiration: `No expiration`
4. Scope: ✅ `repo`
5. Clique em Generate token e cole no início da conversa

> ⚠️ Revogue o token após o uso. Gere um novo na próxima vez.

**Como fazer upload do index.html no GitHub:**
1. Acesse github.com/matheusgasp/index.html
2. Clique no arquivo `index.html`
3. Clique no ícone de lápis (Edit) → "..." → ou vá em "Add file" → "Upload files" na raiz do repo
4. Arraste o novo `index.html`
5. Escreva uma mensagem de commit e clique em "Commit changes"
6. Aguarde ~1 minuto para o GitHub Pages atualizar

---

## Fornecedores e GM% calculadas

| Fornecedor | GM% Real | Base de cálculo |
|---|---|---|
| **Ygloo** (Gelateria Antártica) | 33–43% (média ~37%) | NFs 000.170.710 e 000.169.655 · abril/2026 · com IPI+ICMS-ST rateados |
| **Los Los** (PPPP) | 26–48% (média ~31%) | NF 000.006.000 · abril/2026 · sem impostos adicionais |
| **Cream Color** | a calcular com NFs reais | Compra real = 2× valor NF + impostos sobre 50% |
| **Ice Tasty** | a calcular com NFs reais | Pedidos 1021, 1133, 1165, 1206 |
| **IceGustos** | a calcular com NFs reais | Pedido 1834 |
| **DG Açaizinho** | a calcular com NFs reais | NF 3.194 |
| **Boachá** | estimativa 19–31% | sem NF real ainda |

> GM% serão atualizadas à medida que novas NFs chegarem e os preços de venda forem cruzados.

---

## Observações técnicas

- **Impostos:** Ygloo cobra IPI + ICMS-ST à parte (CST 010) — sempre ratear proporcionalmente no CMV. Los Los embute no preço (CST 060) — sem adicional.
- **Cream Color:** emite NF por 50% do valor real. CMV real = 2× valor unitário da NF + impostos rateados.
- **Preços de venda:** baseados no arquivo `Produtos__18_04_2026.xlsx` do projeto.
- **Storage:** dados salvos em `atacadao_financeiro.json` no Google Drive via Google Apps Script.
- **Backup:** sempre exportar backup antes de restaurar. Cruzar com lançamentos recentes para não perder dados.
- **Valores negativos:** suportados no DRE (implementado 05/2026) — usar para reembolsos e estornos.
- **Unidades:** todas as NFs importadas em UN, nunca CX.
- **Regime de caixa:** CMV e despesas no mês do pagamento. Receitas do PDV lançadas separadamente dos repasses bancários.
