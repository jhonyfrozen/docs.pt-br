---
title: Abreviações de tipo
description: Saiba mais sobre F# abreviações para dar um nome mais significativo de um tipo para facilitar a leitura do código de tipo.
ms.date: 05/16/2016
ms.openlocfilehash: 2930db1dcaa66741900bc91937aa1fd2f006c5f8
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641692"
---
# <a name="type-abbreviations"></a>Abreviações de tipo

Um *abreviação de tipo* é um alias ou nome alternativo para um tipo.

## <a name="syntax"></a>Sintaxe

```fsharp
type [accessibility-modifier] type-abbreviation = type-name
```

## <a name="remarks"></a>Comentários

Você pode usar as abreviações de tipo para fornecer um tipo de um nome mais significativo, para facilitar a leitura do código. Você também pode usá-los para criar um nome fácil de usar para um tipo que de outra forma inconveniente para gravar. Além disso, você pode usar as abreviações de tipo para torná-lo mais fácil de alterar um tipo subjacente, sem alterar o código que usa o tipo. A seguir é uma abreviação de tipo simples.

Acessibilidade de abreviações de tipo padrão é `public`.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2301.fs)]

Abreviações de tipo podem incluir parâmetros genéricos, como no código a seguir.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2302.fs)]

No código anterior, `Transform` é uma abreviação de tipo que representa uma função que aceita um único argumento de qualquer tipo e que retorna um único valor desse mesmo tipo.

Abreviações de tipo não são preservadas no código MSIL do .NET Framework. Portanto, quando você usa um F# assembly de outra linguagem do .NET Framework, você deve usar o nome do tipo subjacente para uma abreviação de tipo.

Abreviações de tipo também podem ser usadas em unidades de medida. Para obter mais informações, consulte [unidades de medida](units-of-measure.md).

## <a name="see-also"></a>Consulte também

- [Referência da Linguagem F#](index.md)
