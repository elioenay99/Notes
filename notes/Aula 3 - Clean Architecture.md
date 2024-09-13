---
title: Aula 3 - Clean Architecture
created: '2024-09-11T12:51:19.626Z'
modified: '2024-09-13T20:56:28.615Z'
---

### Aula 3 - Clean Architecture

---

#### **Introdução à Arquitetura de Software**

A **arquitetura de software** é um aspecto crítico no desenvolvimento de sistemas complexos. Ela define a estrutura organizacional do sistema, facilitando a comunicação entre as partes interessadas e orientando decisões técnicas ao longo do ciclo de vida do software.

**Definições Importantes:**

- **Robert Martin:** *"O objetivo da arquitetura de software é minimizar a quantidade de recursos humanos necessários para construir e manter um determinado sistema."*
- **Martin Fowler:** *"Arquitetura de software são decisões que são ao mesmo tempo importantes e difíceis de mudar."*
- **Rational Unified Process:** *"Uma arquitetura é o conjunto de decisões significativas sobre a organização de um sistema de software, a seleção dos elementos estruturais e suas interfaces, juntamente com seu comportamento conforme especificado nas colaborações entre esses elementos."*
- **Padrão ANSI/IEEE 1471-2000:** *"Arquitetura é definida pela prática recomendada como a organização fundamental de um sistema, incorporada em seus componentes, suas relações entre si e com o ambiente, e os princípios que regem seu design e evolução."*

**Palavras-chave recorrentes:** Organização, estrutura, design, relacionamento e comportamento.

---

#### **Considerações na Definição de uma Arquitetura**

Ao projetar a arquitetura de um sistema, é crucial considerar diversos fatores que influenciam diretamente as decisões arquiteturais:

1. **Escopo do Produto:**
   - Compreender os requisitos funcionais e não funcionais.
   - Identificar as funcionalidades essenciais e as expectativas dos stakeholders.

2. **Volume de Requisições:**
   - Prever a carga esperada no sistema.
   - Planejar para escalabilidade horizontal ou vertical, se necessário.

3. **Tipo de Dispositivo:**
   - Determinar se o sistema será executado em desktops, dispositivos móveis, ou IoT.
   - Considerar restrições de hardware e requisitos de plataforma.

4. **Tamanho e Perfil da Equipe:**
   - Ajustar a complexidade da arquitetura ao nível de experiência da equipe.
   - Facilitar a colaboração e divisão de tarefas.

5. **Prazo de Entrega:**
   - Balancear entre soluções rápidas e a necessidade de uma arquitetura robusta.
   - Planejar entregas incrementais.

6. **Orçamento:**
   - Considerar custos de licenciamento de ferramentas e tecnologias.
   - Avaliar o custo-benefício de soluções open-source versus proprietárias.

**Tipos de Arquitetura Comuns:**

- **Monolítica:** Sistema único onde todas as funcionalidades estão integradas.
- **N Camadas (Multicamadas):** Separação lógica em camadas como apresentação, negócio e dados.
- **Cliente-Servidor:** Divisão entre clientes que solicitam serviços e servidores que os fornecem.
- **Distribuída:** Componentes localizados em diferentes máquinas conectadas em rede.
- **Orientada a Serviços (SOA):** Serviços independentes que se comunicam através de protocolos bem definidos.
- **Microservices:** Evolução do SOA com serviços menores e mais focados.
- **Event-Driven:** Baseada em eventos que desencadeiam ações no sistema.
- **Domain-Driven Design (DDD):** Foco no domínio de negócio e na colaboração com especialistas.

**Nota:** **Não existe uma arquitetura única que seja adequada para todos os projetos.** A escolha deve ser baseada no contexto e nos requisitos específicos do sistema.

---

### **Clean Architecture**

A **Clean Architecture** é um modelo arquitetural proposto por **Robert C. Martin** (também conhecido como Uncle Bob) em 2012. Seu principal objetivo é separar os elementos do design de software em níveis que isolem as regras de negócio (domínio) dos detalhes de implementação, como bancos de dados, interfaces de usuário, frameworks ou qualquer tecnologia específica.

**Princípios Fundamentais:**

