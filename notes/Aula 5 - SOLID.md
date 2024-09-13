---
title: Aula 5 - SOLID
created: '2024-09-12T18:45:49.947Z'
modified: '2024-09-13T20:50:51.897Z'
---

### Aula 5 - SOLID

---

#### **Introdução aos Princípios SOLID**

Os princípios **SOLID** são um conjunto de diretrizes para o desenvolvimento de software orientado a objetos, propostos por **Robert C. Martin** (também conhecido como Uncle Bob). Eles têm como objetivo criar sistemas mais flexíveis, compreensíveis e fáceis de manter. Os princípios são baseados em trabalhos anteriores de especialistas como **Tom DeMarco**, **Bertrand Meyer**, **Barbara Liskov**, entre outros. O acrônimo **SOLID** foi cunhado por **Michael Feathers** ao observar os cinco princípios fundamentais definidos por Robert Martin.

Os princípios SOLID ajudam a combater problemas comuns no desenvolvimento de software, tais como:

- **Rigidez (Rigidity):** Dificuldade de alterar o código porque cada mudança afeta muitas outras partes do sistema.
- **Fragilidade (Fragility):** Alterações em uma parte do sistema causam quebras inesperadas em outras partes.
- **Imobilidade (Immobility):** Dificuldade de reutilizar código porque ele está fortemente acoplado a outros componentes.

**Os cinco princípios SOLID são:**

1. **Single Responsibility Principle (SRP)** — Princípio da Responsabilidade Única
2. **Open/Closed Principle (OCP)** — Princípio Aberto/Fechado
3. **Liskov Substitution Principle (LSP)** — Princípio da Substituição de Liskov
4. **Interface Segregation Principle (ISP)** — Princípio da Segregação de Interfaces
5. **Dependency Inversion Principle (DIP)** — Princípio da Inversão de Dependência

---

#### **1. Single Responsibility Principle (SRP)**

**Definição:**

Uma classe deve ter apenas **uma única razão para mudar**, ou seja, deve ter apenas uma responsabilidade bem definida.

**Explicação:**

O SRP enfatiza que uma classe ou módulo deve ser responsável por apenas um ator ou parte interessada do sistema. Quando uma classe assume múltiplas responsabilidades, mudanças em uma responsabilidade podem afetar ou quebrar outras funcionalidades, aumentando o risco de erros e dificultando a manutenção.

**Benefícios:**

- **Coesão Aumentada:** Classes mais focadas em uma única tarefa.
- **Menor Acoplamento:** Mudanças em uma parte do sistema não afetam outras.
- **Facilidade de Manutenção e Teste:** Código mais simples de entender, modificar e testar.

**Exemplo Prático:**

Imagine uma classe `Relatorio` que:

- Gera dados de um relatório.
- Formata os dados em PDF.
- Envia o relatório por e-mail.

Esta classe tem múltiplas responsabilidades:

1. **Gerar Dados**
2. **Formatar em PDF**
3. **Enviar por E-mail**

**Aplicando o SRP:**

- **Classe `GeradorDeRelatorio`:** Responsável por gerar os dados.
- **Classe `ExportadorPDF`:** Responsável por formatar os dados em PDF.
- **Classe `EmailService`:** Responsável por enviar e-mails.

Dessa forma, se houver uma mudança na forma como os PDFs são gerados, apenas a classe `ExportadorPDF` precisa ser alterada, sem impactar as outras funcionalidades.

---

#### **2. Open/Closed Principle (OCP)**

**Definição:**

Entidades de software (classes, módulos, funções, etc.) devem estar **abertas para extensão**, mas **fechadas para modificação**.

**Explicação:**

O OCP sugere que o comportamento de um módulo deve poder ser estendido sem modificar seu código-fonte original. Isso é alcançado através de abstrações, como interfaces e classes abstratas, permitindo que novas funcionalidades sejam adicionadas através de herança ou composição.

**Benefícios:**

