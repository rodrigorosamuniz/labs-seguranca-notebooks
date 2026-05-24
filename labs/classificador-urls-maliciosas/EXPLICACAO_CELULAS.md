# Explicacao Didatica Das Celulas

Este arquivo explica o que cada celula do notebook faz. A ideia e ajudar alunos que nunca tiveram contato com modelos de IA, aprendizado de maquina ou classificacao automatica.

Antes de comecar, um ponto importante: este notebook nao usa um LLM, como ChatGPT, Gemini ou Claude. Ele usa aprendizado de maquina supervisionado. Isso significa que o modelo aprende a partir de exemplos ja classificados:

- exemplos com `label = 1`: URLs maliciosas;
- exemplos com `label = 0`: URLs benignas.

Depois de ver muitos exemplos, o modelo tenta classificar URLs novas com base nos padroes aprendidos.

## Visao Geral Do Fluxo

O notebook segue este caminho:

1. Instala bibliotecas e importa ferramentas.
2. Baixa bases publicas de URLs.
3. Marca cada URL como maliciosa ou benigna.
4. Transforma URLs, que sao texto, em numeros.
5. Treina um modelo de classificacao.
6. Avalia o desempenho.
7. Mostra exemplos classificados.
8. Permite testar URLs digitadas pelo usuario.

## Celula 1: Titulo E Objetivos

Tipo: Markdown.

Esta celula apresenta o laboratorio:

```text
Laboratorio: Classificador de URLs Maliciosas em Larga Escala
```

Ela tambem explica os objetivos principais:

- carregar datasets grandes de URLs;
- pre-processar URLs;
- treinar um modelo em lotes;
- avaliar o desempenho;
- testar URLs avulsas.

Essa celula nao executa codigo. Ela serve como introducao para o aluno entender o que sera feito.

## Celula 2: Secao De Instalacao E Imports

Tipo: Markdown.

Esta celula apenas cria o titulo da secao:

```text
1. Instalacao e imports
```

Ela prepara o leitor para a primeira celula de codigo.

## Celula 3: Instalar Bibliotecas E Importar Ferramentas

Tipo: Codigo.

Esta celula instala e importa as bibliotecas usadas no lab.

```python
!pip install scikit-learn pandas wget --quiet
```

Esse comando e comum em notebooks do Google Colab. Ele instala pacotes Python dentro do ambiente temporario do Colab.

As bibliotecas principais sao:

- `pandas`: usada para ler, organizar e manipular tabelas de dados;
- `HashingVectorizer`: transforma texto em numeros;
- `SGDClassifier`: modelo de aprendizado de maquina usado para classificacao;
- `accuracy_score`: calcula a porcentagem de acertos;
- `classification_report`: mostra metricas mais detalhadas;
- `train_test_split`: separa dados de treino e teste;
- `wget`: baixa arquivos da internet;
- `zipfile`: abre arquivos compactados.

### Por Que Texto Precisa Virar Numero?

Modelos de aprendizado de maquina nao entendem texto diretamente. Uma URL como:

```text
https://exemplo.com/login
```

precisa ser transformada em uma representacao numerica. Essa transformacao acontece depois, com `HashingVectorizer`.

## Celula 4: Secao De Download E Preparacao Dos Dados

Tipo: Markdown.

Esta celula cria o titulo:

```text
2. Download e preparacao dos dados
```

Ela indica que a proxima etapa sera baixar e organizar as bases de URLs.

## Celula 5: Baixar Feeds, Rotular URLs E Montar O Dataset

Tipo: Codigo.

Esta e uma das celulas mais importantes do notebook. Ela cria a base de treinamento.

### 1. Importacoes Extras

A celula importa:

- `io`: permite ler bytes baixados da internet como se fossem arquivos;
- `requests`: faz requisicoes HTTP;
- `wget`: baixa arquivos;
- `zipfile`: extrai arquivos ZIP;
- `pandas`: manipula os dados.

