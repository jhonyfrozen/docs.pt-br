---
title: Classificando e filtrando dados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
ms.openlocfilehash: 68b2f75681bef6c43b7eb2072d6e9266408ca102
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64607187"
---
# <a name="sorting-and-filtering-data"></a>Classificando e filtrando dados
O <xref:System.Data.DataView> fornece várias maneiras de classificar e filtrar dados em uma <xref:System.Data.DataTable>:  
  
- Você pode usar a propriedade <xref:System.Data.DataView.Sort%2A> para especificar uma ou várias ordens de classificação de coluna, e para incluir parâmetros ASC (crescente) e DESC (decrescente).  
  
- Você pode usar a propriedade <xref:System.Data.DataView.ApplyDefaultSort%2A> para criar automaticamente uma ordem de classificação, em ordem crescente, com base na coluna de chave primária ou nas colunas da tabela. <xref:System.Data.DataView.ApplyDefaultSort%2A> se aplica somente quando o **classificação** propriedade é uma referência nula ou uma cadeia de caracteres vazia, e quando a tabela tem uma chave primária definida.  
  
- Você pode usar a propriedade <xref:System.Data.DataView.RowFilter%2A> para especificar subconjuntos de linhas com base nos valores de coluna. Para obter detalhes sobre expressões válidas para o **RowFilter** propriedade, consulte as informações de referência para o <xref:System.Data.DataColumn.Expression%2A> propriedade do <xref:System.Data.DataColumn> classe.  
  
     Se você quiser retornar os resultados de uma consulta específica nos dados, em vez de fornecer uma exibição dinâmica de um subconjunto dos dados, use o <xref:System.Data.DataView.Find%2A> ou <xref:System.Data.DataView.FindRows%2A> métodos das **DataView** para obter melhor desempenho em vez de Definindo o **RowFilter** propriedade. Definindo o **RowFilter** propriedade recria o índice para os dados, adicionando a sobrecarga ao seu aplicativo e prejudicando o desempenho. O **RowFilter** propriedade é melhor usada em um aplicativo associado a dados em que um controle associado exibe resultados filtrados. O **encontrar** e **FindRows** métodos aproveitam o índice atual sem exigir que o índice seja reconstruído. Para obter mais informações sobre o **encontrar** e **FindRows** métodos, consulte [localizando linhas](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md).  
  
- Você pode usar a propriedade <xref:System.Data.DataView.RowStateFilter%2A> para especificar quais versões de linha serão exibidas. O **DataView** gerencia implicitamente qual versão de linha para expor de acordo com as **RowState** da linha subjacente. Por exemplo, se o **RowStateFilter** é definido como **DataViewRowState. Deleted**, o **DataView** expõe o **Original** versão da linha todos os **Deleted** linhas porque não há nenhuma **atual** versão de linha. Você pode determinar qual versão de linha de uma linha está sendo exposto usando o **RowVersion** propriedade da **DataRowView**.  
  
     A tabela a seguir mostra as opções para **DataViewRowState**.  
  
    |Opções de DataViewRowState|Descrição|  
    |------------------------------|-----------------|  
    |**CurrentRows**|O **atual** versão de linha de todas as **inalterado**, **adicionado**, e **modificado** linhas. Esse é o padrão.|  
    |**Adicionado**|O **atual** versão de linha de todas as **adicionado** linhas.|  
    |**Excluído**|O **Original** versão de linha de todas as **Deleted** linhas.|  
    |**ModifiedCurrent**|O **atual** versão de linha de todas as **modificado** linhas.|  
    |**ModifiedOriginal**|O **Original** versão de linha de todas as **modificado** linhas.|  
    |**Nenhum**|Nenhuma linha.|  
    |**OriginalRows**|O **Original** versão de linha de todas as **inalterado**, **modificado**, e **Deleted** linhas.|  
    |**inalterado**|O **atual** versão de linha de todas as **inalterado** linhas.|  
  
 Para obter mais informações sobre estados de linha e versões de linha, consulte [estados de linha e versões de linha](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
 O exemplo de código a seguir cria uma exibição que mostra todos os produtos em que o número de unidades em estoque é menor ou igual ao nível de reordenação, classificado primeiro por ID do fornecedor e, depois, por nome do produto.  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataViews](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)
- [ADO.NET Managed Providers and DataSet Developer Center](https://go.microsoft.com/fwlink/?LinkId=217917) (Central de desenvolvedores do DataSet e de provedores gerenciados do ADO.NET)
