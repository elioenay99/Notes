---
title: Aula 1 - Clean Code
created: '2024-09-10T15:56:13.776Z'
modified: '2024-09-12T13:08:31.463Z'
---

### Aula 1 - Clean Code

#### Problemas Comuns em Projetos de Software

1. **Código fonte bagunçado**:
   - É difícil saber por onde começar.
   - Exemplo: *Projudi* – auto-explicativo.

2. **Dependência de uma pessoa para mexer em partes do código**:
   - Cria gargalos e dependência excessiva de um único desenvolvedor.

3. **Medo de mexer em algo e estragar outra parte**:
   - Falta de testes pode causar esse receio.
   - Boa prática: melhorar o código existente em vez de adicionar código duplicado.

4. **Mais defeitos do que funcionalidades novas**:
   - O desenvolvimento é afetado, e o projeto fica travado com correções de bugs.

5. **Horas extras necessárias para entregar no prazo**:
   - Reflexo de problemas de qualidade e planejamento do código.

6. **Ninguém quer fazer deploy na sexta-feira**:
   - Falta de confiança no código, geralmente por ausência de testes adequados.

#### Causa comum: Código mal escrito
   - Grande parte dos problemas pode ser atribuída à baixa qualidade do código.

#### Pair Programming (Programação em Dupla)

**Vantagens**:
   - Menos interrupções.
   - Maior qualidade do código.
   - Compartilhamento de conhecimento.
   - Nivelamento técnico da equipe.

#### Sensação de trabalho braçal e desgastante

**Como resolver**:
   - Usar testes automatizados com mocks para evitar o excesso de testes manuais.
   - Testar apenas funcionalidades na tela, não o funcionamento básico.

#### Incidência de defeitos
   - "A lógica deve ser clara para dificultar que os defeitos se escondam." — *Bjarne Stroustrup*.

**Consequências**:
   - Menos produtividade.
   - Sensação de gambiarra no código.
   - A qualidade do código afeta diretamente a rotatividade da equipe.

#### Motivação do time

**O que motiva?**:
   - Dinheiro.
   - Ambiente de trabalho.
   - Crescimento profissional.

#### O impacto de um código mal feito na empresa
   - Gasta-se mais tempo corrigindo problemas do que criando novas funcionalidades.
   - Clientes podem reportar mais problemas, afetando o crescimento da empresa e suas vendas.

### O que é Clean Code?

- "Clean code é simples e direto." — *Grady Booch*.
- "Parece que foi escrito por alguém que se importa." — *Michael Feathers*.
- "Quando você lê uma rotina, ela é praticamente o que você esperava." — *Ward Cunningham*.
- "Qualquer um pode escrever código que o computador entenda, mas bons programadores escrevem código que outros humanos entendem." — *Martin Fowler*.

### Medindo a qualidade do código
   - "A quantidade de vezes que você xinga o código é uma métrica de sua qualidade."

#### Refatoração

- **O que é Refactoring?**
   - "Alteração na estrutura interna do software para torná-lo mais fácil de entender e menos custoso de modificar, sem alterar seu comportamento observável." — *Martin Fowler*.

**Por que refatorar?**:
   - Refactoring é um investimento: torna o software mais sustentável e competitivo.
   - Refatore antes que seja tarde demais. Evite chegar ao ponto de não retorno, onde as mudanças ficam muito caras e arriscadas.

**Quando refatorar?**:
   - Ao adicionar novas funcionalidades.
   - Ao corrigir defeitos.
   - Quando precisar entender uma parte do código.

**Refactoring e a dívida técnica**:
   - A falta de refatoração aumenta a "dívida técnica", tornando o software mais difícil de manter.
   - "Se você quer contar linhas de código, deve pensar nelas como linhas gastas, não produzidas." — *Edsger Dijkstra*.

### Code Smells e Técnicas de Refactoring

1. **Nomes estranhos em variáveis**:
   - Renomeie variáveis com nomes mais significativos.

2. **Variáveis temporárias desnecessárias**:
   - Internalize variáveis temporárias.

3. **Números mágicos**:
   - Substitua números mágicos por constantes significativas.

4. **Comentários explicativos desnecessários**:
   - Substitua por variáveis explicativas.

5. **Código morto**:
   - Apague código que não é mais utilizado.

6. **Linhas em branco desnecessárias**:
   - Apague linhas em branco que não têm função.

7. **Retornos estranhos**:
   - Substitua códigos de erro por exceções.

8. **Condições confusas**:
   - Remova condições aninhadas usando cláusulas de guarda.
   - Consolide fragmentos e expressões condicionais duplicados.
   - Utilize ou remova o operador ternário quando adequado.

9. **Switch Statements**:
   - Substitua por polimorfismo.

10. **Métodos longos**:
    - Extraia métodos menores e mais claros.

11. **Lista longa de parâmetros**:
    - Passe o objeto inteiro ou crie uma classe de parâmetros.

12. **Falta de tratamento de exceções**:
    - Trate exceções adequadamente e forneça informações úteis ao lançar exceções.
    - Relance exceções adequadas ao domínio da aplicação.
    - Substitua o tratamento de exceções por verificações condicionais quando possível.

### Conclusão
Manter o código limpo e constantemente refatorado é essencial para a sustentabilidade de projetos de software. A qualidade do código afeta diretamente a produtividade, a motivação do time e, por fim, o sucesso do produto no mercado.
