# 💳 Detecção de Fraudes em Cartões de Crédito com Machine Learning

Projeto prático desenvolvido para o desafio de Machine Learning com foco em **dados altamente desbalanceados**, explorando o pipeline completo desde a preparação dos dados até a avaliação de métricas críticas de negócio.

---

## 📊 1. O Problema e o Desafio do Desbalanceamento
O dataset utilizado contém transações financeiras reais realizadas por cartões de crédito. O grande desafio deste problema é a **escassez de fraudes**: apenas cerca de **0,17% a 0,31%** das transações representam atividades fraudulentas.

* **Por que a acurácia engana:** Em bases com esse nível de desbalanceamento, um modelo ingênuo que preveja "não é fraude" para 100% dos casos atinge facilmente mais de **99,6% de acurácia**, mas falha totalmente ao não interceptar nenhuma fraude real.
* **A solução:** O foco da avaliação mudou completamente da acurácia global para o **Recall**, **Precision** e **F1-Score** da classe minoritária (fraude).

---

## 🛠️ 2. Preparação e Engenharia de Atributos
Para preparar os dados para o treinamento dos algoritmos, foram aplicadas as seguintes etapas no pipeline:
- **Engenharia de Recursos:** Aplicação de transformação logarítmica (`np.log(Amount + 1)`) na coluna de valores monetários para reduzir a forte assimetria (*skewness*) dos dados.
- **Normalização:** Utilização do `StandardScaler` nas colunas numéricas (`Time` e `LogAmount`) para colocá-las na mesma escala dos componentes gerados por PCA (`V1` a `V28`).
- **Divisão Estratificada:** Emprego de `stratify=y` no `train_test_split` para garantir que a proporção de fraudes fosse mantida de forma idêntica tanto no conjunto de treino quanto no de teste.

---

## 🤖 3. Modelagem e Resultados (Baseline)
Utilizamos uma **Regressão Logística** configurada com ajuste de pesos das classes (`class_weight='balanced'`) como modelo de *baseline*. Essa técnica penaliza erros na classe minoritária, forçando o modelo a prestar mais atenção nas fraudes.

### Métricas Obtidas (Classe 1 - Fraude):
- **Matriz de Confusão:** O modelo apresentou alta capacidade de varredura das transações maliciosas.
- **Recall (Sensibilidade):** Priorizado para garantir que o máximo de fraudes reais fossem detectadas.
- **Precision & F1-Score:** Monitorados de perto para equilibrar a detecção de fraudes sem gerar um volume excessivo de falsos positivos (bloqueios indevidos de clientes legítimos).

*(As saídas detalhadas com o relatório de classificação e a matriz de confusão encontram-se salvas nas células de output do notebook `.ipynb` deste repositório).*

---

## 🚀 4. Como Executar o Projeto
1. Clone este repositório para o seu computador.
2. Baixe o dataset oficial de detecção de fraudes do Kaggle (`creditcard.csv`).
3. Abra o Jupyter Notebook enviado no ambiente de sua preferência (como o Google Colab).
4. Execute as células em sequência para reproduzir o pipeline de pré-processamento, treinamento e avaliação.
