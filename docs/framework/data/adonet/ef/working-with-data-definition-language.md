---
title: Trabalhando com a linguagem de definição de dados
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ec50083d-44f4-4093-9b23-5eacd601f96e
ms.openlocfilehash: da37dc2ff08f127e17cd4e6f7cbeab88f2c8d5e9
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583456"
---
# <a name="working-with-data-definition-language"></a>Trabalhando com a linguagem de definição de dados
Começando com o .NET Framework versão 4, o [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] dá suporte à linguagem de definição de dados (DDL). Isso permite que você crie ou exclua uma instância do banco de dados com base na cadeia de conexão e nos metadados do modelo de armazenamento (SSDL).  
  
 Os métodos a seguir no <xref:System.Data.Objects.ObjectContext> usam a cadeia de conexão e o conteúdo SSDL para criar ou excluir o banco de dados, verificar se o banco de dados existe e exibir o script DDL gerado:  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>  
  
- <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>  
  
- <xref:System.Data.Objects.ObjectContext.CreateDatabaseScript%2A>  
  
> [!NOTE]
>  A execução de comandos DDL pressupõe permissões suficientes.  
  
 Os métodos listados anteriormente delegam a maioria do trabalho para o provedor de dados ADO.NET subjacente. É responsabilidade do provedor garantir que a convenção de nomenclatura usada para gerar objetos de banco de dados seja consistente com as convenções usadas nas consultas e atualizações.  
  
 O exemplo a seguir mostra como gerar o banco de dados com base no modelo existente. Ele também adiciona um novo objeto de entidade ao contexto de objeto e os salva no banco de dados.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-define-a-database-based-on-the-existing-model"></a>Para definir um banco de dados com base no modelo existente  
  
1. Crie um aplicativo de console.  
  
2. Adicione um modelo existente ao seu aplicativo.  
  
    1. Adicionar um modelo vazio chamado `SchoolModel`. Para criar um modelo vazio, consulte o [como: Criar um novo. do EDMX arquivo](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716703(v=vs.100)) tópico.  
  
     O arquivo SchoolModel.edmx é adicionado ao projeto.  
  
    1. Copiar o conceitual, armazenamento e mapeamento de conteúdo para o modelo de escola dos [modelo de escola](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) tópico.  
  
    2. Abra o arquivo SchoolModel.edmx e cole o conteúdo nas marcas `edmx:Runtime`.  
  
3. Adicione o seguinte código à função principal. O código inicializa a cadeia de conexão ao servidor de banco de dados, exibe o script DDL, cria o banco de dados, adiciona uma nova entidade ao contexto e salva as alterações no banco de dados.  
  
     [!code-csharp[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/csharp/VS_Snippets_Data/DP ObjectServices Concepts/CS/Source.cs#ddl)]
     [!code-vb[DP ObjectServices Concepts#DDL](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP ObjectServices Concepts/VB/Source.vb#ddl)]
