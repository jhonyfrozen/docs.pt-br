---
title: Comparações de igualdade – Guia de Programação em C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- object equality [C#]
ms.assetid: 10b865ea-4e7b-4127-9242-c9b8f57d9f04
ms.openlocfilehash: 50b1cdb8b7e5087f1fd6669e7163e2c15e9b23bf
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67423655"
---
# <a name="equality-comparisons-c-programming-guide"></a>Comparações de igualdade (Guia de Programação em C#)

Às vezes, é necessário comparar dois valores em relação à igualdade. Em alguns casos, testa-se a *igualdade de valor*, também conhecida como *equivalência*, o que significa que os valores contidos pelas duas variáveis são iguais. Em outros casos, é necessário determinar se duas variáveis se referem ao mesmo objeto subjacente na memória. Esse tipo de igualdade é chamado *igualdade de referência* ou *identidade*. Este tópico descreve esses dois tipos de igualdade e fornece links para outros tópicos que fornecem mais informações.  
  
## <a name="reference-equality"></a>Igualdade de referência

 Igualdade de referência significa que as duas referências de objeto se referem ao mesmo objeto subjacente. Isso pode ocorrer por meio de uma atribuição simples, conforme mostrado no exemplo a seguir.  
  
 [!code-csharp[csProgGuideStatements#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#18)]  
  
 Nesse código, dois objetos são criados, mas após a instrução de atribuição, ambas as referências se referem ao mesmo objeto. Portanto, eles têm igualdade de referência. Use o método <xref:System.Object.ReferenceEquals%2A> para determinar se duas referências referenciam o mesmo objeto.  
  
 O conceito de igualdade de referência se aplica apenas a tipos de referência. Objetos de tipo de valor não podem ter igualdade de referência, pois quando uma instância de um tipo de valor é atribuída a uma variável, uma cópia do valor é gerada. Portanto, não é possível ter dois structs desconvertidos que referenciam o mesmo local na memória. Além disso, se <xref:System.Object.ReferenceEquals%2A> for usado para comparar dois tipos de valor, o resultado sempre será `false`, mesmo se os valores contidos nos objetos forem idênticos. Isso ocorre porque cada variável é convertido em uma instância de objeto separada. Para obter mais informações, confira [Como: Testar a igualdade de referência (identidade)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).  

## <a name="value-equality"></a>Igualdade de valor

 Igualdade de valor significa que dois objetos contêm o mesmo valor ou valores. Para tipos de valor primitivos, como [int](../../../csharp/language-reference/builtin-types/integral-numeric-types.md) ou [bool](../../../csharp/language-reference/keywords/bool.md), os testes de igualdade de valor são simples. É possível usar o operador [==](../../../csharp/language-reference/operators/equality-operators.md#equality-operator-), conforme mostrado no exemplo a seguir.  
  
```csharp  
int a = GetOriginalValue();  
int b = GetCurrentValue();  
  
// Test for value equality.   
if( b == a)   
{  
    // The two integers are equal.  
}  
```  
  
 Para a maioria dos outros tipos, o teste de igualdade de valor é mais complexo, pois é necessário entender como o tipo o define. Para classes e structs que têm vários campos ou propriedades, a igualdade de valor geralmente é definida para determinar que todos os campos ou propriedades tenham o mesmo valor. Por exemplo, dois objetos `Point` podem ser definidos para serem equivalentes se pointA.X for igual a pointB.X e pointA.Y for igual a pointB.Y.  
  
 No entanto, não há nenhuma exigência de que a equivalência seja baseada em todos os campos em um tipo. Ela pode ser baseada em um subconjunto. Ao comparar tipos que não são de sua propriedade, certifique-se de que a forma como a equivalência é definida especificamente para esse tipo foi entendida. Para saber mais sobre como definir a igualdade de valor em suas próprias classes e structs, confira [Como definir a igualdade de valor para um tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).  
  
### <a name="value-equality-for-floating-point-values"></a>Igualdade de valor para valores de ponto flutuante

 As comparações de igualdade de valores de ponto flutuante ([double](../../../csharp/language-reference/keywords/double.md) e [float](../../../csharp/language-reference/keywords/float.md)) são problemáticas devido à imprecisão da aritmética de ponto flutuante em computadores binários. Para obter mais informações, consulte os comentários no tópico <xref:System.Double?displayProperty=nameWithType>.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|DESCRIÇÃO|  
|-----------|-----------------|  
|[Como: Testar a igualdade de referência (identidade)](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)|Descreve como determinar se duas variáveis têm igualdade de referência.|  
|[Como: Definir a igualdade de valor para um tipo](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)|Descreve como fornecer uma definição personalizada de igualdade de valor a um tipo.|  
|[Guia de Programação em C#](../../../csharp/programming-guide/index.md)|Fornece links para informações detalhadas sobre recursos importantes da linguagem C# e recursos disponíveis para o C# por meio do .NET Framework.|  
|[Tipos](../../../csharp/programming-guide/types/index.md)|Fornece informações sobre o sistema de tipos do C# e links para mais informações.|  
  
## <a name="see-also"></a>Consulte também

- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
