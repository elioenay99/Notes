---
title: Aula 1 - Clean Code
created: '2024-09-10T15:56:13.776Z'
modified: '2024-09-12T15:04:41.584Z'
---

### Aula 1 - Clean Code

#### Problemas Comuns em Projetos de Software

1. **Código fonte bagunçado**:
   - Quando o código é desorganizado, torna-se difícil saber por onde começar.
   - Exemplo: *Projudi* – Um exemplo claro de sistema com complexidade e falta de organização, que dificulta a manutenção.

2. **Dependência de uma pessoa para mexer em partes do código**:
   - Isso cria gargalos e uma dependência excessiva de um único desenvolvedor, que se torna indispensável em áreas específicas do sistema.

3. **Medo de mexer em algo e estragar outra parte**:
   - Esse medo é comum quando não há testes automatizados, tornando arriscado modificar o código.
   - A boa prática é melhorar o código existente, evitando adicionar código duplicado.

4. **Mais defeitos do que funcionalidades novas**:
   - Quando o projeto é travado por correções de bugs, o desenvolvimento de novas funcionalidades é prejudicado.

5. **Horas extras necessárias para entregar no prazo**:
   - Problemas de qualidade e planejamento do código resultam em trabalho extra para cumprir prazos.

6. **Ninguém quer fazer deploy na sexta-feira**:
   - A falta de confiança no código, especialmente em sistemas sem testes adequados, gera receio de fazer deploys perto do fim de semana.

#### Causa comum: Código mal escrito
   - Grande parte desses problemas surge da baixa qualidade do código. Código mal estruturado dificulta a manutenção, a compreensão e a evolução do sistema.

---

### Pair Programming (Programação em Dupla)

**Vantagens:**
   - Redução de interrupções: Com duas pessoas trabalhando juntas, há menos pausas e mais foco.
   - Qualidade do código: Dois pares de olhos garantem maior atenção aos detalhes.
   - Compartilhamento de conhecimento: Um desenvolvedor aprende com o outro, elevando o nível técnico da equipe como um todo.
   - Nivelamento técnico: A troca constante de ideias ajuda a equilibrar o conhecimento entre os membros da equipe.

---

### Sensação de trabalho braçal e desgastante

**Como resolver:**
   - Utilizar testes automatizados com mocks pode reduzir a necessidade de testes manuais extensivos.
   - Concentre os testes apenas nas funcionalidades principais, evitando testar operações básicas da linguagem ou framework.

---

### Incidência de defeitos

- "A lógica deve ser clara para dificultar que os defeitos se escondam." — *Bjarne Stroustrup*.

**Consequências de código mal escrito:**
   - Diminuição da produtividade.
   - Sensação de "gambiarra" no código.
   - A qualidade do código impacta diretamente a motivação da equipe e, consequentemente, a retenção de talentos.

---

### Motivação do time

**O que motiva um time?**
   - **Dinheiro:** Salários justos e benefícios.
   - **Ambiente de trabalho:** Um lugar saudável, sem sobrecarga constante e com oportunidades de aprendizado.
   - **Crescimento profissional:** A equipe precisa sentir que está evoluindo tecnicamente e na carreira.

---

### O impacto de um código mal feito na empresa

- Empresas que não cuidam da qualidade do código acabam gastando mais tempo corrigindo problemas do que desenvolvendo novas funcionalidades.
- Clientes insatisfeitos reportam problemas constantes, afetando diretamente a reputação da empresa e suas vendas.

---

### O que é Clean Code?

**Definições de código limpo:**
- "Clean code é simples e direto." — *Grady Booch*.
- "Parece que foi escrito por alguém que se importa." — *Michael Feathers*.
- "Quando você lê uma rotina, ela é praticamente o que você esperava." — *Ward Cunningham*.
- "Qualquer um pode escrever código que o computador entenda, mas bons programadores escrevem código que outros humanos entendem." — *Martin Fowler*.

---

### Medindo a qualidade do código

- "A quantidade de vezes que você xinga o código é uma métrica de sua qualidade."  
  O nível de frustração dos desenvolvedores ao ler ou mexer no código é um indicador direto de sua qualidade. Código bem escrito flui naturalmente, sem causar dores de cabeça.

---

### Refatoração

**O que é Refatoração?**
- "Alteração na estrutura interna do software para torná-lo mais fácil de entender e menos custoso de modificar, sem alterar seu comportamento observável." — *Martin Fowler*.

**Por que refatorar?**
- Refatoração é um investimento que torna o software mais sustentável a longo prazo.
- Se não for feito de forma contínua, o software atinge um ponto de não retorno, onde mudanças se tornam caras e arriscadas.

**Quando refatorar?**
- Ao adicionar novas funcionalidades.
- Ao corrigir defeitos.
- Quando precisar entender uma parte do código mal escrita.

**Refatoração e a dívida técnica:**
- A falta de refatoração aumenta a **dívida técnica**, o que torna o software cada vez mais difícil de manter.
- "Se você quer contar linhas de código, deve pensar nelas como linhas gastas, não produzidas." — *Edsger Dijkstra*.

---

### Code Smells e Técnicas de Refactoring

1. **Nomes estranhos em variáveis:**
   - Use nomes mais claros e significativos para variáveis e funções.

2. **Variáveis temporárias desnecessárias:**
   - Remova variáveis temporárias que apenas adicionam complexidade ao código.

3. **Números mágicos:**
   - Substitua números "soltos" no código por constantes com significado.

4. **Comentários explicativos desnecessários:**
   - Substitua comentários explicativos por código autoexplicativo e mais claro.

5. **Código morto:**
   - Apague código que não é mais utilizado para evitar confusão.

6. **Linhas em branco desnecessárias:**
   - Remova linhas em branco que não ajudam na legibilidade.

7. **Retornos estranhos:**
   - Substitua códigos de erro por exceções adequadas.

8. **Condições confusas:**
   - Use cláusulas de guarda para evitar condições aninhadas.
   - Consolide expressões condicionais duplicadas.

9. **Switch Statements:**
   - Use polimorfismo para substituir longos blocos de switch case.

10. **Métodos longos:**
    - Quebre métodos grandes em métodos menores e mais claros.

11. **Lista longa de parâmetros:**
    - Passe um objeto completo ou crie uma classe de parâmetros para facilitar a leitura e manutenção.

12. **Falta de tratamento de exceções:**
    - Sempre trate exceções de forma adequada e forneça informações úteis.
    - Relance exceções adequadas ao domínio da aplicação.

---

### Conclusão

Manter o código limpo e constantemente refatorado é fundamental para garantir a sustentabilidade dos projetos de software. A qualidade do código impacta diretamente a produtividade, a motivação do time e, em última análise, o sucesso do produto no mercado.

- Clean code permite que o software seja fácil de entender, modificar e escalar.
- Refatorar o código e aplicar práticas de desenvolvimento como TDD (Test-Driven Development) ajuda a garantir que o código se mantenha limpo e de fácil manutenção.
- Um código de qualidade é um dos principais fatores que impacta o crescimento da empresa e a satisfação dos clientes.


