---
title: Construtores de instâncias – Guia de Programação em C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], instance constructors
- instance constructors [C#]
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
ms.openlocfilehash: a5ed331c6b2960a56d7ab0d7812cb3a687ccfdd5
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67423753"
---
# <a name="instance-constructors-c-programming-guide"></a>Construtores de instâncias (Guia de Programação em C#)

Os construtores de instância são usados para criar e inicializar quaisquer variáveis de membro de instância quando você usa a expressão [new](../../../csharp/language-reference/operators/new-operator.md) para criar um objeto de uma [classe](../../../csharp/language-reference/keywords/class.md). Para inicializar uma classe [estática](../../../csharp/language-reference/keywords/static.md) ou variáveis estáticas em uma classe não estática, defina um construtor estático. Para obter mais informações, consulte [Construtores estáticos](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
 O exemplo a seguir mostra um construtor de instância:  
  
 [!code-csharp[csProgGuideObjects#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#5)]  
  
> [!NOTE]
>  Para maior clareza, essa classe contém campos públicos. O uso de campos públicos não é uma prática de programação recomendada, porque permite que qualquer acesso de programa não restrito e não verificado a trabalhos internos de um objeto. Geralmente os membros de dados devem ser privados e devem ser acessados apenas por meio de propriedades e métodos de classe.  
  
 Esse construtor de instância é chamado sempre que um objeto com base na classe `Coords` é criado. Um construtor como este, que não usa nenhum argumento, é chamado um *construtor sem parâmetros*. No entanto, geralmente é útil fornecer construtores adicionais. Por exemplo, podemos adicionar um construtor à classe `Coords` que nos permite especificar os valores iniciais para os membros de dados:  
  
 [!code-csharp[csProgGuideObjects#76](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#76)]  
  
 Isso permite que objetos `Coords` sejam criados com os valores iniciais padrão ou específicos, como este:  
  
 [!code-csharp[csProgGuideObjects#77](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#77)]  
  
 Se uma classe não tiver um construtor, um construtor sem parâmetros será gerado automaticamente e os valores padrão serão usados para inicializar os campos de objeto. Por exemplo, um [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md) é inicializada como 0. Para obter mais informações sobre valores padrão, consulte [Tabela de valores padrão](../../../csharp/language-reference/keywords/default-values-table.md). Portanto, como construtor sem parâmetros da classe `Coords` inicializa todos os membros de dados como zero, ele pode ser totalmente removido sem alterar a maneira como a classe funciona. Um exemplo completo que usa vários construtores é fornecido no Exemplo 1 posteriormente neste tópico e um exemplo de um construtor gerado automaticamente é fornecido no Exemplo 2.  
  
 Construtores de instância também podem ser usados para chamar os construtores de instância de classes base. O construtor de classe pode invocar o construtor da classe base por meio do inicializador, da seguinte maneira:  
  
 [!code-csharp[csProgGuideObjects#78](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#78)]  
  
 Neste exemplo, a classe `Circle` passa valores que representam o raio e a altura do construtor fornecido pelo `Shape` do qual `Circle` é derivado. Um exemplo completo que usa `Shape` e `Circle` é exibido neste tópico como Exemplo 3.  
  
## <a name="example-1"></a>Exemplo 1  
 O exemplo a seguir demonstra uma classe com dois construtores de classe, um sem argumentos e outro com dois argumentos.  
  
 [!code-csharp[csProgGuideObjects#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#4)]  
  
## <a name="example-2"></a>Exemplo 2  
 Neste exemplo, a classe `Person` não tem nenhum construtor. Nesse caso, um construtor sem parâmetros é fornecido automaticamente e os campos são inicializados com seus valores padrão.  
  
 [!code-csharp[csProgGuideObjects#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#8)]  
  
 Observe que o valor padrão de `age` é `0` e o valor padrão de `name` é `null`. Para obter mais informações sobre valores padrão, consulte [Tabela de valores padrão](../../../csharp/language-reference/keywords/default-values-table.md).  
  
## <a name="example-3"></a>Exemplo 3:  
 O exemplo a seguir demonstra como usar o inicializador de classe base. A classe `Circle` é derivada da classe geral `Shape` e a classe `Cylinder` é derivada da classe `Circle`. O construtor em cada classe derivada está usando seu inicializador de classe base.  
  
 [!code-csharp[csProgGuideObjects#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#9)]  
  
 Para obter mais exemplos sobre a invocação de construtores de classe base, consulte [virtual](../../../csharp/language-reference/keywords/virtual.md), [override](../../../csharp/language-reference/keywords/override.md) e [base](../../../csharp/language-reference/keywords/base.md).  
  
## <a name="see-also"></a>Consulte também

- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [Classes e Structs](../../../csharp/programming-guide/classes-and-structs/index.md)
- [Construtores](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)
- [static](../../../csharp/language-reference/keywords/static.md)
