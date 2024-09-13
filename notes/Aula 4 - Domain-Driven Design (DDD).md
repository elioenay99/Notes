---
attachments: [Clipboard_2024-09-12-07-41-18.png, Clipboard_2024-09-12-08-10-13.png, Clipboard_2024-09-12-08-17-47.png, Clipboard_2024-09-12-08-29-43.png, Clipboard_2024-09-12-09-11-11.png, Clipboard_2024-09-12-09-12-37.png, Clipboard_2024-09-12-09-14-15.png, Clipboard_2024-09-12-09-17-40.png, Clipboard_2024-09-12-09-20-07.png, Clipboard_2024-09-12-09-22-15.png, Clipboard_2024-09-12-09-25-00.png]
title: Aula 4 - Domain-Driven Design (DDD)
created: '2024-09-11T18:33:49.273Z'
modified: '2024-09-13T15:01:12.569Z'
---

### Aula 4 - Domain-Driven Design (DDD)

#### O que é um **DTO (Data Transfer Object)**?

O **DTO (Data Transfer Object)** é um padrão de design utilizado para **transportar dados** entre diferentes camadas de uma aplicação, como entre a camada de serviço e a camada de apresentação (ou entre a aplicação e uma interface externa, como uma API). O principal objetivo do DTO é **agrupar dados que serão transferidos**, evitando a exposição direta das entidades de domínio e **minimizando o acoplamento** entre as camadas.

Originalmente, o DTO surgiu para otimizar o tráfego de dados em sistemas distribuídos, especialmente em arquiteturas que envolviam chamadas remotas. Antes de sua utilização, múltiplas chamadas de rede eram feitas para acessar diferentes partes de dados, resultando em um uso excessivo de banda e aumentando a latência. O DTO permitiu agrupar essas informações e reduziu a quantidade de chamadas necessárias.

### Problemas ao utilizar entidades para entrada e saída de dados

Embora seja tentador usar as entidades do domínio diretamente para transportar dados entre camadas (especialmente em aplicações simples), essa prática gera uma série de problemas:

1. **Acoplamento elevado**: As entidades de domínio estão intimamente ligadas às regras de negócio e estrutura interna do sistema. Se elas forem expostas diretamente para outras camadas (ou fora da aplicação, como em APIs), qualquer mudança na entidade pode ter um impacto em toda a aplicação, aumentando o acoplamento e diminuindo a flexibilidade.

2. **Responsabilidades diferentes**: As **entidades de domínio** são responsáveis por implementar as regras de negócio, validações e comportamentos do sistema. Já o **DTO** tem como única responsabilidade **transportar dados**. Misturar essas responsabilidades pode levar a um código menos coeso e mais difícil de manter, além de violar o princípio de responsabilidade única (SRP).

3. **Segurança e privacidade**: As entidades de domínio podem conter informações sensíveis que não devem ser expostas ou compartilhadas com outras camadas ou sistemas externos. Ao usar um DTO, é possível controlar exatamente quais dados serão expostos e quais permanecerão encapsulados.

4. **Performance**: Expor entidades diretamente pode levar à transferência de dados desnecessários, que não são relevantes para a operação em questão, gerando overhead.

### Exemplo de uso de DTO

Imagine uma aplicação de e-commerce, onde temos uma entidade `Produto`. A entidade contém várias informações, como o preço de custo, fornecedores, histórico de vendas, etc. No entanto, para um cliente que está navegando no catálogo, apenas informações como nome, descrição e preço de venda são relevantes.

```java
class Produto {
    private Long id;
    private String nome;
    private String descricao;
    private double precoCusto;
    private double precoVenda;
    private Fornecedor fornecedor;
    // métodos de negócio e getters/setters
}
```

Se a entidade `Produto` for usada diretamente em uma API ou interface de usuário, todas as suas informações serão expostas, o que pode ser problemático. Para resolver isso, usamos um DTO que contém apenas os dados necessários para aquele contexto:

```java
class ProdutoDTO {
    private String nome;
    private String descricao;
    private double precoVenda;

    // getters/setters
}
```

