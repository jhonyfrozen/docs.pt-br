---
title: Instrução lock – Referência em C#
ms.custom: seodec18
description: Use a instrução lock do C# para sincronizar o acesso de thread com um recurso compartilhado
ms.date: 10/01/2018
f1_keywords:
- lock_CSharpKeyword
- lock
helpviewer_keywords:
- lock keyword [C#]
ms.assetid: 656da1a4-707e-4ef6-9c6e-6d13b646af42
ms.openlocfilehash: c7d5d4ef7d812e186813cd08f9e4e2adf2ab1a58
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67306651"
---
# <a name="lock-statement-c-reference"></a>Instrução lock (referência em C#)

A instrução `lock` obtém o bloqueio de exclusão mútua para um determinado objeto, executa um bloco de instruções e, em seguida, libera o bloqueio. Embora um bloqueio seja mantido, o thread que mantém o bloqueio pode adquiri-lo novamente e liberá-lo. Qualquer outro thread é impedido de adquirir o bloqueio e aguarda até que ele seja liberado.

A instrução `lock` está no formato

```csharp
lock (x)
{
    // Your code...
}
```

em que `x` é uma expressão de um [tipo de referência](reference-types.md). Ela é precisamente equivalente a

```csharp
object __lockObj = x;
bool __lockWasTaken = false;
try
{
    System.Threading.Monitor.Enter(__lockObj, ref __lockWasTaken);
    // Your code...
}
finally
{
    if (__lockWasTaken) System.Threading.Monitor.Exit(__lockObj);
}
```

Como o código usa um bloco [try...finally](try-finally.md), o bloqueio será liberado mesmo se uma exceção for gerada dentro do corpo de uma instrução `lock`.

Não é possível usar a palavra-chave [await](await.md) no corpo de uma instrução `lock`.

## <a name="remarks"></a>Comentários

Ao sincronizar o acesso de thread com um recurso compartilhado, bloqueie uma instância de objeto dedicada (por exemplo, `private readonly object balanceLock = new object();`) ou outra instância que provavelmente não será usada como um objeto de bloqueio por partes não relacionadas do código. Evite usar a mesma instância de objeto de bloqueio para diferentes recursos compartilhados, uma vez que ela poderia resultar em deadlock ou contenção de bloqueio. Especificamente, evite usar os seguintes itens como objetos de bloqueio:

- `this`, uma vez que pode ser usado pelos chamadores como um bloqueio.
- Instâncias <xref:System.Type>, pois podem ser obtidas pelo operador ou reflexão [typeof](../operators/type-testing-and-conversion-operators.md#typeof-operator).
- Instâncias de cadeia de caracteres, incluindo literais de cadeia de caracteres, pois podem ser [internalizadas](/dotnet/api/system.string.intern#remarks).

## <a name="example"></a>Exemplo

O exemplo a seguir define uma classe `Account` que sincroniza o acesso com seu campo privado `balance` bloqueando uma instância `balanceLock` dedicada. Usar a mesma instância para bloquear garante que o campo `balance` não pode ser atualizado simultaneamente por dois threads que tentam chamar os métodos `Debit` ou `Credit` simultaneamente.

[!code-csharp[lock-statement-example](~/samples/snippets/csharp/keywords/LockStatementExample.cs)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.SpinLock?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [Referência de C#](../index.md)
- [Palavras-chave do C#](index.md)
- [Palavras-chave de instrução](statement-keywords.md)
- [Visão geral dos primitivos de sincronização](../../../standard/threading/overview-of-synchronization-primitives.md)
