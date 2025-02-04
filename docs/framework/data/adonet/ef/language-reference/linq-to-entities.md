---
title: LINQ to Entities
ms.date: 03/30/2017
ms.assetid: 641f9b68-9046-47a1-abb0-1c8eaeda0e2d
ms.openlocfilehash: 8a69d74966b99d78b4a7addaa4323d61d82ce8d5
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539767"
---
# <a name="linq-to-entities"></a>LINQ to Entities
O LINQ to Entities fornece suporte a LINQ (Consulta Integrada à Linguagem) que permite aos desenvolvedores escreverem consultas no modelo conceitual do Entity Framework usando Visual Basic ou Visual C#. As consultas no Entity Framework são representadas por consultas de árvore de comando, que são executadas no contexto de objeto. O LINQ to Entities converte consultas do LINQ (Consulta Integrada à Linguagem) para consultas de árvore de comando, executa as consultas no Entity Framework e retorna os objetos que podem ser usados pelo Entity Framework e pelo LINQ. Veja a seguir o processo para criar e executar uma consulta LINQ to Entities:  
  
1. Construa uma instância <xref:System.Data.Objects.ObjectQuery%601> do <xref:System.Data.Objects.ObjectContext>.  
  
2. Componha uma consulta LINQ to Entities no C# ou Visual Basic usando a instância <xref:System.Data.Objects.ObjectQuery%601>.  
  
3. Converta operadores e expressões padrão de consulta LINQ para árvores de comando.  
  
4. Execute a consulta, na representação da árvore de comando, na fonte de dados. Todas as exceções geradas na fonte de dados durante a execução são passadas diretamente até o cliente.  
  
5. Retorne os resultados da consulta de volta para o cliente.  
  
## <a name="constructing-an-objectquery-instance"></a>Construindo uma instância de ObjectQuery  
 A classe genérica <xref:System.Data.Objects.ObjectQuery%601> representa uma consulta que retorna uma coleção de zero ou mais entidades tipadas. Uma consulta de objeto é construída normalmente de um contexto de objeto existente, em vez de ser construído manualmente, e sempre pertence ao contexto de objeto. Esse contexto fornece a conexão e as informações de metadados necessárias para compor e executar a consulta. A classe genérica <xref:System.Data.Objects.ObjectQuery%601> implementa a interface genérica <xref:System.Linq.IQueryable%601>, cujos métodos de construtor habilitam as consultas LINQ para serem criadas incrementalmente. Você também pode permitir que o compilador infira o tipo de entidade usando a palavra-chave `var` do C# (`Dim` no Visual Basic, com inferência de tipo de local habilitada).  
  
## <a name="composing-the-queries"></a>Compondo as consultas  
 As instâncias da classe genérica <xref:System.Data.Objects.ObjectQuery%601>, que implementa a interface de <xref:System.Linq.IQueryable%601>, funcionam como a fonte de dados para consultas LINQ to Entities. Em uma consulta, você especifica exatamente as informações que deseja recuperar da fonte de dados. Uma consulta também pode especificar como essas informações devem ser classificadas, agrupadas e moldadas antes de serem retornadas. No LINQ, uma consulta é armazenada em uma variável. Essa variável de consulta não toma nenhuma ação e não retorna nenhum dado, ela apenas armazena as informações da consulta. Depois de criar uma consulta, você deve executá-la para recuperar todos os dados.  
  
 As consultas LINQ to Entities podem ser compostas de duas sintaxes diferentes: sintaxe de expressão de consulta e sintaxe de consulta baseada em método. A sintaxe da expressão de consulta e a sintaxe da consulta com base em método são novidades no C# 3.0 e no Visual Basic 9.0.  
  
 Para obter mais informações, consulte [consultas no LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md).  
  
