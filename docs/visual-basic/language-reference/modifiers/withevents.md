---
title: WithEvents (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.WithEvents
- WithEvents
helpviewer_keywords:
- WithEvents keyword [Visual Basic]
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
ms.openlocfilehash: e8a8fb571fa65228f3a0acec1f902d21eb9bfe04
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268309"
---
# <a name="withevents-visual-basic"></a>WithEvents (Visual Basic)
Especifica que um ou mais variáveis de membro declaradas se referem a uma instância de uma classe que pode gerar eventos.  
  
## <a name="remarks"></a>Comentários  
 Quando uma variável é definida usando `WithEvents`, você pode especificar declarativamente que um método trata os eventos da variável usando o `Handles` palavra-chave.  
  
 Você pode usar `WithEvents` apenas no nível de classe ou módulo. Isso significa que o contexto da declaração para um `WithEvents` variável deve ser uma classe ou módulo e não pode ser um arquivo de origem, namespace, estrutura ou procedimento.  
  
 Não é possível usar `WithEvents` em um membro da estrutura.  
  
 Você pode declarar apenas variáveis individuais — não matrizes — com `WithEvents`.  
  
## <a name="rules"></a>Regras  
  
- **Tipos de elemento.** Você deve declarar `WithEvents` variáveis sejam variáveis de objeto para que eles possam aceitar instâncias de classe. No entanto, você não pode declará-los como `Object`. Você deve declará-los como a classe específica que pode gerar eventos.  
  
 O `WithEvents` modificador pode ser usado neste contexto: [Instrução Dim](../../../visual-basic/language-reference/statements/dim-statement.md)  
 
## <a name="example"></a>Exemplo

```VB
Dim WithEvents app As Application
```
  
## <a name="see-also"></a>Consulte também

- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
- [Palavras-chave](../../../visual-basic/language-reference/keywords/index.md)
- [Eventos](../../../visual-basic/programming-guide/language-features/events/index.md)
