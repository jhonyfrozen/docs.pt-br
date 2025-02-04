---
title: Palavra-chave double – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- double
- double_CSharpKeyword
helpviewer_keywords:
- double data type [C#]
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
ms.openlocfilehash: f4d6bb4eb698e4afbda6571ba382e828a5f836a4
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424269"
---
# <a name="double-c-reference"></a>double (Referência de C#)

A palavra-chave `double` indica um tipo simples que armazena valores de ponto flutuante de 64 bits. A tabela a seguir mostra a precisão e o intervalo aproximado do tipo `double`.

|Tipo|Intervalo aproximado|Precisão|Tipo .NET|
|----------|-----------------------|---------------|-------------------------|
|`double`|±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup>|Aproximadamente de 15 a 17 dígitos|<xref:System.Double?displayProperty=nameWithType>|

## <a name="literals"></a>Literais

Por padrão, um literal numérico real no lado direito do operador de atribuição é tratado como `double`. No entanto, se você quiser que um número inteiro seja tratado como `double`, use o sufixo d ou D, por exemplo:

```csharp
double x = 3D;
```

## <a name="conversions"></a>Conversões

Você pode misturar tipos integrais numéricos e tipos de ponto flutuante em uma expressão. Nesse caso, os tipos integrais são convertidos em tipos de ponto flutuante. A avaliação da expressão é executada de acordo com as regras a seguir:

- Se um dos tipos de ponto flutuante for `double`, a expressão será avaliada como `double` ou [bool](../../../csharp/language-reference/keywords/bool.md) em comparações relacionais e de igualdade.

- Se não houver um tipo `double` na expressão, ela será avaliada como [float](../../../csharp/language-reference/keywords/float.md) ou [bool](../../../csharp/language-reference/keywords/bool.md) em comparações relacionais e de igualdade.

 Uma expressão de ponto flutuante pode conter os seguintes conjuntos de valores:

- Zero positivo e negativo.

- Infinito positivo e negativo.

- Valor diferente de um número (NaN).

- O conjunto finito de valores diferentes de zero.

Para obter mais informações sobre esses valores, consulte o padrão IEEE para Aritmética de ponto flutuante binário, disponível no site do [IEEE](https://www.ieee.org).

## <a name="example"></a>Exemplo

No exemplo a seguir, um [int](../builtin-types/integral-numeric-types.md), um [short](../../../csharp/language-reference/builtin-types/integral-numeric-types.md), um [float](../../../csharp/language-reference/keywords/float.md) e um `double` são adicionados, levando a um resultado `double`.

[!code-csharp[csrefKeywordsTypes#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#9)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência de C#](../../../csharp/language-reference/index.md)
- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [Palavras-chave do C#](../../../csharp/language-reference/keywords/index.md)
- [Tabela de valores padrão](../../../csharp/language-reference/keywords/default-values-table.md)
- [Tabela de tipos internos](../../../csharp/language-reference/keywords/built-in-types-table.md)
- [Tabela de tipos de ponto flutuante](../../../csharp/language-reference/keywords/floating-point-types-table.md)
- [Tabela de conversões numéricas implícitas](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)
- [Tabela de conversões numéricas explícitas](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