## <a name="query-conversion"></a>Conversão de consulta  
 Para executar uma consulta LINQ to Entities no Entity Framework, a consulta LINQ deve ser convertida em uma representação de árvore de comando que pode ser executada no Entity Framework.  
  
 Consultas LINQ to Entities são compostas de operadores de consulta padrão LINQ (como <xref:System.Linq.Queryable.Select%2A>, <xref:System.Linq.Queryable.Where%2A>, e <xref:System.Linq.Queryable.GroupBy%2A>) e expressões (x > 10, Contact e assim por diante). Os operadores LINQ não são definidos por uma classe, mas são métodos em uma classe. No LINQ, as expressões podem conter tudo o que é permitido por tipos dentro do namespace <xref:System.Linq.Expressions> e, por extensão, tudo o que pode ser representado em uma função lambda. Este é um superconjunto de expressões que são permitidas pelo Entity Framework, que são restritas por definição para as operações permitidas no banco de dados, e têm suporte pelo <xref:System.Data.Objects.ObjectQuery%601>.  
  
 No Entity Framework, os operadores e as expressões são representados por uma única hierarquia de tipo, que são colocadas em uma árvore de comando. A árvore de comando é usada pelo Entity Framework para executar a consulta. Se a consulta LINQ não puder ser expressada como uma árvore de comando, uma exceção será gerada quando a consulta estiver sendo convertida. A conversão de consultas LINQ to Entities envolve duas subconversões: a conversão dos operadores de consulta padrão e a conversão das expressões.  
  
 Há um número de operadores padrão de consulta LINQ que não têm uma tradução válida no LINQ to Entities. As tentativas de usar esses operadores resultarão em uma exceção em tempo de tradução de consulta. Para obter uma lista com suporte operadores LINQ to Entities, consulte [com suporte e os métodos LINQ (LINQ to Entities)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md).  
  
 Para obter mais informações sobre como usar os operadores de consulta padrão no LINQ to Entities, consulte [operadores de consulta padrão em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md).  
  
 Em geral, as expressões no LINQ to Entities são avaliadas no servidor. Portanto, não se deve esperar que o comportamento da expressão siga a semântica de CLR. Para obter mais informações, consulte [expressões em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md).  
  
 Para obter informações sobre como as chamadas de método do CLR são mapeadas para funções canônicas na fonte de dados, consulte [método CLR ao mapeamento canônico de função](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md).  
  
 Para obter informações sobre como chamar canônico, banco de dados e funções personalizadas de dentro do LINQ para consultas de entidades, consulte [chamando funções em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md).  
  
## <a name="query-execution"></a>Execução da Consulta  
 Depois que a consulta LINQ é criada pelo usuário, ela é convertida para uma representação que está compatível com o Entity Framework (na forma de árvores de comando), que é, em seguida, executado na fonte de dados. No tempo de execução de consulta, todas as expressões de consulta (ou componentes da consulta) são avaliados no cliente ou no servidor. Isso inclui as expressões que são usadas na materialização de resultados ou projeções de entidade. Para obter mais informações, consulte [execução de consulta](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md). Para obter informações sobre como melhorar o desempenho ao compilar uma consulta uma vez e, em seguida, executá-la várias vezes com parâmetros diferentes, consulte [consultas compiladas (LINQ to Entities)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md).  
  
## <a name="materialization"></a>Materialização  
 A materialização é o processo de retornar resultados de consulta de volta para o cliente como tipos CLR. No LINQ to Entities, os registros de dados dos resultados da consulta nunca são retornados; há sempre um tipo CLR de suporte, definido pelo usuário ou pelo Entity Framework, ou gerado pelo compilador (tipos anônimos). Qualquer materialização de objeto é executada pelo Entity Framework. Todos os erros que resultarem de uma incapacidade de mapear entre o Entity Framework e o CLR gerarão exceções durante a materialização do objeto.  
  
 Os resultados da consulta são geralmente retornados como um dos seguintes:  
  
- Uma coleção de zero ou mais objetos de entidade tipados ou uma projeção de tipos complexos definidos no modelo conceitual.  
  
- Tipos CLR que têm suporte pelo [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)].  
  
- Coleções internas.  
  
- Tipos anônimos.  
  
 Para obter mais informações, consulte [resultados da consulta](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Consultas no LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)  
  
 [Expressões em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md)  
  
 [Chamando funções em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)  
  
 [Consultas compiladas (LINQ to Entities)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md)  
  
 [Execução de consulta](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md)  
  
 [Resultados da Consulta](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md)  
  
 [Operadores de consulta padrão em consultas LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md)  
  
 [Método CLR para mapeamento de função canônica](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md)  
  
 [Métodos LINQ com e sem suporte (LINQ to Entities)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)  
  
 [Problemas conhecidos e considerações no LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)  
  
## <a name="see-also"></a>Consulte também

- [Problemas conhecidos e considerações no LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)
- [LINQ (consulta integrada à linguagem) – C#](../../../../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ (consulta integrada à linguagem) – Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ e ADO.NET](../../../../../../docs/framework/data/adonet/linq-and-ado-net.md)
- [Entity Framework do ADO.NET](../../../../../../docs/framework/data/adonet/ef/index.md)
