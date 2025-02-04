---
title: Atributos
description: Saiba como F# os atributos permitem que os metadados a ser aplicado a um constructo de programação.
ms.date: 05/16/2016
ms.openlocfilehash: fed4c549b95d6d3701ab81cf5d62add411c16038
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642021"
---
# <a name="attributes"></a>Atributos

Atributos permitem os metadados a ser aplicado a um constructo de programação.

## <a name="syntax"></a>Sintaxe

```fsharp
[<target:attribute-name(arguments)>]
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, o *destino* é opcional e, se presente, especifica o tipo de entidade de programa que o atributo se aplica a. Os valores válidos para *destino* são mostrados na tabela que aparece mais adiante neste documento.

O *nome do atributo* refere-se ao nome (possivelmente qualificado com namespaces) de um tipo de atributo válido, com ou sem o sufixo `Attribute` que geralmente é usado em nomes de tipo de atributo. Por exemplo, o tipo `ObsoleteAttribute` pode ser reduzido para apenas `Obsolete` neste contexto.

O *argumentos* são os argumentos para o construtor para o tipo de atributo. Se um atributo tem um construtor padrão, a lista de argumentos e os parênteses podem ser omitidos. Suportam a atributos argumentos posicionais e argumentos nomeados. *Argumentos posicionais* são argumentos que são usados na ordem em que aparecem. Argumentos nomeados podem ser usados se o atributo tem propriedades públicas. Você pode definir esses itens usando a sintaxe a seguir na lista de argumentos.

```
*property-name* = *property-value*
```

Essas inicializações de propriedade podem estar em qualquer ordem, mas eles devem seguir argumentos posicionais. A seguir está um exemplo de um atributo que usa argumentos posicionais e inicializações de propriedade.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6202.fs)]

Neste exemplo, o atributo é `DllImportAttribute`, aqui é usado de forma abreviada. O primeiro argumento é um parâmetro posicional e o segundo é uma propriedade.

Os atributos são um constructo de programação do .NET que permite que um objeto conhecido como um *atributo* a ser associado um tipo ou outro elemento de programa. O elemento de programa ao qual um atributo é aplicado é conhecido como o *atributo de destino*. O atributo geralmente contém metadados sobre seu destino. Nesse contexto, metadados pode ser quaisquer dados sobre o tipo diferente de seus campos e membros.

Os atributos no F# podem ser aplicadas para as seguintes construções de programação: funções, métodos, assemblies, módulos, tipos (classes, registros, estruturas, interfaces, delegados, enumerações, uniões e assim por diante), construtores, propriedades, campos, parâmetros, parâmetros de tipo e valores de retorno. Atributos não são permitidos em `let` associações dentro de classes, expressões ou expressões de fluxo de trabalho.

Normalmente, a declaração de atributo aparece diretamente antes da declaração de atributo de destino. Várias declarações de atributo podem ser usadas em conjunto, da seguinte maneira.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6603.fs)]

Você pode consultar os atributos em tempo de execução por meio de reflexão do .NET.

Você pode declarar vários atributos individualmente, como no exemplo de código anterior, ou você pode declará-las em um par de colchetes, se você usar um ponto e vírgula para separar os atributos individuais e construtores, conforme mostrado aqui.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6604.fs)]

Atributos encontrados normalmente incluem o `Obsolete` atributos de atributo, atributos para considerações de segurança, para suporte de COM, os atributos relacionados à propriedade do código e atributos que indica se um tipo pode ser serializado. O exemplo a seguir demonstra o uso do `Obsolete` atributo.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6605.fs)]

Para os destinos de atributo `assembly` e `module`, você aplica os atributos a um nível superior `do` associação em seu assembly. Você pode incluir a palavra `assembly` ou `module` na declaração de atributo, da seguinte maneira.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6606.fs)]

Se você omitir o atributo de destino para um atributo aplicado a um `do` associação, o F# compilador tenta determinar o atributo de destino que faça sentido para o atributo. Muitas classes de atributo tem um atributo de tipo `System.AttributeUsageAttribute` que inclui informações sobre os destinos possíveis com suporte para esse atributo. Se o `System.AttributeUsageAttribute` indica que o atributo dá suporte a funções como destinos, o atributo é obtido para aplicar ao ponto de entrada principal do programa. Se o `System.AttributeUsageAttribute` indica que o atributo dá suporte a assemblies como destinos, o compilador usa o atributo a ser aplicado ao assembly. A maioria dos atributos não se aplicam a funções e assemblies, mas em casos em que eles fazem, o atributo é necessário para aplicar a função de principal do programa. Se o atributo de destino for especificado explicitamente, o atributo é aplicado no destino especificado.

Embora normalmente não é necessário especificar o atributo de destino explicitamente, os valores válidos para *destino* em um atributo são mostrados na tabela a seguir, junto com exemplos de uso.

<table>
  <tr>
    <th>Atributo de destino</td>
    <th>Exemplo</td> 
  </tr>
  <tr>
    <td>assembly</td>
    <td><pre lang="fsharp"><code>[&lt;assembly: AssemblyVersionAttribute("1.0.0.0")&gt;]<code></pre></td> 
  </tr>
  <tr>
    <td>return</td>
    <td><pre lang="fsharp"><code>let function1 x : [&lt;return: Obsolete&gt;] int = x + 1<code></pre></td> 
  </tr>
  <tr>
    <td>campo</td>
    <td><pre lang="fsharp"><code>[&lt;field: DefaultValue&gt;] val mutable x: int<code></pre></td> 
  </tr>
  <tr>
    <td>propriedade</td>
    <td><pre lang="fsharp"><code>[&lt;property: Obsolete&gt;] this.MyProperty = x<code></pre></td> 
  </tr>
  <tr>
    <td>param</td>
    <td><pre lang="fsharp"><code>member this.MyMethod([&lt;param: Out&gt;] x : ref&lt;int&gt;) = x := 10<code></pre></td> 
  </tr>
  <tr>
    <td>tipo</td>
    <td>
        <pre lang="fsharp"><code>
        [&lt;type: StructLayout(Sequential)&gt;] 
        type MyStruct = 
        struct 
        x : byte
        y : int
        end
        <code></pre>
    </td>
  </tr>
</table>

## <a name="see-also"></a>Consulte também

- [Referência da Linguagem F#](index.md)
