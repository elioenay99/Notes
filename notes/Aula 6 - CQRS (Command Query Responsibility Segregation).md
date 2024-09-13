---
title: Aula 6 - CQRS (Command Query Responsibility Segregation)
created: '2024-09-13T15:27:58.973Z'
modified: '2024-09-13T20:52:30.465Z'
---

### Aula 6 - CQRS (Command Query Responsibility Segregation)

---

#### **Introdução**

**CQRS (Command Query Responsibility Segregation)** é um padrão arquitetural que separa as operações de leitura e escrita de um sistema em modelos distintos, permitindo que cada um seja otimizado e escalado de forma independente. Esse conceito evoluiu a partir do princípio de **CQS (Command Query Separation)**, proposto por **Bertrand Meyer**, que estabelece:

> **"Cada método em um programa deve ser ou um comando que realiza uma ação ou uma consulta que retorna dados ao chamador, mas não ambos."**

Enquanto o CQS atua no nível de métodos individuais, o **CQRS** aplica esse princípio em toda a arquitetura da aplicação, promovendo uma separação clara entre comandos (operações que alteram o estado do sistema) e consultas (operações que retornam dados sem modificar o estado).

---

#### **Princípio CQS e sua Relação com CQRS**

O **princípio CQS** incentiva a criação de métodos que sejam ou comandos ou consultas, evitando que um único método faça ambos. Isso aumenta a previsibilidade do código e reduz efeitos colaterais indesejados.

**Martin Fowler** complementa:

> **"Prefiro referir-me a eles como 'modificadores' em vez de 'comandos', para evitar confusão com outros usos do termo."**

O **CQRS** expande esse conceito para o nível arquitetural, separando não apenas métodos, mas também modelos de dados e serviços responsáveis por comandos e consultas.

---

#### **Por que Utilizar CQRS?**

A aplicação do CQRS oferece vários benefícios:

- **Desempenho Otimizado:** Permite otimizar as operações de leitura e escrita separadamente, melhorando a eficiência.
- **Escalabilidade Independente:** As camadas de leitura e escrita podem ser escaladas de acordo com suas necessidades específicas.
- **Manutenibilidade Aprimorada:** Facilita a compreensão e manutenção do código ao separar responsabilidades.
- **Flexibilidade na Modelagem de Dados:** Possibilita usar modelos de dados diferentes para leitura e escrita, adequando-se às necessidades de cada operação.

---

#### **Arquitetura CQRS: Separação de Comandos e Consultas**

##### **Modelo de Escrita (Comandos)**

- **Responsabilidade:** Gerenciar operações que alteram o estado do sistema.
- **Características:**
  - Contém a lógica de negócios e regras de validação.
  - Utiliza modelos de domínio ricos (objetos de domínio) para garantir a integridade dos dados.
  - Pode envolver transações complexas e integridade referencial.

##### **Modelo de Leitura (Consultas)**

- **Responsabilidade:** Fornecer dados para exibição ou processamento, sem alterar o estado do sistema.
- **Características:**
  - Utiliza modelos de dados otimizados para consultas, frequentemente desnormalizados.
  - Focado em desempenho e simplicidade.
  - Não contém lógica de negócios complexa.

---

#### **Implementação de CQRS**

##### **Separação dos Modelos de Dados**

- **Banco de Dados de Escrita:**
  - Normalizado para manter a integridade dos dados.
  - Segue práticas tradicionais de modelagem relacional.
- **Banco de Dados de Leitura:**
  - Desnormalizado para melhorar a performance de consultas.
  - Pode utilizar tecnologias diferentes, como bancos NoSQL, caches ou mecanismos de busca.

##### **Fluxo de Comandos**

1. **Recebimento do Comando:**
   - O usuário ou sistema envia um comando que representa uma intenção de mudança.
2. **Processamento no Domínio:**
   - O comando é validado e processado pelos objetos de domínio, aplicando regras de negócios.
3. **Persistência:**
   - As mudanças são salvas no banco de dados de escrita.
