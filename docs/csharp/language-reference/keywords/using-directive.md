---
title: Diretiva using – Referência de C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
ms.openlocfilehash: 072af9850f792cb6d7322724f2adbc978465dc84
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66421749"
---
# <a name="using-directive-c-reference"></a>Diretiva using (Referência de C#)

A diretiva `using` tem três usos:

- Para permitir o uso de tipos em um namespace para que você não precise qualificar o uso de um tipo nesse namespace:

    ```csharp
    using System.Text;
    ```

- Para permitir que você acesse membros estáticos e tipos aninhados de um tipo sem precisar qualificar o acesso com o nome do tipo.

    ```csharp
    using static System.Math;
    ```

    Para obter mais informações, consulte a [diretiva using static](using-static.md).

- Para criar um alias para um namespace ou um tipo. Isso é chamado de uma *diretiva alias de using*.

    ```csharp
    using Project = PC.MyCompany.Project;
    ```

A palavra-chave `using` também é usada para criar *instruções using*, o que ajuda a garantir que objetos <xref:System.IDisposable>, tais como arquivos e fontes, sejam tratados corretamente. Consulte a [Instrução using](using-statement.md) para obter mais informações.

## <a name="using-static-type"></a>Tipo using static

Você pode acessar os membros estáticos de um tipo sem precisar qualificar o acesso com o nome do tipo:

```csharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```

## <a name="remarks"></a>Comentários

O escopo de uma diretiva `using` é limitado ao arquivo em que ele aparece.

A diretiva `using` pode aparecer:

- No início de um arquivo de código-fonte, antes de quaisquer definições de namespace ou tipo.
- Em qualquer namespace, mas antes de qualquer namespace ou tipos declarados neste namespace.

Caso contrário, serão gerados erros do compilador [CS1529](../../misc/cs1529.md).

Crie uma diretiva de alias `using` para tornar mais fácil a qualificação de um identificador para um namespace ou tipo. Em qualquer diretiva `using`, o namespace totalmente qualificado ou o tipo deve ser usado independentemente das diretivas `using` que vêm antes. Nenhum alias `using` pode ser usado na declaração de uma diretiva `using`. Por exemplo, o código a seguir gera um erro de compilador:

```csharp
using s = System.Text;
using s.RegularExpressions;
```

Crie uma diretiva `using` para usar os tipos em um namespace sem precisar especificar o namespace. Uma diretiva `using` não fornece acesso a nenhum namespace aninhado no namespace especificado.

Os namespaces vêm em duas categorias: definidos pelo usuário e definidos pelo sistema. Os namespaces definidos pelo usuário são namespaces definidos em seu código. Para obter uma lista dos namespaces definidos pelo sistema, consulte [Navegador de API do .NET](../../../../api/index.md).

Para obter exemplos sobre como referenciar métodos em outros assemblies, confira [Criar e usar assemblies usando a linha de comando](../../programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md).

## <a name="example-1"></a>Exemplo 1

O exemplo a seguir mostra como definir e usar um alias de `using` para um namespace:

[!code-csharp[csrefKeywordsNamespace#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#8)]

Uma diretiva alias de using não pode ter um tipo genérico aberto no lado direito. Por exemplo, você não pode criar um alias de using para um `List<T>`, mas pode criar um para um `List<int>`.

## <a name="example-2"></a>Exemplo 2

O exemplo a seguir mostra como definir uma diretiva `using` e um alias `using` para uma classe:

[!code-csharp[csrefKeywordsNamespace#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#9)]

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, consulte [Diretivas using](~/_csharplang/spec/namespaces.md#using-directives) na [Especificação da Linguagem C#](../language-specification/index.md). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.

## <a name="see-also"></a>Consulte também

- [Referência de C#](../index.md)
- [Guia de Programação em C#](../../programming-guide/index.md)
- [Usando namespaces](../../programming-guide/namespaces/using-namespaces.md)
- [Palavras-chave do C#](index.md)
- [Namespaces](../../programming-guide/namespaces/index.md)
- [Instrução using](using-statement.md)
