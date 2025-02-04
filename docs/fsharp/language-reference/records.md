---
title: Registros
description: Saiba como F# registros representam agregações simples de valores nomeados, opcionalmente com membros.
ms.date: 06/09/2019
ms.openlocfilehash: cfb8de8272b479571119ae4cf91ea1d6fd5db73c
ms.sourcegitcommit: 5ae6affa0b171be3bb5f4729fb68ea4fe799f959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66816198"
---
# <a name="records"></a>Registros

Registros representam agregações simples de valores nomeados, opcionalmente com membros. Eles podem ser structs ou tipos de referência.  Eles são tipos de referência por padrão.

## <a name="syntax"></a>Sintaxe

```fsharp
[ attributes ]
type [accessibility-modifier] typename =
    { [ mutable ] label1 : type1;
      [ mutable ] label2 : type2;
      ... }
    [ member-list ]
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, *typename* é o nome do tipo de registro, *label1* e *label2* são nomes de valores, conhecidos como *rótulos*, e *type1* e *type2* são os tipos desses valores. *lista de membros* é a lista opcional de membros para o tipo.  Você pode usar o `[<Struct>]` atributo para criar um registro de struct em vez de um registro que é um tipo de referência.

A seguir estão alguns exemplos.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1901.fs)]

Quando cada rótulo está em uma linha separada, o ponto e vírgula é opcional.

Você pode definir valores em expressões, conhecidas como *gravar expressões*. O compilador infere o tipo dos rótulos usados (se os rótulos são suficientemente diferentes de outros tipos de registro). Chaves ({}) coloque a expressão de registro. O código a seguir mostra uma expressão de registro que inicializa um registro com três elementos de flutuante com rótulos `x`, `y` e `z`.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1907.fs)]

Não use a forma abreviada se pode haver outro tipo que também tem os mesmos rótulos.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1903.fs)]

Os rótulos do tipo declarado mais recentemente têm precedência sobre aquelas do tipo declarado anteriormente, portanto, no exemplo anterior, `mypoint3D` será inferida para ser `Point3D`. Você pode especificar explicitamente o tipo de registro, como no código a seguir.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1908.fs)]

Métodos podem ser definidos para tipos de registro, como acontece com tipos de classe.

## <a name="creating-records-by-using-record-expressions"></a>Criação de registros usando expressões de registro

Você pode inicializar os registros usando os rótulos que são definidos no registro. Uma expressão que faz isso é conhecida como um *registre expressão*. Use chaves para coloque a expressão de registro e o ponto e vírgula como delimitador.

O exemplo a seguir mostra como criar um registro.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1904.fs)]

A ponto e vírgula após o último campo na expressão do registro e na definição de tipo é opcional, independentemente se os campos são tudo em uma linha.

Quando você cria um registro, você deve fornecer valores para cada campo. Você não pode referenciar os valores dos outros campos na expressão de inicialização para qualquer campo.

No código a seguir, o tipo de `myRecord2` é inferido dos nomes dos campos. Opcionalmente, você pode especificar explicitamente o nome do tipo.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

Outra forma de construção de registro pode ser útil quando você tem que copiar um registro existente e, possivelmente, alterar alguns dos valores de campo. A linha de código a seguir ilustra isso.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

Essa forma da expressão de registro é chamada de *copiar e atualizar registro expressão*.

Registros são imutáveis por padrão. No entanto, você pode criar facilmente os registros modificados usando uma expressão de copiar e atualizar. Você também pode especificar explicitamente um campo mutável.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1909.fs)]

Não use o atributo DefaultValue com campos de registro. Uma abordagem melhor é definir instâncias padrão dos registros com campos que são inicializados para valores padrão e, em seguida, usar uma cópia e atualizar o registro de expressão para definir todos os campos que são diferentes dos valores padrão.

```fsharp
// Rather than use [<DefaultValue>], define a default record.
type MyRecord =
    { Field1 : int
      Field2 : int }

let defaultRecord1 = { Field1 = 0; Field2 = 0 }
let defaultRecord2 = { Field1 = 1; Field2 = 25 }

// Use the with keyword to populate only a few chosen fields
// and leave the rest with default values.
let rr3 = { defaultRecord1 with Field2 = 42 }
```

## <a name="creating-mutually-recursive-records"></a>Criando mutuamente recursivas registros

Em algum momento durante a criação de um registro, você talvez queira fazer com que ele depende de outro tipo que você deseja definir posteriormente. Esse é um erro de compilação, a menos que você defina os tipos de registro para ser mutuamente recursivas.

Definir mutuamente recursivas registros é feito com o `and` palavra-chave. Isso lhe permite vincular 2 ou mais registros de tipos.

Por exemplo, o código a seguir define uma `Person` e `Address` tipo como mutuamente recursivas:

```fsharp
// Create a Person type and use the Address type that is not defined
type Person =
  { Name: string
    Age: int
    Address: Address }
// Define the Address type which is used in the Person record
and Address =
  { Line1: string
    Line2: string
    PostCode: string }
```

Se você definir o exemplo anterior sem o `and` palavra-chave, em seguida, ele não seria compilado. O `and` palavra-chave é necessária para mutuamente recursivas definições.

## <a name="pattern-matching-with-records"></a>Correspondência de padrões com registros

Registros podem ser usados com correspondência de padrões. Você pode especificar explicitamente o alguns campos e fornecer variáveis para os outros campos que serão atribuídos quando ocorrer uma correspondência. O exemplo de código a seguir ilustra isso.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1910.fs)]

A saída desse código é da seguinte maneira.

```
Point is at the origin.
Point is on the x-axis. Value is 100.000000.
Point is at (10.000000, 0.000000, -1.000000).
```

## <a name="differences-between-records-and-classes"></a>Diferenças entre Classes e registros

Campos de registro são diferentes das classes em que elas são expostas como propriedades automaticamente e eles são usados na criação e cópia de registros. Construção de registro também é diferente da construção de classe. Em um tipo de registro, você não pode definir um construtor. Em vez disso, a sintaxe de construção descrita neste tópico se aplica. Classes não têm nenhuma relação direta entre os parâmetros do construtor, campos e propriedades.

Como os tipos de união e estrutura, os registros têm semântica de igualdade estrutural. As classes têm referência semântica de igualdade. O código de exemplo a seguir demonstra isso.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1911.fs)]

A saída desse código é da seguinte maneira:

```
The records are equal.
```

Se você escrever o mesmo código com classes, os objetos de duas classe seriam desiguais porque os dois valores seriam representam dois objetos no heap e somente os endereços devem ser comparados (a menos que o tipo de classe substitui o `System.Object.Equals` método).

Se você precisa referenciar igualdade para registros, adicione o atributo `[<ReferenceEquality>]` acima do registro.

## <a name="see-also"></a>Consulte também

- [Tipos F#](fsharp-types.md)
- [Classes](classes.md)
- [Referência da Linguagem F#](index.md)
- [Igualdade de referência](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.referenceequalityattribute-class-%5bfsharp%5d)
- [Correspondência Padrão](pattern-matching.md)
