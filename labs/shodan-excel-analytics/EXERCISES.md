# Exercícios: Shodan Excel Analytics

## Objetivo

Usar resultados simulados ou reais do Shodan para criar uma análise tabular e visual no estilo Excel, com agrupamentos, gráficos, score didático, comparação entre queries e exportação de evidências.

## Preparação

Abra o notebook conforme o [README do laboratório](README.md).

Para comecar, mantenha:

```python
MODE = "auto"
MAX_RESULTS = 100
TOP_N = 10
```

Se voce nao tiver `SHODAN_API_KEY`, o notebook usara automaticamente os dados de exemplo.

## Exercício 1: Dataset Normalizado

Execute o notebook ate a exibicao da tabela `df`.

Responda:

1. Quantos registros foram carregados?
2. Quais colunas representam contexto de rede?
3. Quais colunas ajudam a identificar tecnologia?
4. Quais colunas ajudam a priorizar risco?

Resultado esperado:

- o aluno identifica que resultados Shodan viram um dataset estruturado;
- IP e porta nao sao suficientes para análise defensiva.

## Exercício 2: Gráficos Estilo Excel

Execute os gráficos por:

- país;
- porta;
- organização;
- produto;
- ASN.

Responda:

1. Qual porta aparece mais?
2. Qual produto aparece mais?
3. Qual organização concentra mais registros?
4. Qual gráfico seria melhor para explicar o resultado para uma pessoa nao técnica?

Resultado esperado:

- o aluno entende como agregações transformam listas de hosts em resumo visual.

## Exercício 3: Top N Interativo

Altere:

```python
TOP_N = 5
```

Execute novamente as células de resumo e gráficos.

Depois altere:

```python
TOP_N = 15
```

Responda:

1. O que muda nos gráficos?
2. Quando um `TOP_N` menor ajuda?
3. Quando um `TOP_N` maior ajuda?

Resultado esperado:

- `TOP_N` controla a granularidade da visualização;
- gráficos executivos normalmente precisam de menos categorias.

## Exercício 4: Score Didático De Risco

Execute a seção de score.

Responda:

1. Qual host recebeu o maior score?
2. Quais motivos aparecem em `risk_reasons`?
3. O score indica explorabilidade real ou priorização didática?
4. Que informações faltariam para confirmar risco real?

Resultado esperado:

- o score ajuda a priorizar investigação;
- score didático nao substitui validação técnica.

## Exercício 5: Comparação Entre Queries

Observe as tabelas de comparação por `query_label`.

Responda:

1. Qual query concentra mais portas sensíveis?
2. Qual query tem mais produtos diferentes?
3. A comparação ajuda mais que analisar uma query isolada?
4. Que query voce adicionaria para enriquecer a análise?

Resultado esperado:

- comparar queries revela perfis diferentes de exposicao.

## Exercício 6: Análise De CVEs

Execute a seção de vulnerabilidades.

Responda:

1. Quantas CVEs distintas aparecem?
2. Qual CVE aparece mais?
3. Quais produtos estao associados a CVEs?
4. Por que uma CVE listada pelo Shodan ainda precisa de validação?

Resultado esperado:

- CVEs ajudam a priorizar, mas exigem verificação de contexto, versao e explorabilidade.

## Exercício 7: Resumo Executivo

Execute a célula de resumo executivo automatico.

Responda:

1. O resumo e adequado para público técnico?
2. O resumo e adequado para público executivo?
3. Que frase voce adicionaria para explicar limitações?
4. Que gráfico voce anexaria ao resumo?

Resultado esperado:

- o aluno aprende a transformar dados técnicos em narrativa de relatorio.

## Exercício 8: Export Excel E Markdown

Execute a seção de exportação com:

```python
EXPORT_XLSX = True
EXPORT_MARKDOWN_REPORT = True
```

Responda:

1. Quais arquivos foram gerados?
2. Quais abas existem no Excel?
3. Qual aba voce usaria para investigação técnica?
4. Qual aba voce usaria para apresentação?

Resultado esperado:

- o aluno gera artefatos reutilizaveis fora do notebook.

## Exercício 9: Modo Shodan Real

Use somente se tiver autorização, chave Shodan e créditos disponíveis.

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
4. Quantos créditos estavam disponíveis antes da consulta?

Resultado esperado:

- o aluno entende o fluxo real, mas com limite controlado.

## Consolidação Individual

Preencha a tabela:

| Pergunta | Resposta |
| --- | --- |
| Principal porta observada |  |
| Principal produto observado |  |
| Principal organização observada |  |
| Maior score didático |  |
| Principal motivo de risco |  |
| Gráfico mais util para explicar o resultado |  |
| Limitação mais importante dos dados |  |

Depois escreva um paragrafo respondendo:

> Como transformar resultados do Shodan em gráficos e tabelas muda a forma de priorizar investigação defensiva?