- **Independência de Frameworks:** A lógica de negócio não deve depender de frameworks ou bibliotecas externos.
- **Testabilidade:** O sistema deve ser testável de forma isolada das interfaces de usuário, banco de dados ou outros componentes externos.
- **Independência de Interface de Usuário:** Mudanças na UI não devem afetar o núcleo do sistema.
- **Independência de Banco de Dados:** A lógica de negócio não deve ser afetada por alterações no banco de dados.
- **Independência de Agentes Externos:** O sistema deve ser flexível para interagir com sistemas externos sem alterar o núcleo.

---

#### **Componentes e Camadas da Clean Architecture**

A Clean Architecture é frequentemente representada como uma série de círculos concêntricos, onde cada círculo ou camada tem responsabilidades distintas e regras de dependência claras.

![Clean Architecture Diagram](https://miro.medium.com/max/1400/1*ZNIQe-rZg1czIP4nI95mTw.png)

**1. Entidades (Entities):**

- **Responsabilidade:**
  - Representam os objetos de negócio mais genéricos e de alto nível.
  - Contêm regras de negócio corporativas independentes de casos de uso específicos.
- **Características:**
  - Alta estabilidade e baixo nível de mudança.
  - Reutilizáveis em diferentes aplicações.

**2. Casos de Uso (Use Cases):**

- **Responsabilidade:**
  - Contêm regras de negócio específicas da aplicação.
  - Orquestram o fluxo de dados entre as entidades e coordenam as operações.
- **Características:**
  - Definem as interações entre o usuário e o sistema.
  - Não dependem de interfaces de usuário ou bancos de dados.

**3. Adaptadores de Interface (Interface Adapters):**

- **Responsabilidade:**
  - Convertem dados dos casos de uso para uma forma que possa ser apresentada (Views, APIs).
  - Adaptam entradas e saídas para o formato que o sistema interno espera.
- **Componentes:**
  - **Controllers:** Processam requisições e encaminham para os casos de uso.
  - **Presenters e ViewModels:** Preparam dados para exibição.
  - **Gateways:** Interfaces para sistemas externos ou bancos de dados.

**4. Frameworks e Drivers (Frameworks & Drivers):**

- **Responsabilidade:**
  - Contêm detalhes específicos de implementação, como frameworks web, bancos de dados, dispositivos, etc.
- **Características:**
  - Camada mais externa que pode ser facilmente substituída.
  - Implementa interfaces definidas nas camadas internas.

---

#### **Regra da Dependência (Dependency Rule)**

A regra fundamental na Clean Architecture é que **as dependências do código-fonte só podem apontar para dentro**, ou seja:

- Nenhum código interno pode conhecer algo sobre camadas mais externas.
- Nomes de classes, métodos ou variáveis das camadas externas não devem ser mencionados nas camadas internas.
- As camadas externas podem implementar interfaces ou abstrações definidas nas camadas internas.

---

#### **Fluxo de Controle e Dados**

1. **Entrada (Input):**

   - **Controller:** Recebe a entrada do usuário ou de outro sistema externo.
   - **Fluxo:** Controller → Use Case Interactor.

2. **Processamento:**

   - **Use Case Interactor:** Processa a lógica de negócio específica do caso de uso.
   - **Interage com Entidades:** Manipula entidades conforme necessário.

3. **Saída (Output):**

   - **Presenter:** Recebe dados do Use Case e prepara para a visualização.
   - **ViewModel:** Estrutura de dados pronta para ser consumida pela View.

4. **Interfaces Externas:**

   - **Gateways e Repositórios:** Acessam sistemas externos ou bancos de dados.
   - **Implementação:** Realizada na camada de Frameworks & Drivers.

---

#### **Comparação com Domain-Driven Design (DDD)**

**Semelhanças:**

- **Foco no Domínio:** Ambos priorizam as regras de negócio e o domínio sobre detalhes técnicos.
- **Isolamento do Domínio:** Buscam desacoplar a lógica de negócio das infraestruturas externas.

**Diferenças:**

- **DDD:**
  - Enfatiza a colaboração com especialistas do domínio.
  - Utiliza linguagens ubíquas e modelagem de domínio profundo.
  - Inclui padrões como **Entidades**, **Value Objects**, **Aggregates**, **Repositories**, **Services**, etc.

- **Clean Architecture:**
  - Fornece uma estrutura arquitetural clara com camadas e regras de dependência.
  - É mais prescritiva em termos de organização de código e fluxo de dependências.
  - Pode ser utilizada em conjunto com DDD, especialmente nas camadas internas.

**Integração de DDD na Clean Architecture:**

- **Entidades e Value Objects do DDD** podem ser colocados na camada de **Entities**.
- **Serviços de Domínio** se encaixam na camada de **Use Cases**.
- **Repositórios** são representados por **Gateways** ou **Interfaces de Acesso a Dados**.

---

#### **Implementação de Persistência e Acesso a Dados**

Na Clean Architecture, o acesso a dados é abstraído através de interfaces, permitindo que a camada de domínio permaneça independente de detalhes de infraestrutura.

**Padrões Utilizados:**

- **Repository Pattern:**
  - Abstrai a lógica de acesso a dados.
  - Provê uma coleção de entidades como se fossem objetos em memória.

- **Data Mapper:**
  - Mapeia objetos do domínio para representações de dados (e vice-versa).
  - Facilita a transformação entre modelos de domínio e modelos de dados.

- **DAO (Data Access Object):**
  - Fornece uma interface para operações CRUD em bancos de dados.
  - Separa a lógica de negócio da lógica de persistência.

**Implementação:**

- **Interfaces Definidas nas Camadas Internas:**
  - As interfaces de repositório ou gateways são definidas nas camadas de **Use Cases** ou **Entities**.
  - As implementações concretas são fornecidas na camada de **Frameworks & Drivers**.

---

#### **Detalhamento dos Componentes**

**1. Controller:**

- **Função:**
  - Receber e interpretar requisições.
  - Validar dados de entrada.
  - Invocar o caso de uso apropriado.

- **Boas Práticas:**
  - Manter lógica mínima.
  - Delegar processamento ao Use Case Interactor.

**2. Use Case Interactor:**

- **Função:**
  - Coordenar a execução das regras de negócio.
  - Invocar métodos nas entidades.
  - Gerenciar transações, se necessário.

- **Boas Práticas:**
  - Não incluir detalhes de infraestrutura.
  - Manter foco na lógica de aplicação.

**3. Entities (Entidades):**

- **Função:**
  - Representar conceitos do domínio com propriedades e comportamentos.
  - Encapsular regras de negócio genéricas.

- **Boas Práticas:**
  - Evitar dependências externas.
  - Manter integridade e consistência do domínio.

**4. Presenter e ViewModel:**

- **Função:**
  - Transformar dados do domínio em formatos adequados para a apresentação.
  - Isolar a lógica de apresentação das regras de negócio.

- **Boas Práticas:**
  - Evitar lógica de negócio.
  - Manter foco na preparação dos dados para a View.

**5. Data Access Interface e Implementação:**

- **Função:**
  - Definir contratos para operações de persistência.
  - Implementar acesso a dados utilizando tecnologias específicas (ORMs, SQL, NoSQL).

- **Boas Práticas:**
  - Manter implementações independentes das camadas internas.
  - Utilizar injeção de dependência para fornecer implementações concretas.

---

#### **Benefícios da Clean Architecture**

1. **Manutenibilidade:**

   - Código modular e organizado facilita alterações e adições.
   - Isolamento das regras de negócio simplifica a compreensão e evolução.

2. **Testabilidade:**

   - Facilidade para escrever testes unitários e de integração.
   - Possibilidade de mockar dependências externas.

3. **Flexibilidade e Escalabilidade:**

   - Troca de tecnologias ou frameworks sem impacto nas camadas internas.
   - Adaptação a novos requisitos de negócio ou técnicos.

4. **Reutilização:**

   - Componentes bem definidos podem ser reutilizados em outros projetos.
   - Entidades e casos de uso podem ser compartilhados entre diferentes interfaces (web, mobile, desktop).

---

#### **Desafios e Considerações Práticas**

- **Complexidade Inicial:**
  - Implementação da Clean Architecture pode ser complexa para projetos pequenos.
  - Requer investimento em aprendizado e adaptação da equipe.

- **Overengineering:**
  - Evitar adicionar camadas ou abstrações desnecessárias.
  - Adaptar a arquitetura à escala e necessidades do projeto.

- **Performance:**
  - Camadas adicionais podem introduzir overhead.
  - Otimizar apenas se necessário, mantendo a clareza do design.

- **Comunicação na Equipe:**
  - Garantir que todos compreendam os princípios e objetivos da arquitetura.
  - Manter documentação atualizada e promover boas práticas.

---

#### **Boas Práticas para Aplicar a Clean Architecture**

1. **Definir Interfaces Claras:**

   - As interfaces entre camadas devem ser bem definidas e estáveis.
   - Facilita a substituição de implementações e testes.

2. **Utilizar Inversão de Controle e Injeção de Dependência:**

   - As camadas internas definem contratos que as externas implementam.
   - A injeção de dependência permite fornecer implementações concretas em tempo de execução.

3. **Manter o Domínio Limpo:**

   - Evitar vazamento de detalhes técnicos nas entidades e casos de uso.
   - Focar nas regras de negócio e lógica essencial.

4. **Escrever Testes Automatizados:**

   - Cobrir as camadas de domínio com testes unitários.
   - Utilizar testes de integração para verificar a interação entre camadas.

5. **Documentar Decisões Arquiteturais:**

   - Registrar o raciocínio por trás de escolhas específicas.
   - Facilita a manutenção e onboarding de novos membros.

---

#### **Exemplo Prático: Fluxo de Processamento de um Pedido**

1. **Recebimento do Pedido:**

   - **Controller:** Recebe a requisição HTTP para criação de um pedido.
   - **Validação Inicial:** Verifica se os dados básicos estão presentes.

2. **Processamento do Caso de Uso:**

   - **Use Case Interactor:** Executa a lógica para processar o pedido.
     - Verifica disponibilidade de produtos.
     - Calcula valores (subtotal, descontos, impostos).
     - Cria instâncias das entidades necessárias.

3. **Persistência dos Dados:**

   - **Data Access Interface:** Use Case chama métodos para salvar o pedido.
   - **Implementação Concreta:** Repositório salva no banco de dados.

4. **Preparação da Resposta:**

   - **Presenter:** Transforma os dados do pedido em um ViewModel.
   - **ViewModel:** Contém informações formatadas para o cliente.

5. **Envio da Resposta:**

   - **Controller:** Envia a resposta HTTP ao cliente com os dados do ViewModel.

---

### **Conclusão**

A **Clean Architecture** oferece um conjunto de princípios e diretrizes para criar sistemas de software robustos, flexíveis e mantíveis. Ao separar claramente as responsabilidades e controlar as dependências entre as camadas, é possível construir sistemas que resistam ao tempo e às mudanças tecnológicas.

**Benefícios Resumidos:**

- **Facilidade de Manutenção:** Alterações em uma camada têm impacto mínimo em outras.
- **Adaptabilidade:** Troca de tecnologias ou frameworks sem reescrever a lógica de negócio.
- **Testes Eficazes:** Camadas internas podem ser testadas isoladamente.
- **Colaboração Aprimorada:** Estrutura clara facilita a comunicação entre membros da equipe.

**Próximos Passos para Aprofundamento:**

- **Ler Literatura Especializada:**
  - *"Clean Architecture: A Craftsman's Guide to Software Structure and Design"* — **Robert C. Martin**
  - *"Implementing Domain-Driven Design"* — **Vaughn Vernon**

---

### **Dicas Finais**

- **Adaptação é a Chave:** Não se prenda rigidamente a modelos; adapte a arquitetura às necessidades do seu projeto.
- **Comunicação Efetiva:** Mantenha a equipe alinhada sobre as decisões arquiteturais.
- **Refatoração Contínua:** Esteja disposto a melhorar o design à medida que o sistema evolui.
- **Simplicidade:** Evite complexidades desnecessárias; busque soluções simples e eficazes.

---

**Nota Final:** A compreensão e aplicação da Clean Architecture requer tempo e prática. Ao investir no estudo e implementação desses princípios, você estará construindo uma base sólida para desenvolver sistemas de alta qualidade que atendam às demandas atuais e futuras.
