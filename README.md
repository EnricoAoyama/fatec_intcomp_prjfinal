# Atividade Avaliativa Final — Inteligência Computacional
## Tema: Previsão da capacidade instalada de usinas elétricas

Este repositório contém o desenvolvimento da atividade avaliativa final da disciplina de **Inteligência Computacional**, utilizando o dataset **Global Power Plant Database**, disponível no Kaggle.

Link do dataset: <https://www.kaggle.com/datasets/ranafayezz/global-power-plant>

## Problema escolhido

O problema escolhido foi de **regressão supervisionada**.

O objetivo é prever a capacidade instalada de uma usina elétrica, em megawatts (`capacity_mw`), com base em atributos como país, localização geográfica, fonte primária de energia, proprietário, ano de comissionamento e demais informações disponíveis no dataset.

## 2. Dataset

O dataset contém informações globais sobre usinas elétricas, incluindo:

- país;
- nome da usina;
- capacidade instalada;
- latitude e longitude;
- fonte primária de energia;
- combustíveis secundários;
- proprietário;
- ano de comissionamento;
- fonte dos dados;
- informações de geração de energia.

O dataset atende aos requisitos da atividade pois possui:

- mais de 500 registros;
- variáveis categóricas;
- variáveis numéricas;
- valores ausentes;
- necessidade de transformação e pré-processamento.

## Solução desenvolvida

A solução foi desenvolvida em Python utilizando principalmente:

- Pandas;
- NumPy;
- Matplotlib;
- Seaborn;
- Scikit-learn.

O notebook contempla:

- análise exploratória dos dados;
- estatísticas descritivas;
- histogramas;
- boxplots;
- scatterplots;
- heatmap de correlação;
- análise de valores ausentes;
- tratamento de dados ausentes;
- tratamento conservador de outliers;
- engenharia de atributos;
- separação treino/teste;
- construção de `Pipeline`;
- uso de `ColumnTransformer`;
- validação com K-Fold Cross Validation;
- otimização com `GridSearchCV`;
- avaliação com métricas de regressão.

## Engenharia de atributos

Foram criados atributos derivados dos dados originais:

### `is_renewable`

Indica se a fonte primária da usina é renovável ou não.

Essa variável ajuda o modelo a capturar diferenças estruturais entre fontes como solar, eólica, hidrelétrica, carvão, gás e óleo.

### `plant_age`

Representa a idade aproximada da usina, calculada a partir do ano de comissionamento.

Essa variável pode ajudar porque usinas mais antigas e mais novas podem apresentar padrões diferentes de capacidade instalada.

### `capacity_category`

Classifica a usina em categorias de porte, como pequena, média, grande e muito grande.

Essa variável foi utilizada apenas na análise exploratória, pois é derivada diretamente da variável alvo `capacity_mw`. Portanto, ela não foi usada como preditora no modelo para evitar data leakage.

## Prevenção de Data Leakage

Data leakage ocorre quando informações que não estariam disponíveis no momento da previsão são usadas durante o treinamento do modelo.

Para evitar esse problema:

- a variável alvo `capacity_mw` não foi usada como atributo preditor;
- `capacity_category` não foi usado no treinamento, pois deriva da variável alvo;
- colunas relacionadas à geração de energia foram removidas, pois podem estar diretamente associadas à capacidade instalada;
- o pré-processamento foi feito dentro de um `Pipeline`, evitando que imputação, escalonamento ou codificação fossem ajustados usando dados de teste.

## Modelo utilizado
Foi utilizado o algoritmo `KNeighborsRegressor`.

O KNN para regressão prevê um valor com base nas observações mais próximas no conjunto de treino.

Foram testados os seguintes hiperparâmetros com `GridSearchCV`:

- `n_neighbors`: quantidade de vizinhos;
- `weights`: ponderação uniforme ou por distância;
- `p`: métrica de distância, Manhattan ou Euclidiana.

## Métricas de avaliação

Como o problema é de regressão, foram utilizadas métricas adequadas a esse tipo de problema:

- MAE — Mean Absolute Error;
- RMSE — Root Mean Squared Error;
- R² — coeficiente de determinação.

A métrica principal considerada foi o **MAE**, conforme solicitado no enunciado da atividade.

## Resultados

Os resultados finais são obtidos ao executar o notebook, pois podem variar de acordo com a versão do dataset baixado e com o ambiente de execução.

O notebook exibe:

- MAE médio em validação cruzada;
- melhor combinação de hiperparâmetros encontrada pelo `GridSearchCV`;
- MAE final no conjunto de teste;
- RMSE final;
- R² final;
- gráficos comparando valores reais e previstos.

## Dificuldades encontradas

As principais dificuldades foram:

- valores ausentes em diversas colunas;
- presença de outliers reais na capacidade instalada;
- variáveis categóricas com muitas categorias diferentes;
- risco de data leakage com colunas de geração energética;
- assimetria forte na variável alvo.

## Conclusões

O projeto construiu um fluxo completo de Ciência de Dados aplicado a um problema real de regressão.

A preparação dos dados foi uma etapa central, pois o dataset apresenta valores ausentes, categóricas, outliers e variáveis com escalas diferentes.

O uso de `Pipeline` e `ColumnTransformer` tornou o fluxo mais organizado, reproduzível e seguro contra data leakage.

## Como executar o projeto

Este projeto pode ser executado de duas formas: diretamente no Google Colab ou localmente em sua máquina.

### Opção 1: Executar pelo Google Colab

A forma mais simples de executar o projeto é pelo Google Colab, sem necessidade de instalação local.

Acesse o notebook pelo link abaixo:

[Visualizar e executar no Google Colab](https://colab.research.google.com/drive/14RkxwwBu62DeCD9EUThGfCWsb0n7SytA?usp=sharing)

Após abrir o notebook:

1. Clique em Arquivo > Salvar uma cópia no Drive, caso queira editar.
2. Execute as células em ordem.
3. Caso necessário, faça o upload do dataset no ambiente do Colab ou ajuste o caminho do arquivo CSV conforme indicado no notebook.

### Opção 2: Executar localmente

Para executar o projeto em sua máquina, siga os passos abaixo.

1. Clone este repositório:
```bash
git clone https://github.com/EnricoAoyama/fatec_intcomp_prjfinal
```

2. Acesse a pasta do projeto:
```bash
cd <NOME_DA_PASTA_DO_REPOSITORIO>
```

3. Instale as dependências:
```bash
pip install -r requirements.txt
```

4. Abra o notebook:
```bash
jupyter notebook IntComp_Atividade_Final_Global_Power_Plant.ipynb
```

5.Execute as células em ordem.

Observação: certifique-se de que o arquivo CSV do dataset esteja disponível na pasta correta ou ajuste o caminho do arquivo no notebook.
