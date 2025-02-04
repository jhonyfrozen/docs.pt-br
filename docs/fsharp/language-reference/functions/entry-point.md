---
title: Ponto de entrada
description: Saiba como configurar o ponto de entrada um F# programa é compilado como um arquivo executável, onde a execução começa formalmente.
ms.date: 05/16/2016
ms.openlocfilehash: c7aedda5834fb224507bfcecd4688978efa26547
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645446"
---
# <a name="entry-point"></a>Ponto de entrada

Este tópico descreve o método que você use para definir o ponto de entrada para um F# programa.

## <a name="syntax"></a>Sintaxe

```fsharp
[<EntryPoint>]
let-function-binding
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, *associação de função permitem* é a definição de uma função em um `let` associação.

O ponto de entrada para um programa que é compilado como um arquivo executável é onde a execução começa formalmente. Especifique o ponto de entrada para um F# aplicativo aplicando a `EntryPoint` atributo para o programa `main` função. Essa função (criado usando um `let` associação) deve ser a última função no último arquivo compilado. O último arquivo compilado é o último arquivo no projeto ou o último arquivo que é passado para a linha de comando.

A função de ponto de entrada tem tipo `string array -> int`. Os argumentos fornecidos na linha de comando são passados para o `main` função na matriz de cadeias de caracteres. O primeiro elemento da matriz é o primeiro argumento; o nome do arquivo executável não está incluído na matriz, como ele está em outras linguagens. O valor de retorno é usado como o código de saída para o processo. Zero geralmente indica sucesso. valores diferentes de zero indicam um erro. Não há nenhum convenção para o significado específico de códigos de retorno diferente de zero; os significados dos códigos de retorno são específicas do aplicativo.

O exemplo a seguir ilustra um simples `main` função.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/entry-point/snippet501.fs)]

Quando esse código é executado com a linha de comando `EntryPoint.exe 1 2 3`, a saída é da seguinte maneira.

```console
Arguments passed to function : [|"1"; "2"; "3"|]
```

## <a name="implicit-entry-point"></a>Ponto de entrada implícito

Quando um programa não tem nenhum **EntryPoint** atributo que indica explicitamente o ponto de entrada, as associações de nível superior no último arquivo a ser compilado são usados como ponto de entrada.

## <a name="see-also"></a>Consulte também

- [Funções](index.md)
- [Associações let](let-bindings.md)
