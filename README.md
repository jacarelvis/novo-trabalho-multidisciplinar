# Classificacao da Qualidade de Vinhos com KNN

**Trabalho Interdisciplinar — UniEduK**
Disciplinas: Matematica para Computacao | IA e suas Aplicacoes | Fundamentos de Programacao | Fundamentos de Logica

---

## Sobre o Projeto

Este projeto implementa o algoritmo **K-Nearest Neighbors (KNN)** para classificar a qualidade de vinhos com base em atributos fisico-quimicos. O trabalho foi desenvolvido em duas etapas principais: analise exploratoria com pre-processamento dos dados, e implementacao do KNN de forma manual (sem bibliotecas prontas) e com a biblioteca scikit-learn, seguida de comparacao entre os resultados.

**Dataset utilizado:** Wine Quality Dataset (UCI Machine Learning Repository)
**Variavel classificada:** Qualidade binaria — Boa (quality >= 7) vs Ruim (quality < 7)

---

## Estrutura do Repositorio

```
projeto_knn/
│
├── README.md                              <- Este arquivo
│
├── wine_quality_dataset.csv               <- Dado bruto original (6497 amostras, 13 colunas)
├── wine_quality_filtrado.csv              <- Dado preparado (sem coluna 'type', qualidade binarizada)
│
├── Notebook1_EDA_Preprocessamento.ipynb  <- Analise exploratoria + pre-processamento
├── Notebook2_KNN_Comparacao.ipynb        <- KNN manual + KNN sklearn + comparacao
│
├── normalizacao_params.csv               <- Media e desvio padrao por feature (calculados no treino)
├── indices_treino.npy                    <- Indices da divisao de treino (reproducibilidade)
├── indices_teste.npy                     <- Indices da divisao de teste (reproducibilidade)
│
├── eda_distribuicao_qualidade.png        <- Grafico: distribuicao das classes de qualidade
├── eda_correlacao.png                    <- Grafico: heatmap de correlacao entre atributos
├── eda_boxplots.png                      <- Grafico: boxplots dos atributos por qualidade
├── eda_histogramas.png                   <- Grafico: histogramas de todos os atributos
├── prep_binarizacao.png                  <- Grafico: comparacao antes/depois da binarizacao
├── comparacao_acuracia.png              <- Grafico: acuracia por K (manual vs sklearn)
└── knn_matriz_confusao.png              <- Grafico: matriz de confusao do modelo final
```

---

## Descricao Detalhada dos Arquivos

### Dados

| Arquivo | Descricao |
|---------|-----------|
| `wine_quality_dataset.csv` | Dataset bruto com 6497 amostras e 13 colunas: 11 atributos fisico-quimicos, `quality` (nota de 3 a 9) e `type` (red/white) |
| `wine_quality_filtrado.csv` | Dataset preparado: coluna `type` removida, `quality` substituida por `qualidade_binaria` (0=ruim/1=boa) |
| `normalizacao_params.csv` | Media e desvio padrao de cada feature calculados APENAS no conjunto de treino, para uso na normalizacao do Notebook 2 |
| `indices_treino.npy` | Indices aleatorios (seed=42) usados para selecionar as amostras de treino (80%) |
| `indices_teste.npy` | Indices aleatorios (seed=42) usados para selecionar as amostras de teste (20%) |

### Notebooks

#### `Notebook1_EDA_Preprocessamento.ipynb`
Notebook de analise exploratoria e preparacao dos dados. Contem:
- Carregamento e visao geral do dataset
- Estatisticas descritivas
- Verificacao de valores ausentes
- Distribuicao da variavel alvo
- Matriz de correlacao entre atributos
- Boxplots e histogramas
- Pre-processamento completo: remocao de coluna categorica, binarizacao da variavel alvo, normalizacao Z-score e divisao treino/teste
- Geracao dos arquivos de dados preparados

#### `Notebook2_KNN_Comparacao.ipynb`
Notebook principal com a implementacao e comparacao do KNN. Contem:
- **Implementacao manual do KNN**: funcoes `distancia_euclidiana`, `knn_classificar_ponto`, `knn_prever_conjunto` e `calcular_acuracia_manual` — implementadas do zero usando apenas Python/math/collections, sem sklearn
- **Implementacao com sklearn**: uso do `KNeighborsClassifier` com testagem de hiperparametros (K, metric, weights)
- **Comparacao dos resultados**: graficos, tabela comparativa e analise critica das duas abordagens

---

## Como Executar

1. Instale as dependencias:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

2. Execute o Notebook 1 primeiro (gera os arquivos de dados preparados):
```bash
jupyter notebook Notebook1_EDA_Preprocessamento.ipynb
```

3. Execute o Notebook 2 (usa os arquivos gerados pelo Notebook 1):
```bash
jupyter notebook Notebook2_KNN_Comparacao.ipynb
```

> Os notebooks devem ser executados na mesma pasta onde estao os arquivos CSV.

---

## Resultados Obtidos

| Abordagem | Amostras Treino | Amostras Teste | Melhor K | Acuracia |
|-----------|----------------|----------------|----------|----------|
| KNN Manual | 500 | 200 | Veja o notebook | Veja o notebook |
| KNN sklearn | ~5197 | ~1300 | Veja o notebook | Veja o notebook |

> Os valores exatos de K e acuracia sao exibidos ao executar os notebooks.

---

## Atributos do Dataset

| Atributo | Descricao |
|----------|-----------|
| fixed acidity | Acidez fixa (acidos nao volareis) |
| volatile acidity | Acidez volatil (acido acetico — vinagre) |
| citric acid | Acido citrico (frescor e sabor) |
| residual sugar | Acucar residual apos fermentacao |
| chlorides | Concentracao de cloreto de sodio (sal) |
| free sulfur dioxide | SO2 livre (antimicrobiano e antioxidante) |
| total sulfur dioxide | SO2 total (livre + ligado) |
| density | Densidade do liquido |
| pH | Nivel de acidez geral (0=muito acido, 14=muito basico) |
| sulphates | Sulfato de potassio (conservante) |
| alcohol | Teor alcoolico (% por volume) |
| quality | **Variavel alvo** — nota de 0 a 10 dada por especialistas |
| type | Tipo do vinho: red ou white (removida no pre-processamento) |

---
