---
title: Namespaces no Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.global
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- name collisions
- Global keyword [Visual Basic]
- namespace pollution
- names [Visual Basic], avoiding conflicts
- naming conflicts [Visual Basic], namespaces
- namespaces [Visual Basic], assemblies
- Visual Basic code, namespaces
- fully qualified names [Visual Basic]
- naming conventions [Visual Basic], naming conflicts
- namespaces
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
ms.openlocfilehash: bbd8d901f018d95b8a1f5c81c813853838c4a4cd
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586293"
---
# <a name="namespaces-in-visual-basic"></a>Namespaces no Visual Basic
Namespaces organizam objetos definidos em um assembly. Os assemblies podem conter vários namespaces, que por sua vez pode conter outros namespaces. Namespaces evitar a ambiguidade e simplificar as referências ao usar grupos grandes de objetos, como bibliotecas de classes.  
  
 Por exemplo, o .NET Framework define o <xref:System.Windows.Forms.ListBox> classe o <xref:System.Windows.Forms?displayProperty=nameWithType> namespace. O fragmento de código a seguir mostra como declarar uma variável usando o nome totalmente qualificado para esta classe:  
  
 [!code-vb[VbVbalrApplication#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#6)]  
  
## <a name="avoiding-name-collisions"></a>Evitando conflitos de nome  
 Um problema às vezes chamado de endereço de namespaces do .NET framework *poluição de namespace*, no qual o desenvolvedor de uma biblioteca de classes é dificultado pelo uso de nomes semelhantes em outra biblioteca. Esses conflitos com os componentes existentes às vezes são chamados *conflitos de nome*.  
  
 Por exemplo, se você criar uma nova classe chamada `ListBox`, você pode usá-lo dentro de seu projeto sem qualificação. No entanto, se você quiser usar o .NET Framework <xref:System.Windows.Forms.ListBox> classe no mesmo projeto, você deve usar uma referência totalmente qualificada para tornar a referência exclusiva. Se a referência não for exclusiva, o Visual Basic gera um erro informando que o nome é ambíguo. O exemplo de código a seguir demonstra como declarar esses objetos:  
  
 [!code-vb[VbVbalrApplication#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#7)]  
  
 A ilustração a seguir mostra duas hierarquias de namespace, os dois que contém um objeto chamado `ListBox`:  
  
 ![Captura de tela que mostra duas hierarquias de namespace.](./media/namespaces/visual-basic-namespace-hierarchy.gif)  
  
 Por padrão, cada arquivo executável que você criar com o Visual Basic contém um namespace com o mesmo nome que seu projeto. Por exemplo, se você definir um objeto em um projeto chamado `ListBoxProject`, o arquivo executável ListBoxProject.exe contém um namespace chamado `ListBoxProject`.  
  
 Vários assemblies podem usar o mesmo namespace. Visual Basic trata como um único conjunto de nomes. Por exemplo, você pode definir classes para um namespace chamado `SomeNameSpace` em um assembly chamado `Assemb1`e definir classes adicionais para o mesmo namespace de um assembly denominado `Assemb2`.  
  
## <a name="fully-qualified-names"></a>Nomes totalmente qualificados  
 Nomes totalmente qualificados são referências de objeto que são prefixadas com o nome do namespace no qual o objeto é definido. Você pode usar objetos definidos em outros projetos, se você criar uma referência à classe (escolhendo **adicionar referência** da **projeto** menu) e, em seguida, use o nome totalmente qualificado para o objeto em seu código. O fragmento de código a seguir mostra como usar o nome totalmente qualificado para um objeto do namespace do projeto para outro:  
  
 [!code-vb[VbVbalrApplication#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#8)]  
  
 Nomes totalmente qualificados impedem a nomeação entra em conflito porque eles possibilitam que o compilador determine qual objeto está sendo usado. No entanto, os nomes em si podem obter longo e complicado. Para contornar esse problema, você pode usar o `Imports` instrução para definir um *alias*— um nome abreviado, você pode usar no lugar do nome totalmente qualificado. Por exemplo, o exemplo de código a seguir cria aliases para dois nomes totalmente qualificados e usa esses aliases para definir dois objetos.  
  
 [!code-vb[VbVbalrApplication#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#9)]  
  
 [!code-vb[VbVbalrApplication#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#10)]  
  
 Se você usar o `Imports` instrução sem um alias, você pode usar todos os nomes em que o namespace sem qualificação, fornecidas são exclusivos para o projeto. Se o projeto contiver `Imports` instruções para os namespaces que contêm itens com o mesmo nome, você deve qualificar totalmente esse nome quando você usá-lo. Suponha, por exemplo, seu projeto continha os dois seguintes `Imports` instruções:  
  
 [!code-vb[VbVbalrApplication#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#11)]  
  
 Se você tentar usar `Class1` sem qualificá-lo completamente, Visual Basic gera um erro informando que o nome `Class1` é ambíguo.  
  
## <a name="namespace-level-statements"></a>Instruções de nível de Namespace  
 Dentro de um namespace, você pode definir itens como módulos, interfaces, classes, delegados, enumerações, estruturas e outros namespaces. Você não pode definir itens como propriedades, procedimentos, variáveis e eventos no nível de namespace. Esses itens devem ser declarados dentro de contêineres, como módulos, estruturas ou classes.  
  
## <a name="global-keyword-in-fully-qualified-names"></a>Palavra-chave global em nomes totalmente qualificados  
 Se você tiver definido uma hierarquia aninhada de namespaces, o código dentro dessa hierarquia pode ser impedido de acessar o <xref:System?displayProperty=nameWithType> namespace do .NET Framework. O exemplo a seguir ilustra uma hierarquia na qual o `SpecialSpace.System` namespace bloqueia o acesso à <xref:System?displayProperty=nameWithType>.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 Como resultado, o compilador do Visual Basic com êxito não é possível resolver a referência ao <xref:System.Int32?displayProperty=nameWithType>, pois `SpecialSpace.System` nedefinuje `Int32`. Você pode usar o `Global` palavra-chave para iniciar a cadeia de qualificação no nível mais externo da biblioteca de classes do .NET Framework. Isso permite que você especifique o <xref:System?displayProperty=nameWithType> namespace ou qualquer outro namespace na biblioteca de classes. O exemplo a seguir ilustra essa situação.  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 Você pode usar `Global` para acessar outros namespaces no nível raiz, como <xref:Microsoft.VisualBasic?displayProperty=nameWithType>e qualquer namespace associado ao seu projeto.  
  
## <a name="global-keyword-in-namespace-statements"></a>Palavra-chave nas declarações de Namespace global  
 Você também pode usar o `Global` palavra-chave em um [declaração de Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md). Isso permite que você definir um namespace fora do namespace raiz do seu projeto.  
  
 Todos os namespaces no seu projeto baseiam-se no namespace raiz para o projeto.  Visual Studio atribui o nome do projeto como o namespace de raiz padrão para todo o código em seu projeto. Por exemplo, se seu projeto é nomeado `ConsoleApplication1`, seus elementos de programação pertencem ao namespace `ConsoleApplication1`. Se você declarar `Namespace Magnetosphere`, faz referência às `Magnetosphere` no projeto irá acessar `ConsoleApplication1.Magnetosphere`.  
  
 Os exemplos a seguir usam o `Global` palavra-chave para declarar um namespace fora do namespace raiz para o projeto.  
  
 [!code-vb[VbVbalrApplication#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/module1.vb#22)]  
  
 Em uma declaração de namespace, `Global` não pode ser aninhado em outro namespace.  
  
 Você pode usar o [página de aplicativo, Designer de projeto (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic) para exibir e modificar as **Namespace raiz** do projeto.  Para novos projetos, o **Namespace de raiz** assume como padrão o nome do projeto. Para fazer com que `Global` para ser o namespace de nível superior, você pode limpar o **Namespace raiz** entrada para que a caixa estiver vazia. Limpando **Namespace raiz** elimina a necessidade do `Global` palavra-chave nas declarações de namespace.  
  
 Se um `Namespace` instrução declara um nome que também é um namespace do .NET Framework, o namespace do .NET Framework se torna indisponível se o `Global` palavra-chave não é usado em um nome totalmente qualificado. Para habilitar o acesso a esse namespace do .NET Framework sem usar o `Global` palavra-chave, você pode incluir o `Global` palavra-chave no `Namespace` instrução.  
  
 O exemplo a seguir tem o `Global` palavra-chave no `System.Text` declaração de namespace.  
  
 Se o `Global` palavra-chave não estava presente na declaração de namespace, <xref:System.Text.StringBuilder> não pôde ser acessado sem especificar `Global.System.Text.StringBuilder`. Para um projeto chamado `ConsoleApplication1`, faz referência às `System.Text` acessaria `ConsoleApplication1.System.Text` se o `Global` palavra-chave não foi usado.  
  
 [!code-vb[VbVbalrApplication#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/module1.vb#21)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.ListBox>
- <xref:System.Windows.Forms?displayProperty=nameWithType>
- [Assemblies no .NET](../../../standard/assembly/index.md)
- [Como: criar e usar assemblies usando a linha de comando](../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md).
- [Referências e a Instrução Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Instrução Imports (Tipo e Namespace .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [Escrevendo código em soluções do Office](/visualstudio/vsto/writing-code-in-office-solutions)
