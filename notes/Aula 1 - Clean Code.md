---
title: Aula 1 - Clean Code
created: '2024-09-10T15:56:13.776Z'
modified: '2024-09-13T15:11:17.777Z'
---

### Aula 1 - Clean Code

#### Problemas Comuns em Projetos de Software

1. **Código fonte bagunçado**:
   - Quando o código é desorganizado, torna-se difícil saber por onde começar e onde cada funcionalidade está localizada.
   - Exemplo: Sistemas legados com struts – Um exemplo claro de sistema com complexidade e falta de organização, o que dificulta a manutenção e a evolução do sistema.
   - A desorganização geralmente leva a um aumento de **dívida técnica**, dificultando a adição de novas funcionalidades.

2. **Dependência de uma pessoa para mexer em partes do código**:
   - Isso cria gargalos e aumenta o risco de paralisação do projeto se essa pessoa não estiver disponível.
   - A documentação inadequada e a falta de **compartilhamento de conhecimento** dentro da equipe agravam esse problema.

3. **Medo de mexer em algo e estragar outra parte**:
   - Sem testes automatizados, qualquer mudança no código pode introduzir novos erros.
   - A prática de **Test-Driven Development (TDD)** minimiza esse risco, incentivando a criação de testes antes da implementação.

4. **Mais defeitos do que funcionalidades novas**:
   - Projetos onde o foco se desloca da inovação para a correção contínua de bugs, gerando desmotivação.
   - Isso ocorre devido à falta de refatoração contínua e à ausência de boas práticas de **design de software**.

5. **Horas extras necessárias para entregar no prazo**:
   - Má qualidade de código e planejamento inadequado resultam em **retrabalho** e longas jornadas de trabalho, especialmente perto de entregas.

6. **Ninguém quer fazer deploy na sexta-feira**:
   - A falta de confiança no código e a ausência de um pipeline de **CI/CD** robusto e automatizado geram receio de deploys, especialmente antes de finais de semana.

#### Causa comum: Código mal escrito
   - Grande parte desses problemas é fruto de código mal estruturado. Isso torna o código mais difícil de **manter**, **entender** e **escalar** ao longo do tempo, resultando em baixa eficiência da equipe.

---

### Pair Programming (Programação em Dupla)

**Vantagens:**
   - **Redução de erros:** Dois desenvolvedores revisam o código constantemente, identificando problemas mais cedo.
   - **Melhoria contínua:** A troca de ideias estimula a **inovação** e a busca por soluções mais elegantes.
   - **Cultura de feedback:** Facilita a integração de práticas como **code review** em tempo real.

---

### Sensação de trabalho braçal e desgastante

**Como resolver:**
   - A utilização de **ferramentas de automação**, como **CI/CD**, ajuda a reduzir o trabalho manual.
   - Testes automatizados com **mocks** e **stubs** reduzem o esforço e o tempo gastos em testes manuais.

---

### Incidência de defeitos

- "A lógica deve ser clara para dificultar que os defeitos se escondam." — *Bjarne Stroustrup*.

**Consequências de código mal escrito:**
   - Aumento de **dívida técnica** e necessidade constante de refatorações.
   - A equipe perde tempo com correções, e a produtividade **diminui**.
   - Impacto direto na **motivação da equipe**, gerando **turnover** de talentos.

---

### Motivação do time

**Fatores que influenciam a motivação:**
   - **Autonomia:** Desenvolvedores se sentem mais motivados quando têm autonomia para tomar decisões.
   - **Desafios técnicos:** Equipes motivadas buscam superar desafios e adquirir novas habilidades.

---

### O impacto de um código mal feito na empresa

- Empresas que não priorizam a qualidade do código sofrem com **custos de manutenção** elevados e ciclos de desenvolvimento lentos.
- Isso leva à **perda de competitividade** no mercado, afetando diretamente o crescimento e a satisfação dos clientes.

---

### O que é Clean Code?

**Definições de código limpo:**
- "Clean code é simples e direto." — *Grady Booch*.
- "Parece que foi escrito por alguém que se importa." — *Michael Feathers*.
- **Legibilidade** e **clareza** são prioridades no código limpo, tornando-o fácil de entender e modificar.

---

### Medindo a qualidade do código

- A **facilidade de leitura** do código é uma das principais métricas de sua qualidade.
- Código limpo reduz o tempo gasto em **debugging**, favorecendo a produtividade.

---

### Refatoração

**O que é Refatoração?**
- "Alteração na estrutura interna do software para torná-lo mais fácil de entender e menos custoso de modificar, sem alterar seu comportamento observável." — *Martin Fowler*.
- Refatorar constantemente é essencial para evitar o acúmulo de **dívida técnica**.

**Quando refatorar?**
- **Sempre** que houver a oportunidade de simplificar o código sem alterar seu comportamento.
- Refatoração contínua facilita a **evolução do sistema** e reduz a necessidade de grandes reescritas no futuro.

---

### Code Smells e Técnicas de Refatoração

- **Code Smells** indicam áreas do código que podem se tornar problemáticas. Alguns exemplos incluem:
   1. **Métodos longos**: Quebre em métodos menores e mais focados.
   2. **Números mágicos**: Substitua por constantes com significado claro.
   3. **Switch Statements extensos**: Considere o uso de **polimorfismo**.

---

### Conclusão

Manter o código limpo e refatorado de maneira contínua é a chave para a **sustentabilidade** de qualquer projeto de software. A qualidade do código afeta diretamente a capacidade de a equipe manter e evoluir o sistema, e uma base de código limpa garante que novos desenvolvedores possam contribuir sem dificuldades.

- **Clean code** é essencial para garantir a **escalabilidade** e **facilidade de manutenção** do software.
- Aplicar práticas como **TDD** e **refatoração contínua** preserva a qualidade e a longevidade do projeto, aumentando sua capacidade de adaptação e evolução.

--- 

Essas melhorias detalham ainda mais os conceitos, conectando-os com práticas como TDD e CI/CD, além de destacar a importância da motivação da equipe e da sustentabilidade do código.
