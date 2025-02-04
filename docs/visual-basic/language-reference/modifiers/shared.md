---
title: Compartilhado (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Shared
helpviewer_keywords:
- Shared keyword [Visual Basic]
- members [Visual Basic], shared
- shared members
- nonshared
- shared [elements VB]
- elements [Visual Basic], shared
ms.assetid: 2bf7cf2c-b0dd-485e-8749-b5d674dab4cd
ms.openlocfilehash: fd43ef7cb5c16995fff87a65fc0f0974d8f4a47d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647701"
---
# <a name="shared-visual-basic"></a>Compartilhado (Visual Basic)
Especifica que um ou mais elementos de programação declarados estão associados com uma classe ou estrutura em geral e não uma instância específica da classe ou estrutura.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="when-to-use-shared"></a>Quando usar compartilhado  
 Compartilhar um membro de uma classe ou estrutura torna disponível para cada instância, em vez de *não compartilhado*, onde cada instância tem sua própria cópia. Isso é útil, por exemplo, se o valor de uma variável se aplica a todo o aplicativo. Se você declarar essa variável como `Shared`, em seguida, todas as instâncias de acessam o mesmo local de armazenamento e se uma instância muda o valor da variável, todas as instâncias de acessam o valor atualizado.  
  
 Compartilhar não altera o nível de acesso de um membro. Por exemplo, um membro de classe pode ser compartilhado e privado (acessível somente de dentro da classe), ou não compartilhado e público. Para obter mais informações, consulte [acessar níveis no Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## <a name="rules"></a>Regras  
  
- **Contexto da declaração.** Você pode usar `Shared` apenas no nível de módulo. Isso significa que o contexto da declaração para um `Shared` elemento deve ser uma classe ou estrutura e não pode ser um arquivo de origem, namespace ou procedimento.  
  
- **Modificadores combinados.** Não é possível especificar `Shared` junto com [prevalece](../../../visual-basic/language-reference/modifiers/overrides.md), [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md), [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md), [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md), ou [ Estático](../../../visual-basic/language-reference/modifiers/static.md) na mesma declaração.  
  
- **Acessando.** Você pode acessar um elemento compartilhado qualificando com seu nome de classe ou estrutura, não com o nome da variável de uma instância específica de sua classe ou estrutura. Até mesmo, não é preciso criar uma instância de uma classe ou estrutura para acessar seus membros compartilhados.  
  
     O exemplo a seguir chama o procedimento compartilhado <xref:System.Double.IsNaN%2A> expostos pelo <xref:System.Double> estrutura.  
  
     `If Double.IsNaN(result) Then MsgBox("Result is mathematically undefined.")`  
  
- **Compartilhamento implícito.** Não é possível usar o `Shared` modificador em um [instrução Const](../../../visual-basic/language-reference/statements/const-statement.md), mas constantes são implicitamente compartilhadas. Da mesma forma, você não pode declarar um membro de um módulo ou interface seja `Shared`, mas eles são implicitamente compartilhados.  
  
## <a name="behavior"></a>Comportamento  
  
- **Armazenamento.** Uma variável compartilhada ou um evento é armazenado na memória somente uma vez, não importa quantas vezes você cria de sua classe ou estrutura. Da mesma forma, um procedimento compartilhado ou uma propriedade mantém apenas um conjunto de variáveis locais.  
  
- **Acessando por meio de uma variável de instância.** É possível acessar um elemento compartilhado qualificando-o com o nome de uma variável que contém uma instância específica de sua classe ou estrutura. Embora isso geralmente funciona conforme o esperado, o compilador gera uma mensagem de aviso e faz o acesso através do nome de classe ou estrutura em vez da variável.  
  
- **Acessando por meio de uma expressão de instância.** Se você acessar um elemento compartilhado por meio de uma expressão que retorna uma instância de sua classe ou estrutura, o compilador faz o acesso através do nome de classe ou estrutura em vez de avaliar a expressão. Isso produz resultados inesperados se você pretendia que a expressão para executar outras ações, bem como retornar a instância. O exemplo a seguir ilustra essa situação.  
  
    ```vb
    Sub main()  
        shareTotal.total = 10  
        ' The preceding line is the preferred way to access total.  
        Dim instanceVar As New shareTotal  
        instanceVar.total += 100  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of through  
        ' the variable instanceVar. This works as expected and adds  
        ' 100 to total.  
        returnClass().total += 1000  
        ' The preceding line generates a compiler warning message and  
        ' accesses total through class shareTotal instead of calling  
        ' returnClass(). This adds 1000 to total but does not work as  
        ' expected, because the MsgBox in returnClass() does not run.  
        MsgBox("Value of total is " & CStr(shareTotal.total))  
    End Sub  
    Public Function returnClass() As shareTotal  
        MsgBox("Function returnClass() called")  
        Return New shareTotal  
    End Function  
    Public Class shareTotal  
        Public Shared total As Integer  
    End Class  
    ```  
  
     No exemplo anterior, o compilador gera uma mensagem de aviso nas duas vezes o código acessa a variável compartilhada `total` através de uma instância. Em cada caso, ele faz o acesso diretamente por meio da classe `shareTotal` e não faz uso de nenhuma instância. No caso da chamada pretendida para o procedimento `returnClass`, isso significa que ela não gera até mesmo uma chamada para `returnClass`, portanto, a ação adicional de mostrar "Function returnClass () chamado" não é executada.  
  
 O `Shared` modificador pode ser usado nestes contextos:  
  
 [Instrução Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Instrução Event](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Instrução Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Instrução Operator](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Instrução Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Instrução Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>Consulte também

- [Sombras](../../../visual-basic/language-reference/modifiers/shadows.md)
- [Estático](../../../visual-basic/language-reference/modifiers/static.md)
- [Tempo de vida no Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)
- [Procedimentos](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [Estruturas](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Objetos e Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
