# Labs De Seguranca Em Notebooks

Repositório público com notebooks didáticos para aulas de seguranca da informação.

Cada laboratório fica em uma pasta propria dentro de `labs/`, com notebook e instrucoes de execução. Alguns laboratórios tambem incluem exercícios individuais.

## Laboratórios

| Laboratório | Tema | Material |
| --- | --- | --- |
| Codificações e hashes | Base64, URL encoding, SHA-256, SHA-512 e diferencas entre codificação e hash | [Abrir lab](labs/codificações-hashes/README.md) |
| Shodan Excel Analytics | Análise defensiva de resultados Shodan com tabelas, gráficos, score e export Excel | [Abrir lab](labs/shodan-excel-analytics/README.md) |
| Classificador de URLs maliciosas | Classificação supervisionada de URLs com HashingVectorizer e SGDClassifier | [Abrir lab](labs/classificador-urls-maliciosas/README.md) |

## Como Usar

Opcao recomendada para alunos:

1. Abra o `README.md` do laboratório desejado pelo GitHub.
2. Use o link do Google Colab indicado no laboratório.
3. Execute as células do notebook no navegador.
4. Leia os arquivos complementares indicados pelo laboratório.

Opcao local:

1. Clone o repositório:

```bash
git clone https://github.com/rodrigorosamuniz/labs-seguranca-notebooks.git
cd labs-seguranca-notebooks
```

2. Abra a pasta do laboratório desejado.
3. Siga o `README.md` do laboratório.
4. Leia os arquivos complementares indicados pelo laboratório.

## Requisitos Gerais

Os notebooks devem rodar em pelo menos uma destas opcoes:

- Google Colab;
- VS Code com extensao Jupyter;
- Jupyter Notebook;
- JupyterLab.

Cada laboratório informa seus requisitos especificos.

## Cuidados

Nao use dados reais, senhas reais, tokens, chaves privadas, CPFs, emails pessoais ou dados corporativos nos notebooks.

Estes materiais sao didáticos e nao devem ser tratados como implementações prontas para produção.
