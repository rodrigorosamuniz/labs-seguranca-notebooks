# Lab: Codificações E Hashes

Este laboratório usa um notebook Python para demonstrar diferencas entre codificações e funções de hash usadas em seguranca da informação.

## Arquivos

```text
lab_codificacoes_hashes.ipynb
EXERCISES.md
```

## Pré-requisitos

Escolha uma das opcoes abaixo:

- Google Colab;
- VS Code com extensao Jupyter;
- Jupyter Notebook;
- JupyterLab.

Para Google Colab, nao e necessário instalar Python localmente. Para as opcoes locais, e necessário ter Python instalado.

O notebook usa apenas bibliotecas padrao do Python, entao nao precisa instalar pacotes extras para executar as células atuais.

## Opcao 1: Rodar Pelo Google Colab

Abra o notebook diretamente no Colab:

```text
https://colab.research.google.com/github/rodrigorosamuniz/labs-seguranca-notebooks/blob/main/labs/codificacoes-hashes/lab_codificacoes_hashes.ipynb
```

Depois:

1. Clique em `Conectar`, se o Colab pedir.
2. Execute a célula de código.
3. Digite um texto ficticio quando o notebook solicitar.
4. Compare as saídas geradas.

## Como Baixar O Repositório

Use esta opcao se quiser rodar localmente pelo VS Code, Jupyter Notebook ou JupyterLab.

```bash
git clone https://github.com/rodrigorosamuniz/labs-seguranca-notebooks.git
cd labs-seguranca-notebooks
```

## Opcao 2: Rodar Pelo VS Code

1. Abra a pasta `labs-seguranca-notebooks` no VS Code.
2. Instale a extensao `Jupyter`, caso ainda nao tenha.
3. Abra o arquivo `labs/codificacoes-hashes/lab_codificacoes_hashes.ipynb`.
4. Selecione um interpretador Python quando o VS Code pedir.
5. Clique em `Run All` ou execute as células uma por uma.

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
labs/codificacoes-hashes/lab_codificacoes_hashes.ipynb
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
labs/codificacoes-hashes/lab_codificacoes_hashes.ipynb
```

## Como Usar O Notebook

1. Leia a primeira célula Markdown para entender o objetivo.
2. Execute a célula de código.
3. Digite um texto quando o notebook pedir.
4. Compare as saídas geradas.
5. Rode novamente com textos diferentes.
6. Resolva os exercícios em [EXERCISES.md](EXERCISES.md).

Use exemplos simples para comecar:

```text
seguranca
```

```text
Seguranca
```

```text
senha123
```

```text
senha124
```

## O Que Observar

Durante a execução, observe:

- codificações transformam a representação do texto;
- codificações podem ser revertidas quando o algoritmo e conhecido;
- hashes geram resumos de tamanho fixo;
- hashes nao foram feitos para serem revertidos;
- pequenas mudanças no texto geram hashes muito diferentes;
- hashes sao usados para integridade, comparação e armazenamento seguro de verificadores, mas nao substituem criptografia.

## Cuidados Didáticos

Nao use senhas reais, tokens reais, CPFs, emails pessoais ou qualquer dado sensível no notebook. Use apenas exemplos ficticios.

Este notebook e demonstrativo. Ele nao implementa armazenamento seguro de senhas, salt, pepper, KDF, criptografia simétrica ou assinatura digital.
