---
title: 'Como: Chamar funções definidas por modelo como métodos de objeto'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
ms.openlocfilehash: 53ec7122a3601a2da53513f25a546a08c2aa4307
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64631563"
---
# <a name="how-to-call-model-defined-functions-as-object-methods"></a>Como: Chamar funções definidas por modelo como métodos de objeto
Este tópico descreve como chamar uma função o definida como um método em um objeto de <xref:System.Data.Objects.ObjectContext> ou como um método estático em uma classe personalizada. Um *função definida pelo modelo* é uma função que é definida no modelo conceitual. O tópico descrevem como chamar essas funções diretamente em vez de chamá-los de consultas LINQ to Entities. Para obter informações sobre como chamar funções definidas no LINQ para consultas de entidades, consulte [como: Chamar funções definidas em consultas](../../../../../../docs/framework/data/adonet/ef/language-reference/how-to-call-model-defined-functions-in-queries.md).  
  
 Se você chamar uma função o definida como um método de <xref:System.Data.Objects.ObjectContext> ou como um método estático em uma classe personalizada, primeiro você deve mapear o método à função definida com o <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>. No entanto, quando você define um método na classe de <xref:System.Data.Objects.ObjectContext> , você deve usar a propriedade de <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> para expor o provedor LINQ, enquanto quando você define um método estático em uma classe personalizada, você deve usar a propriedade de <xref:System.Linq.IQueryable.Provider%2A> para expor o provedor LINQ. Para obter mais informações, consulte os exemplos a seguir os procedimentos abaixo.  
  
 Os procedimentos a seguir fornecem contornos de alto nível para chamar uma função o definida como um método em um objeto de <xref:System.Data.Objects.ObjectContext> e como um método estático em uma classe personalizada. Os exemplos a seguir fornecem mais detalhes sobre as etapas nos procedimentos. Os procedimentos presumem que você definiu uma função no modelo conceitual. Para obter mais informações, confira [Como: Definir funções personalizadas no modelo conceitual](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a>Para chamar uma função o definida como um método em um objeto ObjectContext  
  
1. Adicione um arquivo de origem para estender a classe parcial derivada da classe de <xref:System.Data.Objects.ObjectContext> , gerado automaticamente por ferramentas de Entity Framework. Defina o stub de CLR em um arquivo de origem separado impedirá que as alterações sejam perdidas quando o arquivo for regenerado.  
  
2. Adicione um método do Common Language Runtime (CLR) a sua classe de <xref:System.Data.Objects.ObjectContext> que faz o seguinte:  
  
    - Mapeados para a função definida no modelo conceitual. Para mapear o método, você deve aplicar <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> para o método. Observe que os parâmetros de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> de atributo é o nome do espaço do modelo conceitual e o nome da função no modelo conceitual, respectivamente. A resolução de nomes de função para LINQ diferencia maiúsculas de minúsculas.  
  
    - Retorna os resultados do método de <xref:System.Linq.IQueryProvider.Execute%2A> retornado pela propriedade de <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> .  
  
3. Chame o método como um membro em uma instância da classe de <xref:System.Data.Objects.ObjectContext> .  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a>Para chamar uma função o definida como o método estático em uma classe personalizada  
  
1. Adicionar uma classe ao seu aplicativo com um método estático que faça o seguinte:  
  
    - Mapeados para a função definida no modelo conceitual. Para mapear o método, você deve aplicar <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> para o método. Observe que os parâmetros de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> e de <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> de atributo é o nome do espaço do modelo conceitual e o nome da função no modelo conceitual, respectivamente.  
  
    - Aceita um argumento de <xref:System.Linq.IQueryable> .  
  
    - Retorna os resultados do método de <xref:System.Linq.IQueryProvider.Execute%2A> retornado pela propriedade de <xref:System.Linq.IQueryable.Provider%2A> .  
  
2. Chame o método como um membro um método estático na classe personalizada  
  
## <a name="example"></a>Exemplo  
 **Chamando uma função definida pelo modelo como um método em um objeto ObjectContext**  
  
 O exemplo a seguir demonstra como chamar uma função o definida como um método em um objeto de <xref:System.Data.Objects.ObjectContext> . O exemplo usa o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
 Considere a função do modelo conceitual abaixo do rendimento do produto returns para um produto especificado. (Para obter informações sobre como adicionar a função ao seu modelo conceitual, consulte [como: Definir funções personalizadas no modelo conceitual](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).)  
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a>Exemplo  
 O código a seguir adiciona um método à classe de `AdventureWorksEntities` que mapeia à função de modelo conceitual anterior.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a>Exemplo  
 O código a seguir chama o método anterior para exibir o rendimento de produto para um produto especificado:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como chamar uma função definida modelo que retorna uma coleção (como um objeto de <xref:System.Linq.IQueryable%601> ). Considere a função do modelo conceitual abaixo dos retornos qualquer `SalesOrderDetails` para uma determinada identificação de produto  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a>Exemplo  
 O código a seguir adiciona um método à classe de `AdventureWorksEntities` que mapeia à função de modelo conceitual anterior.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a>Exemplo  
 O código a seguir chama o método. Observe que a consulta é retornado de <xref:System.Linq.IQueryable%601> mais refinados a linha de retorno totais para cada `SalesOrderDetail`.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a>Exemplo  
 **Chamar uma função definida pelo modelo como um método estático em uma classe personalizada**  
  
 O exemplo a seguir demonstra como chamar uma função o definida como um método estático em uma classe personalizada. O exemplo usa o [modelo de vendas AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
> [!NOTE]
>  Quando você chama uma função o definida como um método estático em uma classe personalizada, a função o definida deve aceitar uma coleção e retornar uma agregação dos valores na coleção.  
  
 Considere a função do modelo conceitual abaixo do rendimento do produto returns para uma coleção de SalesOrderDetail. (Para obter informações sobre como adicionar a função ao seu modelo conceitual, consulte [como: Definir funções personalizadas no modelo conceitual](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).).  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a>Exemplo  
 O código a seguir adiciona uma classe ao seu aplicativo que contém um método estático que os mapeamentos para o modelo conceitual funcionem anterior.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a>Exemplo  
 O código a seguir chama o método anterior para exibir o rendimento de produto para uma coleção de SalesOrderDetail:  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a>Consulte também

- [Visão geral do arquivo. edmx](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [Consultas no LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)
- [Chamando funções em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)