### 2. Baixar URLs Maliciosas Do PhishTank

```python
phish_url_gz = 'https://data.phishtank.com/data/online-valid.csv.gz'
headers = {'User-Agent': 'phishtank/seu_email@example.com'}
resp = requests.get(phish_url_gz, headers=headers)
resp.raise_for_status()
```

O PhishTank publica URLs associadas a phishing. A requisicao usa `User-Agent` porque alguns servicos exigem uma identificacao minima de quem esta acessando.

```python
phish = pd.read_csv(io.BytesIO(resp.content), compression='gzip', usecols=['url'])
phish['label'] = 1
```

Aqui o pandas le o arquivo compactado em memoria e usa apenas a coluna `url`.

Depois, todas essas URLs recebem `label = 1`, que significa:

```text
1 = maliciosa
```

### 3. Baixar Dominios Benignos Da Cisco Umbrella

```python
wget.download('https://s3-us-west-1.amazonaws.com/umbrella-static/top-1m.csv.zip', umbrella_zip)
```

Essa lista contem dominios populares. A ideia didatica e tratar dominios muito acessados como exemplos benignos.

```python
umbrella['label'] = 0
```

Aqui as URLs recebem `label = 0`, que significa:

```text
0 = benigna
```

### 4. Baixar Dominios Benignos Da Majestic Million

```python
wget.download('https://downloads.majestic.com/majestic_million.csv', 'majestic_million.csv')
```

Essa e outra lista publica de dominios conhecidos. Ela aumenta a quantidade de exemplos benignos.

### 5. Remover Duplicatas

```python
benign_all = benign_all.drop_duplicates(subset='url').reset_index(drop=True)
```

Duplicatas podem distorcer o treinamento. Se o mesmo dominio aparece muitas vezes, o modelo pode dar importancia exagerada a ele.

### 6. Balancear A Base

```python
n_mal = len(phish)
n_ben = 2 * n_mal
benign = benign_all.sample(n=n_ben, random_state=42).reset_index(drop=True)
```

Essa parte escolhe duas URLs benignas para cada URL maliciosa.

Exemplo:

```text
10.000 maliciosas -> 20.000 benignas
```

Isso evita uma base completamente desequilibrada. Se houvesse URLs benignas demais, o modelo poderia aprender a responder "benigna" quase sempre.

### 7. Embaralhar O Dataset

```python
data = data.sample(frac=1, random_state=42).reset_index(drop=True)
```

Embaralhar evita que o modelo veja todos os exemplos de uma classe primeiro e todos os da outra depois.

### O Que E `random_state=42`?

`random_state` fixa a aleatoriedade. Assim, se duas pessoas executarem o notebook com os mesmos dados, a amostragem e a divisao tendem a ser reproduziveis.

O numero `42` nao tem efeito especial no modelo. Ele e apenas uma semente aleatoria escolhida pelo autor.

## Celula 6: Secao De Pre-processamento

Tipo: Markdown.

Esta celula cria o titulo:

```text
3. Pre-processamento com HashingVectorizer
```

Pre-processamento e a etapa que prepara os dados para o modelo.

## Celula 7: Transformar URLs Em Vetores Numericos

Tipo: Codigo.

Esta celula prepara as URLs para o treinamento.

### 1. Garantir Que Toda URL Seja Texto

```python
data['url'] = data['url'].astype(str)
```

Mesmo que alguma URL venha como valor estranho ou nulo, essa linha forca o conteudo a virar texto.

### 2. Separar Treino E Teste

```python
urls_train, urls_test, y_train, y_test = train_test_split(
    data['url'], data['label'].values,
    test_size=0.2, random_state=42
)
```

A base e dividida em duas partes:

- treino: usado para o modelo aprender;
- teste: usado para avaliar se o modelo aprendeu algo util.

`test_size=0.2` significa:

```text
20% dos dados ficam para teste
80% dos dados ficam para treino
```

### 3. Criar O `HashingVectorizer`

