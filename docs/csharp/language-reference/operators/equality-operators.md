---
title: Operadores de igualdade - Referência de C#
description: Saiba mais sobre operadores de comparação de igualdade em C#.
ms.date: 03/28/2019
author: pkulikov
f1_keywords:
- ==_CSharpKeyword
- '!=_CSharpKeyword'
helpviewer_keywords:
- comparison operators [C#]
- relational operators [C#]
- equality operator [C#]
- equals operator [C#]
- == operator [C#]
- inequality operator [C#]
- not equals operator [C#]
- '!= operator [C#]'
ms.openlocfilehash: f60d62d1823a8bd06b0417638719a81e95d7438b
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67267692"
---
# <a name="equality-operators-c-reference"></a>Operadores de igualdade (Referência de C#)

Os operadores [`==` (igualdade)](#equality-operator-) e [`!=` (desigualdade)](#inequality-operator-) verificam se os operandos são iguais ou não.

## <a name="equality-operator-"></a>Operador de igualdade ==

O operador de igualdade `==` retornará `true` se seus operandos forem iguais; caso contrário, `false`.

### <a name="value-types-equality"></a>Igualdade de tipos de valor

Os operandos dos [tipos de valor internos](../keywords/value-types-table.md) serão iguais se seus valores forem iguais:

[!code-csharp-interactive[value types equality](~/samples/csharp/language-reference/operators/EqualityOperators.cs#ValueTypesEquality)]

> [!NOTE]
> Para os operadores `==`, [`<`, `>`, `<=` e `>=`](comparison-operators.md), se nenhum dos operandos for um número (<xref:System.Double.NaN?displayProperty=nameWithType> ou <xref:System.Single.NaN?displayProperty=nameWithType>), o resultado da operação será `false`. Isso significa que o valor `NaN` não é superior, inferior nem igual a nenhum outro valor `double` (ou `float`), incluindo `NaN`. Para obter mais informações e exemplos, consulte o artigo de referência <xref:System.Double.NaN?displayProperty=nameWithType> ou <xref:System.Single.NaN?displayProperty=nameWithType>.

Dois operandos do mesmo tipo de [enum](../keywords/enum.md) serão iguais se os valores correspondentes do tipo integral subjacente forem iguais.

Os tipos [struct](../keywords/struct.md) definidos pelo usuário não dão suporte ao operador `==`, por padrão. Para dar suporte ao operador `==`, um struct definido pelo usuário precisa [sobrecarregá-lo](#operator-overloadability).

A partir do C# 7.3, os operadores `==` e `!=` são compatíveis com as [tuplas](../../tuples.md) do C#. Para obter mais informações, consulte a seção [Igualdade e tuplas](../../tuples.md#equality-and-tuples) do artigo [Tipos de tupla do C#](../../tuples.md).

### <a name="string-equality"></a>Igualdade da cadeia de caracteres

Dois operandos da [cadeia de caracteres](../keywords/string.md) serão iguais quando ambos forem `null` ou ambas as instâncias da cadeia de caracteres tiverem o mesmo comprimento e caracteres idênticos em cada posição de caractere:

[!code-csharp-interactive[string equality](~/samples/csharp/language-reference/operators/EqualityOperators.cs#StringEquality)]

Essa é uma comparação ordinal que diferencia maiúsculas de minúsculas. Para obter mais informações sobre a comparação de cadeias de caracteres, confira [Como comparar cadeias de caracteres no C#](../../how-to/compare-strings.md).

### <a name="reference-types-equality"></a>Igualdade de tipos de referência

Dois operandos de um tipo de referência diferente de `string` serão iguais quando eles se referirem ao mesmo objeto:

[!code-csharp[reference type equality](~/samples/csharp/language-reference/operators/EqualityOperators.cs#ReferenceTypesEquality)]

Como mostra o exemplo, os tipos de referência definidos pelo usuário dão suporte ao operador `==`, por padrão. No entanto, um tipo de referência definido pelo usuário pode sobrecarregar o operador `==`. Se um tipo de referência sobrecarregar o operador `==`, use o método <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> para verificar se as duas referências desse tipo dizem respeito ao mesmo objeto.

## <a name="inequality-operator-"></a>Operador de desigualdade !=

O operador de desigualdade `!=` retornará `true` se seus operandos não forem iguais; caso contrário, `false`. No caso dos operandos de [tipos internos](../keywords/built-in-types-table.md), a expressão `x != y` gera o mesmo resultado que a expressão `!(x == y)`. Para obter mais informações sobre a igualdade de tipos, confira a seção [Operador de igualdade](#equality-operator-).

O exemplo a seguir demonstra o uso do operador `!=`:

[!code-csharp-interactive[non-equality examples](~/samples/csharp/language-reference/operators/EqualityOperators.cs#NonEquality)]

## <a name="operator-overloadability"></a>Capacidade de sobrecarga do operador

Os tipos definidos pelo usuário podem [sobrecarregar](../keywords/operator.md) os operadores `==` e `!=`. Se um tipo sobrecarregar um dos dois operadores, ele também precisará sobrecarregar o outro.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte a seção [Operadores de teste de tipo e relacional](~/_csharplang/spec/expressions.md#relational-and-type-testing-operators) na [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Operadores do C#](index.md)
- <xref:System.IEquatable%601?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>
- [Comparações de igualdade](../../programming-guide/statements-expressions-operators/equality-comparisons.md)
- [Operadores de comparação](comparison-operators.md)
