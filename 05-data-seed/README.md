# 💾 05. Data Seeding & Stress Testing

[PT-BR]
Esta pasta contém o ecossistema de simulação de carga e volume do repositório. O objetivo é validar a resiliência da arquitetura e a eficiência dos índices em um cenário que mimetiza o ambiente de produção em larga escala.

[EN]
This folder contains the load and volume simulation ecosystem for the repository. The goal is to validate architectural resilience and index efficiency in a scenario that mimics a large-scale production environment.

---

## 🏗️ Metodologia de Validação | Validation Methodology

### 1. Seed Scripts (Geração de Massa Crítica)
O projeto utiliza scripts otimizados para popular o banco de dados com milhões de registros sintéticos, garantindo que os testes de performance não sejam enviesados por tabelas pequenas.
* **Técnica:** Uso de geradores nativos e inserções em massa (Bulk Inserts) para criar volumes de dados realistas (1M+ de linhas) em segundos. | *Uses native generators and bulk inserts to create realistic data volumes (1M+ rows) in seconds.*

### 2. Stress Testing (Batismo de Fogo)
Simulação de alta concorrência e carga de processamento para identificar gargalos antes do deploy.
* **O funcionamento:** Scripts que executam consultas pesadas simultaneamente, monitorando o comportamento dos índices e a ocorrência de *Deadlocks*. | *Scripts that execute heavy concurrent queries to monitor index behavior and deadlock occurrences.*

### 3. Validação de Índices sob Carga
Monitoramento do custo de I/O e tempo de execução enquanto o banco está sob estresse.
* **Objetivo:** Garantir que a latência se mantenha estável mesmo quando o cache do sistema está sob pressão. | *Ensuring latency remains stable even when the system cache is under pressure.*

---

## 🔬 Como o sistema é testado | How the system is tested

[PT-BR]
A abordagem aqui é **empírica**. O script contido nesta pasta executa o seguinte fluxo:
1. **Inflação:** O banco é inflado artificialmente até atingir gigabytes de dados.
2. **Execução:** Consultas complexas (vistas na pasta 04) são rodadas contra essa massa.
3. **Análise:** Verificamos se o plano de execução (`EXPLAIN`) continua utilizando os índices corretamente ou se a performance degrada linearmente.

[EN]
The approach here is **empirical**. The script in this folder follows this workflow:
1. **Inflation:** The database is artificially inflated to reach gigabytes of data.
2. **Execution:** Complex queries (from folder 04) are run against this dataset.
3. **Analysis:** We verify if the execution plan (`EXPLAIN`) still uses indexes correctly or if performance degrades linearly.

---

## 📈 Impacto de Engenharia | Engineering Impact

| Recurso / Feature | Benefício / Benefit |
| :--- | :--- |
| **Previsibilidade** | Evita surpresas de performance no primeiro dia de produção. / *Prevents performance surprises on launch day.* |
| **Robustez / Robustness** | Identifica limites de hardware e configuração de memória. / *Identifies hardware limits and memory configuration.* |
| **Escalabilidade** | Prova que o "Vanilla SQL" suporta escala real. / *Proves that Vanilla SQL supports real scale.* |

