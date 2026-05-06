# TCC — Crawler AI: Próximas Etapas

## Status Geral

| Seção | Status |
|---|---|
| Estrutura do documento | ✅ Concluído |
| Metadados (título, autor, siglas) | ✅ Concluído |
| Cap. 1 — Introdução | ✅ Concluído |
| Cap. 2 — Justificativa | ✅ Concluído |
| Cap. 3 — Objetivos | ✅ Concluído |
| Cap. 4 — Revisão de Literatura | 🔲 Pendente |
| Cap. 5 — Metodologia (sistema) | 🟡 Parcial |
| Cap. 5 — Metodologia (comparação) | 🔲 Pendente |
| Cap. 6 — Resultados | 🔲 Pendente (aguarda experimentos) |
| Cap. 7 — Conclusão | 🔲 Pendente (aguarda resultados) |
| Resumo e Abstract | 🔲 Pendente (escrever por último) |
| Agradecimentos | 🔲 Pendente |
| Figuras e diagramas | 🔲 Pendente |
| Banca examinadora | 🔲 Preencher nomes |

---

## Etapas Detalhadas

### 1. Revisão de Literatura (Cap. 4) — PRÓXIMA PRIORIDADE

Seções a escrever (cada uma com ~400–600 palavras):

- [ ] **4.1 Web Scraping: Conceito e Evolução**
  - Definição, histórico (anos 90 → AJAX → SPAs), casos de uso, aspectos legais
  - Refs: Mitchell (2018), GlezPena (2014)

- [ ] **4.2 Abordagens Tradicionais**
  - BeautifulSoup, XPath, CSS selectors, Scrapy, Selenium/Playwright
  - Vantagens e limitações de cada
  - Refs: Mitchell (2018), GlezPena (2014), Scrapy, BeautifulSoup docs

- [ ] **4.3 Modelos de Linguagem de Grande Escala**
  - Transformer (Vaswani 2017), pré-treinamento, GPT-3/GPT-4
  - Conceito de tokens, context window, custo
  - Refs: Vaswani (2017), Brown (2020), OpenAI (2023), Zhao (2023)

- [ ] **4.4 LLMs para Extração de Informação Estruturada**
  - IE como tarefa de NLP, zero-shot/few-shot, JSON mode
  - Alucinação, latência, privacidade
  - Refs: Brown (2020), OpenAI (2023)

- [ ] **4.5 Engenharia de Prompts**
  - zero-shot, few-shot, chain-of-thought (Wei 2022)
  - Boas práticas para extração de dados
  - Refs: Wei (2022), Zhao (2023)

- [ ] **4.6 Trabalhos Relacionados**
  - Pesquisar ferramentas: ScrapeGraphAI, Firecrawl, Jina AI Reader
  - Artigos que usam LLMs para extração de dados
  - Identificar lacuna que este TCC preenche

---

### 2. Metodologia — Completar seções pendentes (Cap. 5)

- [ ] **5.4 Tabela de Tecnologias** — criar tabela com todas as tecnologias por camada
- [ ] **5.5 Módulo Baseline (scraping tradicional)** — implementar e documentar
  - Definir quais sites/cenários terão seletores manuais
  - Documentar como os seletores foram construídos
- [ ] **5.6 Cenários de Teste** — definir e documentar
  - Sugestão: 3 categorias × N URLs cada
  - Categoria A: e-commerce (produto com preço, título, disponibilidade)
  - Categoria B: portal de notícias (título, autor, data, resumo)
  - Categoria C: dados tabulares (ranking, lista estruturada)
- [ ] **Figuras de arquitetura** — criar diagrama do sistema e do pipeline

---

### 3. Experimentos de Comparação

- [ ] Implementar módulo baseline (BeautifulSoup + seletores manuais) no projeto
- [ ] Selecionar URLs para cada cenário de teste (gabarito manual)
- [ ] Executar extração LLM em todas as URLs
- [ ] Executar extração tradicional nas mesmas URLs
- [ ] Registrar métricas: acurácia, cobertura, tempo, custo, taxa de falha
- [ ] Organizar dados em planilha para análise

---

### 4. Resultados e Discussão (Cap. 6)

- [ ] Tabelas de resultados por cenário (LLM vs Tradicional)
- [ ] Gráficos comparativos
- [ ] Análise de custo-benefício
- [ ] Discussão das limitações

---

### 5. Conclusão (Cap. 7)

- [ ] Contribuições do trabalho
- [ ] Limitações identificadas
- [ ] Trabalhos futuros

---

### 6. Elementos Finais

- [ ] Resumo em português (~300 palavras)
- [ ] Abstract em inglês (~300 palavras)
- [ ] Agradecimentos
- [ ] Preencher nomes da banca examinadora em `main.tex`
- [ ] Revisão geral de ortografia e formatação ABNT
- [ ] Compilação final e geração do PDF

---

## Datas

| Marco | Data |
|---|---|
| Entrega do TCC | 15/06/2026 |
| Defesa | 22/06/2026 |