Agora, a API ou a camada de apresentação só manipula os dados do DTO, enquanto a entidade `Produto` permanece encapsulada dentro da camada de domínio.

### Quem deve criar o DTO?

O DTO pode ser criado de diferentes maneiras, dependendo da arquitetura e das necessidades do projeto:

1. **Manual**: O DTO pode ser criado manualmente na camada de aplicação ou serviço. Nesse caso, os desenvolvedores são responsáveis por construir os objetos DTO a partir das entidades ou de outras fontes de dados. Embora simples, essa abordagem pode gerar muito código repetitivo, especialmente em projetos grandes.

2. **Automatizada com um Assembler**: Um **Assembler** é um padrão que facilita a conversão entre objetos de domínio e DTOs. Ele atua como um intermediário que **movimenta dados entre entidades e DTOs**, centralizando a lógica de conversão. Isso ajuda a manter o código mais organizado e desacoplado.

   Um Assembler típico pode ter a seguinte forma:

```java
class ProdutoAssembler {
    public static ProdutoDTO toDTO(Produto produto) {
        ProdutoDTO dto = new ProdutoDTO();
        dto.setNome(produto.getNome());
        dto.setDescricao(produto.getDescricao());
        dto.setPrecoVenda(produto.getPrecoVenda());
        return dto;
    }

    public static Produto toEntity(ProdutoDTO dto) {
        Produto produto = new Produto();
        produto.setNome(dto.getNome());
        produto.setDescricao(dto.getDescricao());
        produto.setPrecoVenda(dto.getPrecoVenda());
        return produto;
    }
}
```

Com um **Assembler**, a responsabilidade de converter entidades para DTOs (e vice-versa) é isolada em uma classe específica, facilitando a manutenção e o reaproveitamento de código.

3. **Bibliotecas automáticas**: Existem bibliotecas como **MapStruct** ou **ModelMapper**, que automatizam a conversão entre entidades e DTOs. Essas ferramentas podem ser configuradas para realizar mapeamentos automáticos, economizando tempo e reduzindo o código boilerplate.

### Conclusão

O **DTO (Data Transfer Object)** é uma abordagem fundamental para o design de sistemas que precisam transportar dados entre camadas ou através de interfaces externas, como APIs. Ele oferece as seguintes vantagens:

- Reduz o **acoplamento** entre camadas.
- Mantém as **entidades de domínio** focadas em suas responsabilidades de negócio.
- Melhora a **segurança e privacidade** dos dados.
- Facilita a **testabilidade** e **evolução** do sistema.

Em sistemas modernos, o uso de DTOs é uma prática comum e recomendada para garantir que as diferentes partes de uma aplicação estejam bem desacopladas, tornando o código mais flexível e fácil de manter.

---

### Domain-Driven Design (DDD)

No contexto do Domain-Driven Design (DDD), o domínio é o coração do software, pois representa o problema real que a organização ou os usuários enfrentam. Quando falamos de "domínio", estamos nos referindo ao conjunto de regras de negócio, processos e necessidades específicas que o software precisa solucionar.

Por exemplo, ao desenvolver um sistema de compra de produtos, você precisa entender como os clientes fazem pedidos, quais são os requisitos de estoque, as regras de pagamento, e como os produtos são entregues. O mesmo vale para cálculo de impostos, onde você deve modelar as alíquotas, regimes tributários e leis fiscais. Cada cenário envolve um conjunto único de regras e desafios que constituem o domínio desse problema.

![](@attachment/Clipboard_2024-09-12-08-10-13.png)

Para entender o problema que você está resolvendo, é essencial fazer as perguntas certas. E quem nos ajuda nesse processo é o Especialista no Domínio. Esse especialista é a pessoa que possui conhecimento profundo sobre o problema real, seja um gerente de negócios, cliente ou qualquer pessoa que entenda as minúcias do domínio que você está modelando. Eles te ajudam a enxergar as regras e exceções que o sistema precisa lidar.