```python
vectorizer = HashingVectorizer(analyzer='char', ngram_range=(3,5), n_features=5000)
```

Esse e um ponto central da parametrizacao da IA.

O `HashingVectorizer` transforma texto em uma matriz numerica. Cada URL vira um vetor com varios numeros. O modelo nao ve a URL como texto; ele ve o vetor.

#### Parametro `analyzer='char'`

Esse parametro diz que o texto sera analisado por caracteres, nao por palavras.

Para URLs, isso faz sentido porque padroes maliciosos podem aparecer em pedacos pequenos:

```text
login
verify
secure
wp-
php
token
```

Tambem podem aparecer em combinacoes de caracteres, como:

```text
//-
.ru
%2f
```

Se o analisador fosse por palavra, muitos desses padroes poderiam ser perdidos.

#### Parametro `ngram_range=(3,5)`

Um n-grama e um pedaco sequencial do texto.

Com `ngram_range=(3,5)`, o vetorizador considera sequencias de:

- 3 caracteres;
- 4 caracteres;
- 5 caracteres.

Exemplo com o texto `login`:

```text
3 caracteres: log, ogi, gin
4 caracteres: logi, ogin
5 caracteres: login
```

Isso ajuda o modelo a perceber pequenos padroes dentro da URL.

#### Parametro `n_features=5000`

Esse parametro define o tamanho do vetor final.

```text
Cada URL vira um vetor com 5000 posicoes.
```

Um valor maior permite representar mais padroes, mas tambem consome mais memoria e processamento.

Um valor menor e mais leve, mas pode misturar padroes diferentes na mesma posicao do vetor.

### 4. Vetor Esparso

```python
print(vectorizer.transform([urls_train.iloc[0]]).shape)
```

A saida esperada e:

```text
(1, 5000)
```

Isso significa:

- 1 URL analisada;
- 5000 posicoes numericas no vetor.

O vetor e chamado de esparso porque a maioria das posicoes fica vazia ou igual a zero. Isso economiza memoria.

## Celula 8: Secao De Treinamento E Avaliacao

Tipo: Markdown.

Esta celula cria o titulo:

```text
4. Treinamento online com SGDClassifier e Avaliacao
```

Treinamento online significa que o modelo pode aprender em partes, usando lotes de dados.

## Celula 9: Treinar O Modelo Em Lotes E Avaliar

Tipo: Codigo.

Esta celula treina o classificador.

### 1. Separar URLs E Rotulos

```python
urls = data['url'].astype(str)
labels = data['label'].values
```

Aqui o notebook separa:

- entradas: as URLs;
- respostas esperadas: os rotulos `0` ou `1`.

### 2. Dividir Treino E Teste Novamente

```python
urls_train, urls_test, y_train, y_test = train_test_split(
    urls, labels, test_size=0.2, random_state=42
)
```

Essa divisao repete o que ja apareceu na celula 7. Como usa os mesmos parametros, tende a gerar a mesma separacao.

### 3. Criar O Vetorizador

```python
vectorizer = HashingVectorizer(analyzer='char', ngram_range=(3,5), n_features=5000)
```

O vetorizador e criado de novo para garantir que esta celula tenha o objeto `vectorizer` pronto para o treinamento.

### 4. Inicializar O Classificador

```python
clf = SGDClassifier(loss='log_loss', max_iter=1, warm_start=True)
```

Esse e o principal ponto de parametrizacao do modelo de IA.

`SGDClassifier` e um classificador linear treinado com uma tecnica chamada Stochastic Gradient Descent.

Em termos simples:

1. O modelo faz uma previsao.
2. Compara a previsao com o rotulo correto.
3. Mede o erro.
4. Ajusta seus pesos internos para errar menos na proxima vez.
5. Repete isso muitas vezes.

#### Parametro `loss='log_loss'`

Esse parametro define como o erro sera calculado.

Com `log_loss`, o modelo se comporta como uma regressao logistica para classificacao. Isso e adequado para problemas binarios, como:

