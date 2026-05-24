# Exercicios: Shodan Excel Analytics

## Objetivo

Usar resultados simulados ou reais do Shodan para criar uma analise tabular e visual no estilo Excel, com agrupamentos, graficos, score didatico, comparacao entre queries e exportacao de evidencias.

## Preparacao

Abra o notebook conforme o [README do laboratorio](README.md).

Para comecar, mantenha:

```python
MODE = "auto"
MAX_RESULTS = 100
TOP_N = 10
```

Se voce nao tiver `SHODAN_API_KEY`, o notebook usara automaticamente os dados de exemplo.

## Exercicio 1: Dataset Normalizado

Execute o notebook ate a exibicao da tabela `df`.

Responda:

1. Quantos registros foram carregados?
2. Quais colunas representam contexto de rede?
3. Quais colunas ajudam a identificar tecnologia?
4. Quais colunas ajudam a priorizar risco?

Resultado esperado:

- o aluno identifica que resultados Shodan viram um dataset estruturado;
- IP e porta nao sao suficientes para analise defensiva.

## Exercicio 2: Graficos Estilo Excel

Execute os graficos por:

- pais;
- porta;
- organizacao;
- produto;
- ASN.

Responda:

1. Qual porta aparece mais?
2. Qual produto aparece mais?
3. Qual organizacao concentra mais registros?
4. Qual grafico seria melhor para explicar o resultado para uma pessoa nao tecnica?

Resultado esperado:

- o aluno entende como agregacoes transformam listas de hosts em resumo visual.

## Exercicio 3: Top N Interativo

Altere:

```python
TOP_N = 5
```

Execute novamente as celulas de resumo e graficos.

Depois altere:

```python
TOP_N = 15
```

Responda:

1. O que muda nos graficos?
2. Quando um `TOP_N` menor ajuda?
3. Quando um `TOP_N` maior ajuda?

Resultado esperado:

- `TOP_N` controla a granularidade da visualizacao;
- graficos executivos normalmente precisam de menos categorias.

## Exercicio 4: Score Didatico De Risco

Execute a secao de score.

Responda:

1. Qual host recebeu o maior score?
2. Quais motivos aparecem em `risk_reasons`?
3. O score indica explorabilidade real ou priorizacao didatica?
4. Que informacoes faltariam para confirmar risco real?

Resultado esperado:

- o score ajuda a priorizar investigacao;
- score didatico nao substitui validacao tecnica.

## Exercicio 5: Comparacao Entre Queries

Observe as tabelas de comparacao por `query_label`.

Responda:

1. Qual query concentra mais portas sensiveis?
2. Qual query tem mais produtos diferentes?
3. A comparacao ajuda mais que analisar uma query isolada?
4. Que query voce adicionaria para enriquecer a analise?

Resultado esperado:

- comparar queries revela perfis diferentes de exposicao.

## Exercicio 6: Analise De CVEs

Execute a secao de vulnerabilidades.

Responda:

1. Quantas CVEs distintas aparecem?
2. Qual CVE aparece mais?
3. Quais produtos estao associados a CVEs?
4. Por que uma CVE listada pelo Shodan ainda precisa de validacao?

Resultado esperado:

- CVEs ajudam a priorizar, mas exigem verificacao de contexto, versao e explorabilidade.

## Exercicio 7: Resumo Executivo

Execute a celula de resumo executivo automatico.

Responda:

1. O resumo e adequado para publico tecnico?
2. O resumo e adequado para publico executivo?
3. Que frase voce adicionaria para explicar limitacoes?
4. Que grafico voce anexaria ao resumo?

Resultado esperado:

- o aluno aprende a transformar dados tecnicos em narrativa de relatorio.

## Exercicio 8: Export Excel E Markdown

Execute a secao de exportacao com:

```python
EXPORT_XLSX = True
EXPORT_MARKDOWN_REPORT = True
```

Responda:

1. Quais arquivos foram gerados?
2. Quais abas existem no Excel?
3. Qual aba voce usaria para investigacao tecnica?
4. Qual aba voce usaria para apresentacao?

Resultado esperado:

- o aluno gera artefatos reutilizaveis fora do notebook.

## Exercicio 9: Modo Shodan Real

Use somente se tiver autorizacao, chave Shodan e creditos disponiveis.

Configure `SHODAN_API_KEY` e use uma query pequena, por exemplo:

```python
MODE = "shodan"
COMPARE_QUERIES = ["apache country:BR"]
MAX_RESULTS = 100
```

Responda:

1. Quantos resultados foram retornados?
2. A distribuicao por porta foi parecida com o CSV de exemplo?
3. Apareceram CVEs?
4. Quantos creditos estavam disponiveis antes da consulta?

Resultado esperado:

- o aluno entende o fluxo real, mas com limite controlado.

## Consolidacao Individual

Preencha a tabela:

| Pergunta | Resposta |
| --- | --- |
| Principal porta observada |  |
| Principal produto observado |  |
| Principal organizacao observada |  |
| Maior score didatico |  |
| Principal motivo de risco |  |
| Grafico mais util para explicar o resultado |  |
| Limitacao mais importante dos dados |  |

Depois escreva um paragrafo respondendo:

> Como transformar resultados do Shodan em graficos e tabelas muda a forma de priorizar investigacao defensiva?