4. **Emissão de Eventos (Opcional):**
   - Eventos de domínio podem ser publicados para notificar outras partes do sistema.

##### **Fluxo de Consultas**

1. **Recebimento da Consulta:**
   - O usuário ou sistema solicita dados específicos.
2. **Acesso ao Modelo de Leitura:**
   - A consulta é realizada diretamente no banco de dados de leitura.
3. **Retorno dos Dados:**
   - Os dados são retornados ao chamador, geralmente na forma de DTOs (Data Transfer Objects).

---

#### **Sincronização entre os Modelos de Escrita e Leitura**

A sincronização entre os modelos de escrita e leitura é crucial para garantir que os dados apresentados ao usuário estejam atualizados.

##### **Sincronização Sincrônica**

- **Como Funciona:**
  - Durante a operação de escrita, o sistema atualiza simultaneamente o modelo de leitura.
- **Vantagens:**
  - Consistência imediata entre os modelos.
- **Desvantagens:**
  - Pode afetar o desempenho das operações de escrita.
  - Aumenta o acoplamento entre as camadas.

##### **Sincronização Assíncrona**

- **Como Funciona:**
  - Após a escrita, eventos são publicados em um barramento ou fila.
  - Processos assíncronos consomem esses eventos e atualizam o modelo de leitura.
- **Vantagens:**
  - Melhor desempenho nas operações de escrita.
  - Maior escalabilidade e desacoplamento.
- **Desvantagens:**
  - Introduz **consistência eventual**, onde o modelo de leitura pode estar desatualizado por um curto período.
  - Requer mecanismos adicionais para gerenciamento de eventos e resolução de conflitos.

---

#### **Consistência Eventual e o Teorema CAP**

O uso de sincronização assíncrona leva à **consistência eventual**, onde os dados no modelo de leitura eventualmente refletem as mudanças feitas no modelo de escrita.

##### **Teorema CAP**

O teorema CAP afirma que, em um sistema distribuído, é impossível garantir simultaneamente:

1. **Consistência (Consistency):** Todos os nós veem os mesmos dados ao mesmo tempo.
2. **Disponibilidade (Availability):** O sistema continua operacional mesmo em caso de falhas.
3. **Tolerância a Partições (Partition Tolerance):** O sistema continua funcionando mesmo com perda de comunicação entre os nós.

**CQRS**, especialmente quando combinado com sincronização assíncrona, geralmente escolhe:

- **Disponibilidade** e **Tolerância a Partições**, aceitando **consistência eventual**.

---

#### **Event Sourcing (Fonte de Eventos)**

**Event Sourcing** é um padrão que pode ser utilizado junto com CQRS, onde o estado do sistema é determinado por uma sequência de eventos.

##### **Como Funciona:**

- Em vez de armazenar o estado atual dos dados, o sistema armazena uma lista de eventos que representam mudanças de estado.
- O estado atual pode ser reconstruído ao reproduzir todos os eventos na ordem em que ocorreram.

##### **Vantagens:**

- **Auditabilidade Completa:** Histórico detalhado de todas as mudanças.
- **Flexibilidade:** Possibilidade de recriar estados passados ou projetar novos modelos de leitura.

##### **Desafios:**

- **Complexidade Adicional:** Requer gerenciamento cuidadoso dos eventos.
- **Evolução do Modelo:** Mudanças na estrutura dos eventos precisam ser gerenciadas (versionamento).

---

#### **Normalização vs. Desnormalização**

##### **Normalização (Modelo de Escrita):**

- Evita redundância de dados.
- Garante integridade referencial.
- Pode resultar em operações de leitura menos eficientes devido a junções complexas.

##### **Desnormalização (Modelo de Leitura):**

- Duplica dados para otimizar consultas.
- Melhora o desempenho de leitura.
- Pode introduzir inconsistências se a sincronização não for gerenciada corretamente.

---

#### **Escolha de Tecnologias**

##### **Banco de Dados de Escrita:**

- Geralmente utiliza bancos de dados relacionais.
- Foca em transações e integridade dos dados.

##### **Banco de Dados de Leitura:**

