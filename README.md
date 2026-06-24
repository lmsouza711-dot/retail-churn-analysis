# Retenção Preditiva: Modelagem de Churn de Clientes usando Árvores de Decisão

Este projeto apresenta o desenvolvimento e a validação de um modelo preditivo de evasão de clientes (*churn*), estruturado sob a perspectiva de **Customer Experience (CX)** e **Market Ops**. O objetivo principal é antecipar a perda de clientes de forma empírica para fundamentar ações de retenção personalizadas e eficientes.

---

## 🎯 Contexto de Negócio e Rigor Teórico

Conforme destacado pela literatura clássica de marketing e gestão (como os estudos da *Harvard Business Review* e relatórios da *McKinsey & Company*), a aquisição de um novo cliente é de **5 a 25 vezes mais dispendiosa** do que a retenção de um cliente atual. 

Neste contexto, a incapacidade de prever o churn de forma proativa gera dois grandes problemas operacionais:
1. **Ineficiência Alocativa:** Gastos de marketing de relacionamento direcionados a clientes saudáveis (falsos alarmes).
2. **Perda Silenciosa:** Clientes com alto risco de abandono que deixam a marca sem que qualquer ação de retenção seja aplicada (falsos negativos).

Este projeto utiliza ciência de dados e machine learning para mitigar ambos os problemas, encontrando o ponto ideal entre precisão operacional e cobertura de detecção.

---

## 🔬 Metodologia e Modelagem

### 1. Base de Dados
O estudo foi realizado utilizando uma base de dados contendo o histórico de **100.000 clientes**, que foi dividida metodologicamente em:
* **70.000 amostras (70%)** para o treinamento do modelo.
* **30.000 amostras (30%)** para o teste e validação de performance.

### 2. Seleção de Recursos (Features)
Após a análise exploratória e estudo de correlação das variáveis, selecionamos 4 variáveis críticas de comportamento de consumo e psicologia de consumo do cliente:
* `recency_days` (Há quantos dias o cliente não realiza compras - principal termômetro de engajamento).
* `cart_abandonment_rate` (A taxa média de abandono de produtos no carrinho).
* `loyalty_score` (Pontuação de lealdade computada pela marca).
* `engagement_score` (Métricas agregadas de engajamento nos canais digitais).

### 3. Mitigação de Sobreauste (*Overfitting*)
Durante a modelagem inicial com a **Árvore de Decisão** (`DecisionTreeClassifier`), constatou-se que um modelo sem restrições cresceu até atingir **25 níveis de profundidade**, alcançando **100% de acurácia nos dados de treino**, mas apresentando sinais claros de memorização exagerada dos ruídos (sobreajuste).

Para construir um modelo estável e interpretável no dia a dia da operação, aplicamos uma **técnica de poda** restringindo a profundidade máxima da árvore para 3 níveis (`max_depth=3`). Isso gerou um modelo extremamente enxuto e de fácil interpretação estratégica.

---

## 📈 Resultados e Performance do Modelo

O modelo podado de 3 níveis foi submetido à base de testes (dados inéditos) e avaliado com as seguintes métricas:

| Métrica | Performance (Classe Churn) | O que significa na Prática? |
| :--- | :---: | :--- |
| **Acurácia** | **89.91%** | A taxa de acertos geral do modelo ao classificar todos os clientes do teste. |
| **Precisão (*Precision*)** | **88.00%** | Das vezes em que o modelo alertou sobre um churn iminente, ele estava correto em **88%** delas (reduzindo o desperdício com falsos alarmes). |
| **Sensibilidade (*Recall*)** | **91.00%** | O modelo conseguiu mapear e antecipar **91%** de todos os clientes que iriam dar churn de verdade. |
| **F1-Score** | **89.00%** | Média harmônica balanceada entre precisão e recall, garantindo a robustez do modelo. |

### Matriz de Confusão (Validação de Erros)
A matriz de confusão gráfica gerada com as 30.000 previsões de teste detalha a assertividade do modelo:

* **Verdadeiros Negativos (Acerto - Ativo):** 14.343 clientes
* **Verdadeiros Positivos (Acerto - Churn):** 12.631 clientes
* **Falsos Positivos (Erro - Falso Alarme):** 1.737 clientes
* **Falsos Negativos (Erro Perigoso - Evasão não mapeada):** 1.289 clientes

---

## 🌳 Árvore de Decisão e Lógica de Negócios

A árvore de decisão gerada aponta que a variável mais crítica para identificar o risco de churn é `recency_days`, respondendo por cerca de **69% de importância** nas tomadas de decisão da árvore.

O fluxo de regras estruturado no modelo segue a lógica abaixo:
1. **Filtro Primário:** O cliente está sem comprar há mais de **193 dias**?
   * **Se NÃO (Menos de 6 meses):** A probabilidade de retenção é alta, refinada pela taxa de abandono do carrinho (limite de 63.5%).
   * **Se SIM (Mais de 6 meses):** O risco de churn aumenta drasticamente, sendo refinado pelo tempo limite de 243.5 dias (8 meses) sem compras e o volume de carrinhos abandonados.

---

## 🚀 Conclusão e Recomendações Táticas (CX)

Com um **Recall de 91%**, o modelo se mostra uma ferramenta altamente confiável para a operação de mercado. Recomenda-se a integração dos alertas gerados por este modelo aos sistemas de CRM da empresa para disparar ações automáticas:
* **Automação de Retenção:** Clientes classificados na folha de risco devem ser incluídos em fluxos de nutrição prioritária ou receber contatos proativos do time de Customer Experience.
* **Otimização de Orçamento:** A alta precisão (88%) garante que o investimento financeiro em cupons ou ofertas de retenção não seja desperdiçado com clientes saudáveis.

---

## 🛠️ Tecnologias Utilizadas
* **Python 3**
* **Pandas** e **NumPy** (Manipulação de dados)
* **Matplotlib** (Visualização gráfica)
* **Scikit-Learn** (Pré-processamento, Modelagem e Métricas de Avaliação)
