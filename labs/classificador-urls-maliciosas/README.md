# Lab: Classificador De URLs Maliciosas Em Larga Escala

Este laboratório usa Python, pandas e scikit-learn para construir um classificador de URLs maliciosas. O notebook combina URLs maliciosas do PhishTank com dominios benignos de listas publicas, transforma as URLs em vetores numéricos e treina um modelo de classificação incremental.

O objetivo e mostrar, de forma prática, como uma IA supervisionada aprende padroes a partir de exemplos rotulados. Este lab nao usa LLM. Ele usa um modelo classico de aprendizado de maquina, mais leve e adequado para demonstrar os fundamentos de classificação.

## Arquivos

```text
malicious_url_classifier_lab_large.ipynb
EXPLICACAO_CELULAS.md
requirements.txt
```

## Pré-requisitos

Opcao recomendada:

- Google Colab.

Opcoes locais:

- Python 3.10 ou superior;
- VS Code com extensao Jupyter;
- Jupyter Notebook;
- JupyterLab.

O notebook instala automaticamente parte das dependencias quando executado no Colab:

```python
!pip install scikit-learn pandas wget --quiet
```

Para executar localmente, instale os pacotes antes de abrir o notebook:

```bash
python -m pip install -r labs/classificador-urls-maliciosas/requirements.txt
```

## Opcao 1: Rodar Pelo Google Colab

Abra o notebook diretamente no Colab:

```text
https://colab.research.google.com/github/rodrigorosamuniz/labs-seguranca-notebooks/blob/main/labs/classificador-urls-maliciosas/malicious_url_classifier_lab_large.ipynb
```

Depois:

1. Clique em `Conectar`, se o Colab pedir.
2. Execute as células em ordem, de cima para baixo.
3. Na célula do PhishTank, troque `seu_email@example.com` por um identificador seu no `User-Agent`, se desejar.
4. Aguarde os downloads das bases publicas.
5. Leia as métricas de avaliação do modelo.
6. Teste URLs ficticias ou publicas na ultima célula.

## Como Baixar O Repositório

Use esta opcao se quiser rodar localmente pelo VS Code, Jupyter Notebook ou JupyterLab.

```bash
git clone https://github.com/rodrigorosamuniz/labs-seguranca-notebooks.git
cd labs-seguranca-notebooks
```

## Opcao 2: Rodar Pelo VS Code

1. Abra a pasta `labs-seguranca-notebooks` no VS Code.
2. Instale a extensao `Jupyter`, caso ainda nao tenha.
3. Abra o arquivo `labs/classificador-urls-maliciosas/malicious_url_classifier_lab_large.ipynb`.
4. Selecione um interpretador Python quando o VS Code pedir.
5. Execute as células uma por uma.

## Opcao 3: Rodar Pelo Jupyter Notebook

Instale o Jupyter, se necessário:

```bash
python -m pip install notebook
```

Suba o Jupyter:

```bash
jupyter notebook
```

No navegador, abra:

```text
labs/classificador-urls-maliciosas/malicious_url_classifier_lab_large.ipynb
```

## Opcao 4: Rodar Pelo JupyterLab

Instale o JupyterLab, se necessário:

```bash
python -m pip install jupyterlab
```

Suba o JupyterLab:

```bash
jupyter lab
```

No navegador, abra:

```text
labs/classificador-urls-maliciosas/malicious_url_classifier_lab_large.ipynb
```

## Como Usar O Notebook

1. Leia a introducao do notebook.
2. Execute a célula de instalação e imports.
3. Execute a célula que baixa e organiza as bases de URLs.
4. Execute a célula de pre-processamento para transformar URLs em vetores numéricos.
5. Execute a célula de treinamento e avaliação.
6. Veja exemplos de classificações geradas pelo modelo.
7. Use a ultima célula para testar URLs avulsas.

Para entender cada etapa antes de executar, leia [EXPLICACAO_CELULAS.md](EXPLICACAO_CELULAS.md).

## O Que Observar

Durante a execução, observe:

- as URLs precisam de rótulos para que o modelo aprenda;
- `label = 1` representa URL maliciosa;
- `label = 0` representa URL benigna;
- texto nao entra diretamente no modelo, por isso as URLs sao convertidas em numeros;
- `HashingVectorizer` transforma cada URL em um vetor numérico esparso;
- `SGDClassifier` aprende de forma incremental, em lotes;
- as métricas mostram acertos, erros e equilibrio entre classes.

## Cuidados Didáticos

Nao use senhas reais, tokens reais, CPFs, emails pessoais, URLs internas da empresa ou qualquer dado sensível no notebook.

O classificador e didático. Ele nao deve ser usado como mecanismo único de bloqueio, deteccao ou resposta a incidentes em ambiente real.

Feeds públicos podem mudar, ficar indisponíveis ou impor limites de acesso. Se alguma célula de download falhar, aguarde alguns minutos e execute novamente.
