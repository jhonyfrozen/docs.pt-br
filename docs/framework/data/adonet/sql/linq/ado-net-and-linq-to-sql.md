---
title: O ADO.NET e LINQ to SQL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49ac6da0-f2e1-46fa-963e-1b6dcb63fef7
ms.openlocfilehash: 4f2f9fa1cb1be421be57ae0671573150871ebd1d
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65880476"
---
# <a name="adonet-and-linq-to-sql"></a>O ADO.NET e LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] faz parte da família de tecnologias do ADO.NET. Ele se baseia em serviços fornecidos pelo modelo de provedor do ADO.NET. Portanto, você pode misturar [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] de código com aplicativos existentes do ADO.NET e migrar soluções atuais do ADO.NET para [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. A ilustração a seguir fornece uma exibição de alto nível de relacionamento.  
  
 ![LINQ to SQL e ADO.NET](../../../../../../docs/framework/data/adonet/sql/linq/media/dlinq-3.png "DLinq_3")  
  
## <a name="connections"></a>Conexões  
 Você pode fornecer uma conexão ADO.NET existente quando você cria um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.DataContext>. Todas as operações em relação a <xref:System.Data.Linq.DataContext> (incluindo consultas) usam isso fornecido a conexão. Se a conexão já está aberto, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] deixa a cargo como é quando tiver terminado com ele.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
 Você sempre pode acessar a conexão e fechá-lo você mesmo usando a propriedade de <xref:System.Data.Linq.DataContext.Connection%2A> , como no código a seguir:  
  
 [!code-csharp[DLinqAdoNet#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#1)]
 [!code-vb[DLinqAdoNet#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#1)]  
  
## <a name="transactions"></a>Transações  
 Você pode fornecer seu <xref:System.Data.Linq.DataContext> com sua própria transação de base de dados quando seu aplicativo é iniciado na transação e você deseja que o <xref:System.Data.Linq.DataContext> a ser empacotado.  
  
 O método preferido de fazer transações com o .NET Framework é usar o <xref:System.Transactions.TransactionScope> objeto. Usando essa abordagem, você pode fazer as transações distribuídas que funcionam através de bases de dados e outros gerentes de recurso de memória residente. Escopos de transação exigem alguns recursos iniciar. Elevam-se a transações distribuídas somente quando há várias conexões dentro do escopo da transação.  
  
 [!code-csharp[DLinqAdoNet#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#2)]
 [!code-vb[DLinqAdoNet#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#2)]  
  
 Você não pode usar essa abordagem para todos os bases de dados. Por exemplo, a conexão SqlClient não pode elevar transações do sistema quando trabalha em um servidor de [!INCLUDE[ss2k](../../../../../../includes/ss2k-md.md)] . Em vez disso, inscreve-se automaticamente para uma transação completa, distribuído consulta sempre que um escopo de transação que está sendo usado.  
  
## <a name="direct-sql-commands"></a>Comandos SQL diretos  
 Às vezes você pode encontrar situações onde a capacidade de <xref:System.Data.Linq.DataContext> de consulte ou enviar alterações insuficientes para a tarefa específica que você deseja executar. Nesteas circunstâncias você pode usar o método de <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> para emitir comandos SQL a base de dados e para converter os resultados da consulta a objetos.  
  
 Por exemplo, suponha que os dados para a classe de `Customer` são espalhado sobre duas tabelas (customer1 e customer2). A seguinte consulta retorna uma sequência de objetos `Customer` :  
  
 [!code-csharp[DLinqAdoNet#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#3)]
 [!code-vb[DLinqAdoNet#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#3)]  
  
 Desde que os nomes de coluna nos resultados tabulares coincidam propriedades da coluna de sua classe de entidade, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] cria seus objetos a partir de qualquer consulta SQL.  
  
### <a name="parameters"></a>Parâmetros  
 O método de <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> aceita parâmetros. O código a seguir executa uma consulta parametrizada:  
  
 [!code-csharp[DlinqAdoNet#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#4)]
 [!code-vb[DlinqAdoNet#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#4)]  
  
> [!NOTE]
>  Os parâmetros são expressos no texto da consulta usando a mesma notação encaracolado usada por `Console.WriteLine()` e por `String.Format()`. `String.Format()` leva a cadeia de caracteres de consulta que você fornece e substitui os parâmetros encaracolado- apoiados com nomes de parâmetro gerados como `@p0`, `@p1` …, `@p(n)`.  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)
- [Como: Reutilizar uma Conexão entre um comando ADO.NET e um DataContext](../../../../../../docs/framework/data/adonet/sql/linq/how-to-reuse-a-connection-between-an-ado-net-command-and-a-datacontext.md)
