---
title: Operador => – referência do C#
ms.custom: seodec18
ms.date: 01/22/2019
f1_keywords:
- =>_CSharpKeyword
helpviewer_keywords:
- lambda operator [C#]
- => operator [C#]
- lambda expressions [C#], => operator
ms.openlocfilehash: a7fea9810cb02269278638ec71cd106463b029e9
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025018"
---
# <a name="-operator-c-reference"></a>Operador => (referência do C#)

Há suporte para o token `=>` de duas formas: como o operador lambda e como um separador de um nome de membro e a implementação de membro em uma definição de corpo da expressão.

## <a name="lambda-operator"></a>Operador lambda

Em [expressões lambda](../../programming-guide/statements-expressions-operators/lambda-expressions.md), o operador lambda `=>` separa as variáveis de entrada no lado esquerdo do corpo lambda no lado direito.

O seguinte exemplo usa o recurso [LINQ](../../programming-guide/concepts/linq/index.md) com a sintaxe de método para demonstrar o uso de expressões lambda:

[!code-csharp-interactive[infer types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#InferredTypes)]

As variáveis de entrada de expressões lambda são fortemente tipadas no tempo de compilação. Quando o compilador pode inferir os tipos de variáveis de entrada, como no exemplo anterior, você pode omitir as declarações de tipo. Caso precise especificar o tipo de variáveis de entrada, faça isso para cada variável, como mostra o seguinte exemplo:

[!code-csharp-interactive[specify types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#ExplicitTypes)]

O seguinte exemplo mostra como definir uma expressão lambda sem variáveis de entrada:

[!code-csharp-interactive[without input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#WithoutInput)]

Para obter mais informações, confira [Expressões lambda](../../programming-guide/statements-expressions-operators/lambda-expressions.md).

## <a name="expression-body-definition"></a>Definição de corpo da expressão

Uma definição de corpo da expressão tem a seguinte sintaxe geral:

```csharp
member => expression;
```

em que *expression* é uma expressão válida. Observe que *expression* pode ser uma *expressão de instrução* apenas se o tipo de retorno do membro é `void` ou se o membro é um construtor, um finalizador ou um acessador `set` de propriedade.

O seguinte exemplo mostra uma definição de corpo da expressão para um método `Person.ToString`:

```csharp
public override string ToString() => $"{fname} {lname}".Trim();
```

É uma versão abreviada da seguinte definição de método:

```csharp
public override string ToString()
{
   return $"{fname} {lname}".Trim();
}
```

Há suporte para definições de corpo da expressão em métodos e propriedades somente leitura do C# 6 em diante. Há suporte para definições de corpo da expressão em construtores, finalizadores, acessadores de propriedade e indexadores do C# 7.0 em diante.

Para obter mais informações, consulte [Membros aptos para expressão](../../programming-guide/statements-expressions-operators/expression-bodied-members.md).

## <a name="operator-overloadability"></a>Capacidade de sobrecarga do operador

O operador `=>` não pode ser sobrecarregado.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira a seção [Expressões de função anônima](~/_csharplang/spec/expressions.md#anonymous-function-expressions) da [Especificação da linguagem C#](../language-specification/index.md).

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Operadores do C#](index.md)
- [Expressões lambda](../../programming-guide/statements-expressions-operators/lambda-expressions.md)
- [Membros de expressão incorporada](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)
