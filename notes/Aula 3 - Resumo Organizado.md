---
attachments: [Clipboard_2024-09-11-11-09-03.png, Clipboard_2024-09-11-11-10-02.png, Clipboard_2024-09-11-11-10-50.png, Clipboard_2024-09-11-11-11-06.png, Clipboard_2024-09-11-11-11-14.png, Clipboard_2024-09-11-11-49-08.png, Clipboard_2024-09-11-16-12-55.png]
title: Aula 3 - Resumo Organizado
created: '2024-09-11T12:51:19.626Z'
modified: '2024-09-11T20:20:44.924Z'
---

### Aula 3 - Resumo Organizado

#### Clean Architecture

**O que é arquitetura de software?**
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

A arquitetura para um ERP é diferente de uma plataforma de streaming ou de um jogo de celular. Existem vários tipos de arquitetura, como cliente-servidor, N camadas, monolítica, distribuída, orientada a serviços ou eventos, orientada ao domínio, entre outras.

**Lembre-se:** Você não é obrigado a adotar a mesma arquitetura para todos os sistemas.

#### Modelos que influenciaram o mercado

![](@attachment/Clipboard_2024-09-11-11-09-03.png)
![](@attachment/Clipboard_2024-09-11-11-10-02.png)
![](@attachment/Clipboard_2024-09-11-11-10-50.png)
![](@attachment/Clipboard_2024-09-11-11-11-06.png)

**Características comuns entre as arquiteturas:**
- Isolam regras de negócio.
- Definem camadas e suas responsabilidades.
- Criam um fluxo de controle e dependência ordenado.
- Favorecem a testabilidade.
- São independentes de recursos externos.
- Facilitam a evolução tecnológica.

#### O que é Clean Architecture?
Clean Architecture é um modelo orientado ao desacoplamento entre as regras de negócio (domínio) e os recursos externos, como frameworks e banco de dados.

**O que é domínio?**
- O domínio é o problema que você está resolvendo.
- "O centro da sua aplicação não é o banco de dados ou o framework que você usa, mas os casos de uso." — *Robert Martin*

#### Clean Architecture

![](@attachment/Clipboard_2024-09-11-11-11-14.png)

![](@attachment/Clipboard_2024-09-11-16-12-55.png)

1. **Controller**: O controlador é responsável por receber os dados de entrada vindos da interface do usuário (UI). Ele orquestra o fluxo de dados entre as camadas, enviando os dados para o próximo passo, que é a camada de fronteira de entrada.

2. **Input Boundary**: A fronteira de entrada (Input Boundary) define uma interface que o **Use Case Interactor** (que será descrito adiante) implementa. Ele recebe os **dados de entrada** do controlador e os utiliza para acionar os casos de uso específicos do sistema.

3. **Use Case Interactor**: Esta é a principal lógica de negócio da aplicação. Ele implementa os casos de uso e interage com as **Entities** (entidades) para processar os dados, aplicar regras de negócio e tomar decisões. O **Use Case Interactor** é uma camada central, pois deve estar isolada de qualquer detalhe externo, como frameworks ou bancos de dados.

4. **Entities**: As entidades representam os objetos de negócio mais puros, contendo as regras de negócio fundamentais. O **Use Case Interactor** usa essas entidades para realizar as operações necessárias.

5. **Output Boundary**: Após processar as informações com o interator de caso de uso, o sistema precisa preparar os dados para a apresentação. A fronteira de saída (Output Boundary) define uma interface para que o **Use Case Interactor** envie os dados de saída para a camada de apresentação.

6. **Presenter**: O apresentador pega os dados do **Output Boundary** e os transforma em um formato que seja apropriado para a exibição. Ele prepara o **View Model**, que contém todos os dados que a **View** (interface de usuário) necessita para renderizar a informação.

7. **View Model**: Este é um objeto que contém os dados prontos para serem exibidos na **View**. Ele é passado para a camada de visualização final.

8. **View**: A view é a interface gráfica ou textual do sistema, onde o usuário interage diretamente com a aplicação. Ela consome o **View Model** e exibe as informações para o usuário.

9. **Data Access Interface**: Essa interface define como o **Use Case Interactor** deve interagir com o banco de dados ou qualquer outro sistema de persistência de dados. Ela garante que a lógica de negócio não depende de implementações específicas de acesso a dados.

10. **Data Access**: Esta é a implementação concreta da **Data Access Interface**, onde os dados são realmente acessados, seja em um banco de dados, sistema de arquivos ou outro meio de armazenamento.

11. **Database**: O banco de dados é onde as informações da aplicação são armazenadas de forma persistente.

### Fluxo de Dados:
O fluxo de dados começa com o **Controller**, que recebe a entrada do usuário. Esses dados são encaminhados para o **Use Case Interactor** via o **Input Boundary**. O interator realiza a lógica de negócio, interage com as **Entities**, e os resultados são enviados para a camada de saída via o **Output Boundary**. O **Presenter** formata os dados para exibição, preenchendo o **View Model**, que então é mostrado na **View**. Ao mesmo tempo, o interator pode acessar e modificar os dados através da **Data Access Interface** e do **Database**, sem violar a independência das camadas.

### Conclusão:
A Clean Architecture é poderosa por garantir a separação clara de responsabilidades e dependências, promovendo a manutenibilidade e escalabilidade da aplicação. Cada camada tem um papel específico e conhece apenas as interfaces com as quais deve interagir, o que facilita a substituição e teste das partes do sistema.

**Entidades** são responsáveis por modelar as regras de negócios independentes que podem ser aplicadas em qualquer contexto.

**Regras de negócio independentes:**
- O CPF do cliente é válido?
- Qual é o valor total do pedido?
- O desconto é válido?
- Qual é o frete de um item?

**Domínio Anêmico:** É o problema de entidades sem regras de negócio.

**Exceções de negócio:** As entidades devem lançar exceções de negócio para proteger seu estado interno (invariância).

#### Aplicação das regras de negócios
Os casos de uso contêm regras de negócio específicas, aplicando-as em um contexto particular.

**Exemplos de casos de uso:**
- Fazer um pedido.
- Cancelar um pedido.
- Validar um cupom de desconto.
- Emitir uma nota fiscal.

Os casos de uso orquestram entidades e lançam exceções de negócios relevantes ao contexto.

**Caso de uso ≠ CRUD:** Casos de uso envolvem orquestração e persistência.

#### Acessando o banco de dados
Como os casos de uso acessam o banco de dados? Por meio de:
- **Repositórios** (associados ao Domain-Driven Design).
- **DAO** (Data Access Object).
- **Gateway** (encapsula acesso a sistemas externos).
- **Active Record** (antipadrão por violar o SRP).
- **Data Mapper** (como os ORMs fazem).

#### Implementação da persistência
A implementação é feita pelo padrão **Adapter**, que conecta o I/O ao domínio.

**Drivers:** Componentes de baixo nível que realizam conexões com o banco de dados ou HTTP.

#### Regras de negócio e dependências
As dependências devem apontar apenas para dentro (círculos internos).

#### Quantas camadas existem?
Você pode ter mais ou menos camadas, dependendo da complexidade.

**As camadas são fronteiras lógicas, não físicas.**

#### Inicialização da aplicação
O **Main** é o ponto de entrada, onde fábricas e injeções de dependência são configuradas.

#### Dicas:
- Não se apegue a nomes de padrões de projeto ou estruturas de pastas.
- Invista em testes de unidade desde o início.
- Aplique os princípios onde fizer mais sentido, evitando complexidade desnecessária.

