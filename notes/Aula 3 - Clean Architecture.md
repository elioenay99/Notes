---
attachments: [Clipboard_2024-09-11-11-09-03.png, Clipboard_2024-09-11-11-10-02.png, Clipboard_2024-09-11-11-10-50.png, Clipboard_2024-09-11-11-11-06.png, Clipboard_2024-09-11-11-11-14.png, Clipboard_2024-09-11-11-49-08.png, Clipboard_2024-09-11-16-12-55.png]
title: Aula 3 - Clean Architecture
created: '2024-09-11T12:51:19.626Z'
modified: '2024-09-12T15:01:43.011Z'
---

### Aula 3 - Clean Architecture

#### O que é arquitetura de software?

- "O objetivo da arquitetura de software é minimizar a quantidade de recursos humanos necessários para construir e manter um determinado sistema." — *Robert Martin*
- "Arquitetura de Software são decisões que são ao mesmo tempo importantes e difíceis de mudar." — *Martin Fowler*
- "Uma arquitetura é o conjunto de decisões significativas sobre a organização de um sistema de software, a seleção dos elementos estruturais e suas interfaces, juntamente com seu comportamento conforme especificado nas colaborações entre esses elementos." — *Rational Unified Process*
- "Arquitetura é definida pela prática recomendada como a organização fundamental de um sistema, incorporada em seus componentes, suas relações entre si e com o ambiente, e os princípios que regem seu design e evolução." — *Padrão ANSI/IEEE 1471-2000*

**Palavras-chave recorrentes:**
- Organização, estrutura, design, relacionamento e comportamento.

#### O que deve ser levado em consideração na definição de uma arquitetura?
- Escopo do produto.
- Volume de requisições.
- Tipo de dispositivo.
- Tamanho e perfil da equipe.
- Prazo de entrega.
- Orçamento.

Cada tipo de sistema, como um ERP, uma plataforma de streaming ou um jogo de celular, exige uma abordagem arquitetônica diferente. Existem vários tipos de arquitetura, como cliente-servidor, N camadas, monolítica, distribuída, orientada a serviços ou eventos, orientada ao domínio, entre outras.

**Lembre-se:** A escolha da arquitetura depende do contexto, não há uma solução única para todos os casos.

---

### Clean Architecture

A **Clean Architecture** é um modelo arquitetural orientado ao desacoplamento das regras de negócio (domínio) dos recursos externos, como frameworks, banco de dados ou interfaces de usuário. Ela promove a separação de responsabilidades, facilitando a manutenção, evolução e testabilidade do sistema.

**O que é domínio?**  
O **domínio** é o problema central que sua aplicação está resolvendo.  
"O centro da sua aplicação não é o banco de dados ou o framework, mas sim os casos de uso." — *Robert Martin*

---

### Componentes da Clean Architecture

![](@attachment/Clipboard_2024-09-11-11-11-14.png)

#### 1. **Controller**
O **Controller** é responsável por receber dados de entrada vindos da interface do usuário (UI) e orquestrar o fluxo entre as camadas. Ele envia os dados para o próximo passo, que é a fronteira de entrada.

#### 2. **Input Boundary**
A **Input Boundary** é uma interface que define como o **Use Case Interactor** recebe os dados de entrada. Ela garante que a lógica de negócios esteja desacoplada de detalhes externos, como frameworks e dispositivos.

#### 3. **Use Case Interactor**
O **Use Case Interactor** contém a principal lógica de negócio da aplicação. Ele implementa os casos de uso e interage com as **Entities** (entidades) para processar dados, aplicar regras de negócio e tomar decisões. Ele também interage com as camadas de persistência e de apresentação, mantendo-se independente de tecnologias específicas.

#### 4. **Entities (Entidades)**
As **entities** representam os objetos mais puros do domínio, contendo as regras de negócio fundamentais. O **Use Case Interactor** utiliza essas entidades para realizar as operações necessárias no domínio.

#### 5. **Output Boundary**
Após processar as informações no interator de caso de uso, o sistema precisa preparar os dados para a apresentação. A **Output Boundary** define uma interface que permite que o **Use Case Interactor** envie dados de saída para a camada de apresentação.

#### 6. **Presenter**
O **Presenter** transforma os dados recebidos pela **Output Boundary** em um formato apropriado para a exibição. Ele prepara o **View Model**, que contém todas as informações necessárias para a **View** (interface de usuário).

#### 7. **View Model**
O **View Model** é um objeto que contém os dados prontos para serem exibidos na **View**. Ele é passado para a interface de usuário para ser renderizado.

#### 8. **View**
A **View** é a interface onde o usuário interage diretamente com a aplicação. Ela consome o **View Model** e exibe as informações formatadas para o usuário.

#### 9. **Data Access Interface**
Essa interface define como o **Use Case Interactor** interage com o banco de dados ou qualquer outro sistema de persistência. Ela garante que a lógica de negócio não dependa de implementações específicas de acesso a dados.

