---
attachments: [Clipboard_2024-09-12-07-41-18.png, Clipboard_2024-09-12-08-10-13.png, Clipboard_2024-09-12-08-17-47.png, Clipboard_2024-09-12-08-29-43.png, Clipboard_2024-09-12-09-11-11.png, Clipboard_2024-09-12-09-12-37.png, Clipboard_2024-09-12-09-14-15.png, Clipboard_2024-09-12-09-17-40.png, Clipboard_2024-09-12-09-20-07.png, Clipboard_2024-09-12-09-22-15.png, Clipboard_2024-09-12-09-25-00.png]
title: Aula 4 - Domain-Driven Design (DDD)
created: '2024-09-11T18:33:49.273Z'
modified: '2024-09-12T14:45:05.363Z'
---

### Aula 4 - Domain-Driven Design (DDD)

#### DTO (Data Transfer Object)

**O que é DTO?**  
O **DTO** é um objeto usado para transportar dados entre diferentes camadas da aplicação. Originalmente, foi criado para interagir com interfaces remotas, reduzindo a quantidade de chamadas à rede. No passado, eram necessárias várias chamadas a diferentes métodos, o que resultava em um uso excessivo da rede.

![](@attachment/Clipboard_2024-09-12-07-41-18.png)

**Problema em utilizar entidades para entrada e saída da aplicação:**
- Gera acoplamento elevado: qualquer mudança na entidade pode causar impacto em outras partes do sistema.
- As entidades têm responsabilidades diferentes: são responsáveis por implementar regras de negócio, não por transportar dados.

**Quem deve criar o DTO?**  
O DTO pode ser criado diretamente na camada de aplicação ou por um **Assembler**, que movimenta dados entre um objeto de domínio e um DTO. Essa conversão também pode ser feita manualmente, dependendo da necessidade.

---

### Domain-Driven Design (DDD)

Desenvolvemos software para resolver problemas reais no mundo. Exemplos de problemas que o DDD visa modelar:
- Compra de produtos
- Cálculo de impostos
- Agendamento de exames
- Matrícula de alunos

#### O que é domínio?
O **domínio** é o problema que uma organização precisa resolver para criar um software que realmente atenda às necessidades de seus clientes.

#### Quem nos ajuda a entender o problema?
![](@attachment/Clipboard_2024-09-12-08-10-13.png)

Uma das habilidades mais importantes de um desenvolvedor é saber fazer perguntas.  
![](@attachment/Clipboard_2024-09-12-08-17-47.png)

#### Linguagem Ubíqua
A **linguagem ubíqua** é o vocabulário comum entre especialistas no domínio e a equipe de desenvolvimento, dentro de um determinado contexto delimitado, onde o domínio se aplica.

**Exemplo:**  
Em uma editora de livros, a linguagem pode incluir termos como:
- Assinatura de contrato com autores.
- Tradução de livros para outros idiomas.
- Produção de edições impressas.
- Comercialização do livro online.
- Pagamento de direitos autorais.

---

### Subdomínios

Cada empresa atua em diferentes domínios de negócio. Alguns exemplos:

- **SAP:** Gestão financeira, produção, RH, etc.
- **HubSpot:** Prospecção e conversão de leads.
- **Salesforce:** Gestão de relacionamento com clientes.
- **Vimeo:** Streaming de vídeo.

**Subdomínios em um sistema de vendas online:**
![](@attachment/Clipboard_2024-09-12-08-29-43.png)

**Tipos de subdomínios:**
- **Core (ou Basic):** É o mais importante e traz o maior valor para o negócio. Recebe os maiores esforços.
- **Support (ou Auxiliary):** Complementa o core domain e é essencial para o sucesso do negócio.
- **Generic:** Subdomínios que podem ser delegados a outras empresas ou comprados como produtos de mercado.

Se não diferenciarmos corretamente os subdomínios, corremos o risco de criar uma **big ball of mud** — um sistema sem organização, com acoplamento excessivo entre componentes.

---

### Clean Architecture e Domain-Driven Design

Um **bounded context** é o limite onde o problema é resolvido e o modelo de domínio é implementado. É essencial entender a modelagem estratégica e a importância de um **context map**, que detalha as interfaces de integração entre diferentes contextos delimitados.

![](@attachment/Clipboard_2024-09-12-09-11-11.png)

**Exemplo de relações entre contextos:**
- **Upstream e Downstream:** Parceria entre contextos, ajustando as interfaces de acordo com as necessidades do negócio (ex.: integração com ERP).  
![](@attachment/Clipboard_2024-09-12-09-14-15.png)
- **Conformista:** Adequação a uma interface externa, como um gateway de pagamento.  
![](@attachment/Clipboard_2024-09-12-09-17-40.png)

Essas relações geralmente exigem tradução do domínio, o que pode ser feito por adaptadores que facilitam a integração com diferentes fornecedores e sistemas.

