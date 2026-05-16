# Lab: Shodan Excel Analytics

Este laboratorio mostra como transformar resultados do Shodan em uma analise no estilo Excel: tabela normalizada, agrupamentos, graficos, score didatico, resumo executivo e exportacao para `.xlsx`.

O notebook funciona em modo hibrido:

- `sample`: usa um CSV didatico incluido neste repositorio;
- `shodan`: usa a API real do Shodan quando `SHODAN_API_KEY` estiver configurada;
- `auto`: usa Shodan quando houver chave e usa o CSV de exemplo quando nao houver.

## Arquivos

```text
shodan_excel_analytics.ipynb
EXERCISES.md
requirements.txt
data/sample_shodan_results.csv
```

## Opcao 1: Rodar Pelo Google Colab

Abra o notebook diretamente no Colab:

```text
https://colab.research.google.com/github/rodrigorosamuniz/labs-seguranca-notebooks/blob/main/labs/shodan-excel-analytics/shodan_excel_analytics.ipynb
```

Para usar apenas o modo demonstrativo, nao precisa configurar nada. O notebook usa o CSV de exemplo.

Para usar Shodan real:

1. Crie ou acesse sua conta no Shodan.
2. Copie sua API key.
3. No Colab, abra o painel de secrets.
4. Crie um secret chamado `SHODAN_API_KEY`.
5. Execute o notebook com `MODE = "auto"` ou `MODE = "shodan"`.

Nao cole sua API key diretamente em celulas do notebook.

## Opcao 2: Rodar Localmente

Clone o repositorio:

```bash
git clone https://github.com/rodrigorosamuniz/labs-seguranca-notebooks.git
cd labs-seguranca-notebooks/labs/shodan-excel-analytics
```

Instale as dependencias:

```bash
python -m pip install -r requirements.txt
```

Abra com VS Code, Jupyter Notebook ou JupyterLab:

```bash
jupyter lab
```

Se for usar Shodan real, configure a variavel:

```bash
export SHODAN_API_KEY="sua-chave-aqui"
```

## O Que O Lab Gera

- tabela normalizada com IP, porta, transporte, organizacao, ASN, pais, cidade, produto, versao, hostnames, CVEs e timestamp;
- graficos estilo Excel por pais, porta, organizacao, ASN, produto e query;
- comparacao entre queries;
- analise de CVEs;
- score didatico de risco;
- resumo executivo automatico;
- exportacao opcional para Excel;
- exportacao opcional para relatorio Markdown.

## Valor Didatico

O Shodan mostra resultados e filtros, mas o lab ensina a transformar esses resultados em dataset analisavel:

- agrupar exposicao por dimensoes relevantes;
- priorizar investigacao;
- separar dado bruto de insight;
- gerar evidencia para relatorio;
- comparar consultas diferentes;
- interpretar limites e vieses dos dados.

## Limites E Cuidados Com A API

Consultas reais ao Shodan podem consumir creditos. O notebook limita `MAX_RESULTS` por padrao e mostra uma estimativa didatica de consumo antes de consultar.

Use consultas pequenas e controladas durante a aula. Evite automacao massiva, varredura ofensiva ou qualquer uso fora de contexto defensivo/educacional.

Referencias oficiais:

- Shodan API: https://developer.shodan.io/api
- Tipos de creditos: https://help.shodan.io/the-basics/credit-types-explained
- Download de dados via API: https://help.shodan.io/guides/how-to-download-data-with-api

## Dados De Exemplo

O arquivo `data/sample_shodan_results.csv` usa IPs de documentacao e dados ficticios. Ele serve para que todos consigam executar o lab mesmo sem conta, chave ou creditos no Shodan.

## Cuidados

Nao use o lab para atacar, explorar ou tentar acessar sistemas. Resultados do Shodan indicam exposicao observada, mas nao provam explorabilidade. Qualquer achado real deve ser tratado com autorizacao, contexto e processo responsavel.