```text
benigna ou maliciosa
```

Ele tambem permite trabalhar com a ideia de probabilidade interna, mesmo que o notebook use apenas a classe final prevista.

#### Parametro `max_iter=1`

Esse parametro define quantas passagens internas o classificador faz por chamada de treinamento.

No notebook, ele esta como `1` porque o treinamento sera controlado manualmente com `partial_fit`.

Em vez de mandar o modelo treinar tudo de uma vez, o notebook envia lotes de dados.

#### Parametro `warm_start=True`

Esse parametro indica que o modelo deve reaproveitar o que ja aprendeu em chamadas anteriores.

Sem essa ideia, cada novo treino poderia recomecar do zero. Para treinamento incremental, reaproveitar o aprendizado anterior e essencial.

### 5. Primeiro `partial_fit`

```python
X_init = vectorizer.transform(urls_train.iloc[0:1000])
y_init = y_train[0:1000]
clf.partial_fit(X_init, y_init, classes=[0,1])
```

`partial_fit` treina o modelo com apenas uma parte dos dados.

Na primeira chamada, o parametro `classes=[0,1]` e obrigatorio porque o modelo precisa saber quais classes existem.

Aqui:

- `0` significa benigna;
- `1` significa maliciosa.

### 6. Treinamento Em Batches

```python
batch_size = 100_000
for start in range(1000, len(urls_train), batch_size):
```

`batch_size` define quantas URLs entram em cada lote de treinamento.

Com `batch_size = 100_000`, o modelo processa ate 100 mil URLs por vez.

Isso e util porque bases grandes podem nao caber confortavelmente na memoria se forem processadas de uma vez.

Para cada lote, o notebook faz:

```python
X_batch = vectorizer.transform(batch_urls)
clf.partial_fit(X_batch, y_batch)
```

Ou seja:

1. transforma URLs em vetores;
2. entrega esses vetores ao modelo;
3. atualiza os pesos internos do modelo.

### 7. Avaliacao

```python
X_test = vectorizer.transform(urls_test)
y_pred = clf.predict(X_test)
```

Aqui o conjunto de teste e vetorizado, e o modelo gera previsoes.

```python
print("Acuracia:", accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

`accuracy_score` mostra a porcentagem geral de acertos.

`classification_report` mostra metricas mais detalhadas:

- precision: quando o modelo diz que e malicioso, quantas vezes ele esta certo;
- recall: de todas as URLs maliciosas reais, quantas ele conseguiu encontrar;
- f1-score: equilibrio entre precision e recall;
- support: quantidade de exemplos de cada classe no teste.

### Cuidado Com Acuracia

Acuracia alta nao significa automaticamente que o modelo e bom para producao.

Em seguranca, falsos negativos podem ser graves:

```text
URL maliciosa real classificada como benigna.
```

Falsos positivos tambem causam impacto:

```text
URL benigna bloqueada como maliciosa.
```

Por isso e importante olhar o relatorio completo.

## Celula 10: Secao De Exemplos De Classificacao

Tipo: Markdown.

Esta celula cria o titulo:

```text
5. Mostrar exemplos das classificacoes
```

A ideia e sair das metricas e observar exemplos concretos.

## Celula 11: Mostrar URLs Classificadas Como Benignas E Maliciosas

Tipo: Codigo.

Esta celula transforma novamente as URLs de teste:

```python
X_test = vectorizer.transform(urls_test)
```

Depois gera previsoes:

```python
y_pred = clf.predict(X_test)
```

Em seguida monta uma tabela:

```python
results = pd.DataFrame({
    'url': urls_test.values,
    'true_label': y_test,
    'pred_label': y_pred
})
```

Essa tabela tem:

- `url`: a URL analisada;
- `true_label`: o rotulo real;
- `pred_label`: o rotulo previsto pelo modelo.

Por fim, a celula mostra algumas URLs previstas como benignas e algumas previstas como maliciosas.

Essa etapa e importante porque ajuda o aluno a entender que o modelo nao e uma caixa magica. Ele gera uma classificacao que pode ser comparada com o rotulo real.

## Celula 12: Secao De Analise De URLs Avulsas

Tipo: Markdown.

Esta celula cria o titulo:

```text
6. Analise de URLs avulsas
```

A proxima celula permite digitar uma URL manualmente.

## Celula 13: Testar URLs Digitadas Pelo Usuario

Tipo: Codigo.

Esta celula cria uma funcao:

```python
def prever_url(url, vectorizer, model):
```

Ela recebe:

- `url`: texto digitado pelo usuario;
- `vectorizer`: o mesmo vetorizador usado no treinamento;
- `model`: o classificador treinado.

Dentro da funcao:

```python
X = vectorizer.transform([url])
pred = model.predict(X)[0]
```

A URL digitada e transformada em vetor e enviada ao modelo.

Depois:

```python
return 'MALICIOSA' if pred == 1 else 'BENIGNA'
```

Se o modelo devolver `1`, a funcao mostra `MALICIOSA`.

Se devolver `0`, mostra `BENIGNA`.

### Loop Interativo

```python
while True:
    url_teste = input("Digite uma URL para classificacao...")
