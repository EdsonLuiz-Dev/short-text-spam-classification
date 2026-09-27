# short-text-spam-classification

Trabalho de Graduação — Fatec Itapetininga
Curso: Análise e Desenvolvimento de Sistemas
Aluno: Edson Luiz Vieira de Souza
Orientador: Prof. Danilo Ruy Gomes

---

## Sobre o projeto

Este repositório contém o código e os notebooks desenvolvidos para o TG intitulado:

> **Classificação de Spam em Emails: Um Estudo Comparativo de Algoritmos de Machine Learning Aplicados a Textos Curtos**

O trabalho investiga como o recorte deliberado das **150 primeiras palavras** do corpo de um email afeta o desempenho comparativo de algoritmos de aprendizado de máquina supervisionado na tarefa de detecção de spam.

### Algoritmos avaliados

- Naive Bayes Multinomial
- Support Vector Machine (SVM)
- Random Forest
- Regressão Logística

### Métricas utilizadas

- Acurácia
- Precisão
- Recall
- F1-score (métrica principal)

### Dataset

[TREC 2007 Public Spam Corpus](https://www.kaggle.com/datasets/imdeepmind/preprocessed-trec-2007-public-corpus-dataset)
73.932 emails rotulados (48.714 spam, 25.218 ham). Mediana de 192 palavras por email.

---

## Principais resultados

| Algoritmo | F1-score (150 pal.) | F1-score (texto integral) | Delta |
|-----------|:---:|:---:|:---:|
| Random Forest | 0.9947 | 0.9961 | -0.0014 |
| SVM | 0.9944 | 0.9960 | -0.0016 |
| Regressão Logística | 0.9919 | 0.9944 | -0.0025 |
| Naive Bayes | 0.9630 | 0.9627 | +0.0003 |

- A truncagem de 150 palavras retém **99.75%+** do F1-score em todos os modelos.
- SVM e Random Forest são **estatisticamente equivalentes** (McNemar p=1.0) e superiores aos demais (p<0.001).
- O platô de desempenho começa em ~75–100 palavras; 150 é uma escolha conservadora e segura.
- Naive Bayes é significativamente inferior, especialmente em recall (deixa spam passar).

---

## Estrutura do repositório

```
short-text-spam-classification/
├── data/
│   ├── trec_2007.csv               # Dataset principal (não versionado)
│   └── README.md
├── figures/
│   ├── exploratory_analysis_trec.png
│   ├── comparative_metrics_trec.png
│   ├── confusion_matrices_trec.png
│   ├── descriptive_stats_trec.png
│   ├── preliminary_results.png
│   └── conclusions/                 # Figuras das análises finais
│       ├── error_overlap_heatmap.png
│       ├── error_word_count_distribution.png
│       ├── f1_score_intervalo_confianca.png
│       ├── feature_importance_*.png
│       ├── learning_curves_*.png
│       ├── truncation_*.png
│       └── tabela_significancia.png
├── models/
│   └── trec/                        # Modelos treinados e artefatos
│       ├── model_naive_bayes.pkl
│       ├── model_svm.pkl
│       ├── model_random_forest.pkl
│       ├── model_regressao_logística.pkl
│       ├── tfidf.pkl
│       ├── X_train_tfidf.pkl
│       ├── X_test_tfidf.pkl
│       ├── y_train.pkl
│       ├── y_test.pkl
│       └── results.csv
├── notebooks/
│   ├── analise_exploratoria.ipynb        # Análise exploratória do corpus
│   ├── 02_preprocessing_trec.ipynb       # Pré-processamento TREC 2007
│   ├── 03_models_evaluation_trec.ipynb   # Treinamento e avaliação dos modelos
│   └── conclusions/                      # Análises finais
│       ├── 01_error_analysis.ipynb       # Análise detalhada de erros
│       ├── 02_truncation_impact.ipynb    # Impacto do recorte (150 pal. vs integral)
│       ├── 03_learning_curves.ipynb      # Curvas de aprendizado
│       ├── 04_feature_importance.ipynb   # Importância das features
│       ├── 05_statistical_tests.ipynb    # Testes estatísticos (Friedman, McNemar)
│       └── 06_truncation_comparison.ipynb # Comparação de múltiplos recortes (25–500)
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Instalação

### Pré-requisitos

- Python 3.10 ou superior
- pip

### Passo a passo

```bash
# 1. Clone o repositório
git clone https://github.com/seu-usuario/short-text-spam-classification.git
cd short-text-spam-classification

# 2. Crie e ative o ambiente virtual
python3 -m venv venv
source venv/bin/activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Baixe os dados do NLTK
python3 -c "import nltk; nltk.download('stopwords'); nltk.download('punkt'); nltk.download('punkt_tab')"

# 5. Inicie o Jupyter
jupyter notebook
```

### Dataset

O dataset não está versionado neste repositório por questões de tamanho. Para reproduzir os experimentos:

1. Acesse o [TREC 2007 no Kaggle](https://www.kaggle.com/datasets/imdeepmind/preprocessed-trec-2007-public-corpus-dataset)
2. Baixe o dataset e mova o CSV para `data/trec_2007.csv`

Alternativamente, o notebook `02_preprocessing_trec.ipynb` faz o download automático via `kagglehub`.

---

## Pipeline de pré-processamento

1. Truncagem para as **150 primeiras palavras**
2. Conversão para minúsculas
3. Remoção de caracteres não-alfabéticos
4. Tokenização (NLTK `word_tokenize`)
5. Remoção de stopwords (inglês)
6. Vetorização TF-IDF (`max_features=10000`, `ngram_range=(1,2)`, `sublinear_tf=True`)
7. Split estratificado 80/20 (`random_state=42`)

---

## Dependências principais

```
pandas==2.2.0
numpy==1.26.4
scikit-learn==1.4.0
nltk==3.8.1
matplotlib==3.8.2
seaborn==0.13.2
jupyter==1.0.0
ipykernel==6.29.0
```

---

## Referências

GATTANI, G.; MANTRI, S.; NAYAK, S. Comparative Analysis for Email Spam Detection Using Machine Learning Algorithms. In: **Modern Electronics Devices and Communication Systems**. Lecture Notes in Electrical Engineering, vol. 948. Springer, Singapore, 2023.

METSIS, V.; ANDROUTSOPOULOS, I.; PALIOURAS, G. Spam filtering with Naive Bayes — Which Naive Bayes? In: **Conference on Email and Anti-Spam (CEAS)**, 3., 2006, Mountain View. Proceedings [...] Mountain View: CEAS, 2006.

PHAN, X.; NGUYEN, L.; HORIGUCHI, S. Learning to classify short and sparse text & web with hidden topics from large-scale data collections. In: **International World Wide Web Conference**, 17., 2008, Beijing. Proceedings [...] New York: ACM, 2008. p. 91–100.