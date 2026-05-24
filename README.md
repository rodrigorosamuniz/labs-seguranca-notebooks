# Labs De Seguranca Em Notebooks

Repositorio publico com notebooks didaticos para aulas de seguranca da informacao.

Cada laboratorio fica em uma pasta propria dentro de `labs/`, com notebook e instrucoes de execucao. Alguns laboratorios tambem incluem exercicios individuais.

## Laboratorios

| Laboratorio | Tema | Material |
| --- | --- | --- |
| Codificacoes e hashes | Base64, URL encoding, SHA-256, SHA-512 e diferencas entre codificacao e hash | [Abrir lab](labs/codificacoes-hashes/README.md) |
| Shodan Excel Analytics | Analise defensiva de resultados Shodan com tabelas, graficos, score e export Excel | [Abrir lab](labs/shodan-excel-analytics/README.md) |
| Classificador de URLs maliciosas | Classificacao supervisionada de URLs com HashingVectorizer e SGDClassifier | [Abrir lab](labs/classificador-urls-maliciosas/README.md) |

## Como Usar

Opcao recomendada para alunos:

1. Abra o `README.md` do laboratorio desejado pelo GitHub.
2. Use o link do Google Colab indicado no laboratorio.
3. Execute as celulas do notebook no navegador.
4. Leia os arquivos complementares indicados pelo laboratorio.

Opcao local:

1. Clone o repositorio:

```bash
git clone https://github.com/rodrigorosamuniz/labs-seguranca-notebooks.git
cd labs-seguranca-notebooks
```

2. Abra a pasta do laboratorio desejado.
3. Siga o `README.md` do laboratorio.
4. Leia os arquivos complementares indicados pelo laboratorio.

## Requisitos Gerais

Os notebooks devem rodar em pelo menos uma destas opcoes:

- Google Colab;
- VS Code com extensao Jupyter;
- Jupyter Notebook;
- JupyterLab.

Cada laboratorio informa seus requisitos especificos.

## Cuidados

Nao use dados reais, senhas reais, tokens, chaves privadas, CPFs, emails pessoais ou dados corporativos nos notebooks.

Estes materiais sao didaticos e nao devem ser tratados como implementacoes prontas para producao.
