---
title: Classes static e membros de classes static – Guia de Programação em C#
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, static members
- static members [C#]
- static classes [C#]
- C# language, static classes
- static class members [C#]
ms.assetid: 235614b5-1371-4dbd-9abd-b406a8b0298b
ms.openlocfilehash: 11cbe6600a75b2db6174841790aa69efdf5da035
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398287"
---
# <a name="static-classes-and-static-class-members-c-programming-guide"></a>Classes static e membros de classes static (Guia de Programação em C#)

Uma classe [static](../../../csharp/language-reference/keywords/static.md) é basicamente o mesmo que uma classe não estática, mas há uma diferença: uma classe estática não pode ser instanciada. Em outras palavras, você não pode usar o operador [new](../../../csharp/language-reference/operators/new-operator.md) para criar uma variável do tipo de classe. Como não há nenhuma variável de instância, você acessa os membros de uma classe estática usando o próprio nome de classe. Por exemplo, se houver uma classe estática chamada `UtilityClass` com um método público chamado `MethodA`, chame o método, como mostra o exemplo a seguir:  
  
```csharp  
UtilityClass.MethodA();  
```  
  
 Uma classe estática pode ser usada como um contêiner conveniente para conjuntos de métodos que operam apenas em parâmetros de entrada e não precisam obter ou definir campos de instância internos. Por exemplo, na biblioteca de classes .NET Framework, a classe estática <xref:System.Math?displayProperty=nameWithType> contém métodos que executam operações matemáticas, sem a necessidade de armazenar ou recuperar dados que são exclusivos de uma determinada instância da classe <xref:System.Math>. Ou seja, você aplica os membros da classe especificando o nome de classe e o nome do método, conforme mostrado no exemplo a seguir.  
  
```csharp  
double dub = -3.14;  
Console.WriteLine(Math.Abs(dub));  
Console.WriteLine(Math.Floor(dub));  
Console.WriteLine(Math.Round(Math.Abs(dub)));  
  
// Output:  
// 3.14  
// -4  
// 3  
```  
  
 Como é o caso com todos os tipos de classe, as informações de tipo de uma classe estática são carregadas pelo CLR (Common Language Runtime) do .NET Framework quando o programa que faz referência à classe é carregado. O programa não pode especificar exatamente quando a classe é carregada. No entanto, é garantido que ela será carregada e terá seus campos inicializados e seu construtor estático chamado antes que a classe seja referenciada pela primeira vez em seu programa. Um construtor estático é chamado apenas uma vez e uma classe estática permanece na memória pelo tempo de vida do domínio do aplicativo em que seu programa reside.  
  
> [!NOTE]
>  Para criar uma classe não estática que permite que apenas uma instância de si mesma seja criada, consulte [Implementando singleton no C#](https://docs.microsoft.com/previous-versions/msp-n-p/ff650316%28v=pandp.10%29).  
  
 A lista a seguir fornece os principais recursos de uma classe estática:  
  
- Contém apenas membros estáticos.  
  
- Não pode ser instanciada.  
  
- É lacrada.  
  
- Não pode conter [Construtores de instância](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md).  
  
 Criar uma classe estática é, portanto, basicamente o mesmo que criar uma classe que contém apenas membros estáticos e um construtor particular. Um construtor particular impede que a classe seja instanciada. A vantagem de usar uma classe estática é que o compilador pode verificar se nenhum membro de instância foi adicionado acidentalmente. O compilador garantirá que as instâncias dessa classe não possam ser criadas.  
  
 Classes estáticas são lacradas e, portanto, não podem ser herdadas. Elas não podem herdar de qualquer classe, exceto por <xref:System.Object>. Classes estáticas não podem conter um construtor de instância. No entanto, elas podem conter um construtor estático. Classes não estáticas também devem definir um construtor estático se a classe contiver membros estáticos que exigem inicialização não trivial. Para obter mais informações, consulte [Construtores estáticos](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
## <a name="example"></a>Exemplo  
 Temos aqui um exemplo de uma classe estática que contém dois métodos que convertem a temperatura de Celsius em Fahrenheit e de Fahrenheit em Celsius:  
  
 [!code-csharp[csProgGuideObjects#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#31)]  
  
## <a name="static-members"></a>Membros Estáticos  
 Uma classe não estática não pode conter métodos, campos, propriedades ou eventos estáticos. O membro estático pode ser chamado em uma classe, mesmo quando nenhuma instância da classe foi criada. O membro estático sempre é acessado pelo nome de classe, não pelo nome da instância. Existe apenas uma cópia de um membro estático, independentemente de quantas instâncias da classe forem criadas. Propriedades e métodos estáticos não podem acessar eventos e campos não estáticos no tipo que os contêm e não podem acessar uma variável de instância de nenhum objeto, a menos que ele seja passado explicitamente em um parâmetro de método.  
  
 É mais comum declarar uma classe não estática com alguns membros estáticos do que declarar uma classe inteira como estática. Dois usos comuns dos campos estáticos são manter uma contagem do número de objetos que foram instanciados ou armazenar um valor que deve ser compartilhado entre todas as instâncias.  
  
 Métodos estáticos podem ser sobrecarregados, mas não substituídos, porque pertencem à classe e não a qualquer instância da classe.  
  
 Embora um campo não possa ser declarado como `static const`, um campo [const](../../../csharp/language-reference/keywords/const.md) é essencialmente estático em seu comportamento. Ele pertence ao tipo e não a instâncias do tipo. Portanto, campos constantes podem ser acessados usando a mesma notação `ClassName.MemberName` usada para campos estáticos. Nenhuma instância de objeto é necessária.  
  
 O C# não dá suporte a variáveis locais estáticas (variáveis que são declaradas no escopo do método).  
  
 Você declara membros de classe estática usando a palavra-chave `static` antes do tipo de retorno do membro, conforme mostrado no exemplo a seguir:  
  
 [!code-csharp[csProgGuideObjects#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#29)]  
  
 Membros estáticos são inicializados antes que o membro estático seja acessado pela primeira vez e antes que o construtor estático, se houver, seja chamado. Para acessar um membro de classe estática, use o nome da classe em vez de um nome de variável para especificar o local do membro, conforme mostrado no exemplo a seguir:  
  
 [!code-csharp[csProgGuideObjects#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#30)]  
  
 Se sua classe contiver campos estáticos, forneça um construtor estático que os inicializa quando a classe é carregada.  
  
 Uma chamada para um método estático gera uma instrução de chamada em MSIL (Microsoft Intermediate Language), enquanto uma chamada para um método de instância gera uma instrução `callvirt`, que também verifica se há referências de objeto nulas. No entanto, na maioria das vezes, a diferença de desempenho entre os dois não é significativa.  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  

Para saber mais, confira [Classes estáticas](~/_csharplang/spec/classes.md#static-classes) e [Membros estáticos e de instância](~/_csharplang/spec/classes.md#static-and-instance-members) na [Especificação da linguagem C#](../../language-reference/language-specification/index.md). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.
  
## <a name="see-also"></a>Consulte também

- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)
- [static](../../../csharp/language-reference/keywords/static.md)
- [Classes](../../../csharp/programming-guide/classes-and-structs/classes.md)
- [class](../../../csharp/language-reference/keywords/class.md)
- [Construtores estáticos](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)
- [Construtores de instância](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)
