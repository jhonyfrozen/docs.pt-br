---
title: Problemas conhecidos e considerações no LINQ to Entities
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: acd71129-5ff0-4b4e-b266-c72cc0c53601
ms.openlocfilehash: e84319c60534c3ecf154c3f58973bcc429a73842
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539817"
---
# <a name="known-issues-and-considerations-in-linq-to-entities"></a>Problemas conhecidos e considerações no LINQ to Entities
Esta seção fornece informações sobre problemas conhecidos com o LINQ para consultas de entidades.  
  
- [Consultas LINQ que não podem ser armazenados em cache](#LINQQueriesThatAreNotCached)  
  
- [Informações de ordenação perdidas](#OrderingInfoLost)  
  
- [Inteiros sem sinal não tem suportados](#UnsignedIntsUnsupported)  
  
- [Erros de conversão de tipo](#TypeConversionErrors)  
  
- [Referenciando variáveis não escalares não tem suportadas](#RefNonScalarClosures)  
  
- [Consultas aninhadas podem falhar com o SQL Server 2000](#NestedQueriesSQL2000)  
  
- [Projetando para um tipo anônimo](#ProjectToAnonymousType)  
  
<a name="LINQQueriesThatAreNotCached"></a>   
## <a name="linq-queries-that-cannot-be-cached"></a>Consultas LINQ que não podem ser armazenadas em cache  
 A partir do .NET Framework 4.5, as consultas LINQ to Entities são automaticamente armazenadas em cache. No entanto, as consultas LINQ to Entities que aplicam o operador `Enumerable.Contains` a coleções na memória não são armazenadas em cache automaticamente. Além disso, não é permitido parametrizar coleções na memória em consultas LINQ compiladas.  
  
<a name="OrderingInfoLost"></a>   
## <a name="ordering-information-lost"></a>Informações de ordenação perdidas  
 Projetar colunas em um tipo anônimo fará com que as informações de ordenação sejam perdidas em algumas consultas executadas em um banco de dados [!INCLUDE[ssVersion2005](../../../../../../includes/ssversion2005-md.md)] definido com um nível de compatibilidade de “80".  Isso ocorre quando um nome de coluna na lista order-by corresponde a um nome de coluna no seletor, conforme mostrado no exemplo a seguir:  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt543840)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt543840)]  
  
<a name="UnsignedIntsUnsupported"></a>   
## <a name="unsigned-integers-not-supported"></a>Inteiros sem sinal não suportados  
 Não há suporte a especificação de um tipo de inteiro sem sinal em uma consulta LINQ to Entities porque o [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] não oferece suporte a inteiros sem sinal. Se você especificar um inteiro sem sinal, um <xref:System.ArgumentException> exceção será gerada durante a conversão de expressão de consulta, conforme mostrado no exemplo a seguir. Este exemplo consulta um pedido com a ID 48000.  
  
 [!code-csharp[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#uintasqueryparam)]
 [!code-vb[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#uintasqueryparam)]  
  
<a name="TypeConversionErrors"></a>   
## <a name="type-conversion-errors"></a>Erros de conversão de tipos  
 No Visual Basic, quando uma propriedade é mapeada para uma coluna de tipo bit do SQL Server com um valor igual a 1 usando a função `CByte`, um <xref:System.Data.SqlClient.SqlException> é gerado com uma mensagem de “Erro de estouro aritmético". O exemplo a seguir consulta a coluna `Product.MakeFlag` no banco de dados de exemplo AdventureWorks e uma exceção é gerada quando os resultados da consulta são iterados sobre.  
  
 [!code-vb[DP L2E Conceptual Examples#SBUDT544355](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt544355)]  
  
<a name="RefNonScalarClosures"></a>   
## <a name="referencing-non-scalar-variables-not-supported"></a>Referenciando variáveis não escalares não suportadas  
 A referência a variáveis não escalares, como uma entidade, em uma consulta não é suportada. Quando uma consulta desse tipo é executada, é gerada uma exceção <xref:System.NotSupportedException> com a mensagem "Não foi possível criar um valor constante de tipo `EntityType`. Apenas tipos primitivos ('como Int32, String e GUID') são suportados nesse contexto."  
  
> [!NOTE]
>  A referência a uma coleção de variáveis escalares é suportada.  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt555877)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt555877)]  
  
<a name="NestedQueriesSQL2000"></a>   
## <a name="nested-queries-may-fail-with-sql-server-2000"></a>Pode haver falha em consultas aninhadas com o SQL Server 2000  
 Com o SQL Server 2000, pode haver falha em consultas do LINQ to Entities se elas gerarem consultas Transact-SQL aninhadas com três ou mais níveis de profundidade.  
  
<a name="ProjectToAnonymousType"></a>   
## <a name="projecting-to-an-anonymous-type"></a>Projetando para um tipo anônimo  
 Se você definir o caminho da consulta inicial para incluir objetos relacionados usando o método <xref:System.Data.Objects.ObjectQuery%601.Include%2A> no <xref:System.Data.Objects.ObjectQuery%601> e, em seguida, usar o LINQ para projetar os objetos retornados para um tipo anônimo, os objetos especificados no método de inclusão não serão incluídos nos resultados da consulta.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype1)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype1)]  
  
 Para obter objetos relacionados, não projete tipos retornados para um tipo anônimo.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype2)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype2)]  
  
## <a name="see-also"></a>Consulte também

- [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)