A Habilidade de Fazer Perguntas
Fazer perguntas é uma das habilidades mais importantes para um desenvolvedor. Perguntas bem formuladas te permitem explorar e descobrir o verdadeiro escopo do domínio. Você vai além de uma visão superficial do problema e mergulha em como as coisas realmente funcionam. Perguntas como:

Quais são os processos críticos que o sistema precisa suportar?
Existem exceções às regras gerais?
Como os usuários interagem com o sistema atualmente?
Essas perguntas ajudam a construir um modelo que reflete fielmente o problema real e que, ao ser traduzido em código, trará valor ao cliente.

Essa troca de informações entre o desenvolvedor e o especialista no domínio é fundamental no DDD, pois leva a uma melhor modelagem do domínio e, consequentemente, a um software mais alinhado com as necessidades reais dos usuários.



#### Linguagem Ubíqua

![](@attachment/Clipboard_2024-09-12-08-17-47.png)

A **Linguagem Ubíqua** é um dos pilares centrais do **Domain-Driven Design (DDD)**, e sua função é assegurar que tanto os **especialistas no domínio** quanto a **equipe de desenvolvimento** falem a mesma língua. Isso significa que todos os envolvidos no projeto devem usar os mesmos termos e definições ao discutir e implementar o domínio, eliminando ambiguidades e reduzindo o risco de mal-entendidos.

No exemplo da **editora de livros**, a linguagem ubíqua seria formada por termos específicos do negócio, como:

- **Assinatura de contrato com autores**: o processo formal em que a editora e o autor entram em acordo sobre as condições de publicação do livro.
- **Tradução de livros para outros idiomas**: a tarefa de converter o conteúdo original para uma nova língua, respeitando nuances culturais e de contexto.
- **Produção de edições impressas**: o processo de transformar o manuscrito em um livro físico, desde a diagramação até a impressão.
- **Comercialização do livro online**: a venda do livro em plataformas digitais, o que inclui a gestão de preços, estoque e canais de distribuição.
- **Pagamento de direitos autorais**: a remuneração devida ao autor com base nas vendas do livro, em conformidade com o contrato assinado.

### Benefícios da Linguagem Ubíqua
1. **Comunicação Clara**: Todos os envolvidos no projeto, sejam desenvolvedores ou especialistas de negócios, podem discutir o sistema sem a necessidade de traduzir conceitos ou adaptar vocabulário.
2. **Redução de Ambiguidade**: A linguagem comum garante que os termos têm o mesmo significado para todos, evitando mal-entendidos que possam causar erros no desenvolvimento.
3. **Reflexo no Código**: O vocabulário do domínio deve ser refletido no código, garantindo que o software seja mais fácil de entender e mantenha a coerência com a realidade do negócio. Por exemplo, em vez de usar nomes genéricos como `executeProcess`, podemos ter métodos e classes como `comercializarLivro` ou `realizarPagamentoDireitosAutorais`.

### Um Exemplo Prático de Linguagem Ubíqua no Código

```java
public class ContratoAutor {
    private Autor autor;
    private Livro livro;
    private LocalDate dataAssinatura;
    private BigDecimal valorDireitosAutorais;

    public void assinarContrato(Autor autor, Livro livro) {
        // implementação
    }

    public void calcularDireitosAutorais(Venda venda) {
        // implementação
    }
}
```

Aqui, os termos usados no código (`ContratoAutor`, `assinarContrato`, `calcularDireitosAutorais`) refletem diretamente a linguagem usada pela editora no dia a dia, facilitando a comunicação entre a equipe de desenvolvimento e os especialistas no domínio.

Ao utilizar a **linguagem ubíqua**, criamos um ciclo contínuo de entendimento e alinhamento entre o software e o problema real que ele pretende resolver.

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

As **entities** representam **objetos com identidade única** dentro do domínio e sofrem mutações ao longo do tempo. Elas são fundamentais no DDD, pois carregam as **regras de negócio** e garantem que a **consistência** do sistema seja mantida, mesmo que seu estado se altere.

