# 📊 04. Analytics & BI Layer (Power BI Ready)

[PT-BR]
Esta pasta contém a camada de abstração desenhada exclusivamente para ferramentas de visualização (Power BI, Tableau). O foco aqui é a **Refinaria de Dados**: transformar registros brutos em métricas executivas diretamente no motor do banco de dados.

[EN]
This folder contains the abstraction layer designed exclusively for visualization tools (Power BI, Tableau). The focus here is the **Data Refinery**: transforming raw records into executive metrics directly within the database engine.

---

## 🧠 Arquitetura do Projeto: The Growth Engine

[PT-BR]
O projeto contido nesta pasta demonstra como centralizar indicadores de performance (KPIs) complexos no SQL, utilizando uma abordagem de **três estágios lógicos**:

### 1. Agregação Temporal (CTE - Staging)
O código agrupa milhões de transações individuais por janelas temporais (mensais). Isso reduz a granularidade do dado para o nível necessário à tomada de decisão, eliminando o processamento pesado no front-end de BI.

### 2. Inteligência Comparativa (Window Functions)
Utilizamos funções de janela como `LAG()` para realizar viagens no tempo entre os registros. 
* **O funcionamento:** O SQL olha para o registro do mês atual e o compara com o mês anterior em uma única linha, permitindo o cálculo de **Crescimento Mensal (MoM)** e **Churn Rate** sem a necessidade de múltiplas subqueries lentas.

### 3. Persistência de Performance (Materialized Views)
Para garantir que um dashboard carregue instantaneamente, o resultado final é encapsulado em uma **Materialized View**.
* **Diferencial:** Ao contrário de uma View comum, esta armazena o resultado fisicamente. Isso significa que o Power BI lê uma tabela "pré-calculada", garantindo performance de milissegundos mesmo com milhões de vendas na origem.

---

## 📈 Impacto Técnico | Technical Impact

| Técnica / Technique | Por que usar? / Why use it? |
| :--- | :--- |
| **Window Functions** | Evita loops e subqueries complexas, otimizando o custo de CPU. / *Avoids loops and complex subqueries, optimizing CPU cost.* |
| **Materialized Views** | Transforma consultas de segundos em respostas instantâneas. / *Turns multi-second queries into instant responses.* |
| **Null Handling** | Tratamento de divisões por zero e meses sem dados, garantindo robustez. / *Handles division by zero and empty months, ensuring robustness.* |

---

[EN]
## 🧠 Project Architecture: The Growth Engine

The project in this folder demonstrates how to centralize complex KPIs in SQL using a **three-stage logical approach**:

1. **Temporal Aggregation (CTE - Staging):** Groups millions of transactions into monthly windows, reducing data granularity to the executive level.
2. **Comparative Intelligence (Window Functions):** Uses `LAG()` to perform "time travel" between records, calculating **MoM Growth** and **Churn** efficiently.
3. **Performance Persistence (Materialized Views):** Encapsulates the logic into a physical snapshot, allowing BI tools to read pre-calculated data in milliseconds.

---
> **"Abstrações custam caro; a precisão é gratuita."**
