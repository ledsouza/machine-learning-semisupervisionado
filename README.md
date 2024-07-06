## Classificação de Qualidade do Leite com Aprendizado Semi-Supervisionado

![Static Badge](https://img.shields.io/badge/Status-Finalizado-green)

## Descrição

Este projeto utiliza algoritmos de aprendizado de máquina semi-supervisionado para classificar a qualidade do leite como alta, média ou baixa. O objetivo é treinar um modelo capaz de prever a qualidade de novas amostras de leite com base em suas características físico-químicas, mesmo com um conjunto limitado de dados rotulados.

## Tecnologias Utilizadas

- Python
- Pandas
- Scikit-learn
- joblib

## Dicionário de Dados

| Coluna | Descrição | Tipo de Dado |
|---|---|---|
| pH | Nível de acidez ou alcalinidade do leite | float64 |
| Temperatura | Temperatura do leite em graus Celsius | int64 |
| Sabor | Indicador binário de qualidade do sabor (1 para alta, 0 para baixa) | int64 |
| Odor | Indicador binário de qualidade do odor (1 para alta, 0 para baixa) | int64 |
| Gordura | Indicador binário de qualidade da gordura (1 para alta, 0 para baixa) | int64 |
| Turbidez | Indicador binário de qualidade da turbidez (1 para alta, 0 para baixa) | int64 |
| Cor | Valor numérico representando a tonalidade da cor do leite | int64 |
| Qualidade | Classificação da qualidade do leite ("alta", "média", "baixa") | object |

## Descrição Detalhada do Projeto

### Contexto

O projeto foi desenvolvido durante um curso da Alura sobre algoritmos de machine learning semi-supervisionado. Os dados utilizados foram previamente tratados e disponibilizados para o curso.

### Pré-processamento de Dados

- **Normalização:** Os dados numéricos foram normalizados utilizando o `MinMaxScaler` do Scikit-learn.
- **Tratamento de Rótulos:** A variável alvo "Qualidade" foi codificada numericamente usando o `LabelEncoder`.
- **Dados Não Rotulados:** Para os algoritmos semi-supervisionados, os dados não rotulados foram representados pelo valor -1.

### Modelagem

- **Modelo Base (Supervisionado):** Um modelo base foi treinado utilizando o algoritmo SVM (`SVC`) com kernel linear, apenas com os dados rotulados.
- **Self-Training:** O modelo base foi aprimorado utilizando o algoritmo Self-Training. As amostras não rotuladas foram inicialmente classificadas pelo modelo base, e aquelas com alta probabilidade de pertencer a uma classe específica foram adicionadas ao conjunto de treino com seus rótulos previstos. O modelo foi então retreinado com o novo conjunto de dados.
- **Label Propagation:** O algoritmo Label Propagation foi aplicado aos dados rotulados e não rotulados. Este algoritmo propaga os rótulos conhecidos para os dados não rotulados com base na estrutura do grafo de similaridade entre as amostras.

### Avaliação do Modelo

O desempenho dos modelos foi avaliado utilizando a métrica `classification_report` do Scikit-learn, que fornece as métricas de precisão, recall e F1-score para cada classe, além da acurácia geral do modelo.

### Resultados

Os resultados mostraram que o modelo Label Propagation obteve o melhor desempenho, superando o modelo SVM supervisionado e o modelo Self-Training.

### Salvando e Carregando o Modelo

O modelo final (Label Propagation) e o `MinMaxScaler` foram salvos em arquivos pickle utilizando a biblioteca `joblib`. O código para carregar o modelo e o scaler também é fornecido, permitindo a utilização do modelo treinado para classificar novos dados.