#### Decisões independentes e sem integração

Nem todos os bounded contexts precisam ser desenvolvidos da mesma forma. A modelagem orientada ao domínio é ótima para regras de negócio complexas, mas pode ser desnecessária em situações mais simples.  
![](@attachment/Clipboard_2024-09-12-09-25-00.png)

---

### Componentes do Domain-Driven Design (DDD)

#### 1. **Entities (Entidades)**

As **entities** modelam regras de negócio no domínio e possuem identidade única. Elas sofrem mutações ao longo do tempo e são responsáveis por garantir a consistência do sistema.

**Características principais:**
- **Identidade única:** A identidade pode ser gerada manualmente, pela aplicação, pelo banco de dados, ou por outro bounded context.
- **Estado:** A entidade tem estado, ou seja, seus atributos podem ser modificados ao longo do tempo.
- **Regras de negócio:** As entidades carregam as regras de negócio que garantem a consistência do domínio.

**Exemplo:**  
Um `Pedido` em um sistema de vendas, que contém itens, quantidade, valor total, etc. Suas alterações são feitas diretamente na entidade `Pedido`, garantindo que as regras de negócio sejam respeitadas.

---

#### 2. **Value Objects (Objetos de Valor)**

**Value objects** são imutáveis e definidos pelos seus valores, não tendo identidade própria. Eles descrevem ou quantificam entidades.

**Características principais:**
- **Imutabilidade:** Um value object é substituído por outro em vez de ser modificado.
- **Sem identidade:** São identificados pelo valor, não por uma identidade única.

**Exemplo:**  
`Endereço` em um sistema de vendas, onde qualquer mudança gera a substituição completa do objeto.

---

#### 3. **Domain Services (Serviços de Domínio)**

Os **domain services** são responsáveis por operações de negócio que não pertencem a uma entidade ou value object. Eles não mantêm estado próprio e são usados para processar múltiplas entidades ou aplicar regras de negócio complexas.

**Exemplo:**  
O serviço `CalcularFrete` não pertence a uma entidade específica, mas é responsável por calcular o valor do frete baseado em múltiplos fatores, como peso e distância.

---

#### 4. **Aggregates (Agregados)**

Um **aggregate** é um conjunto de entidades e value objects que formam uma unidade de consistência e transação. A entidade raiz (aggregate root) é o ponto de entrada para todas as operações sobre o aggregate.

**Características principais:**
- **Aggregate root (raiz):** Entidade principal pela qual as operações no aggregate são realizadas.
- **Consistência:** Assegura a consistência dentro do limite transacional.

**Exemplo:**  
O `Pedido` é a raiz do aggregate, contendo `Itens do Pedido` como parte dele. Todas as alterações no `Pedido` passam pela entidade raiz.

---

#### 5. **Domain Events (Eventos de Domínio)**

**Domain events** capturam fatos relevantes no domínio e são usados para comunicar mudanças importantes dentro do sistema.

**Exemplo:**  
O evento `PedidoFinalizado` é disparado quando um pedido é finalizado, notificando outras partes do sistema, como envio de e-mail ou atualização de estoque.

---

#### 6. **Application Services (Serviços de Aplicação)**

Os **application services** orquestram as operações do modelo de domínio, coordenando interações entre aggregates, domain services e infraestrutura. Não devem conter regras de negócio.

**Exemplo:**  
Um serviço de aplicação que gerencia o processo de `FinalizarPedido`, chamando o aggregate `Pedido` e orquestrando a lógica necessária.

---

#### 7. **Infrastructure Services (Serviços de Infraestrutura)**

Os **infrastructure services** interagem com recursos externos, como persistência, envio de e-mails e comunicação com APIs.

**Exemplo:**  
Um serviço que envia um e-mail de confirmação de pedido ao cliente.

---

#### 8. **Repositories (Repositórios)**

Os **repositories** são responsáveis pela persistência dos aggregates, desacoplando o domínio dos detalhes de infraestrutura, como bancos de dados.

**Exemplo:**  
O `PedidoRepository` gerencia a persistência dos pedidos, escondendo os detalhes de como eles são armazenados.

---

#### 9. **Modules (Módulos)**

Os **modules** organizam fisicamente o código em torno de bounded contexts e agrupam objetos de domínio relacionados. Eles ajudam a manter o código coeso e organizado, especialmente em projetos grandes.

**Exemplo:**  
O módulo `Pedidos` agrupa todas as entidades, serviços e repositórios relacionados ao processamento de pedidos.

---

### Conclusão

O **Domain-Driven Design (DDD)** fornece uma estrutura sólida para modelar regras de negócio complexas, separando preocupações e promovendo um código mais limpo e organizado. Com componentes como **entities**, **value objects**, **domain services**, **aggregates**, e **repositories**, o DDD ajuda a garantir que o software seja alinhado com as necessidades reais do negócio, proporcionando flexibilidade e escalabilidade ao sistema.
