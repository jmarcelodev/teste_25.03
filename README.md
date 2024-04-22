Dados e scrip da analise feita no dia 25 de março de 2024. Na planilha 'valid' estão os dados referentes aos talhões: 607_3; 605_7; 606_6; 605_2. Os demais foram usados para treinar o algoritmo presentes na planilha 'train_test'

Primeiramente, foi importando todas as bibliotecas que seriam utilizadas para a manipulação dos dados.
As planilhas foram carregadas, onde na planilha def2 ='valid.csv' são os dados que serão usados para a predição. Os dados dos demais talhões estão na planilha df1 ='train_test.csv'
Utilizando a biblioteca sklearn. Foi criado uma matriz X, removendos as variaveis não desejaveis para o treinamento e a variavel alvo, produtividade.
Na matriz y existe apenas a variavel alvo
Depois o conjunto de dados df1 foi dividido em que 70% foi para o treinamento e 30% para o teste

Foi importado a classe RandomForestRegression da biblioteca sklearn

Alguns parametros especificos foram organizados. min_samples_leaf=30: Esse parâmetro define o número mínimo de amostras necessárias para serem consideradas em um nó folha da árvore. Isso ajuda a evitar o excesso de ajuste (overfitting) ao limitar a complexidade da árvore.
n_estimators=1000: Este é o número de árvores na floresta.
n_jobs=-1: Isso utiliza todos os núcleos do processador para paralelizar o treinamento, o que pode acelerar o processo.
random_state=42: Isso define a semente aleatória para garantir que os resultados sejam reproduzíveis.
rfr.fit(X_train, y_train), o algoritmo está sendo treinando com os padrões de divisão feitos anteriormente

No trecho seguinte, foi feito um gráfico de barras horizontais para se verificar a importância das variaveis no algoritmo treinado.
feat_list = X.columns.values: obtem uma lista dos nomes das colunas do DataFrame X, que representam os recursos que foram utilizados para treinar o modelo.
feat_imp = rfr.feature_importances_: obtem as importâncias dos recursos do modelo RandomForestRegressor que foram treinados anteriormente. Isso fornece uma medida de quão importante cada recurso foi para fazer previsões.
sort_idx = np.argsort(feat_imp):se ordena os índices dos recursos com base em suas importâncias em ordem crescente.
plt.figure(figsize=(5,7)):  cria uma nova figura para o gráfico com dimensões 5x7 polegadas
plt.barh(range(len(sort_idx)),feat_imp[sort_idx], align='center'): cria um gráfico de barras horizontais. O eixo y representa os recursos ordenados por importância, enquanto o comprimento das barras representa a importância de cada recurso.
plt.yticks(range(len(sort_idx)),feat_list[sort_idx]): Esta linha define os rótulos do eixo y como os nomes dos recursos ordenados por importância.
plt.xlabel('Importancia dos Fatores'): Você está definindo o rótulo do eixo x como "Importância dos Fatores".
plt.title('Fatores importantes'): Esta linha define o título do gráfico como "Fatores importantes".
plt.draw(): Este comando desenha o gráfico.
plt.show(): Este comando exibe o gráfico na tela.

No trecho seguinte, o algoritmo RandomForest fará as predições para os dados do df2.
Remove as mesmas colunas que foram removidas anteriormente do DataFrame df1 durante o treinamento do modelo, mantendo apenas os recursos relevantes para fazer previsões.
O método .predict() do modelo RandomForestRegressor (rfr) para fazer previsões com base nos dados fornecidos. O argumento passado para este método é o conjunto de dados de teste pré-processado, contendo apenas os recursos relevante

Na próxima parte, o código calcula algumas métricas de avaliação do desempenho do seu modelo RandomForestRegressor em relação às previsões feitas para o conjunto de dados de validação (df2). mae = metrics.mean_absolute_error(df2['produtivid'], y_pred): Isso calcula o erro médio absoluto (MAE), rmse np.sqrt(metrics.mean_squared_log_error(df2['produtivid'], y_pred)): Isso calcula a raiz do erro quadrático médio (RMSE) logarítmico, r2 = r2_score(df2['produtivid'], y_pred): Isso calcula o coeficiente de determinação (R²)