- Pode utilizar bancos NoSQL, caches distribuídos ou mecanismos de busca.
- Escolhido com base nas necessidades de consulta e desempenho.

---

#### **Considerações Práticas**

##### **Benefícios:**

- **Desempenho Aprimorado:** Modelos de leitura otimizados aceleram as consultas.
- **Escalabilidade:** Leitura e escrita podem ser escaladas de forma independente.
- **Manutenção Facilitada:** Separação de responsabilidades simplifica o desenvolvimento e a manutenção.

##### **Desafios:**

- **Complexidade Arquitetural:** A implementação de CQRS é mais complexa do que arquiteturas tradicionais.
- **Consistência Eventual:** Necessidade de lidar com possíveis desatualizações temporárias nos dados de leitura.
- **Sincronização de Dados:** Requer mecanismos adicionais para manter os modelos de leitura atualizados.

---

#### **Quando Utilizar CQRS**

**CQRS** é especialmente útil em cenários onde:

- **Alto Volume de Leitura e Escrita:** Sistemas com demandas intensas e diferenciadas.
- **Necessidade de Escalabilidade:** Quando se espera um crescimento significativo no uso do sistema.
- **Domínio Complexo:** Sistemas com lógica de negócios complexa que se beneficiam da separação.
- **Requisitos de Performance Específicos:** Necessidade de otimizar operações de leitura ou escrita.

**Não é recomendado** para sistemas simples ou com recursos limitados, onde a complexidade adicional não justifica os benefícios.

---

#### **Exemplo Prático**

Imagine um sistema de e-commerce:

- **Operações de Escrita:**
  - Criação de pedidos.
  - Atualização de estoque.
  - Processamento de pagamentos.
- **Operações de Leitura:**
  - Consulta de produtos.
  - Visualização de carrinho de compras.
  - Histórico de pedidos.

**Implementação com CQRS:**

- **Modelo de Escrita:**
  - Utiliza objetos de domínio ricos para garantir que todas as regras de negócios sejam aplicadas corretamente ao criar ou atualizar dados.
- **Modelo de Leitura:**
  - Armazena informações desnormalizadas sobre produtos, categorias e preços para consultas rápidas.
  - Pode utilizar um mecanismo de busca para facilitar filtragens e ordenações.

**Sincronização:**

- **Eventos de Domínio:**
  - Quando um novo produto é adicionado, um evento é publicado.
- **Atualização do Modelo de Leitura:**
  - Processos assíncronos consomem o evento e atualizam o banco de leitura.

---

#### **Conclusão**

O **CQRS** oferece uma abordagem poderosa para lidar com desafios de desempenho e escalabilidade em sistemas complexos. Ao separar claramente as operações de leitura e escrita, é possível otimizar cada parte do sistema de acordo com suas necessidades específicas.

**Antes de adotar o CQRS**, é importante considerar:

- **Complexidade do Sistema:** Se o sistema é suficientemente complexo para justificar a implementação.
- **Recursos Disponíveis:** Equipe capacitada e tempo para lidar com a complexidade adicional.
- **Requisitos de Negócio:** Se os benefícios em desempenho e escalabilidade são críticos para o sucesso do projeto.

---

#### **Referências Adicionais**

- **Artigos e Blogs:**
  - *"CQRS Documents"*, por **Greg Young**.
  - *"CQRS"*, por **Martin Fowler**.
- **Livros:**
  - *"Domain-Driven Design: Tackling Complexity in the Heart of Software"*, por **Eric Evans**.
  - *"Implementing Domain-Driven Design"*, por **Vaughn Vernon**.

---


**Nota Final:**

A decisão de utilizar **CQRS** deve ser baseada em uma análise cuidadosa dos benefícios e trade-offs. Embora possa oferecer melhorias significativas em certos cenários, a complexidade adicional requer uma equipe experiente e um entendimento profundo dos padrões envolvidos. Com planejamento e execução adequados, o CQRS pode ser uma ferramenta valiosa para construir sistemas robustos e escaláveis.

---
