---
title: Matrizes de parâmetros (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- parameter arrays [Visual Basic], about parameter arrays
- ParamArray keyword [Visual Basic], parameter arrays
- Visual Basic code, procedures
- parameters [Visual Basic], parameter arrays
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], indefinite number of argument values
- arrays [Visual Basic], parameter arrays
ms.assetid: c43edfae-9114-4096-9ebc-8c5c957a1067
ms.openlocfilehash: 372d5fdd2702d6f85f784ee5addea91abe46d3bd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64639015"
---
# <a name="parameter-arrays-visual-basic"></a>Matrizes de parâmetros (Visual Basic)
Normalmente, você não pode chamar um procedimento com mais argumentos do que especifica a declaração de procedimento. Quando você precisa de um número indefinido de argumentos, você pode declarar uma *matriz de parâmetros*, que permite que um procedimento aceitar uma matriz de valores para um parâmetro. Você não precisa saber o número de elementos na matriz de parâmetros quando você define o procedimento. O tamanho da matriz é determinado individualmente por cada chamada ao procedimento.  
  
## <a name="declaring-a-paramarray"></a>Declarando um ParamArray  
 Você usa o [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) palavra-chave para denotar uma matriz de parâmetros na lista de parâmetros. As seguintes regras se aplicam:  
  
- Um procedimento pode definir apenas uma matriz de parâmetro, e ele deve ser o último parâmetro na definição do procedimento.  
  
- A matriz de parâmetros deve ser passada por valor. Ela é boa prática para incluir explicitamente o [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) palavra-chave na definição do procedimento.  
  
- A matriz de parâmetros é automaticamente opcional. Seu valor padrão é uma matriz unidimensional vazia do tipo de elemento da matriz de parâmetros.  
  
- Todos os parâmetros que precedem a matriz de parâmetros devem ser necessários. A matriz de parâmetros deve ser o único parâmetro opcional.  
  
## <a name="calling-a-paramarray"></a>Chamar um ParamArray  
 Quando você chama um procedimento que define uma matriz de parâmetros, você pode fornecer o argumento em qualquer uma das seguintes maneiras:  
  
- Nada — ou seja, você poderá omitir as [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) argumento. Nesse caso, uma matriz vazia é passada para o procedimento. Você também pode passar o [nada](../../../../visual-basic/language-reference/nothing.md) palavra-chave, com o mesmo efeito.  
  
- Uma lista de um número arbitrário de argumentos, separados por vírgulas. O tipo de dados de cada argumento deve ser implicitamente conversível para o `ParamArray` tipo de elemento.  
  
- Uma matriz com o mesmo tipo de elemento como o tipo de elemento da matriz de parâmetros.  
  
 Em todos os casos, o código dentro do procedimento trata a matriz de parâmetros como uma matriz unidimensional com elementos do mesmo tipo de dados como o `ParamArray` tipo de dados.  
  
> [!IMPORTANT]
>  Sempre que você lida com uma matriz que pode ser indefinidamente grande, há um risco de ultrapassar alguma capacidade interna do seu aplicativo. Se você aceitar uma matriz de parâmetros, você deve testar o tamanho da matriz que o código de chamada passado para ele. Execute as etapas apropriadas se ele for muito grande para o seu aplicativo. Para obter mais informações, consulte [matrizes](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir define e chama a função `calcSum`. O `ParamArray` modificador para o parâmetro `args` permite que a função aceite um número variável de argumentos.  
  
 [!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]  
  
 O exemplo a seguir define um procedimento com uma matriz de parâmetros e gera os valores de todos os elementos da matriz passados para a matriz de parâmetros.  
  
 [!code-vb[VbVbcnProcedures#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#48)]  
  
 [!code-vb[VbVbcnProcedures#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#49)]  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [Procedimentos](./index.md)
- [Parâmetros e Argumentos de Procedimento](./procedure-parameters-and-arguments.md)
- [Passando Argumentos por Valor e por Referência](./passing-arguments-by-value-and-by-reference.md)
- [Passando Argumentos por Posição e Nome](./passing-arguments-by-position-and-by-name.md)
- [Parâmetros Opcionais](./optional-parameters.md)
- [Sobrecarga de Procedimento](./procedure-overloading.md)
- [Matrizes](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Opcional](../../../../visual-basic/language-reference/modifiers/optional.md)
