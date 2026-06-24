# Registro de Progresso (PROGRESSO.md)

Este documento registra o estado atual do projeto de Análise de Churn, servindo como ponto de partida para qualquer nova sessão.

---

## 📌 Status Atual

* **Fase:** Modelagem de Machine Learning - Passo 6 (Avaliação e Interpretação do Modelo).
* **Última ação concluída:** O modelo de Árvore de Decisão foi treinado e avaliado com uma acurácia de 91,40% no conjunto de teste.
* **Ponto exato de parada:** O usuário avaliou a acurácia e está pronto para interpretar quais variáveis foram mais importantes para as decisões da árvore.

---

## 🏆 Conquistas do Projeto (O que já foi feito)

1. **Análise Exploratória (EDA):**
   * Inspeção inicial da base de dados de 100.000 clientes.
   * Criação e ajuste do gráfico de calor (Heatmap) com `plt.figure(figsize=(12, 8))` para facilitar a leitura.
   * Identificação das variáveis com maior correlação com a evasão de clientes (`churn_flag`).

2. **Preparação dos Dados (Preprocessing):**
   * Seleção dos 4 principais recursos (*Features*): `recency_days`, `cart_abandonment_rate`, `loyalty_score`, e `engagement_score`.
   * Criação das variáveis `X` (pistas) e `y` (alvo/churn_flag).
   * Instalação da biblioteca `scikit-learn` usando o comando mágico `%pip install scikit-learn`.
   * Divisão em treino/teste de 70/30 (`test_size=0.3`) com `random_state=42`.

3. **Treinamento e Avaliação do Modelo:**
   * Instanciação e treinamento do modelo de Árvore de Decisão (`DecisionTreeClassifier`).
   * Geração de previsões no conjunto de teste e cálculo da acurácia final de 91,40%.

---

## 📅 Próximos Passos (A Fazer)

* [x] Instanciar e treinar o modelo de Árvore de Decisão (`modelo.fit(X_train, y_train)`).
* [x] Fazer previsões nos dados de teste (`X_test`).
* [x] Avaliar o modelo medindo a acurácia com a métrica `accuracy_score` comparando com o gabarito real (`y_test`).
* [x] Interpretar as regras de decisão geradas pela árvore (importância dos recursos).
* [x] Discutir os riscos de a árvore crescer demais ("decorar" os dados ou overfitting) e testar podá-la.
* [x] Comparar a acurácia entre o modelo completo e o modelo podado nos dados de teste.
* [x] Desenhar visualmente a árvore podada para entender as regras de decisão na prática.
* [x] Introduzir e calcular a Matriz de Confusão para entender os erros e acertos em detalhe.
* [x] Explicar e avaliar o modelo usando métricas adicionais: Precisão, Recall (Sensibilidade) e F1-Score.
* [ ] Escrever o arquivo README.md documentando o projeto com rigor acadêmico/científico.
* [ ] Escrever o post profissional/científico para o LinkedIn explicando as descobertas e impactos de negócio.
