# Projeto Python IA: Inteligência Artificial e Previsões

### Case: Score de Crédito dos Clientes

Este projeto foi desenvolvido durante uma aula gratuita da **Jornada Python**.
Você foi contratado por um banco para definir o score de crédito dos clientes. O objetivo deste projeto é analisar todos os clientes do banco e, com base nessa análise, criar um modelo que consiga ler as informações do cliente e indicar automaticamente o score de crédito: **Ruim**, **Ok** ou **Bom**.

## Arquivos da Aula
Os arquivos utilizados neste projeto estão disponíveis [neste link](https://drive.google.com/drive/folders/1FbDqVq4XLvU85VBlVIMJ73p9oOu6u2-J?usp=drive_link).

## Ferramentas
- [Pandas](https://pandas.pydata.org/): Biblioteca para manipulação e análise de dados.
- [Scikit-learn](https://scikit-learn.org/stable/): Biblioteca para aprendizado de máquina em Python.

## Passo a Passo

### Passo 0: Entender o desafio da empresa e da sua área
Compreender o problema e os requisitos do banco para desenvolver um modelo eficaz.

### Passo 1: Importar a base de dados
```python
import pandas as pd

tabela = pd.read_csv('clientes.csv')
display(tabela)
```

### Passo 2: Preparar a base de dados para a inteligência artificial
- Verificar se a base tem problemas:
  ```python
  display(tabela.info())
  ```
- Tratar os dados para que estejam em formato numérico:
  - As colunas profissao, mix_credito e comportamento_pagamento precisam ser codificadas usando LabelEncoder.
  ```python
  from sklearn.preprocessing import LabelEncoder

  codificador = LabelEncoder()
  
  # Codificando as colunas
  tabela['profissao'] = codificador.fit_transform(tabela['profissao'])
  tabela['mix_credito'] = codificador.fit_transform(tabela['mix_credito'])
  tabela['comportamento_pagamento'] = codificador.fit_transform(tabela['comportamento_pagamento'])
  ```
### Passo 3: Criar um modelo de IA
- Preparar os dados de entrada (x) e a variável alvo (y):
  ```python
  x = tabela.drop(columns=["score_credito", "id_cliente"])
  y = tabela['score_credito']
  ```

### Passo 4: Escolher o melhor modelo
- Importar e treinar modelos de aprendizado de máquina, como RandomForestClassifier e KNeighborsClassifier.
  ```python
  from sklearn.model_selection import train_test_split
  from sklearn.ensemble import RandomForestClassifier
  from sklearn.neighbors import KNeighborsClassifier
  
  x_treino, x_teste, y_treino, y_teste = train_test_split(x, y, test_size=0.3)
  
  modelo_arvoredecisao = RandomForestClassifier()
  modelo_knn = KNeighborsClassifier()
  
  modelo_arvoredecisao.fit(x_treino, y_treino)
  modelo_knn.fit(x_treino, y_treino)
  ```

### Passo 5: Fazer previsões
- Avaliar a acurácia dos modelos e usar o melhor modelo para prever scores de novos clientes:
  ```python
  from sklearn.metrics import accuracy_score
  
  previsa_arvoredecisao = modelo_arvoredecisao.predict(x_teste)
  previsao_knn = modelo_knn.predict(x_teste)
  
  accuracy_arvoredecisao = accuracy_score(y_teste, previsa_arvoredecisao)
  accuracy_knn = accuracy_score(y_teste, previsao_knn)
  
  print("Acurácia do modelo de Árvore de Decisão:", accuracy_arvoredecisao)
  print("Acurácia do modelo KNN:", accuracy_knn)
  ```

### Importando Novos Clientes para Prever
- O modelo escolhido pode ser utilizado para prever scores de novos clientes, com as mesmas etapas de tratamento de dados aplicadas.
  ```python
    novos_clientes = pd.read_csv('novos_clientes.csv')
  # Realizar o mesmo processo de codificação e previsões
  ```

### Conclusão
Este projeto visa ajudar o banco a classificar o score de crédito dos clientes de forma automática, utilizando inteligência artificial para melhorar a tomada de decisões.

## Licença
Este projeto é para fins educacionais e não possui uma licença específica. Todos os direitos reservados à Jornada Python.
### Agradecimentos
Este projeto foi desenvolvido durante a aula gratuita da Jornada Python.

## Licença
Este projeto é para fins educacionais e não possui uma licença específica. Todos os direitos reservados à Jornada Python.