#### 10. **Data Access**
Essa é a implementação concreta da **Data Access Interface**, onde os dados são realmente acessados e manipulados, seja em um banco de dados, sistema de arquivos ou qualquer outro repositório.

#### 11. **Database**
O **Database** é o repositório final onde as informações da aplicação são armazenadas de forma persistente.

---

### Fluxo de Dados

O fluxo de dados na Clean Architecture segue um caminho bem definido:
1. O **Controller** recebe os dados de entrada do usuário e os passa para o **Use Case Interactor** por meio da **Input Boundary**.
2. O **Use Case Interactor** executa as regras de negócio usando as **Entities** e prepara os dados de saída, enviando-os pela **Output Boundary**.
3. O **Presenter** transforma esses dados em um formato apropriado e preenche o **View Model**, que será consumido pela **View**.
4. Simultaneamente, o **Use Case Interactor** pode acessar ou modificar dados por meio da **Data Access Interface**, interagindo com o **Database** para realizar operações de persistência.

Esse ciclo garante que as camadas permaneçam desacopladas e testáveis, além de promover a flexibilidade para mudanças tecnológicas sem impactar a lógica de negócio.

---

### Comparação com Domain-Driven Design (DDD)

O **DDD** se concentra em modelar o domínio do problema, focando nas regras de negócio e na organização do código em torno dos casos de uso e das entidades. A **Clean Architecture** complementa o DDD ao definir como estruturar o sistema em camadas, mantendo o foco no domínio e garantindo que as dependências externas (bancos de dados, frameworks, APIs) não contaminem a lógica de negócio.

**Semelhanças:**
- Ambos isolam as regras de negócio do restante do sistema.
- Ambos promovem a testabilidade e independência de frameworks e tecnologias externas.

**Diferenças:**
- **Clean Architecture** foca mais na organização estrutural em camadas, enquanto o **DDD** dá mais ênfase à modelagem de domínio e subdomínios.

---

### Aplicando Clean Architecture

**Como aplicar as regras de negócio?**  
Na **Clean Architecture**, as regras de negócio são encapsuladas nos **Use Cases** (casos de uso), que orquestram as **Entities** para realizar as operações específicas.

**Exemplos de casos de uso:**
- Fazer um pedido.
- Cancelar um pedido.
- Validar um cupom de desconto.
- Emitir uma nota fiscal.

Esses casos de uso não envolvem diretamente a infraestrutura do sistema (como banco de dados ou APIs), mas sim a lógica de negócio. O acesso a esses recursos é feito por meio de interfaces e adaptadores, garantindo que o domínio esteja sempre desacoplado de detalhes técnicos.

---

### Persistência e Acesso a Dados

O acesso a dados na Clean Architecture é feito por meio de interfaces que separam a lógica de negócio dos detalhes de implementação. Existem vários padrões que podem ser usados para esse propósito:
- **Repositórios:** Abstraem o acesso a coleções de entidades, geralmente usados no **Domain-Driven Design**.
- **DAO (Data Access Object):** Um padrão que separa a lógica de domínio da lógica de persistência.
- **Gateway:** Um objeto que encapsula o acesso a sistemas externos.
- **Active Record:** Encapsula o acesso ao banco de dados diretamente na entidade (geralmente considerado um antipadrão por violar o princípio de responsabilidade única).
- **Data Mapper:** Um padrão onde os dados são mapeados de e para o banco de dados e o modelo de domínio, muito comum em ORMs.

**Como implementar a persistência?**  
A implementação da persistência é feita por meio do padrão **Adapter**, que conecta a camada de entrada e saída de dados ao domínio, mantendo a independência das tecnologias específicas.

---

### Regras de negócio e dependências

As dependências na Clean Architecture seguem a **Dependency Rule**, onde o fluxo de dependências deve sempre apontar para dentro, ou seja, as camadas mais externas (como interfaces de usuário, frameworks ou bancos de dados) dependem das camadas mais internas (como casos de uso e entidades), mas nunca o contrário.

---

### Dicas e Boas Práticas

1. **Testabilidade:** Invista em testes desde o início. A separação em camadas facilita a criação de testes isolados para cada parte do sistema.
2. **Desacoplamento:** Sempre desacople a lógica de negócio dos detalhes externos. Isso aumenta a flexibilidade e facilita a troca de tecnologias.
3. **Camadas:** Não se apegue demais à quantidade ou nome das camadas. A estrutura deve ser flexível para se adequar ao seu projeto.
4. **Simplicidade:** Não complique sua arquitetura desnecessariamente. Adapte os princípios da Clean Architecture às necessidades do seu projeto.

---

### Conclusão

A **Clean Architecture** promove uma separação clara entre as diferentes partes do sistema, garantindo que as regras de negócio sejam protegidas e desacopladas de tecnologias externas. Isso

 facilita a manutenção, a evolução e a testabilidade do sistema, além de garantir que ele possa se adaptar facilmente a mudanças tecnológicas sem comprometer o núcleo do domínio.
