# Plano de Experimentos — Crawler AI TCC

## Contexto

O sistema Crawler AI está funcional end-to-end (pipeline LLM). O módulo baseline (scraping tradicional) ainda não existe. Os experimentos compararão as duas abordagens em 15 URLs distribuídas em 3 categorias, com resultados registrados em planilha Excel/Google Sheets. A entrega é em 15/06/2026.

---

## Visão Geral das Etapas

1. Selecionar e documentar as 15 URLs + construir gabarito
2. Implementar módulo baseline no worker Python
3. Criar script de benchmark que roda ambas as abordagens
4. Executar experimentos e preencher planilha
5. Usar os dados para escrever o Cap. 6 (Resultados)

---

## Etapa 1 — Seleção de URLs e Gabarito

### Critérios de seleção
- Sites públicos, sem login
- Mistura de conteúdo estático e dinâmico (JS)
- Sites conhecidos e estáveis (menor risco de mudar durante os experimentos)
- Preferência por sites em português (contexto real do usuário)

### Sugestões de URLs por categoria

**Categoria A — E-commerce** (campos: nome, preço_atual, preço_original, disponível, avaliação)
- Americanas (produto específico)
- Mercado Livre (produto específico)
- Magazine Luiza (produto específico)
- Shopee (produto específico)
- Amazon Brasil (produto específico)

**Categoria B — Notícias** (campos: título, autor, data_publicação, veículo, resumo)
- G1 (artigo específico)
- UOL Notícias (artigo específico)
- Folha de S.Paulo (artigo específico)
- BBC Brasil (artigo específico)
- Agência Brasil (artigo específico)

**Categoria C — Dados Tabulares** (campos: lista de itens com posição, nome, atributo)
- IBGE (tabela de dados)
- Ranking de universidades (QS ou similar)
- Tabela da Bolsa de Valores (B3)
- Wikipedia (tabela estruturada)
- transfermarkt.com.br (tabela de jogadores)

### Gabarito manual
Para cada URL, inspecionar a página e preencher manualmente os valores corretos de cada campo em uma aba "Gabarito" da planilha. Esse gabarito é a fonte da verdade para calcular acurácia.

---

## Etapa 2 — Implementar Módulo Baseline

### O que criar no projeto (worker Python)

**`worker/baseline/extractor.py`**
```python
class BaselineExtractor:
    def extract(self, html: str, url: str, schema: dict) -> dict:
        # Carrega seletores do arquivo de config para essa URL
        # Aplica BeautifulSoup com os seletores
        # Retorna mesmo formato que o pipeline LLM
        ...
```

**`worker/baseline/selectors.json`**
```json
{
  "https://url-do-site.com/produto": {
    "nome": "h1.product-title",
    "preco_atual": "span.price-value",
    "disponivel": "#stock-status"
  }
}
```

### Processo de definição dos seletores
1. Abrir cada URL no Chrome
2. Inspecionar elemento → copiar seletor CSS
3. Validar no console: `document.querySelector('seletor')`
4. Registrar no `selectors.json`
5. Repetir para todos os campos de cada URL

> **Registrar o tempo gasto nessa etapa** — será usado como métrica de "esforço de implementação".

---

## Etapa 3 — Script de Benchmark

### `experiments/run_benchmark.py`

O script deve:
1. Ler lista de URLs e schemas de `experiments/urls.json`
2. Para cada URL:
   - Rodar extração LLM → registrar resultado, tempo, tokens, custo
   - Rodar extração baseline → registrar resultado e tempo
   - Comparar ambos contra o gabarito em `experiments/ground_truth.json`
   - Calcular acurácia e cobertura campo a campo
3. Exportar tudo para `experiments/results.csv`

### `experiments/urls.json`
```json
[
  {
    "category": "A",
    "url": "https://...",
    "schema": { "nome": "string", "preco_atual": "number", "disponivel": "boolean" }
  }
]
```

### `experiments/ground_truth.json`
```json
{
  "https://...": {
    "nome": "Smartphone XYZ 128GB",
    "preco_atual": 1299.90,
    "disponivel": true
  }
}
```

### Cálculo das métricas
| Métrica | Como calcular |
|---|---|
| Acurácia | campos corretos (match com gabarito) / total de campos |
| Cobertura | campos preenchidos (não null) / total de campos |
| Custo LLM | tokens_entrada × $0,00000015 + tokens_saída × $0,0000006 |
| Taxa de falha | extrações com exceção ou JSON inválido / total |

**Regras de match por tipo:**
- `string` → normalizar (strip + lowercase), comparar exato
- `number` → tolerância de ±1%
- `boolean` → exato

---

## Etapa 4 — Estrutura da Planilha

| Aba | Colunas principais |
|---|---|
| **Gabarito** | URL, Categoria, Campo, Valor esperado |
| **Resultados LLM** | URL, Campo, Valor extraído, Correto?, Tokens, Custo USD, Tempo (s), Método fetch |
| **Resultados Baseline** | URL, Campo, Valor extraído, Correto?, Tempo (s), Observações |
| **Resumo por URL** | URL, Acurácia LLM, Acurácia Baseline, Cobertura LLM, Cobertura Baseline, Tempo LLM, Tempo Baseline, Custo LLM |
| **Resumo por Categoria** | Categoria, Acurácia LLM, Acurácia Baseline, Δ Acurácia, Tempo médio, Custo total, Falhas |

---

## Etapa 5 — Sequência de Execução

- [ ] Definir as 15 URLs concretas (escolher páginas específicas)
- [ ] Preencher gabarito manual para cada URL
- [ ] Definir seletores CSS via Chrome DevTools + registrar tempo gasto
- [ ] Implementar `baseline/extractor.py` + `selectors.json`
- [ ] Criar `run_benchmark.py`
- [ ] Rodar com 1 URL de cada categoria para validar
- [ ] Rodar experimento completo (15 URLs)
- [ ] Importar `results.csv` na planilha e formatar abas
- [ ] Escrever Cap. 6 com base nos dados

---

## Arquivos a criar no projeto

| Arquivo | Descrição |
|---|---|
| `experiments/urls.json` | Lista de URLs com schemas por categoria |
| `experiments/ground_truth.json` | Gabarito manual por URL |
| `experiments/run_benchmark.py` | Script de execução e comparação |
| `worker/baseline/extractor.py` | Módulo baseline com BeautifulSoup |
| `worker/baseline/selectors.json` | Seletores CSS por URL e campo |
| `experiments/results.csv` | Saída do benchmark para importar na planilha |
