---
title: Aula 7 - Eventos
created: '2024-09-16T12:20:36.848Z'
modified: '2024-09-16T15:15:03.755Z'
---

### Aula 7 - Eventos

Uma **arquitetura orientada a eventos** (Event-Driven Architecture) utiliza eventos para disparar e comunicar serviços desacoplados. Ela é amplamente utilizada em ambientes de micro serviços devido à sua flexibilidade e escalabilidade.

#### Benefícios de uma Arquitetura Orientada a Eventos:
- **Baixo acoplamento** entre serviços, facilitando a manutenção e evolução do sistema.
- **Tolerância a falhas**, já que a comunicação é assíncrona.
- **Controle de débito técnico**, permitindo um fluxo controlado de mensagens e eventos.
- **Escalabilidade mais alta**, possibilitando o escalonamento horizontal dos consumidores.
- **Menores custos de infraestrutura**, devido ao uso eficiente de recursos.
- **Ponto de Recuperação no Tempo (PITR)**: Melhor rastreamento dos eventos e o que aconteceu em momentos específicos.
- **Diversidade tecnológica**, permitindo o uso de diferentes tecnologias para diferentes componentes.

#### Desafios ao Adotar uma Arquitetura Orientada a Eventos:
- **Complexidade mais alta** para garantir que os eventos fluam corretamente.
- **Duplicação de eventos**, que pode ocorrer se não houver um controle rígido.
- **Falta de clareza no workflow**, tornando mais difícil entender o fluxo completo.
- **Transações distribuídas**, que precisam ser controladas em múltiplos serviços.
- **Dificuldade de diagnosticar erros**, já que o fluxo de eventos pode ser complicado de rastrear.
- **Diversidade tecnológica**, que requer expertise em várias ferramentas e frameworks.

#### Estrutura de um Evento
Um evento pode conter desde identificadores até informações completas. Quando faltam informações para processar o evento, o sistema deve ter mecanismos de resolução, como retries ou compensações. Cada evento é processado por um **handler** ou tratador.

### Padrão **Producer-Consumer**
Este padrão é amplamente utilizado em sistemas distribuídos. Ele envolve a utilização de uma **fila de eventos** para garantir que o processamento das mensagens seja feito de forma desacoplada.

#### Componentes do Padrão:

1. **Produtor (Producer)**:
   - Responsável por gerar e enviar eventos para a fila. O produtor não espera o processamento imediato dos eventos.
   
2. **Fila de Eventos (Queue)**:
   - Atua como buffer intermediário, armazenando os eventos até que os consumidores estejam prontos para processá-los.
   
3. **Intermediário de Eventos (Event Broker)**:
   - Gerencia a fila de eventos e distribui as mensagens para os consumidores disponíveis.
   
4. **Consumidor (Consumer)**:
   - Processa as mensagens retiradas da fila e executa as operações necessárias.

Esse padrão oferece alta flexibilidade e resiliência, permitindo o processamento assíncrono e desacoplado.

### Diferença entre Comando e Evento

- **Comando**: Representa uma intenção de um usuário ou sistema, podendo ser aceito ou rejeitado.
  - Exemplos: `PlaceOrder`, `PayInvoice`, `EnrollStudent`.
  - **Características**:
    - Imperativo, ou seja, descreve o que deve ser feito.
    - Pode ser armazenado e executado posteriormente.
    - Promove o desacoplamento entre o solicitante e quem executa a ação.

- **Evento**: Notifica o sistema de algo que aconteceu no passado, e que não pode ser rejeitado.
  - Exemplo: `OrderPlaced`, `InvoicePaid`.

### Uso de Filas
As filas permitem que múltiplos pedidos sejam processados de forma eficiente. Elas são necessárias quando não há recursos suficientes para atender todos os pedidos de forma imediata, ajudando a evitar o desperdício de recursos e permitindo o balanceamento de carga.

### Controle de Transações Distribuídas

As transações em arquiteturas orientadas a eventos são **eventualmente consistentes** e controladas de forma distribuída. O **padrão SAGA** é comumente utilizado para gerenciar essas transações.

### Event Sourcing
**Event Sourcing** é uma estratégia onde o estado de um sistema é derivado da sequência de eventos que ocorreram ao longo do tempo. Ele é amplamente utilizado quando a sequência exata dos eventos é essencial, como em sistemas financeiros (exemplo: **conta bancária**).

#### Benefícios do Event Sourcing:
- **Segurança aumentada**, já que todos os eventos são registrados.
- Possibilidade de reverter operações apenas invertendo o evento.
- **Auditabilidade**, fornecendo um histórico completo de todas as operações.

**Desvantagens**:
- Processar eventos pode ser trabalhoso, especialmente para relatórios e estatísticas.

### CQRS (Command Query Responsibility Segregation)
Para lidar com a separação entre operações de leitura e escrita, utiliza-se o padrão **CQRS**, que divide o sistema em duas pilhas:

1. **Pilha de Comandos (Command Stack)**: Lida com as operações de escrita, aplicando regras de negócio e modificando o estado do sistema.
2. **Pilha de Consultas (Query Stack)**: Focada em operações de leitura, otimizando consultas ao banco de dados para garantir performance.

#### Event Bus
Um **Event Bus** é utilizado para coordenar a comunicação entre as camadas do sistema, publicando eventos e garantindo que as alterações de estado sejam refletidas em todas as partes do sistema.

#### Banco de Dados de Escrita e Leitura
- **Banco de Dados de Escrita**: Armazena as operações de modificação de dados.
- **Banco de Dados de Leitura**: Otimizado para consultas rápidas e eficiente recuperação de dados.

### Conclusão

Adotar uma arquitetura orientada a eventos oferece alta flexibilidade e escalabilidade, mas também traz desafios que exigem uma boa estratégia de controle de transações e manejo de filas. A utilização de padrões como **Event Sourcing**, **SAGA** e **CQRS** ajuda a manter a consistência e a eficiência do sistema.
