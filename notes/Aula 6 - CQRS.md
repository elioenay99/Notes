---
title: Aula 6 - CQRS
created: '2024-09-13T15:27:58.973Z'
modified: '2024-09-13T20:21:28.306Z'
---

### Aula 6 - CQRS

---

#### **Introdução**

**CQRS (Command Query Responsibility Segregation)** é um padrão arquitetural que surgiu a partir do princípio de **CQS (Command Query Separation)**, proposto por **Bertrand Meyer**. O princípio CQS estabelece que:

> **"Cada método deve ser um comando que realiza uma ação ou uma consulta que retorna dados, mas não ambos."**

Essa separação visa melhorar a clareza e a previsibilidade do código, eliminando efeitos colaterais indesejados ao invocar métodos.

**Martin Fowler** complementa:

> **"Como o termo 'comando' é amplamente usado em outros contextos, prefiro me referir a eles como 'modificadores'. Você também vê o termo 'mutadores'."**

O princípio **CQS** ajuda a eliminar efeitos colaterais e respeita o **Princípio da Responsabilidade Única (Single Responsibility Principle)**, evitando que um método mude por motivos diferentes. No entanto, é mais um conselho do que uma regra rígida, pois em muitos cenários é complexo de aplicar, como ao desempilhar um elemento ou em ambientes multi-thread intensos.

---

#### **Relação entre CQS e CQRS**

Enquanto o **CQS** atua no nível de classes e métodos, o **CQRS**, criado por **Greg Young**, aplica o princípio de separação de comandos e consultas de forma mais ampla, afetando o modelo de domínio e a arquitetura da aplicação.

No **Domain-Driven Design (DDD)**, modelamos as regras de negócio através de objetos de domínio. A execução de uma regra de negócio está mais relacionada à escrita, pois envolve mutação de estado. Exemplos:

- **Compra de um produto**
- **Cálculo de impostos**
- **Realização de um exame**
- **Matrícula de um aluno**

Essas operações modificam o estado do sistema e estão associadas a comandos.

---

#### **Repositórios e Agregados**

- **Persistência de Agregados:** Feita através de **Repositórios**, com granularidade no nível de **Aggregate Root**.
- **Relacionamento entre Agregados:** Feito por **identidade**, não por referência direta.
- **Desafios:** Nem todos os dados precisam ser obtidos via repositório. Consultas complexas podem envolver múltiplos agregados, tornando o processo ineficiente.

---

#### **DTOs e Assemblers**

No cenário de um **Pedido (Order)** com diversos componentes (data, código, itens, total, frete, cliente, impostos), é comum:

- **Decompor em Objetos de Domínio:** `Order`, `Item`, `Customer`, `Taxes`.
- **Utilizar DTOs:** Para transferência de dados entre camadas.
- **Aplicar DTO Assemblers:** Responsáveis por converter DTOs em objetos de domínio e vice-versa, desacoplando a estrutura interna da aplicação do formato de transporte dos dados.

---

#### **Padrão CQRS**

**CQRS** promove a separação entre:

- **Modelo de Escrita (Comandos):** Focado em mutações de estado e regras de negócio.
- **Modelo de Leitura (Consultas):** Focado em recuperar dados para exibição, sem lógica de negócio.

**Características:**

- **Comandos:**
  - Orientados a tarefas específicas.
  - Podem ser processados de forma assíncrona (filas).
- **Consultas:**
  - Nunca modificam dados.
  - Retornam DTOs diretamente.
  - Não envolvem o domínio.

---

#### **Arquitetura CQRS: Command Stack e Query Stack**

##### **Command Stack (Pilha de Comandos)**

- **Responsabilidade:** Operações de escrita e atualização.
- **Domínio:** Contém o **Domain Model** com regras de negócio.
- **Processo:** Recebe comandos, aplica lógica de negócio e persiste mudanças.

##### **Query Stack (Pilha de Consultas)**

- **Responsabilidade:** Operações de leitura.
- **Modelo de Leitura:** Otimizado para consultas eficientes.
- **Processo:** Acessa diretamente o banco de leitura para retornar dados.

**Benefícios:**

- **Desempenho Otimizado:** Consultas são mais rápidas sem a sobrecarga do domínio.
- **Escalabilidade Independente:** Leitura e escrita podem ser escaladas separadamente.
- **Manutenção Simplificada:** Regras de negócio centralizadas no modelo de domínio.