**Características principais:**
- **Identidade única:** A identidade de uma entidade a distingue de todas as outras, mesmo que tenham os mesmos atributos. Essa identidade pode ser gerada de várias maneiras, como pela aplicação, banco de dados ou outros contextos.
- **Estado mutável:** Entidades têm um estado que muda ao longo do tempo à medida que as regras de negócio são aplicadas.
- **Regras de negócio:** As entidades são responsáveis por garantir que as regras de negócio do domínio sejam respeitadas e mantidas.

**Exemplo:**
- Um `Pedido` em um sistema de vendas é uma entidade, pois tem uma identidade única (como um número de pedido) e pode mudar ao longo do tempo (adicionando ou removendo itens, alterando o valor total, etc.).

---

#### 2. **Value Objects (Objetos de Valor)**

Os **Value Objects** são caracterizados por **não terem identidade própria** e serem **imutáveis**. Eles são definidos por seus **atributos**, ou seja, dois value objects são iguais se seus valores forem iguais. Como resultado, eles podem ser substituídos completamente quando algo muda.

**Características principais:**
- **Imutabilidade:** Um value object não muda. Se houver uma alteração, ele é substituído por outro value object.
- **Sem identidade:** Value objects são definidos pelos seus valores, e não possuem uma identidade persistente.
- **Descrevem entidades:** Eles complementam as entidades ao fornecer características ou medições.

**Exemplo:**
- Um `Endereço` é um value object em um sistema de vendas. Ele pode ser substituído integralmente (por exemplo, ao mudar de residência), mas não precisa ter uma identidade única.

---

#### 3. **Domain Services (Serviços de Domínio)**

Os **domain services** são usados para **operações de negócio** que não se encaixam diretamente em uma entidade ou value object. Eles representam **lógica de negócio** que não pertence a nenhum objeto em particular, mas que precisa ser aplicada em várias entidades ou objetos de valor.

**Características principais:**
- **Sem estado:** Serviços de domínio não armazenam estado próprio. Eles aplicam lógica de negócio e retornam resultados.
- **Operações complexas:** Serviços são usados para processos de negócios que envolvem várias entidades ou que não podem ser representados dentro de uma única entidade ou value object.

**Exemplo:**
- O serviço `CalcularFrete` em um sistema de vendas é responsável por determinar o custo do frete com base em critérios como peso do pedido, distância e local de entrega. Esse serviço não pertence a uma entidade específica, mas sua lógica é fundamental para o domínio.

---

#### 4. **Aggregates (Agregados)**

Um **aggregate** é um **conjunto de entidades e value objects** que são tratados como uma **unidade única de consistência**. Dentro de um aggregate, uma **entidade raiz (aggregate root)** serve como ponto de entrada para todas as operações que afetam o conjunto. Isso garante que as alterações no aggregate sejam feitas de maneira controlada, preservando a **consistência transacional**.

**Características principais:**
- **Aggregate root (raiz do agregado):** Uma entidade principal que gerencia e coordena as outras entidades e value objects dentro do agregado.
- **Consistência:** Assegura que todas as mudanças dentro do aggregate sejam consistentes. Qualquer modificação em suas partes deve passar pela entidade raiz.
- **Unidade de transação:** O aggregate define o limite para transações. Todas as mudanças no agregado ocorrem como parte de uma única transação.

**Exemplo:**
- Em um sistema de vendas, o `Pedido` pode ser a raiz de um aggregate que inclui as entidades `Item do Pedido` e `Endereço de Entrega`. Todas as operações que afetam o `Pedido` e seus itens são realizadas através da entidade `Pedido`, que garante a consistência do aggregate.

Esses componentes são essenciais para modelar corretamente um sistema orientado por domínio, garantindo que o software seja consistente, fácil de manter e reflita corretamente as regras de negócio.

---

#### 5. **Domain Events (Eventos de Domínio)**

Os **domain events** capturam **mudanças importantes** e **fatos relevantes** que ocorrem dentro do domínio. Esses eventos permitem que diferentes partes do sistema sejam notificadas de que algo importante aconteceu, sem depender diretamente umas das outras, promovendo um baixo acoplamento.

**Características principais:**
- **Fatos do domínio:** Representam acontecimentos que são importantes para o domínio.
- **Notificação de mudanças:** Permitem que outros componentes ou serviços sejam notificados e reajam a esses eventos.

