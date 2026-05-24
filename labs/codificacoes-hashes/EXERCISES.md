# Exercícios: Codificações E Hashes

## Objetivo

Práticar conceitos de codificação e hash usando o notebook `lab_codificacoes_hashes.ipynb`.

Ao final, o aluno deve conseguir diferenciar representação reversível de resumo criptográfico, interpretar saídas e explicar usos básicos em seguranca da informação.

## Preparação

Abra o notebook conforme o [README do laboratório](README.md).

Execute a célula principal pelo menos uma vez usando:

```text
seguranca
```

Anote as saídas geradas.

## Exercício 1: Primeira Execução

Execute o notebook com o texto:

```text
laboratorio
```

Responda:

1. Quais saídas foram geradas?
2. Quais saídas parecem codificações?
3. Quais saídas parecem hashes?
4. Alguma saída permite reconhecer facilmente o texto original?

Resultado esperado:

- o notebook gera representações diferentes para o mesmo texto;
- codificações e hashes nao devem ser interpretados como a mesma coisa.

## Exercício 2: Maiusculas E Minusculas

Execute o notebook duas vezes:

```text
seguranca
```

```text
Seguranca
```

Compare as saídas.

Responda:

1. As saídas foram iguais ou diferentes?
2. Uma única letra maiuscula alterou o hash?
3. O que isso mostra sobre sensibilidade a pequenas mudanças?

Resultado esperado:

- os hashes mudam quando o texto muda;
- `seguranca` e `Seguranca` sao entradas diferentes.

## Exercício 3: Pequena Alteração No Texto

Execute o notebook com:

```text
senha123
```

Depois execute com:

```text
senha124
```

Responda:

1. A diferenca visual entre os textos e pequena?
2. A diferenca entre os hashes tambem parece pequena?
3. Por que essa propriedade e importante para integridade?

Resultado esperado:

- pequenas alterações na entrada geram hashes muito diferentes;
- isso ajuda a detectar alterações em arquivos, mensagens ou registros.

## Exercício 4: Codificação Nao E Criptografia

Execute o notebook com:

```text
dados publicos
```

Observe as codificações geradas.

Responda:

1. Codificar o texto torna a informação secreta?
2. Uma pessoa que conhece o algoritmo consegue reverter a codificação?
3. Por que Base64 nao deve ser tratado como criptografia?

Resultado esperado:

- codificação muda a representação;
- codificação nao garante confidencialidade;
- Base64 nao protege segredo.

## Exercício 5: Hash Nao E Codificação

Execute o notebook com:

```text
mensagem de teste
```

Observe os hashes gerados.

Responda:

1. O hash permite recuperar diretamente o texto original?
2. Por que hashes sao usados para comparação de integridade?
3. O que acontece se duas pessoas calcularem o mesmo hash para o mesmo texto?

Resultado esperado:

- hash nao e feito para ser revertido;
- a mesma entrada deve produzir o mesmo hash;
- hashes ajudam a verificar se algo foi alterado.

## Exercício 6: Entrada Vazia Ou Muito Curta

Execute o notebook com uma entrada curta:

```text
a
```

Se o notebook permitir, teste tambem uma entrada vazia apenas pressionando `Enter`.

Responda:

1. O notebook gera hash para texto curto?
2. O tamanho do hash muda conforme o tamanho da entrada?
3. O que isso mostra sobre funções de hash?

Resultado esperado:

- hashes possuem tamanho de saída definido pelo algoritmo;
- a saída nao cresce proporcionalmente ao texto de entrada.

## Exercício 7: Comparar SHA-256 E SHA-512

Execute o notebook com:

```text
comparacao de algoritmos
```

Responda:

1. Qual saída e maior: SHA-256 ou SHA-512?
2. O numero no nome do algoritmo tem relação com o tamanho da saída?
3. Em quais situações pode fazer sentido escolher algoritmos de hash mais fortes?

Resultado esperado:

- SHA-512 produz saída maior que SHA-256;
- o tamanho do resumo depende do algoritmo.

## Exercício 8: Uso Em Seguranca Da Informação

Escolha um texto qualquer ficticio e execute o notebook.

Depois responda:

1. Qual saída voce usaria para transportar texto em um formato seguro para sistemas?
2. Qual saída voce usaria para verificar integridade?
3. Qual saída voce nao usaria para esconder segredo?
4. O que ainda faltaria para armazenar senha de forma segura em produção?

Resultado esperado:

- codificação pode ajudar em transporte/representação;
- hash pode ajudar em integridade;
- Base64 nao deve ser usado para esconder segredo;
- armazenamento seguro de senha exige controles adicionais, como salt e algoritmos apropriados para senha.

## Consolidação Individual

Preencha a tabela:

| Conceito | E reversível? | Protege confidencialidade? | Uso tipico |
| --- | --- | --- | --- |
| Base64 |  |  |  |
| URL encoding |  |  |  |
| SHA-256 |  |  |  |
| SHA-512 |  |  |  |

Depois escreva, com suas palavras:

1. A diferenca entre codificação e hash.
2. Um exemplo de uso correto de codificação.
3. Um exemplo de uso correto de hash.
4. Um erro comum ao confundir codificação com seguranca.