---

#### **Separação dos Dados de Escrita e Leitura**

- **Necessidade:** Não é obrigatório separar fisicamente os bancos de dados, mas é comum para otimização.
- **Motivos:**
  - **Desempenho:** Modelos de leitura podem ser desnormalizados para consultas rápidas.
  - **Escalabilidade:** Bancos de leitura podem ser replicados conforme a demanda.

---

#### **Normalização vs. Desnormalização**

- **Normalização (Escrita):**
  - Evita duplicação de dados.
  - Garante consistência e integridade.
- **Desnormalização (Leitura):**
  - Duplica dados para melhorar desempenho de consultas.
  - Pode levar a inconsistências se não sincronizado adequadamente.

---

#### **Desafios de Sincronização**

**Consistência Eventual:**

- **Definição:** Os dados no modelo de leitura serão eventualmente consistentes com o modelo de escrita.
- **Desafios:**
  - **Latência de Propagação:** Tempo entre a escrita e a atualização da leitura.
  - **Gestão de Eventos:** Necessidade de garantir que todas as mudanças sejam refletidas no modelo de leitura.

---

#### **Teorema CAP**

**Elementos:**

1. **Consistência (Consistency):** Todos os nós veem os mesmos dados simultaneamente.
2. **Disponibilidade (Availability):** O sistema responde a todas as requisições.
3. **Tolerância a Partições (Partition Tolerance):** O sistema continua operando mesmo com falhas de comunicação.

**Implicações:**

- **Escolha de Dois:** Não é possível garantir todos os três simultaneamente.
- **CQRS Geralmente Favorece:**
  - **Disponibilidade (A)**
  - **Tolerância a Partições (P)**
  - **Aceita Consistência Eventual (C)**

---

#### **Escolha do Banco de Dados**

- **Banco de Escrita:**
  - Geralmente relacional.
  - Prioriza integridade transacional.
- **Banco de Leitura:**
  - Pode ser NoSQL.
  - Flexibilidade para diferentes projeções.
  - Otimizado para consultas específicas.

---

#### **Sincronização entre Escrita e Leitura**

##### **Sincronização Sincrônica:**

- **Como Funciona:** Atualiza o banco de leitura durante a transação de escrita.
- **Vantagens:**
  - Consistência imediata.
- **Desvantagens:**
  - Impacto no desempenho.
  - Maior acoplamento entre modelos.

##### **Sincronização Assíncrona:**

- **Como Funciona:**
  - **Eventos de Domínio:** Após uma operação de escrita, eventos são publicados.
  - **Processadores de Eventos:** Consumidores atualizam o banco de leitura.
- **Vantagens:**
  - Melhor desempenho.
  - Maior escalabilidade.
- **Desvantagens:**
  - Consistência eventual.
  - Complexidade adicional.

---

#### **Event Sourcing**

- **Definição:** Armazenamento do estado do sistema como uma sequência de eventos.
- **Benefícios:**
  - **Auditabilidade:** Histórico completo de mudanças.
  - **Flexibilidade:** Possibilidade de recriar estados passados.
- **Considerações:**
  - Aumenta a complexidade.
  - Requer gerenciamento eficiente de eventos e versões.

---

#### **Considerações Práticas**

- **Avaliação de Necessidade:**
  - **Complexidade do Domínio:** Justifica a separação?
  - **Escalabilidade Requerida:** Leitura e escrita têm demandas diferentes?
- **Benefícios vs. Custos:**
  - **Benefícios:**
    - Desempenho otimizado.
    - Escalabilidade.
    - Manutenção facilitada.
  - **Custos:**
    - Complexidade arquitetural.
    - Necessidade de sincronização.
    - Maior esforço de desenvolvimento.

---

#### **Conclusão**

A adoção do **CQRS** deve ser cuidadosamente considerada. Embora ofereça benefícios significativos em termos de desempenho e escalabilidade, também introduz complexidade adicional. É especialmente útil em sistemas:

- Com alta carga de leitura e escrita.
- Que exigem escalabilidade independente.
- Onde a lógica de negócio é complexa e beneficia da separação clara entre comandos e consultas.

Para sistemas menores ou menos complexos, uma arquitetura tradicional pode ser mais apropriada. A chave é equilibrar os benefícios potenciais com os custos e desafios de implementação.