- **Redução de Riscos:** Menos chances de introduzir bugs em código existente.
- **Facilidade de Extensão:** Novas funcionalidades podem ser adicionadas sem alterar o código já testado e em produção.
- **Melhor Manutenção:** Código mais modular e organizado.

**Exemplo Prático:**

Considere uma classe que calcula descontos para diferentes tipos de clientes:

```java
public class CalculadoraDescontos {
    public double calcularDesconto(Cliente cliente, double valorCompra) {
        if (cliente.isVip()) {
            return valorCompra * 0.10;
        } else {
            return valorCompra * 0.05;
        }
    }
}
```

**Problema:**

Se um novo tipo de cliente for adicionado, como um "Cliente Premium", precisamos modificar a classe `CalculadoraDescontos`, violando o OCP.

**Aplicando o OCP:**

- Criar uma interface `Desconto`:

```java
public interface Desconto {
    double calcular(double valorCompra);
}
```

- Implementar classes concretas para cada tipo de desconto:

```java
public class DescontoVip implements Desconto {
    public double calcular(double valorCompra) {
        return valorCompra * 0.10;
    }
}

public class DescontoRegular implements Desconto {
    public double calcular(double valorCompra) {
        return valorCompra * 0.05;
    }
}

public class DescontoPremium implements Desconto {
    public double calcular(double valorCompra) {
        return valorCompra * 0.15;
    }
}
```

- A classe `CalculadoraDescontos` usa a abstração:

```java
public class CalculadoraDescontos {
    public double calcular(Desconto desconto, double valorCompra) {
        return desconto.calcular(valorCompra);
    }
}
```

Agora, ao adicionar um novo tipo de desconto, criamos uma nova classe que implementa `Desconto`, sem modificar o código existente.

---

#### **3. Liskov Substitution Principle (LSP)**

**Definição:**

Objetos de uma classe devem poder ser substituídos por objetos de suas subclasses sem que isso quebre a aplicação.

**Explicação:**

O LSP enfatiza que subclasses devem ser substituíveis por suas superclasses. Isso significa que a classe derivada deve estender o comportamento da classe base, não restringi-lo.

**Regras Importantes:**

1. **Pré-condições não devem ser fortalecidas na subclasse.**
2. **Pós-condições não devem ser enfraquecidas na subclasse.**
3. **Invariantes da superclasse devem ser preservadas na subclasse.**

**Exemplo Prático:**

Considere as classes `Retangulo` e `Quadrado`:

```java
public class Retangulo {
    protected int largura;
    protected int altura;

    public void setLargura(int largura) { this.largura = largura; }
    public void setAltura(int altura) { this.altura = altura; }

    public int getArea() { return largura * altura; }
}

public class Quadrado extends Retangulo {
    @Override
    public void setLargura(int tamanho) {
        this.largura = tamanho;
        this.altura = tamanho;
    }

    @Override
    public void setAltura(int tamanho) {
        this.largura = tamanho;
        this.altura = tamanho;
    }
}
```

**Problema:**

Embora matematicamente um quadrado seja um retângulo, a classe `Quadrado` quebra o LSP porque altera o comportamento esperado de `Retangulo`. Ao substituir um `Retangulo` por um `Quadrado`, podemos obter resultados inesperados.

**Solução:**

- Não utilizar herança nesse caso.
- Criar classes separadas ou usar composição.

---

#### **4. Interface Segregation Principle (ISP)**

**Definição:**

Nenhum cliente deve ser forçado a depender de métodos que não utiliza.

**Explicação:**

O ISP recomenda dividir interfaces extensas em interfaces menores e mais específicas, evitando que classes sejam obrigadas a implementar métodos desnecessários.

**Benefícios:**

- **Redução de Acoplamento:** Classes dependem apenas dos métodos que realmente usam.
- **Maior Coesão:** Interfaces mais focadas em funcionalidades específicas.
- **Facilidade de Manutenção:** Mudanças em uma interface afetam menos classes.

**Exemplo Prático:**

Uma interface ampla:

