# 🏋️‍♀️ Recomendação de Atividade Física (Regras de Associação)

---

## 🎯 Visão Geral

Esta aplicação demonstra a eficácia da **Mineração de Regras de Associação** (utilizando a lógica do Algoritmo Apriori) para construir um sistema de recomendação de treino.

O objetivo é analisar o comportamento de usuários e identificar associações fortes entre um **Objetivo de Treino** (antecedente) e os **Exercícios Praticados** (consequente), gerando recomendações com alta probabilidade de sucesso.

---

## 💡 Metodologia: Regras de Associação (Apriori)

O Apriori é a base para a mineração, focando em encontrar itemsets frequentes. A principal métrica de avaliação utilizada é a **Confiança**, que mede a validade da regra:

### Definição da Regra:

$$\text{Se Objetivo} \rightarrow \text{Exercício}$$

### Cálculo da Confiança:

A Confiança é a probabilidade condicional.

$$\text{Confiança}(\text{Objetivo} \rightarrow \text{Exercício}) = \frac{\text{Suporte}(\text{Objetivo} \cap \text{Exercício})}{\text{Suporte}(\text{Objetivo})}$$

Onde:
* **Suporte ($\text{Objetivo} \cap \text{Exercício}$):** É a frequência de transações que contêm **ambos** os itens.
* **Suporte ($\text{Objetivo}$):** É a frequência de transações que contêm apenas o objetivo (antecedente).



---

## 💾 Estrutura e Preparação dos Dados

Os dados brutos foram fornecidos em formato de texto (`CSV`) e processados em um formato de **transação**, onde cada elemento é uma lista contendo o objetivo e todos os exercícios praticados por um usuário (ID).

### Exemplo do Formato de Transação

| Transação | Objetivos e Exercícios |
| :---: | :--- |
| `[0]` | `['Massa', 'Levantamento_Peso', 'Flexao', 'Rosca_Direta', 'Supino']` |
| `[1]` | `['Peso', 'Corrida', 'Yoga', 'Pular_Corda', 'HIIT']` |
| `...` | `...` |

### Tratamento de Dados (Fix para Pandas NaN)

Para garantir a robustez, a leitura do arquivo foi feita diretamente na *string* para evitar que linhas com número inconsistente de itens fossem interpretadas como `float` pelo Pandas, o que causaria o erro de `AttributeError: 'float' object has no attribute 'split'`.

---

## 📊 Resultados e Recomendações Finais

O sistema foi executado com uma **Confiança Mínima de 75%** ($\text{min\_confianca}=0.75$) para garantir que apenas as associações mais fortes fossem recomendadas. O modelo simulado encontrou associações perfeitas (100% de Confiança) para os objetivos focais.

| Objetivo de Treino | Regras de Associação Encontradas (Confiança) | Insights de Domínio |
| :---: | :--- | :--- |
| **Ganho de Massa** | **Levantamento de Peso (1.00)**, **Rosca Direta (1.00)**, **Supino (1.00)** | Ações concentradas em hipertrofia e força máxima, como esperada pela teoria do treinamento. |
| **Perda de Peso** | **Corrida (1.00)**, **Yoga (1.00)**, **Pular Corda (1.00)**, **HIIT (1.00)** | Combinação de atividades de alto gasto calórico (HIIT, Corrida) e atividades que promovem recuperação e flexibilidade (Yoga). |
| **Recuperação Pós-Lesão** | **Yoga (1.00)**, **Ciclismo (1.00)**, **Alongamento (1.00)** | Ênfase em exercícios de baixo impacto que são cruciais para a reabilitação articular e muscular controlada. |

---

### 💻 Tecnologias

* `Python`
* `Pandas` (Para manipulação inicial de dados)
* `defaultdict` e `re` (Implementação da lógica Apriori e pré-processamento)
