---
attachments: [Clipboard_2024-09-10-15-15-42.png, Clipboard_2024-09-10-15-26-27.png]
title: Aula 2 - Test-Driven Development (TDD)
created: '2024-09-10T18:01:03.743Z'
modified: '2024-09-12T15:03:02.283Z'
---

### Aula 2 - Test-Driven Development (TDD)

#### A importância dos testes

**Problemas em não ter testes:**
- Sem testes, há sempre o risco de torcer para que o código funcione, o que não é uma boa prática.
- Desenvolvedores acabam testando manualmente as funcionalidades, o que torna o processo mais demorado e propenso a erros.
- Essa abordagem cria a sensação de que o sistema é frágil, como um castelo de cartas que pode desmoronar a qualquer momento.

**Por que evitamos refatorar?**
- O maior motivo para não refatorar código é a falta de testes. Sem eles, a refatoração pode introduzir novos erros.
- Mesmo com testes automatizados, não há garantia total de que não existam defeitos, mas os testes ajudam a reduzir consideravelmente os riscos.

---

#### O que é um teste automatizado?

Um teste automatizado é uma verificação programática de que o comportamento de uma parte do código funciona conforme esperado. Ele segue uma estrutura conhecida como **AAA** (Arrange, Act, Assert), que pode ser descrita da seguinte forma:

- **Given (Arrange):** Configura os dados ou o estado necessário para executar o comportamento que será testado.
- **When (Act):** Executa o comportamento que está sendo testado.
- **Then (Assert):** Verifica os resultados, comparando com as expectativas.

---

#### Tipos de testes automatizados

O ideal é combinar diferentes tipos de testes para cobrir vários aspectos do sistema. Alguns exemplos incluem testes de unidade, integração, e2e (end-to-end), entre outros. Usar apenas testes de unidade pode não garantir que o sistema completo funcione corretamente, já que eles testam partes isoladas.

![](@attachment/Clipboard_2024-09-10-15-15-42.png)

---

#### O que é Test-Driven Development (TDD)?

**TDD** é um método de desenvolvimento de software que utiliza testes para guiar o processo de codificação. Ele se baseia em ciclos curtos de feedback e começa criando testes antes mesmo da implementação do código.

![](@attachment/Clipboard_2024-09-10-15-26-27.png)

**TDD ajuda a gerenciar o medo de quebrar funcionalidades existentes durante o desenvolvimento** — *Kent Beck*.

**Three Laws of TDD** — *Robert C. Martin*:
1. Não se escreve nenhum código até que um teste que falhe seja criado.
2. Escreva apenas o suficiente de um teste para ver o código falhar.
3. Escreva apenas o suficiente de código para que os testes passem.

---

#### Dificuldades ao escrever testes

- **Disciplina:** Escrever testes exige uma mudança de mentalidade e um comprometimento maior com a qualidade do código.
- **Ansiedade:** Há uma tendência de querer ver o sistema funcionando rapidamente, o que pode prejudicar a qualidade do código e levar ao abandono dos testes.
- **Foco errado:** Muitas vezes, os desenvolvedores focam em testar apenas a interface ou banco de dados, em vez de se concentrar no domínio e nas regras de negócio.
- **Arquiteturas não testáveis:** Sistemas mal arquitetados tornam a tarefa de testar quase impossível. Arquiteturas acopladas dificultam a criação de testes isolados.

---

#### O que fazer com uma arquitetura acoplada?

Utilize o conceito de **Test Doubles** para isolar o comportamento que deseja testar. Test Doubles são objetos que simulam o comportamento de dependências externas para permitir que as partes do sistema sejam testadas de maneira independente. Existem várias formas de Test Doubles:

- **Dummy:** Objetos que existem apenas para completar parâmetros, mas que não são utilizados no teste.
- **Stub:** Fornece respostas pré-programadas para métodos que são chamados durante o teste.
- **Spy:** Espiona o comportamento de um método, armazenando informações sobre como ele foi chamado.
- **Mock:** Simula comportamentos mais complexos, verificando se determinadas interações ocorrem como esperado.
- **Fake:** Implementa uma versão simplificada de uma funcionalidade real.

---

#### "Não tenho tempo para testes automatizados"

Embora a criação de testes possa parecer demorada, a falta de testes resulta em maior tempo gasto com:
- Reclamações de clientes devido a bugs.
- Correção de defeitos em produção.
- Dificuldade em manter e evoluir o código.
- Testes manuais demorados e menos eficientes.
- Treinamento contínuo de novos desenvolvedores que têm dificuldade para entender um código sem testes ou documentação.

---

#### Como praticar no dia a dia?

- **Comece criando seus primeiros testes**: Experimente começar escrevendo testes para funcionalidades novas ou para corrigir defeitos.
- **Coding Dojo:** Participe ou organize eventos como Coding Dojo, onde equipes praticam técnicas como TDD em conjunto, aumentando a confiança nas técnicas.
- **Plataformas de desafios:** Use plataformas como *HackerRank* para praticar escrita de testes e solucionar desafios de programação com base em testes.

---

### Conclusão

**Test-Driven Development (TDD)** não é apenas uma prática de teste, mas uma filosofia de desenvolvimento que permite que o código seja mais sustentável e confiável. Ao integrar testes ao processo de desenvolvimento, é possível refatorar com confiança, minimizar defeitos e aumentar a qualidade do software. Essas práticas também ajudam a construir um código mais flexível e preparado para mudanças, reduzindo a dependência de verificações manuais e aumentando a produtividade da equipe.
