---
attachments: [Clipboard_2024-09-10-15-15-42.png, Clipboard_2024-09-10-15-26-27.png]
title: Aula 2 - Resumo Organizado
created: '2024-09-10T18:01:03.743Z'
modified: '2024-09-11T12:50:53.777Z'
---

### Aula 2 - Resumo Organizado

#### A importância dos testes

**Problema em não ter testes:**
- Estamos sempre torcendo para que o código funcione.
- Nos tornamos executores rápidos e práticos de telas, sendo nós mesmos os "testes".
- Isso cria a sensação de estar em um castelo de cartas que pode cair a qualquer momento.

**Por que não refatoramos?**
- O maior motivo é a falta de testes.
- Ter testes automatizados não garante a ausência de defeitos, mas minimiza os riscos.

#### O que é um teste automatizado?

- **Given:** Definição das informações necessárias para executar o comportamento que será testado.
- **When:** Execução do comportamento.
- **Then:** Verificação do que aconteceu após a execução, comparando o resultado com a expectativa.

Este conceito é similar ao AAA (Arrange, Act, Assert).

#### Tipos de testes automatizados

O ideal é combinar diferentes tipos de testes, pois apenas testes unitários não garantem o funcionamento completo do sistema.

![](@attachment/Clipboard_2024-09-10-15-15-42.png)

#### Test-Driven Development (TDD)

- **TDD** é um método para construir software, não apenas para testá-lo.

![](@attachment/Clipboard_2024-09-10-15-26-27.png)

- "TDD é uma forma de gerenciar o medo durante a programação" — *Kent Beck*.
  
**Three Laws of TDD** — *Robert C. Martin*:
1. Você não pode escrever nenhum código antes de criar um teste que falhe.
2. Não escreva mais testes do que o suficiente para detectar falhas.
3. Não escreva mais código do que o suficiente para passar nos testes.

#### Dificuldades ao escrever testes

- Escrever testes exige disciplina.
- Queremos ver tudo funcionando rapidamente, o que gera ansiedade.
- Muitas vezes, nos acostumamos a desenvolver com foco na interface ou no banco de dados, e não no domínio.
- Arquiteturas não testáveis podem ser um grande obstáculo.

#### O que fazer com uma arquitetura acoplada?

Utilize o **Test Double**, um padrão que substitui um componente dependente (DOC) por razões de performance ou segurança.

Nem tudo é **mock**. Existem outros tipos de objetos usados em testes:

- **Dummy:** Objeto usado apenas para preencher parâmetros.
- **Stubs:** Retornam respostas prontas, usadas por questões de performance ou segurança.
- **Spies:** Monitoram e armazenam execuções de métodos para verificação posterior.
- **Mocks:** Similares aos stubs e spies, mas permitem definir comportamentos esperados de forma mais rígida.
- **Fake:** Implementações que simulam o comportamento real de um objeto.

#### "Não tenho tempo para testes automatizados"

Embora muitos acreditem não ter tempo para criar testes, acabam tendo tempo para:
- Ouvir reclamações de clientes.
- Corrigir bugs e lidar com código de baixa qualidade.
- Testar manualmente e treinar novos membros da equipe.
- Reclamarem do projeto.

#### Como praticar no dia a dia?

- Crie seus primeiros testes.
- Organize eventos como Coding Dojo.
- Pratique em plataformas como *HackerRank*, que oferecem desafios interativos e são usadas por empresas no processo de contratação.

---

Com essas práticas, será possível melhorar a qualidade do código, reduzir a incidência de defeitos e aumentar a confiança nas entregas.
