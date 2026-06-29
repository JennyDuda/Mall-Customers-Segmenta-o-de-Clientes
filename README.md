# 🛍 Mall Customers — Segmentação de Clientes

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/JennyDuda/Mall-Customers-Segmenta-o-de-Clientes/blob/main/Segmenta%C3%A7%C3%A3oClientes.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-orange?logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/status-concluído-brightgreen)

---

## Objetivo de negócio

Um shopping quer entender **quem são seus clientes** e **como agir diferente com cada grupo**.

A partir de dados demográficos e comportamentais de 200 clientes, identificamos segmentos naturais usando K-Means e traduzimos cada grupo em recomendações acionáveis de marketing — sem necessidade de dados rotulados.

---

## Dataset

**Fonte:** [Mall Customers — Kaggle](https://www.kaggle.com/datasets/abdallahwagih/mall-customers-segmentation)

| Variável | Descrição |
|---|---|
| `CustomerID` | Identificador único |
| `Gender` | Gênero (Female / Male) |
| `Age` | Idade em anos |
| `Annual Income (k$)` | Renda anual em milhares de dólares |
| `Spending Score (1–100)` | Score de propensão a gasto atribuído pelo shopping |

200 registros · sem valores ausentes · sem duplicatas.

---

## Metodologia

### 1. Limpeza e feature engineering

- Renomeação de colunas para consistência
- Criação de faixas etárias interpretáveis (`Age_Group`)
- Codificação de gênero com `map()` explícito — evita ordenação implícita do `LabelEncoder`
- Padronização com `StandardScaler` (necessária: K-Means usa distância euclidiana)

### 2. EDA — *Quem são nossos clientes?*

Cada visualização responde a uma pergunta de negócio: perfil demográfico, distribuição de renda e score, correlações. O scatter Renda × Score já antecipa os 5 grupos naturais antes de qualquer modelagem.

### 3. Seleção de k — Elbow + Silhouette

Dois critérios complementares:

- **Elbow (inércia):** cotovelo claro em k = 5
- **Silhouette Score:** 0.555 para k = 5, indicando boa separação entre clusters

### 4. Clustering com K-Means (k = 5)

| Cluster | Perfil | N |
|---|---|---|
| C0 | Renda média, gasto médio | ~39 |
| C1 | Renda alta, gasto baixo | ~40 |
| C2 | Renda baixa, gasto baixo | ~39 |
| C3 | Renda alta, gasto alto | ~35 |
| C4 | Renda baixa, gasto alto | ~35 |

### 5. Validação de estabilidade (bootstrap)

> Por que **não** usar classificação supervisionada para validar?
>
> Treinar um classificador para prever os próprios clusters do K-Means gera ~96% de acurácia de forma trivial — é uma validação circular. O modelo aprende a imitar o K-Means, não a detectar padrões reais.
>
> A pergunta correta é: **os clusters são estáveis?** Medimos isso com bootstrap (100 re-amostras com reposição) e calculamos o Adjusted Rand Index (ARI) entre cada resultado e o clustering original. ARI ≈ 1 significa que os mesmos grupos reaparecem independentemente da amostra.

### 6. Visualização avançada — PCA e t-SNE

Aplicados sobre as **4 features** da modelagem completa (`Age`, `Income`, `Score`, `Gender`). Com apenas 2 variáveis — como em versões anteriores — o PCA é redundante: ele já opera no próprio plano de visualização. A redução dimensional só faz sentido quando há mais dimensões do que o eixo de saída.

---

## Principais resultados

- **5 segmentos distintos** com Silhouette Score de 0.555 (boa separação)
- **Estabilidade confirmada** por bootstrap: clusters se reproduzem em re-amostras independentes
- **Cluster VIP (C3):** clientes de alta renda e alto gasto — segmento mais rentável, candidato a programa de fidelidade premium
- **Cluster de oportunidade (C1):** alta renda, baixo gasto — não estão gastando aqui; alvo de campanhas de conversão
- **Cluster jovem (C4):** baixa renda, alto engajamento — potencial de longo prazo com estratégias de acessibilidade

---

## Recomendações por segmento

| Cluster | Estratégia |
|---|---|
| C0 — Renda média, gasto médio | Programa de pontos, cupons e comunicação racional sobre valor |
| C1 — Renda alta, gasto baixo | Experiências exclusivas, amostras premium, campanhas personalizadas |
| C2 — Renda baixa, gasto baixo | Promoções de entrada, parcelamento, combos de baixo ticket |
| C3 — Renda alta, gasto alto | Clube VIP, pré-venda de lançamentos, upselling de categorias premium |
| C4 — Renda baixa, gasto alto | Cashback, desafios de compra, incentivos para aumentar ticket médio |

---

## Decisões técnicas

| Escolha | Justificativa |
|---|---|
| K-Means com k = 5 | Validado por Elbow + Silhouette; clusters bem separados e interpretáveis |
| `StandardScaler` antes do clustering | Sem padronização, renda (~15–137k) domina sobre score (1–99) na distância euclidiana |
| `map()` para gênero, não `LabelEncoder` | Variável binária: `map` é explícito e sem risco de ordenação implícita |
| Bootstrap em vez de classificação supervisionada | Valida robustez real dos clusters, não capacidade de imitar o próprio modelo |
| PCA/t-SNE em 4 features | Redução dimensional só agrega valor com mais dimensões do que o espaço de saída |

---

## Limitações

- Dataset pequeno (200 registros): resultados são ilustrativos, não generalizáveis sem mais dados
- Apenas 3 variáveis de comportamento: histórico de compras e frequência enriqueceriam os clusters
- K-Means assume clusters esféricos; DBSCAN ou GMM podem revelar formas diferentes — com 200 registros, o ganho seria marginal

---

## Arquivos do projeto

```
├── SegmentacaoClientes.ipynb   # Notebook principal
├── cluster_assignments.csv     # Dataset com coluna Cluster e Cluster_Label
├── cluster_summary.csv         # Médias e contagens por cluster
└── README.md
```

---

## Como executar

**Opção 1 — Google Colab (recomendado)**

Clique no badge Open in Colab no topo. O notebook baixa o dataset automaticamente via `kagglehub` (requer conta Kaggle gratuita).

**Opção 2 — Localmente**

```bash
pip install pandas numpy scikit-learn seaborn matplotlib scipy kagglehub
jupyter notebook SegmentacaoClientes.ipynb
```

Se preferir sem `kagglehub`, baixe o CSV em [kaggle.com/datasets/abdallahwagih/mall-customers-segmentation](https://www.kaggle.com/datasets/abdallahwagih/mall-customers-segmentation) e salve como `Mall_Customers.csv` na mesma pasta — o notebook detecta automaticamente.

---

## Stack

Python · pandas · NumPy · scikit-learn · seaborn · matplotlib · SciPy

---

📎 **Contato:** [LinkedIn](https://www.linkedin.com/in/jennifer-freitas-mendes) · [GitHub](https://github.com/JennyDuda)
