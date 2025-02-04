---
title: Parâmetros de tipo resolvidos estaticamente
description: Saiba como usar um F# parâmetro de tipo estaticamente resolvidos, o que é substituído por um tipo real em tempo de compilação em vez de em tempo de execução.
ms.date: 05/16/2016
ms.openlocfilehash: 337d4f40418ee76cb18397add27acba75f756091
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645253"
---
# <a name="statically-resolved-type-parameters"></a>Parâmetros de tipo resolvidos estaticamente

Um *parâmetro de tipo estaticamente resolvido* é um parâmetro de tipo que é substituído por um tipo real em tempo de compilação em vez de em tempo de execução. Eles são precedidos por um símbolo de acento circunflexo (^).

## <a name="syntax"></a>Sintaxe

```
ˆtype-parameter
```

## <a name="remarks"></a>Comentários

No F# linguagem, há dois tipos diferentes de parâmetros de tipo. O primeiro tipo é o parâmetro de tipo genérico padrão. Eles são indicados por um apóstrofo ('), como em `'T` e `'U`. Eles são equivalentes aos parâmetros de tipo genérico em outras linguagens do .NET Framework. O outro tipo é estaticamente resolvido e indicado por um símbolo de acento circunflexo, como em `^T` e `^U`.

Parâmetros de tipo estaticamente resolvidos são úteis principalmente em conjunto com restrições de membro, que são restrições que permitem que você especifique que um argumento de tipo deve ter um determinado membro ou membros para ser usado. Não há nenhuma maneira de criar esse tipo de restrição usando um parâmetro de tipo genérico normal.

A tabela a seguir resume as semelhanças e diferenças entre os dois tipos de parâmetros de tipo.

|Recurso|Genérico|Resolvidos estaticamente|
|-------|-------|-------------------|
|Sintaxe|`'T`, `'U`|`^T`, `^U`|
|Tempo de resolução|Tempo de execução|Tempo de compilação|
|Restrições de membro|Não pode ser usado com restrições de membro.|Pode ser usado com restrições de membro.|
|Geração de código|Um tipo (ou método) com parâmetros de tipo genéricos padrão resulta na geração de um único tipo genérico ou método.|Várias instanciações de tipos e métodos são geradas, uma para cada tipo que é necessária.|
|Use com tipos|Pode ser usada em tipos.|Não pode ser usada em tipos.|
|Use com funções embutidas|Nº Uma função embutida não pode ser parametrizada com um parâmetro de tipo genérico padrão.|Sim. Parâmetros de tipo estaticamente resolvidos não podem ser usados em funções ou métodos que não estejam embutidos.|

Muitos F# funções de biblioteca principal, principalmente operadores, resolveram estaticamente os parâmetros de tipo. Essas funções e operadores são embutidos e resultam na geração de código eficiente para cálculos numéricos.

Métodos embutidos e funções que usam operadores ou usam outras funções que resolveram estaticamente os parâmetros de tipo, também podem usar parâmetros de tipo estaticamente resolvidos. Muitas vezes, a inferência de tipo infere tais funções embutidas para parâmetros de tipo estaticamente resolvidos. O exemplo a seguir ilustra uma definição de operador que é inferida para ter um parâmetro de tipo estaticamente resolvidos.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet401.fs)]

O tipo resolvido de `(+@)` baseia-se no uso de ambos `(+)` e `(*)`, ambos fazem com que a inferência de tipo infira restrições de membros nos parâmetros de tipo estaticamente resolvidos. O tipo resolvido, como mostra a F# interpretador, é o seguinte.

```fsharp
^a -> ^c -> ^d
when (^a or ^b) : (static member ( + ) : ^a * ^b -> ^d) and
(^a or ^c) : (static member ( * ) : ^a * ^c -> ^b)
```

A saída é a seguinte.

```
2
1.500000
```

Começando com F# 4.1, você também pode especificar nomes de tipo concreto em assinaturas de parâmetro de tipo estaticamente resolvidos.  Nas versões anteriores da linguagem, o nome do tipo, na verdade, poderia ser inferido pelo compilador, mas, na verdade, não pôde ser especificado na assinatura.  Como de F# 4.1, você também pode especificar nomes de tipo concreto em assinaturas de parâmetro de tipo estaticamente resolvidos. Veja um exemplo:

```fsharp
let inline konst x _ = x

type CFunctor() = 
    static member inline fmap (f: ^a -> ^b, a: ^a list) = List.map f a
    static member inline fmap (f: ^a -> ^b, a: ^a option) =
        match a with
        | None -> None
        | Some x -> Some (f x)

    // default implementation of replace
    static member inline replace< ^a, ^b, ^c, ^d, ^e when ^a :> CFunctor and (^a or ^d): (static member fmap: (^b -> ^c) * ^d -> ^e) > (a, f) =
        ((^a or ^d) : (static member fmap : (^b -> ^c) * ^d -> ^e) (konst a, f))

    // call overridden replace if present
    static member inline replace< ^a, ^b, ^c when ^b: (static member replace: ^a * ^b -> ^c)>(a: ^a, f: ^b) =
        (^b : (static member replace: ^a * ^b -> ^c) (a, f))

let inline replace_instance< ^a, ^b, ^c, ^d when (^a or ^c): (static member replace: ^b * ^c -> ^d)> (a: ^b, f: ^c) =
        ((^a or ^c): (static member replace: ^b * ^c -> ^d) (a, f))

// Note the concrete type 'CFunctor' specified in the signature
let inline replace (a: ^a) (f: ^b): ^a0 when (CFunctor or  ^b): (static member replace: ^a *  ^b ->  ^a0) =
    replace_instance<CFunctor, _, _, _> (a, f)
```

## <a name="see-also"></a>Consulte também

- [Genéricos](index.md)
- [Inferência de Tipos](../type-inference.md)
- [Generalização Automática](automatic-generalization.md)
- [Restrições](constraints.md)
- [Funções Embutidas](../functions/inline-functions.md)
