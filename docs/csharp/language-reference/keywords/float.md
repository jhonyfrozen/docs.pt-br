---
title: Palavra-chave float – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- float
- float_CSharpKeyword
helpviewer_keywords:
- float keyword [C#]
- floating-point numbers [C#], float keyword
ms.assetid: 1e77db7b-dedb-48b7-8dd1-b055e96a9258
ms.openlocfilehash: db0139f2000c1bc2c5a13a3a542164201e73f0fb
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424217"
---
# <a name="float-c-reference"></a>float (Referência de C#)

A palavra-chave `float` indica um tipo simples que armazena valores de ponto flutuante de 32 bits. A tabela a seguir mostra a precisão e o intervalo aproximado do tipo `float`.

|Tipo|Intervalo aproximado|Precisão|Tipo .NET|  
|----------|-----------------------|---------------|-------------------------|  
|`float`|±1,5 x 10<sup>−45</sup> para ±3,4 x 10<sup>38</sup>|Aproximadamente de 6 a 9 dígitos|<xref:System.Single?displayProperty=nameWithType>|  

## <a name="literals"></a>Literais

Por padrão, um literal numérico real no lado direito do operador de atribuição é tratado como [double](double.md). Portanto, para inicializar uma variável float, use o sufixo `f` ou `F`, como no exemplo a seguir:

```csharp
float x = 3.5F;
```

Se você não usar o sufixo na declaração anterior, obterá um erro de compilação porque está tentando armazenar um valor [double](double.md) em uma variável `float`.

## <a name="conversions"></a>Conversões

Você pode misturar tipos integrais numéricos e tipos de ponto flutuante em uma expressão. Nesse caso, os tipos integrais são convertidos em tipos de ponto flutuante. A avaliação da expressão é executada de acordo com as regras a seguir:

- Se um dos tipos de ponto flutuante for [duplo](double.md), a expressão será avaliada como [double](double.md) ou [booliana](bool.md) em comparações relacionais ou de igualdade.

- Se não houver nenhum tipo [double](double.md) na expressão, a expressão será avaliada como `float` ou como [booliana](bool.md) em comparações relacionais ou de igualdade.

Uma expressão de ponto flutuante pode conter os seguintes conjuntos de valores:

- Zero positivo e negativo

- Infinito positivo e negativo

- Valor NaN (não é um número)

- O conjunto finito de valores diferentes de zero

Para obter mais informações sobre esses valores, consulte o padrão IEEE para Aritmética de ponto flutuante binário, disponível no site do [IEEE](https://www.ieee.org).

## <a name="example"></a>Exemplo

No exemplo a seguir, um [int](../builtin-types/integral-numeric-types.md), um [short](../builtin-types/integral-numeric-types.md) e um `float` são incluídos em uma expressão matemática dando um resultado `float`. (Lembre-se de que `float` é um alias para o tipo <xref:System.Single?displayProperty=nameWithType>.) Observe que não há nenhum [double](double.md) na expressão.

[!code-csharp[csrefKeywordsTypes#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#13)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- <xref:System.Single>
- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Transmissões e conversões de tipo](../../programming-guide/types/casting-and-type-conversions.md)
- [Palavras-chave do C#](index.md)
- [Tipos integrais](../../../csharp/language-reference/builtin-types/integral-numeric-types.md)
- [Tabela de tipos internos](built-in-types-table.md)
- [Tabela de conversões numéricas implícitas](implicit-numeric-conversions-table.md)
- [Tabela de conversões numéricas explícitas](explicit-numeric-conversions-table.md)
