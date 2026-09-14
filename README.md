# Reconhecimento de Dígitos Manuscritos com MNIST

Mini-projeto avaliativo do Módulo 2 do curso de Análise Preditiva com Python — SCTEC.

## Objetivo

Construir e comparar modelos de classificação capazes de reconhecer dígitos de 0 a 9 utilizando o dataset MNIST. O projeto também investiga o comportamento de um modelo diante de classes ausentes do treinamento e testa o reconhecimento de uma imagem própria.

## Tecnologias utilizadas

- Python 3.12.
- NumPy e Pandas: manipulação dos dados.
- Matplotlib e Seaborn: gráficos e matrizes de confusão.
- Scikit-learn: carregamento do MNIST, treinamento e avaliação dos modelos.
- Pillow: processamento da imagem própria.
- VS Code com as extensões Python e Jupyter: execução do notebook.

## Organização do projeto

- `notebooks/01_eda_mnist.ipynb`: código, gráficos e análises de todas as fases.
- `images/`: imagens próprias disponíveis para testes.
- `requirements.txt`: dependências e respectivas versões.
- `.gitignore`: arquivos e pastas que não devem ser versionados.
- `README.md`: apresentação e instruções de execução.

## Etapas desenvolvidas

### Fase 1 — Análise exploratória

Carregamento das 70.000 imagens do MNIST, verificação das dimensões, análise da distribuição das classes e visualização dos dígitos. Cada imagem possui 28 × 28 pixels, representados por 784 características.

### Fase 2 — Pré-processamento

Divisão estratificada em treino (70%), validação (10%) e teste (20%). Os pixels foram normalizados para o intervalo entre 0 e 1.

### Fase 3 — Treinamento

Foram comparadas quatro configurações para cada modelo, variando dois hiperparâmetros:

| Modelo | Hiperparâmetros avaliados |
|---|---|
| KNN | `n_neighbors` e `weights` |
| Random Forest | `n_estimators` e `max_depth` |
| MLP | `hidden_layer_sizes` e `alpha` |

As configurações foram selecionadas pelo desempenho no conjunto de validação.

### Fase 4 — Avaliação comparativa

Os três modelos foram avaliados no conjunto de teste com acurácia, precisão, recall e F1-score ponderados, matrizes de confusão e tempos de treinamento e predição.

| Modelo | Acurácia no teste |
|---|---:|
| MLP | 97,76% |
| KNN | 97,21% |
| Random Forest | 96,51% |

O MLP apresentou o melhor desempenho. A maior taxa de confusão entre um par de classes foi do dígito 4 classificado como 9 nos três modelos.

### Fases 5.1 e 5.2 — Classes ocultadas e teste OOD

Uma nova instância do MLP foi treinada sem os dígitos 4 e 7. Depois, recebeu apenas imagens dessas classes.

O modelo atribuiu classes conhecidas a esses dígitos, principalmente a classe 9. A análise discute essa limitação e o risco de falsa certeza, sem afirmar que a confiança elevada foi medida nesse experimento.

### Fase 5.3 — Imagem própria

A foto `images/imagem_thi_.jpeg`, contendo o dígito 3, foi convertida para cinza e teve suas cores invertidas. Foram aplicados recorte manual, separação do traço por limite de intensidade, centralização em 28 × 28 pixels e normalização.

O MLP completo classificou corretamente essa imagem como 3. O notebook apresenta a imagem processada ao lado das probabilidades das classes.

As outras imagens da pasta estão disponíveis para testes, mas não fazem parte desse resultado.

## Como executar

As instruções abaixo utilizam Linux e VS Code.

### 1. Obter o projeto

No terminal:

```bash
git clone https://github.com/ThiOliver/projeto-mnist.git
cd projeto-mnist
```

### 2. Criar e ativar o ambiente virtual

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Instalar as dependências

```bash
python -m pip install -r requirements.txt
```

### 4. Executar o notebook

1. Abra a pasta `projeto-mnist` no VS Code.
2. Instale as extensões Python e Jupyter, caso ainda não estejam instaladas.
3. Abra `notebooks/01_eda_mnist.ipynb`.
4. Selecione o ambiente `.venv` como kernel do notebook.
5. Execute as células em ordem, do início ao fim.

Os caminhos `../images/` consideram a pasta `notebooks` como diretório de execução do notebook.

É necessário acesso à internet para baixar o MNIST na primeira execução. Os modelos são treinados durante a execução; o tempo necessário varia conforme o computador.

## Limitações e melhorias possíveis

- O MLP utiliza um limite de 20 iterações e apresentou avisos de que a otimização ainda não havia convergido. Esse limite foi adotado para controlar o custo computacional.
- O recorte e o limite de intensidade da imagem própria foram ajustados para a foto utilizada.
- Um acerto em uma imagem própria não comprova desempenho equivalente em outras fotografias.
- Como melhorias, podem ser avaliados mais exemplos próprios, centralização automática e um limite maior de iterações, usando a validação para comparar as configurações.

## Versionamento

O desenvolvimento utiliza branches por etapa, com Pull Requests para a branch `develop`. A versão final será integrada à `main`, preservando as branches utilizadas.

## Vídeo de apresentação

O vídeo apresenta o objetivo do projeto, sua execução, a organização das tarefas e branches, as escolhas técnicas e as melhorias possíveis.

[Assistir ao vídeo de apresentação](https://drive.google.com/file/d/182HJvaaeOqzdzKzLoGM85ZZ1FuQBTePE/view?usp=drive_link)
