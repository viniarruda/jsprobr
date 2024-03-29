---
layout: post
title: Entenda de uma vez por todas a pilha de chamadas (Callstack) do JavaScript
image: img/pilha-chamadas.jpg
author: Andre
permalink: callstack-entenda-pilha-chamadas-javascript
date: 2019-06-01T10:00:00.000Z
tags:
  - 33 Conceitos
draft: false
---

A pilha de chamadas ( callstack ) é o mecanismo que os interpretadores de linguagens de programação utilizam para salvar as funções na memória do computador, de maneira que elas sejam executadas na ordem correta.

Este é o primeiro artigo da série 33 conceitos de JavaScript que todo desenvolvedor deveria conhecer, baseado [neste projeto](https://github.com/leonardomso/33-js-concepts).

---

## O que é a pilha de chamadas

A pilha de chamadas é maneira como o compilador do JavaScript organiza as múltiplas funções que serão executadas em um programa, sempre que uma função é chamada ela é adicionada ao topo da pilha e executada na ordem LIFO(Last In, First Out) que no português signifca último a chegar primeiro a sair, uma vez que a função é totalmente executada ele é removida da pilha e o código continua a ser executado de onde parou antes de chamar a função.

Se uma pilha de chamadas fica muito grande (isso acontece facilmente se fizer uma função recursiva errada.) o compilador gera o erro "stack overflow".

## Exemplos

```javascript
function bemVindo() {
  // [1]  Código executado antes da função digaOla
  digaOla();
  // [2] *Continua executando
}
function digaOla() {
  return 'Olá!';
}

// chama a função de `bemVindo`
bemVindo();

// [3]  Resto do programa
```

O código acima será executado na seguinte ordem:

1. Ignora tudo até chegar na chama da função bemVindo.
2. A Função bemVindo é adicionada a pilha de chamadas ordem.

   | Callstack |
   | --------- |
   | bemVindo  |

3. O código da função **bemVindo()** é executado até chegar a função **digaOla()**
4. A função **digaOla()** é adicionada a pilha de chamas

   | Callstack |
   | --------- |
   | digaOla   |
   | bemVindo  |

5. O Código da função **digaOla()** é executado até o fim
6. A função **digaOla()** é removida da pilha de chamadas.

   | Callstack |
   | --------- |
   | bemVindo  |

7. A funcão **bemVindo()** volta a ser executada apartir da linha de onde o programa tinha parado até fim.
8. A função **bemVindo()** é removida da pilhas chamadas.

   | Callstack |
   | --------- |
   | VAZIO     |

De maneira resumida começamos com uma pilha vazia, e as funções do programa são adicionadas a pilha de chamadas conforme elas são chamadas no código, a execução acontece na ordem LIFO ( Last In, First Out), ou seja a última função adiciona a pilha é sempre a primeira a ser executada.

![Gif da execução completa](img/callstack-js.gif)
Confira no GIF acima uma explicação mais visual da ordem em que o programa é executado.

### Referências

- Callstack - MDN web docs
  : https://developer.mozilla.org/en-US/docs/Glossary/Call_stack
- Understanding Javascript Function Executions — Call Stack, Event Loop , Tasks & more
  : https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec

Espero que esse artigo tenha te ajudo, e até a próxima.
