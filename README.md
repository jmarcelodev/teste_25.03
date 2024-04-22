Dados e scrip da analise feita no dia 25 de março de 2024. Na planilha 'valid' estão os dados referentes aos talhões: 607_3; 605_7; 606_6; 605_2. Os demais foram usados para treinar o algoritmo presentes na planilha 'train_test'

Primeiramente, foi importando todas as bibliotecas que seriam utilizadas para a manipulação dos dados.
As planilhas foram carregadas, onde na planilha def2 ='valid.csv' são os dados que serão usados para a predição. Os dados dos demais talhões estão na planilha df1 ='train_test.csv'
Utilizando a biblioteca sklearn. Foi criado uma matriz X, removendos as variaveis não desejaveis para o treinamento e a variavel alvo, produtividade.
Na matriz y existe apenas a variavel alvo
Depois o conjunto de dados df1 foi dividido em que 70% foi para o treinamento e 30% para o teste
