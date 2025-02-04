---
title: 'Funções recursivas: A palavra-chave rec'
description: Saiba como o F# palavra-chave 'rec' é usado com a palavra-chave 'let' para definir uma função recursiva.
ms.date: 05/16/2016
ms.openlocfilehash: 86eaf1c8a5566d8b9cbc4dcb72f945e2497e5439
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645312"
---
# <a name="recursive-functions-the-rec-keyword"></a>Funções recursivas: A palavra-chave rec

O `rec` palavra-chave é usada junto com o `let` palavra-chave para definir uma função recursiva.

## <a name="syntax"></a>Sintaxe

```fsharp
// Recursive function:
let rec function-nameparameter-list =
function-body

// Mutually recursive functions:
let rec function1-nameparameter-list =
function1-body
and function2-nameparameter-list =
function2-body
...
```

## <a name="remarks"></a>Comentários

Funções recursivas, funções que chamam seu site, são identificadas explicitamente no F# idioma. Isso disponibiliza o identificador que está sendo definido no escopo da função.

O código a seguir ilustra uma função recursiva que calcula a *n*<sup>th</sup> número Fibonacci.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet4001.fs)]

> [!NOTE]
> Na prática, o código acima como esse é um desperdício de tempo do processador e memória porque ela envolve o recálculo dos valores computados anteriormente.

Métodos são implicitamente recursivos dentro do tipo; não é necessário adicionar o `rec` palavra-chave. Associações Let em classes não são implicitamente recursivos.

## <a name="mutually-recursive-functions"></a>Funções mutuamente recursivas

Às vezes, são funções *mutuamente recursivas*, que significa que chamadas formam um círculo, em que uma função chama outra que por sua vez chama o primeiro, com qualquer número de chamadas entre os dois. Você deve definir essas funções juntas em um `let` vinculação, usando o `and` palavra-chave para vinculá-los.

O exemplo a seguir mostra dois mutuamente funções recursivas.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet4002.fs)]

## <a name="see-also"></a>Consulte também

- [Funções](index.md)