```

O notebook fica pedindo URLs ate o usuario digitar:

```text
sair
exit
quit
```

Essa parte ajuda o aluno a perceber o fluxo completo:

```text
URL digitada -> vetor numerico -> modelo treinado -> classe prevista
```

## Parametros Mais Importantes Do Lab

Esta secao resume os parametros que mais afetam o comportamento da IA.

| Parametro | Onde Aparece | O Que Controla |
| --- | --- | --- |
| `label = 1` | Preparacao dos dados | Define exemplo malicioso |
| `label = 0` | Preparacao dos dados | Define exemplo benigno |
| `test_size=0.2` | Divisao treino/teste | Reserva 20% dos dados para avaliacao |
| `random_state=42` | Amostragem e divisao | Torna resultados mais reproduziveis |
| `analyzer='char'` | `HashingVectorizer` | Analisa a URL por caracteres |
| `ngram_range=(3,5)` | `HashingVectorizer` | Usa pedacos de 3 a 5 caracteres |
| `n_features=5000` | `HashingVectorizer` | Define o tamanho do vetor numerico |
| `loss='log_loss'` | `SGDClassifier` | Usa erro adequado para classificacao binaria |
| `max_iter=1` | `SGDClassifier` | Faz uma iteracao por chamada de treino |
| `warm_start=True` | `SGDClassifier` | Reaproveita aprendizado anterior |
| `classes=[0,1]` | Primeiro `partial_fit` | Informa as classes possiveis |
| `batch_size=100_000` | Loop de treino | Define quantas URLs entram por lote |

## Como Explicar Para Alunos Iniciantes

Uma forma simples de explicar o notebook:

```text
O modelo nao sabe o que e phishing por intuicao.
Ele aprende olhando muitos exemplos ja rotulados.
Cada URL vira uma lista de numeros.
O modelo ajusta pesos internos para separar URLs benignas de maliciosas.
Quando recebe uma URL nova, ele aplica os mesmos passos e escolhe a classe mais provavel.
```

## Limitacoes Do Lab

Este notebook e didatico e tem algumas limitacoes importantes:

- dominios populares nao sao garantia absoluta de benignidade;
- feeds publicos podem estar incompletos ou desatualizados;
- o modelo olha principalmente padroes textuais da URL;
- o modelo nao acessa o conteudo da pagina;
- o modelo nao analisa certificados, DNS, WHOIS, JavaScript ou comportamento;
- bons resultados no notebook nao significam prontidao para producao.

Em um ambiente real, classificacao de URLs deve combinar varias fontes e tecnicas, como reputacao, sandboxing, analise de conteudo, telemetria, regras, listas de bloqueio e revisao humana.
