---
title: Os limites de matriz não podem ser exibidos em especificadores de tipo
ms.date: 07/20/2015
f1_keywords:
- vbc30638
- bc30638
helpviewer_keywords:
- BC30638
ms.assetid: 93b654f4-70fa-4a48-baed-ffae42075550
ms.openlocfilehash: 50e1cd0e41da467a9e816c8e5d64d09a36923d65
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665743"
---
# <a name="array-bounds-cannot-appear-in-type-specifiers"></a>Os limites de matriz não podem ser exibidos em especificadores de tipo
Tamanhos de matriz não podem ser declarados como parte de um especificador de tipo de dados.  
  
 **ID do erro:** BC30638  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Especifique o tamanho da matriz imediatamente após o nome da variável em vez de colocar o tamanho da matriz após o tipo, conforme mostrado no exemplo a seguir.  
  
    ```  
    Dim Array(8) As Integer   
    ```  
  
- Definir uma matriz e inicialize-o com o número desejado de elementos, conforme mostrado no exemplo a seguir.  
  
    ```  
    Dim Array2() As Integer = New Integer(8) {}  
    ```  
  
## <a name="see-also"></a>Consulte também

- [Matrizes](../../../visual-basic/programming-guide/language-features/arrays/index.md)
