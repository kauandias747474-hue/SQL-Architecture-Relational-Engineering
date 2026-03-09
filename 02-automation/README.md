# ⚙️ 01. Database Automation & Business Logic

Este diretório contém a camada de inteligência processual do banco de dados. O objetivo principal é demonstrar como centralizar a lógica de negócio no core da infraestrutura para garantir consistência atômica e reduzir a latência de rede.

## 🚀 Projeto Demonstrativo: Motor de Clearing Financeiro

O código contido nesta pasta implementa um sistema de transferência de ativos com auditoria automatizada, utilizando o poder total do motor relacional para garantir que a precisão dos dados seja mantida sob qualquer circunstância.

### 🏗️ Arquitetura da Solução



1. **Stored Procedures (Fluxo Atômico):** - Gerencia o ciclo de vida completo de uma transação (Débito/Crédito).
   - Implementa controle de concorrência e **Rollback Automático** em caso de falhas, garantindo que o dinheiro nunca "desapareça" entre contas.

2. **Functions (Lógica Reutilizável):**
   - Encapsula regras de validação (ex: verificação de saldo e limites) que podem ser chamadas tanto pela aplicação quanto por outras consultas SQL.
   - Segue a filosofia **Vanilla-First**: cálculos pesados feitos diretamente onde o dado reside.

3. **Triggers (Auditoria Passiva):**
   - Cria uma trilha de auditoria imutável. Sempre que um saldo é alterado, o Trigger registra automaticamente o valor anterior e o novo valor em uma tabela de logs protegida.
   - **Diferencial:** Garante segurança mesmo se um comando `UPDATE` for executado manualmente fora da aplicação.

### 🛡️ Benefícios Técnicos
* **Consistência ACID:** Garantia de que todas as operações de um fluxo complexo terminem com sucesso ou sejam totalmente revertidas.
* **Integridade Blindada:** A lógica de negócio reside no banco, impedindo que bugs no Front-end ou Back-end corrompam os dados financeiros.
* **Performance:** Menor volume de dados trafegando entre servidor e aplicação (Single Round-trip).

---
> "Abstrações custam caro; a precisão é gratuita."
