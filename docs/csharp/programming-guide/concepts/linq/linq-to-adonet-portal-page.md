---
title: LINQ to ADO.NET (página do portal)
ms.date: 07/20/2015
ms.assetid: 6bd269b4-3509-4688-b672-836008704182
ms.openlocfilehash: b21d19aaa0b470bd59acb59c84b0777d099e6274
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67307170"
---
# <a name="linq-to-adonet-portal-page"></a>LINQ to ADO.NET (página do portal)
O [!INCLUDE[linq_adonet](~/includes/linq-adonet-md.md)] permite que você realize consultas em qualquer objeto enumerável em ADO.NET usando o modelo de programação [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)].  
  
> [!NOTE]
>  A documentação do [!INCLUDE[linq_adonet](~/includes/linq-adonet-md.md)] está localizada na seção ADO.NET do SDK do .NET Framework: [LINQ e ADO.NET](../../../../framework/data/adonet/linq-and-ado-net.md).  
  
 Há três tecnologias separadas do [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] do ADO.NET: [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)], [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] e [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)]. O [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)] fornece consultas mais sofisticadas e otimizadas do que o <xref:System.Data.DataSet>, o [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] permite que você consulte diretamente os esquemas de banco de dados do SQL Server e o [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)] permite que você consulte um Modelo de Dados de Entidade.  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 O <xref:System.Data.DataSet> é um dos componentes mais amplamente usados em ADO.NET e é um elemento fundamental do modelo de programação desconectada no qual o ADO.NET se baseia. No entanto, apesar dessa importância, o <xref:System.Data.DataSet> limitou os recursos de consulta.  
  
 O [!INCLUDE[linq_dataset](~/includes/linq-dataset-md.md)] permite que você crie mais recursos sofisticados de consulta no <xref:System.Data.DataSet> usando a mesma funcionalidade de consulta que está disponível para muitas outras fontes de dados.  
  
 Para obter mais informações, consulte [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md).  
  
## <a name="linq-to-sql"></a>LINQ to SQL  
 O [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] fornece uma infraestrutura em tempo de execução para gerenciar dados relacionais como objetos. No [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)], o modelo de dados de um banco de dados relacional é mapeado para um modelo de objeto expresso na linguagem de programação do desenvolvedor. Quando você executa o aplicativo, o [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] converte consultas integradas da linguagem no modelo de objeto no SQL e as envia para o banco de dados para execução. Quando o banco de dados retorna os resultados, o [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] os converte em objetos que podem ser manipulados.  
  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] inclui suporte para procedimentos armazenados e funções definidas pelo usuário no banco de dados e para herança no modelo de objeto.  
  
 Para obter mais informações, consulte [LINQ to SQL](../../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
## <a name="linq-to-entities"></a>LINQ to Entities  
 Por meio do Modelo de Dados de Entidade, os dados relacionais são expostos como objetos no ambiente .NET. Isso torna a camada do objeto um destino ideal para o suporte do [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] permitindo que os desenvolvedores formulem consultas no banco de dados na linguagem usada para criar a lógica de negócios. Esse recurso é conhecido como [!INCLUDE[linq_entities](~/includes/linq-entities-md.md)]. Consulte [LINQ to Entities](../../../../framework/data/adonet/ef/language-reference/linq-to-entities.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também

- [LINQ e ADO.NET](../../../../framework/data/adonet/linq-and-ado-net.md)
- [LINQ (consulta integrada à linguagem) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)
