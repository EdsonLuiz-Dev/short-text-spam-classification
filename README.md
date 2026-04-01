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
- F1-score

### Dataset

[Enron Email Dataset — Metsis, Androutsopoulos e Paliouras (2006)](https://github.com/MWiechmann/enron_spam_data)  
33.716 emails rotulados como spam ou ham em proporção aproximadamente equilibrada.

---

## Estrutura do repositório

```
short-text-spam-classification/
├── data/
│   ├── enron_spam_data.csv       # Dataset (não versionado — ver instruções abaixo)
│   └── README.md                 # Instruções para download do dataset
├── figures/
│   └── exploratory_analysis.png  # Gráficos gerados pela análise
├── notebooks/
│   ├── analise_exploratoria.ipynb
│   └── main.ipynb
├── src/
│   └── methods/
│       ├── evaluation.py         # Métricas e avaliação dos modelos
│       ├── models.py             # Definição e treinamento dos classificadores
│       └── preprocessing.py     # Pré-processamento e vetorização do texto
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
python3 -c "import nltk; nltk.download('stopwords'); nltk.download('punkt')"

# 5. Inicie o Jupyter
jupyter notebook
```

### Dataset

O dataset não está versionado neste repositório por questões de tamanho. Para reproduzir os experimentos:

1. Acesse [github.com/MWiechmann/enron_spam_data](https://github.com/MWiechmann/enron_spam_data)
2. Baixe o arquivo `enron_spam_data.zip`
3. Extraia e mova o arquivo `enron_spam_data.csv` para a pasta `data/`

---

## Dependências

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