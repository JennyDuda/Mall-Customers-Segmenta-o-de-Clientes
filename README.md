# Mall-Customers-Segmenta-o-de-Clientes
Notebook completo que realiza download automático do dataset (via kagglehub), limpeza, EDA, clustering (K-Means), comparação de modelos supervisionados, visualizações avançadas (PCA/t-SNE) e geração automática de insights por cluster.

# 🛍 Mall Customers — Segmentação de Clientes

## 🎯 Objetivo
Gerar segmentos acionáveis de clientes e fornecer recomendações de negócio a partir de dados de clientes de um shopping.

---

## 📂 Dataset
- Fonte: [Mall Customers — Kaggle](https://www.kaggle.com/datasets/abdallahwagih/mall-customers-segmentation)  
- Contém 200 registros de clientes com as variáveis:
  - `CustomerID`
  - `Gender`
  - `Age`
  - `Annual_Income (k$)`
  - `Spending_Score (1-100)`

---

## 🧰 Metodologia
1. **Limpeza e Feature Engineering**
   - Criação de faixas etárias (`Age_Group`)  
   - Codificação de gênero (`Gender_Code`)  
   - Padronização das variáveis numéricas (`StandardScaler`)  

2. **Análise Exploratória de Dados (EDA)**
   - Histogramas, scatter plots e mapa de correlação  
   - Distribuição de clientes por faixa etária, gênero, renda e score de gastos  

3. **Clustering com K-Means**
   - Escolha do número de clusters baseada em Elbow e Silhouette Score  
   - Clusters visualizados em gráficos 2D (scatter, PCA, t-SNE)  
   - Silhouette Score obtido: 0.555  

4. **Comparativo de Modelos Supervisionados**
   - Modelos testados: Logistic Regression, Random Forest, Gradient Boosting  
   - Objetivo: prever a atribuição de clusters a partir das features originais  
   - Resultados (Accuracy / F1-Score):
     - Logistic Regression: 0.967 / 0.966  
     - Random Forest: 0.967 / 0.966  
     - Gradient Boosting: 0.950 / 0.950  

5. **Geração de Insights Automáticos e Recomendações**
   - Insights por cluster com idade média, renda média e nível de engajamento  
   - Recomendação de ação de marketing e fidelização para cada cluster  

---

## 🔹 Principais insights
- **Cluster 0:** adultos moderadamente engajados (~$55k). **Recomendação:** programas de fidelidade e marketing direcionado  
- **Cluster 1:** adultos altamente engajados (~$86k). **Recomendação:** ofertas premium e upselling  
- **Cluster 2:** jovens altamente engajados (~$26k). **Recomendação:** ofertas premium e upselling  
- **Cluster 3:** adultos pouco engajados (~$88k). **Recomendação:** campanhas de incentivo e promoções  
- **Cluster 4:** adultos pouco engajados (~$26k). **Recomendação:** campanhas de incentivo e promoções  

---

## 🚀 Próximos passos / Melhorias
- Testar diferentes valores de `k` com Elbow e Silhouette Score detalhados  
- Tuning dos modelos supervisionados com GridSearchCV  
- Criar dashboard interativo (Streamlit / Power BI) para filtrar e visualizar clusters  
- Avaliar estabilidade dos clusters com diferentes seeds ou bootstrap  
- Considerar variáveis adicionais (como histórico de compras, frequência) para segmentação mais precisa  

---

## 📝 Arquivos de saída
- `cluster_assignments.csv` — DataFrame com coluna `Cluster` adicionada  
- `cluster_summary.csv` — médias e contagens por cluster  

---

📎 **Contato:** [LinkedIn](https://www.linkedin.com/in/jennifer-freitas-mendes)
