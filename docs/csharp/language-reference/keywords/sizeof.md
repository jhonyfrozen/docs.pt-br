---
title: sizeof – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: a00c4f96e62f7fd7d7c352aece097acd5b600ae2
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66422404"
---
# <a name="sizeof-c-reference"></a>sizeof (Referência de C#)

Usado para obter o tamanho, em bytes, de um tipo não gerenciado.

Os tipos não gerenciados incluem:

- Os tipos simples que são listados na tabela a seguir:

   |Expressão|Valor constante|
   |----------------|--------------------|
   |`sizeof(sbyte)`|1|
   |`sizeof(byte)`|1|
   |`sizeof(short)`|2|
   |`sizeof(ushort)`|2|
   |`sizeof(int)`|4|
   |`sizeof(uint)`|4|
   |`sizeof(long)`|8|
   |`sizeof(ulong)`|8|
   |`sizeof(char)`|2 (Unicode)|
   |`sizeof(float)`|4|
   |`sizeof(double)`|8|
   |`sizeof(decimal)`|16|
   |`sizeof(bool)`|1|

- Tipos enumerados.

- Tipos de ponteiro.

- Os structs definidos pelo usuário que não contêm campos de instância ou propriedades de instância autoimplementadas que são tipos de referência ou tipos construídos.

O exemplo a seguir mostra como recuperar o tamanho de um `int`:

```csharp
// Constant value 4:
int intSize = sizeof(int);
```

## <a name="remarks"></a>Comentários

A partir da versão 2.0 do C#, aplicar `sizeof` a tipos simples ou enumerados não exige mais que o código seja compilado em um contexto [não seguro](unsafe.md).

O operador `sizeof` não pode ser sobrecarregado. Os valores retornados pelo operador `sizeof` são do tipo `int`. A tabela anterior mostra os valores constantes que são substituídos por expressões `sizeof` que têm determinados tipos simples como operandos.

Para todos os outros tipos, incluindo structs, o operador `sizeof` pode ser usado somente em blocos de código não seguro. Embora você possa usar o método <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType>, o valor retornado por esse método não é sempre o mesmo que o valor retornado por `sizeof`. <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> retorna o tamanho após o tipo ter passado por marshaling, enquanto `sizeof` retorna o tamanho como ele foi alocado pelo Common Language Runtime, incluindo qualquer preenchimento.

## <a name="example"></a>Exemplo

[!code-csharp[csrefKeywordsOperator#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#11)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
- [enum](enum.md)
- [Código não seguro e ponteiros](../../programming-guide/unsafe-code-pointers/index.md)
- [Estruturas](../../programming-guide/classes-and-structs/structs.md)
- [Constantes](../../programming-guide/classes-and-structs/constants.md)
