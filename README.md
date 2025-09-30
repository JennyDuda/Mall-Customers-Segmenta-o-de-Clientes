# Mall-Customers-Segmenta-o-de-Clientes
Notebook completo que realiza download automático do dataset (via kagglehub), limpeza, EDA, clustering (K-Means), comparação de modelos supervisionados, visualizações avançadas (PCA/t-SNE) e geração automática de insights por cluster.
🛍️ Mall Customers — Segmentação de Clientes
🎯 Objetivo

Gerar segmentos acionáveis de clientes e fornecer recomendações de negócio a partir de dados de clientes de um shopping.

📂 Dataset

Fonte: Mall Customers — Kaggle

Contém 200 registros com as seguintes variáveis:

CustomerID

Gender

Age

Annual_Income (k$)

Spending_Score (1-100)

🧰 Metodologia

Limpeza e Feature Engineering

Criação de faixas etárias (Age_Group)

Codificação de gênero (Gender_Code)

Padronização das variáveis numéricas (StandardScaler)

Análise Exploratória de Dados (EDA)

Histogramas, scatter plots e mapa de correlação

Distribuição de clientes por faixa etária, gênero, renda e score de gastos

Clustering com K-Means

Escolha do número de clusters baseada em Elbow e Silhouette Score

Visualização de clusters em gráficos 2D (scatter, PCA, t-SNE)

Silhouette Score: 0.555

Comparativo de Modelos Supervisionados

Modelos testados: Logistic Regression, Random Forest, Gradient Boosting

Objetivo: prever a atribuição de clusters a partir das features originais

Resultados (Accuracy / F1-Score):

Logistic Regression: 0.967 / 0.966

Random Forest: 0.967 / 0.966

Gradient Boosting: 0.950 / 0.950

Geração de Insights Automáticos e Recomendações

Insights por cluster com idade média, renda média e nível de engajamento

Recomendação de ações de marketing e fidelização para cada cluster

🔹 Principais Insights
Cluster	Perfil	Idade Média	Renda Média	Engajamento	Recomendação
0	Adultos	42.7	$55.3k	Moderado	Programas de fidelidade e marketing direcionado
1	Adultos	32.7	$86.5k	Alto	Ofertas premium e upselling
2	Jovens	25.3	$25.7k	Alto	Ofertas premium e upselling
3	Adultos	41.1	$88.2k	Baixo	Campanhas de incentivo e promoções
4	Adultos	45.2	$26.3k	Baixo	Campanhas de incentivo e promoções
🚀 Próximos Passos / Melhorias

Testar diferentes valores de k com Elbow e Silhouette Score detalhados

Tuning dos modelos supervisionados com GridSearchCV

Criar dashboard interativo (Streamlit / Power BI) para filtrar e visualizar clusters

Avaliar estabilidade dos clusters com diferentes seeds ou bootstrap

Considerar variáveis adicionais para segmentação mais precisa

📝 Arquivos de saída

cluster_assignments.csv — DataFrame com coluna Cluster adicionada

cluster_summary.csv — Médias e contagens por cluster