**Exemplo:**
- O evento `PedidoFinalizado` é disparado quando o pedido é finalizado com sucesso. Esse evento pode desencadear ações como o envio de um e-mail de confirmação ao cliente, a atualização de estoque ou a geração de uma nota fiscal.

---

#### 6. **Application Services (Serviços de Aplicação)**

Os **application services** são responsáveis por **orquestrar o fluxo de operações** do sistema, interagindo com os aggregates, domain services, e a infraestrutura. Eles **não devem conter lógica de negócios**. Seu papel é mediar a interação entre os objetos de domínio e outras camadas do sistema.

**Características principais:**
- **Orquestração:** Coordenam as operações entre diferentes componentes.
- **Sem lógica de negócio:** A lógica de negócio permanece nas entidades, services e domain events.

**Exemplo:**
- Um serviço de aplicação `FinalizarPedidoService` pode coordenar o processo de finalizar um pedido. Ele invoca métodos no aggregate `Pedido` para atualizar o status do pedido, chama um `CalcularFreteService`, e dispara o evento `PedidoFinalizado`.

---

#### 7. **Infrastructure Services (Serviços de Infraestrutura)**

Os **infrastructure services** lidam com **interações externas**, como persistência de dados, envio de e-mails, logging, ou comunicação com APIs externas. Eles são serviços que suportam as operações de infraestrutura, mas não devem conter regras de negócio.

**Características principais:**
- **Interação externa:** Responsáveis por integração com sistemas externos e infraestrutura técnica.
- **Sem lógica de domínio:** A lógica de domínio permanece nos services e entities.

**Exemplo:**
- Um serviço que envia um e-mail de confirmação após a finalização de um pedido, utilizando um provedor de e-mail externo.

---

#### 8. **Repositories (Repositórios)**

Os **repositories** fornecem um mecanismo para armazenar e recuperar **aggregates** do sistema. Eles **abstraem** os detalhes de persistência (como SQL, NoSQL, etc.), permitindo que o domínio se concentre nas regras de negócio sem se preocupar com os detalhes de armazenamento de dados.

**Características principais:**
- **Persistência de aggregates:** Gerenciam o ciclo de vida dos aggregates.
- **Desacoplamento da infraestrutura:** Abstraem os detalhes de como os dados são armazenados ou recuperados.

**Exemplo:**
- Um `PedidoRepository` pode ser responsável por salvar e recuperar objetos `Pedido` do banco de dados, sem que o domínio precise conhecer os detalhes da infraestrutura de persistência.

---

#### 9. **Modules (Módulos)**

Os **modules** organizam o código em torno de **bounded contexts** e agrupam objetos de domínio relacionados, como entidades, serviços e repositórios, em um único lugar. Eles ajudam a manter o código **coeso** e **organizado**, especialmente em sistemas maiores, garantindo que o código associado a uma funcionalidade específica esteja centralizado.

**Características principais:**
- **Organização coesa:** Agrupam objetos de domínio relacionados.
- **Bounded contexts:** Cada módulo agrupa objetos pertencentes a um contexto delimitado.

**Exemplo:**
- O módulo `Pedidos` pode agrupar todas as entidades, repositórios, serviços de domínio e eventos relacionados ao processamento de pedidos. Esse agrupamento facilita a manutenção e evolução do código.

---

Esses componentes ajudam a estruturar o sistema em torno do domínio, permitindo que o software seja **robusto**, **fácil de manter** e **flexível** para mudanças futuras. No DDD, a organização do código e a comunicação clara entre os componentes são fundamentais para garantir que o sistema reflita com precisão as necessidades do negócio.

---

### Conclusão

O **Domain-Driven Design (DDD)** fornece uma estrutura sólida para modelar regras de negócio complexas, separando preocupações e promovendo um código mais limpo e organizado. Com componentes como **entities**, **value objects**, **domain services**, **aggregates**, e **repositories**, o DDD ajuda a garantir que o software seja alinhado com as necessidades reais do negócio, proporcionando flexibilidade e escalabilidade ao sistema.
