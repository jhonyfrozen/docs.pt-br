---
title: Métodos de System.Math
ms.date: 03/30/2017
ms.assetid: 0f299521-6f41-4720-bd70-67c93fc50948
ms.openlocfilehash: 5200f31bd319bad49651c3096e1c1364a8003377
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64613769"
---
# <a name="systemmath-methods"></a>Métodos de System.Math
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] não oferece suporte aos seguintes métodos de <xref:System.Math> .  
  
- <xref:System.Math.DivRem%28System.Int32%2CSystem.Int32%2CSystem.Int32%40%29?displayProperty=nameWithType>  
  
- <xref:System.Math.DivRem%28System.Int64%2CSystem.Int64%2CSystem.Int64%40%29?displayProperty=nameWithType>  
  
- <xref:System.Math.IEEERemainder%28System.Double%2CSystem.Double%29?displayProperty=nameWithType>  
  
## <a name="differences-from-net"></a>Diferenças do .NET  
 O.NET Framework tem a semântica por arredondamento diferente do SQL Server. O <xref:System.Math.Round%2A> método no .NET Framework realiza *arredondamento bancário*, onde os números que terminam em. 5 são arredondados para o dígito em vez de para o dígito mais próximo mais próximo. Por exemplo, círculos 2,5 a 2, quando círculos 3,5 a 4. (Essa técnica ajuda a evitar a polarização sistemática para os valores mais altos em grandes transações de dados.)  
  
 Em SQL, a função de `ROUND` vez arredondará sempre fora de 0. Portanto círculos 2,5 a 3, contrastado com o arredondamento para 2 no.NET Framework.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] passa completamente a semântica do SQL `ROUND` e não tenta implementar arredondamento bancário.  
  
## <a name="see-also"></a>Consulte também

- [Funções e tipos de dados](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)