```java
public interface Operacoes {
    void adicionar();
    void atualizar();
    void deletar();
    void visualizar();
}
```

Uma classe que só precisa visualizar seria forçada a implementar métodos que não usa.

**Aplicando o ISP:**

Dividir em interfaces menores:

```java
public interface Adicionar {
    void adicionar();
}

public interface Atualizar {
    void atualizar();
}

public interface Deletar {
    void deletar();
}

public interface Visualizar {
    void visualizar();
}
```

Agora, uma classe implementa apenas as interfaces necessárias.

---

#### **5. Dependency Inversion Principle (DIP)**

**Definição:**

- Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.
- Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.

**Explicação:**

O DIP sugere que dependências devem ser invertidas, fazendo com que módulos de alto nível não dependam das implementações concretas de módulos de baixo nível, mas sim de interfaces ou classes abstratas.

**Benefícios:**

- **Desacoplamento:** Facilita a substituição de componentes sem afetar outros.
- **Facilidade de Testes:** Permite o uso de mocks ou stubs.
- **Evolução do Sistema:** Implementações podem ser alteradas sem impactar módulos de alto nível.

**Exemplo Prático:**

Sem DIP:

```java
public class EmailService {
    public void enviarEmail(String mensagem) {
        // Código para enviar e-mail
    }
}

public class Notificacao {
    private EmailService emailService;

    public Notificacao() {
        emailService = new EmailService();
    }

    public void novaNotificacao(String mensagem) {
        emailService.enviarEmail(mensagem);
    }
}
```

**Problema:**

A classe `Notificacao` depende diretamente da implementação concreta `EmailService`.

**Aplicando o DIP:**

- Criar uma interface:

```java
public interface Mensageiro {
    void enviarMensagem(String mensagem);
}
```

- Implementar a interface:

```java
public class EmailService implements Mensageiro {
    public void enviarMensagem(String mensagem) {
        // Código para enviar e-mail
    }
}
```

- Modificar a classe `Notificacao`:

```java
public class Notificacao {
    private Mensageiro mensageiro;

    public Notificacao(Mensageiro mensageiro) {
        this.mensageiro = mensageiro;
    }

    public void novaNotificacao(String mensagem) {
        mensageiro.enviarMensagem(mensagem);
    }
}
```

Agora, `Notificacao` depende da abstração `Mensageiro`, permitindo substituir `EmailService` por outras implementações, como `SmsService`.

---

### **Conclusão**

Os princípios **SOLID** são fundamentais para o desenvolvimento de software orientado a objetos de alta qualidade. Eles promovem:

- **Flexibilidade:** Código adaptável a mudanças.
- **Manutenibilidade:** Facilita correções e melhorias.
- **Reutilização:** Componentes podem ser reutilizados em diferentes contextos.
- **Legibilidade:** Código mais claro e fácil de entender.

**Resumo dos Princípios:**

1. **SRP:** Mantenha uma classe focada em uma única responsabilidade.
2. **OCP:** Estruture o código para ser estendido sem ser modificado.
3. **LSP:** Garanta que subclasses possam substituir suas superclasses sem alterar o comportamento esperado.
4. **ISP:** Use interfaces específicas para evitar dependências desnecessárias.
5. **DIP:** Dependa de abstrações, não de implementações concretas.

---

### **Referências Adicionais**

- **Livros:**
  - *"Agile Software Development, Principles, Patterns, and Practices"* — **Robert C. Martin**
  - *"Clean Code: A Handbook of Agile Software Craftsmanship"* — **Robert C. Martin**
  - *"Clean Architecture: A Craftsman's Guide to Software Structure and Design"* — **Robert C. Martin**
---

**Nota Final:**

Aplicar os princípios **SOLID** é um investimento na qualidade e longevidade do software. Embora possa exigir um esforço adicional no início, os benefícios em termos de manutenibilidade, extensibilidade e qualidade geral do código são inestimáveis. Ao incorporar esses princípios em sua prática diária, você estará aprimorando não apenas seu código, mas também suas habilidades como desenvolvedor.

---
