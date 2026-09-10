# Predição de Churn de Clientes — Pipeline Modularizado de MLOps

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge\&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-F7931E?style=for-the-badge\&logo=scikit-learn)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge\&logo=pandas)
![VS Code](https://img.shields.io/badge/VS%20Code-IDE-007ACC?style=for-the-badge\&logo=visualstudiocode)

Projeto desenvolvido para a **Atividade Prática 06 (Trabalho I)** da Unidade Curricular de **Engenharia de Dados & MLOps**, da **UniSENAI**.

O objetivo do projeto é desenvolver um **pipeline modularizado de Machine Learning em Python** capaz de identificar clientes com alto risco de **Churn**, utilizando dados históricos de transações de um e-commerce.

A solução integra etapas de **Engenharia de Dados, Ciência de Dados e MLOps**, permitindo realizar desde o processamento dos dados até o treinamento do modelo e a inferência para novos clientes.

---

## Cenário de Negócio

Uma loja virtual deseja identificar clientes que apresentam comportamento de inatividade ou baixa frequência de compras.

A partir do histórico de transações, o sistema processa os dados dos clientes, cria variáveis relevantes para análise e utiliza um modelo de classificação para prever quais clientes apresentam maior risco de Churn.

Neste projeto, o conceito de Churn é definido com base na **frequência de compras do cliente**, considerando como cliente em risco aquele que apresenta:

```text
Frequência de compras < 8
```

---

## Objetivos do Projeto

* Processar dados brutos de transações.
* Consolidar informações por cliente e categoria de produto.
* Criar uma variável de classificação para representar o Churn.
* Dividir os dados em conjuntos de treinamento e teste.
* Treinar um modelo de classificação utilizando Random Forest.
* Avaliar o desempenho do modelo.
* Modularizar o pipeline em diferentes arquivos Python.
* Realizar inferência para um novo cliente.
* Demonstrar uma estrutura básica de integração entre Engenharia de Dados, Ciência de Dados e MLOps.

---

## Arquitetura do Pipeline

O projeto foi dividido em três etapas principais:

```text
                    ┌─────────────────────────┐
                    │   raw_transactions.csv  │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │   data_processing.py    │
                    │                         │
                    │ • Leitura dos dados     │
                    │ • pivot_table           │
                    │ • Agregação             │
                    │ • Regra de Churn        │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │    model_training.py    │
                    │                         │
                    │ • Train/Test 70/30      │
                    │ • Random Forest         │
                    │ • Métricas              │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │         main.py          │
                    │                         │
                    │ • Orquestração           │
                    │ • Execução do pipeline  │
                    │ • Inferência             │
                    └─────────────────────────┘
```

---

## Estrutura do Projeto

```text
ATV_06_Projeto_Modular_Trio/
│
├── data/
│   └── raw_transactions.csv
│
├── data_processing.py
├── model_training.py
├── main.py
└── README.md
```

### Descrição dos arquivos

| Arquivo                     | Responsabilidade                                                                          |
| --------------------------- | ----------------------------------------------------------------------------------------- |
| `data/raw_transactions.csv` | Dataset bruto contendo o histórico de transações dos clientes.                            |
| `data_processing.py`        | Responsável pela leitura, tratamento, agregação dos dados e criação da variável de Churn. |
| `model_training.py`         | Responsável pelo treinamento do modelo Random Forest e cálculo das métricas.              |
| `main.py`                   | Ponto de entrada da aplicação e responsável pela orquestração do pipeline e inferência.   |
| `README.md`                 | Documentação do projeto.                                                                  |

---

## Módulo de Processamento de Dados

### `data_processing.py`

Este módulo representa a etapa de **Engenharia de Dados**.

A função `process_data()` realiza as seguintes operações:

1. Leitura do arquivo `raw_transactions.csv`.
2. Tratamento e organização dos dados.
3. Utilização do `pivot_table` do Pandas para consolidar as informações.
4. Agrupamento dos dados por cliente e categoria de produto.
5. Cálculo da frequência total de compras.
6. Criação da variável alvo utilizada pelo modelo.

A regra utilizada para classificação é:

```text
Frequência < 8  →  Churn
Frequência ≥ 8  →  Não Churn
```

---

## Módulo de Treinamento

### `model_training.py`

Este módulo representa a etapa de **Ciência de Dados**.

A função `train_model()` recebe os dados processados e executa as etapas necessárias para treinamento do modelo.

### Processo de treinamento

```text
Dados processados
       │
       ▼
Separação das variáveis
       │
       ▼
Divisão Train/Test
       │
       ├── 70% Treinamento
       │
       └── 30% Teste
       │
       ▼
Random Forest
       │
       ▼
Avaliação
```

O modelo utilizado é o:

```python
RandomForestClassifier
```

As principais métricas utilizadas são:

* Acurácia
* Matriz de Confusão
* Precision
* Recall
* F1-Score

---

## Orquestração e Inferência

### `main.py`

O arquivo `main.py` funciona como ponto de entrada da aplicação.

Ele é responsável por:

1. Executar o processamento dos dados.
2. Enviar os dados tratados para o módulo de treinamento.
3. Treinar o modelo.
4. Exibir as métricas de avaliação.
5. Criar um novo cliente de exemplo.
6. Realizar a previsão de Churn.
7. Exibir o resultado da inferência no terminal.

Dessa forma, o projeto mantém as responsabilidades separadas entre os diferentes módulos.

---

## Tecnologias e Bibliotecas

| Tecnologia   | Versão recomendada | Utilização                             |
| ------------ | -----------------: | -------------------------------------- |
| Python       |              3.10+ | Linguagem principal do projeto         |
| Pandas       |               2.0+ | Manipulação e análise dos dados        |
| NumPy        |              1.24+ | Operações numéricas                    |
| Scikit-Learn |               1.3+ | Machine Learning e avaliação do modelo |
| VS Code      |              Atual | Ambiente de desenvolvimento            |

### Principais recursos utilizados

**Pandas**

* Leitura de arquivos CSV.
* Manipulação de DataFrames.
* `pivot_table()`.
* Agregação e transformação de dados.

**NumPy**

* Operações numéricas.
* Manipulação de arrays.

**Scikit-Learn**

* `train_test_split()`
* `RandomForestClassifier`
* `accuracy_score()`
* `confusion_matrix()`
* `classification_report()`

---

## Como Executar

### 1. Pré-requisitos

Certifique-se de possuir instalado:

* Python 3.10 ou superior.
* Visual Studio Code.
* Terminal integrado do VS Code.

Para verificar a versão do Python:

```powershell
python --version
```

---

### 2. Instalar as dependências

Abra o terminal na pasta raiz do projeto e execute:

```powershell
python -m pip install pandas numpy scikit-learn
```

---

### 3. Executar o Pipeline

Após instalar as dependências, execute:

```powershell
python main.py
```

O sistema realizará automaticamente todo o fluxo:

```text
Processamento dos dados
        ↓
Treinamento do modelo
        ↓
Avaliação
        ↓
Inferência
        ↓
Resultado da previsão
```

---

## Resultado da Execução

Com a base utilizada no projeto, o pipeline apresentou o seguinte resultado:

```text
============================================================
INICIANDO PIPELINE DE CLASSIFICAÇÃO DE CHURN
============================================================

1. Carregando e tratando os dados de 'data/raw_transactions.csv'...

   -> Dataset processado: 50 clientes mapeados.

2. Treinando o modelo de ML (Random Forest) com divisão 70/30...

RESULTADOS E MÉTRICAS DO MODELO:

   • Acurácia: 100.00%

   • Matriz de Confusão:

[[8 0]
 [0 7]]

   • Relatório de Classificação:

              precision    recall  f1-score   support

           0       1.00      1.00      1.00         8
           1       1.00      1.00      1.00         7

    accuracy                           1.00        15

3. Realizando inferência para um Novo Cliente de Exemplo...

============================================================

RESULTADO DA PREVISÃO DO NOVO CLIENTE:

   • Previsão: 1
   • Classificação: ALTO RISCO DE CHURN (Inativo)
   • Confiança do Modelo: 100.00%

============================================================
```

> **Observação:** a acurácia de 100% apresentada corresponde aos resultados obtidos com o conjunto de dados utilizado neste trabalho. Em cenários reais, uma avaliação mais robusta deveria considerar diferentes divisões dos dados, validação cruzada e um conjunto de dados maior e mais representativo.

---

## Divisão do Trabalho

O desenvolvimento foi organizado em três responsabilidades principais:

| Papel                          | Responsabilidade                                                                    | Peso |
| ------------------------------ | ----------------------------------------------------------------------------------- | ---: |
| Pessoa A — Engenharia de Dados | Leitura do CSV, processamento dos dados, `pivot_table` e criação da regra de Churn. |  35% |
| Pessoa B — Ciência de Dados    | Treinamento do Random Forest, divisão dos dados e cálculo das métricas.             |  35% |
| Pessoa C — MLOps & Integração  | Desenvolvimento do `main.py`, orquestração dos módulos e realização da inferência.  |  30% |

---

## Fluxo de Dados

O fluxo completo da aplicação pode ser resumido da seguinte maneira:

```text
raw_transactions.csv
        │
        ▼
Processamento e agregação
        │
        ▼
Criação da variável Churn
        │
        ▼
Divisão dos dados 70/30
        │
        ▼
Random Forest
        │
        ▼
Avaliação do modelo
        │
        ▼
Novo cliente
        │
        ▼
Inferência
        │
        ▼
Risco de Churn
```

---

## Conceitos Aplicados

Durante o desenvolvimento foram aplicados conceitos relacionados a:

* Engenharia de Dados
* Ciência de Dados
* Machine Learning
* Classificação supervisionada
* Feature Engineering
* Manipulação de dados
* Agregação de dados
* Treinamento e teste de modelos
* Avaliação de modelos
* Inferência
* Modularização de código
* Orquestração de pipeline
* Fundamentos de MLOps

---

## Possíveis Evoluções

O projeto pode ser expandido futuramente com:

* Pipeline automatizado de treinamento.
* Validação cruzada.
* Ajuste de hiperparâmetros.
* Comparação entre diferentes algoritmos.
* Persistência do modelo treinado.
* API para disponibilização das previsões.
* Dashboard para acompanhamento dos clientes em risco.
* Banco de dados para armazenamento das previsões.
* Monitoramento de desempenho do modelo.
* Containerização com Docker.
* Automação utilizando CI/CD.
* Implementação de versionamento de modelos e dados.

---

## Licença e Créditos

Projeto acadêmico desenvolvido para a **Unidade Curricular de Engenharia de Dados & MLOps da UniSENAI**, como parte da **Atividade Prática 06 (Trabalho I)**.

O projeto possui finalidade educacional e demonstra a construção de um pipeline modularizado de Machine Learning aplicado à previsão de Churn de clientes.
