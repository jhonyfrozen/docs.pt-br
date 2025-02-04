---
title: Instrução fixed – Referência de C#
ms.custom: seodec18
ms.date: 05/10/2018
f1_keywords:
- fixed_CSharpKeyword
- fixed
helpviewer_keywords:
- fixed keyword [C#]
ms.openlocfilehash: 88e2b93fda786db15b3a3a693bdb9293ed31df4c
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833214"
---
# <a name="fixed-statement-c-reference"></a>Instrução fixed (Referência de C#)

A instrução `fixed` impede que o coletor de lixo faça a realocação de uma variável móvel. A instrução `fixed` é permitida somente em um contexto [não seguro](unsafe.md). Você também pode usar a palavra-chave `fixed` para criar [buffers de tamanho fixo](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md).

A instrução `fixed` define um ponteiro para uma variável gerenciada e "fixa" essa variável durante a execução da instrução. Os ponteiros móveis gerenciados são úteis apenas em um contexto `fixed`. Sem um contexto `fixed`, a coleta de lixo poderia realocar as variáveis de forma imprevisível. O compilador do C# só permite que você atribua um ponteiro a uma variável gerenciada em uma instrução `fixed`.

[!code-csharp[Accessing fixed memory](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#1)]

Você pode inicializar um ponteiro usando uma matriz, uma cadeia de caracteres, um buffer de tamanho fixo ou o endereço de uma variável. O exemplo a seguir ilustra o uso de endereços de variáveis, matrizes e sequências de caracteres:

[!code-csharp[Initializing fixed size buffers](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#2)]

Começando com o C# 7.3, a instrução `fixed` opera em tipos adicionais além de cadeias de caracteres, matrizes, buffers de tamanho fixo ou variáveis não gerenciadas. Qualquer tipo que implementa um método chamado `GetPinnableReference` pode ser anexado. O `GetPinnableReference` deve retornar uma variável `ref` para um tipo não gerenciado. Consulte o tópico sobre [tipos de ponteiro](../../programming-guide/unsafe-code-pointers/pointer-types.md) para obter mais informações. Os tipos .NET <xref:System.Span%601?displayProperty=nameWithType> e <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> introduzidos no .NET Core 2.0 usam esse padrão e podem ser anexados. Isso é mostrado no exemplo a seguir:

[!code-csharp[Accessing fixed memory](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#FixedSpan)]

Se você estiver criando tipos que devem participar desse padrão, consulte <xref:System.Span%601.GetPinnableReference?displayProperty=nameWithType> para obter um exemplo da implementação do padrão.

Vários ponteiros podem ser inicializados em uma instrução quando eles são do mesmo tipo:

```csharp
fixed (byte* ps = srcarray, pd = dstarray) {...}
```

Para inicializar ponteiros de tipos diferentes, basta aninhar instruções `fixed`, conforme mostrado no exemplo a seguir.

[!code-csharp[Initializing multiple pointers](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#3)]

Depois que o código na instrução é executado, todas as variáveis fixadas são desafixadas e ficam sujeiras à coleta de lixo. Portanto, não aponte para essas variáveis fora da instrução `fixed`. As variáveis declaradas na instrução `fixed` estão no escopo dessa instrução, facilitando isto:

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
   ...
}
// ps and pd are no longer in scope here.
```

Os ponteiros inicializados em instruções `fixed` são variáveis somente leitura. Se você quiser modificar o valor do ponteiro, será necessário declarar uma segunda variável de ponteiro e modificá-la. A variável declarada na instrução `fixed` não pode ser modificada:

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
    byte* pSourceCopy = ps;
    pSourceCopy++; // point to the next element.
    ps++; // invalid: cannot modify ps, as it is declared in the fixed statement.
}
```

É possível alocar memória na pilha, local que não está sujeito à coleta de lixo e, portanto, não precisa ser fixado. Para fazer isso, use o [operador `stackalloc`](../operators/stackalloc.md).

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para saber mais, confira a seção [A instrução corrigida](~/_csharplang/spec/unsafe-code.md#the-fixed-statement) na [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
- [unsafe](unsafe.md)
- [Buffers de tamanho fixo](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)
