---
title: where (restrição de tipo genérico) – Referência de C#
ms.custom: seodec18
ms.date: 04/12/2018
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 3982c97bc56b42237700343b2572d1bba930bbbd
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66422766"
---
# <a name="where-generic-type-constraint-c-reference"></a>where (restrição de tipo genérico) (Referência de C#)

A cláusula `where` em uma definição genérica especifica restrições sobre os tipos que são usados como argumentos para parâmetros de tipo em um tipo genérico, método, delegado ou função local. Restrições podem especificar interfaces, classes base ou exigir que um tipo genérico seja uma referência, valor ou tipo não gerenciado. Elas declaram funcionalidades que o argumento de tipo deve ter.

Por exemplo, você pode declarar uma classe genérica, `MyGenericClass`, de modo que o parâmetro de tipo `T` implementa a interface <xref:System.IComparable%601>:

[!code-csharp[using an interface constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#1)]

> [!NOTE]
> Para obter mais informações sobre a cláusula where em uma expressão de consulta, consulte [Cláusula where](where-clause.md).

A cláusula `where` também pode incluir uma restrição de classe base. A restrição de classe base declara que um tipo a ser usado como um argumento de tipo para aquele tipo genérico tem a classe especificada como uma classe base (ou é que a classe base) a ser usada como um argumento de tipo para aquele tipo genérico. Se a restrição de classe base for usada, ela deverá aparecer antes de qualquer outra restrição nesse parâmetro de tipo. Alguns tipos não têm permissão como uma restrição de classe base: <xref:System.Object>, <xref:System.Array> e <xref:System.ValueType>. Antes do C# 7.3, <xref:System.Enum>, <xref:System.Delegate> e <xref:System.MulticastDelegate> também não tinham permissão como restrições de classe base. O exemplo a seguir mostra os tipos que agora podem ser especificados como classe base:

[!code-csharp[using an interface constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#2)]

A cláusula `where` pode especificar que o tipo é um `class` ou um `struct`. A restrição `struct` elimina a necessidade de especificar uma restrição de classe base de `System.ValueType`. O tipo `System.ValueType` não pode ser usado como uma restrição de classe base. O exemplo a seguir mostra as restrições `class` e `struct`:

[!code-csharp[using the class and struct constraints](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#3)]

A cláusula `where` também pode incluir uma restrição `unmanaged`. A restrição `unmanaged` limita o parâmetro de tipo a tipos conhecidos como **tipos não gerenciados**. Um **tipo não gerenciado** é um tipo que não é um tipo de referência e não contém campos de tipo de referência em nenhum nível de aninhamento. Usando a restrição `unmanaged`, é mais fácil escrever o código de interoperabilidade de nível baixo em C#. Essa restrição habilita rotinas reutilizáveis em todos os tipos não gerenciados. A restrição `unmanaged` não pode ser combinada à restrição `class` ou `struct`. A restrição `unmanaged` impõe que o tipo deve ser um `struct`:

[!code-csharp[using the unmanaged constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#4)]

A cláusula `where` também pode incluir uma restrição de construtor, `new()`. Essa restrição torna possível criar uma instância de um parâmetro de tipo usando o operador `new`. A [restrição new()](new-constraint.md) informa o compilador que qualquer argumento de tipo fornecido deve ter um construtor – ou padrão – sem parâmetros acessível. Por exemplo:

[!code-csharp[using the new constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#5)]

A restrição `new()` aparece por último na cláusula `where`. A restrição `new()` não pode ser combinada às restrições `struct` ou `unmanaged`. Todos os tipos que satisfazem as restrições devem ter um construtor sem parâmetros acessível, tornando a restrição `new()` redundante.

Com vários parâmetros de tipo, use uma cláusula `where` para cada parâmetro de tipo, por exemplo:

[!code-csharp[using multiple where constraints](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#6)]

Você também pode anexar restrições a parâmetros de tipo de métodos genéricos, como mostrado no exemplo a seguir:

[!code-csharp[where constraints with generic methods](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#7)]

Observe que a sintaxe para descrever as restrições de parâmetro de tipo em delegados é a mesma que a dos métodos:

[!code-csharp[where constraints with generic methods](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#8)]

Para obter informações sobre delegados genéricos, consulte [Delegados genéricos](../../../csharp/programming-guide/generics/generic-delegates.md).

Para obter detalhes sobre a sintaxe e o uso de restrições, consulte [Restrições a parâmetros de tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md).

## <a name="c-language-specification"></a>Especificação da linguagem C#

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência de C#](../../../csharp/language-reference/index.md)
- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [Introdução aos genéricos](../../../csharp/programming-guide/generics/index.md)
- [Restrição new](../../../csharp/language-reference/keywords/new-constraint.md)
- [Restrições a parâmetros de tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)
