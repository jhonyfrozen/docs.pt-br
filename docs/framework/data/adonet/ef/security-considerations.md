---
title: Considerações de segurança (Entity Framework)
ms.date: 03/30/2017
ms.assetid: 84758642-9b72-4447-86f9-f831fef46962
ms.openlocfilehash: cf42787d7cc67d80f43a08b5fa71161fee20f5c3
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539831"
---
# <a name="security-considerations-entity-framework"></a>Considerações de segurança (Entity Framework)
Este tópico descreve considerações de segurança específicas para desenvolver, implantar e executar aplicativos [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Você também deve seguir as recomendações para criar aplicativos seguros do .NET Framework. Para obter mais informações, consulte [visão geral de segurança](../../../../../docs/framework/data/adonet/security-overview.md).  
  
## <a name="general-security-considerations"></a>Considerações gerais de segurança  
 As considerações de segurança a seguir se aplicam a todos os aplicativos que usam o [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
#### <a name="use-only-trusted-data-source-providers"></a>Use apenas provedores de fontes de dados confiáveis.  
 Para se comunicar com a fonte de dados, um provedor deve fazer o seguinte:  
  
- Receber a cadeia de conexão do [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
- Converter a árvore de comandos na linguagem de consulta nativa da fonte de dados.  
  
- Reunir e retornar conjuntos de resultados.  
  
 Durante a operação de logon, as informações baseadas na senha do usuário são passadas para o servidor através das bibliotecas de rede da fonte de dados subjacente. Um provedor mal-intencionado pode roubar credenciais do usuário, gerar consultas mal-intencionadas ou violar o conjunto de resultados.  
  
#### <a name="encrypt-your-connection-to-protect-sensitive-data"></a>Criptografe sua conexão para proteger dados confidenciais.  
 O [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] não trata diretamente da criptografia de dados. Se os usuários acessam dados por uma rede pública, seu aplicativo deve estabelecer uma conexão criptografada com a fonte de dados para aumentar a segurança. Para obter mais informações, consulte a documentação relacionada à segurança da sua fonte de dados. Para uma fonte de dados do SQL Server, consulte [criptografando conexões com o SQL Server](https://go.microsoft.com/fwlink/?LinkId=119544).  
  
#### <a name="secure-the-connection-string"></a>Proteja a cadeia de conexão.  
 A proteção do acesso à fonte de dados é essencial para a segurança do aplicativo. Uma cadeia de conexão é potencialmente vulnerável caso não esteja protegida ou se tiver sido construída incorretamente. Quando você armazena informações de conexão em texto sem formatação ou persiste essas informações na memória, corre o risco de comprometer seu sistema inteiro. Os seguintes métodos são recomendados para proteger cadeias de conexão:  
  
- Usar a Autenticação do Windows com uma fonte de dados do SQL Server.  
  
     Quando você usa a Autenticação do Windows para se conectar a uma fonte de dados do SQL Server, a cadeia de conexão não contém informações de logon e de senha.  
  
- Criptografar seções de arquivos de configuração usando configuração protegida.  
  
     O ASP.NET fornece um recurso chamado configuração protegida que permite criptografar informações confidenciais em um arquivo de configuração. Embora esse recurso tenha sido basicamente projetado para ASP.NET, você também pode usá-lo para criptografar seções de arquivos de configuração em aplicativos do Windows. Para obter uma descrição detalhada dos novos recursos de configuração protegida, consulte [Criptografando informações de configuração usando configuração protegida](https://docs.microsoft.com/previous-versions/aspnet/53tyfkaw(v=vs.100)).  
  
- Armazenar cadeias de conexão em arquivos de configuração protegida.  
  
     Você nunca deve inserir cadeias de conexão no código-fonte. Você pode armazenar cadeias de conexão em arquivos de configuração, o que elimina a necessidade de inseri-las no código do aplicativo. Por padrão, o Assistente do Modelo de Dados de Entidade armazena cadeias de conexão no arquivo de configuração do aplicativo. É necessário proteger esse arquivo para impedir o acesso não autorizado.  
  
- Usar construtores de cadeias de conexão para criar conexões dinamicamente.  
  
     Se você precisar criar cadeias de conexão em tempo de execução, use a classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder>. Essa classe de construtor de cadeias de caracteres ajuda a evitar ataques de injeção de cadeias de conexão validando e escapando informações de entrada inválidas. Para obter mais informações, confira [Como: Compilar uma cadeia de Conexão EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md). Também usar a classe de construtor de cadeia de caracteres apropriada para construir a cadeia de conexão de fonte de dados que faz parte do [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] cadeia de caracteres de conexão. Para obter informações sobre construtores de cadeia de caracteres de conexão para provedores ADO.NET, consulte [construtores de cadeia de Conexão](../../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
 Para obter mais informações, consulte [Protegendo informações de conexão](../../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
#### <a name="do-not-expose-an-entityconnection-to-untrusted-users"></a>Não exponha um objeto EntityConnection a usuários não confiáveis.  
 Um objeto <xref:System.Data.EntityClient.EntityConnection> expõe a cadeia de conexão subjacente. Um usuário com acesso a um objeto <xref:System.Data.EntityClient.EntityConnection> também pode alterar o <xref:System.Data.ConnectionState> da conexão subjacente. A classe <xref:System.Data.EntityClient.EntityConnection> não é segura para threads.  
  
#### <a name="do-not-pass-connections-outside-the-security-context"></a>Não passe conexões fora do contexto de segurança.  
 Após uma conexão ser estabelecida, você não deve passá-la fora do contexto de segurança. Por exemplo, um thread com permissão para abrir uma conexão não deve armazenar a conexão em um local global. Se a conexão estiver disponível em um local global, então outro thread mal-intencionado poderá usar a conexão aberta sem ter a permissão explícita para isso.  
  
#### <a name="be-aware-that-logon-information-and-passwords-may-be-visible-in-a-memory-dump"></a>Esteja ciente de que informações de logon e senhas podem ser visíveis em um despejo de memória.  
 Quando informações de logon e de senha da fonte de dados são especificadas na cadeia de conexão, essas informações são mantidas na memória até que a coleta de lixo recupere os recursos. Isso impossibilita determinar quando uma cadeia de caracteres de senha não está mais na memória. Se um aplicativo falha, um arquivo de despejo de memória pode conter informações de segurança confidenciais, e o usuário que executa o aplicativo e qualquer usuário com acesso administrativo ao computador podem exibir o arquivo de despejo de memória. Use a Autenticação do Windows para conexões com o Microsoft SQL Server.  
  
#### <a name="grant-users-only-the-necessary-permissions-in-the-data-source"></a>Conceda aos usuários apenas as permissões necessárias para a fonte de dados.  
 Um administrador de fonte de dados deve conceder somente as permissões necessárias aos usuários. Embora [!INCLUDE[esql](../../../../../includes/esql-md.md)] não dê suporte a instruções DML que modificam dados, como INSERT, UPDATE ou DELETE, os usuários ainda podem acessar a conexão com a fonte de dados. Um usuário mal-intencionado pode usar essa conexão para executar instruções DML na linguagem nativa da fonte de dados.  
  
#### <a name="run-applications-with-the-minimum-permissions"></a>Execute aplicativos com as permissões mínimas.  
 Quando você permite que um aplicativo gerenciado ser executado com permissão de confiança total, o .NET Framework não limita o acesso do aplicativo em seu computador. Isso pode tornar vulnerável a segurança do seu aplicativo e comprometer o sistema inteiro. Para usar a segurança de acesso do código e outros mecanismos de segurança no .NET Framework, você deve executar aplicativos usando permissões de confiança parcial e com o conjunto mínimo de permissões que são necessárias para habilitar o aplicativo funcione. As seguintes permissões de acesso do código são as permissões mínimas que seu aplicativo [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] precisa:  
  
- <xref:System.Security.Permissions.FileIOPermission>: <xref:System.Security.Permissions.FileIOPermissionAccess.Write> para abrir os arquivos de metadados especificados ou <xref:System.Security.Permissions.FileIOPermissionAccess.PathDiscovery> para pesquisar arquivos de metadados em um diretório.  
  
- <xref:System.Security.Permissions.ReflectionPermission>: <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess> para dar suporte a consultas LINK to Entities.  
  
- <xref:System.Transactions.DistributedTransactionPermission>: <xref:System.Security.Permissions.PermissionState.Unrestricted> para se inscrever em uma <xref:System.Transactions><xref:System.Transactions.Transaction>.  
  
- <xref:System.Security.Permissions.SecurityPermission>: <xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter> para serializar exceções usando a interface <xref:System.Runtime.Serialization.ISerializable>.  
  
- Permissão para abrir uma conexão de banco de dados e executar comandos no banco de dados, tais como <xref:System.Data.SqlClient.SqlClientPermission> para um banco de dados do SQL Server.  
  
 Para obter mais informações, consulte [Segurança de acesso do código e ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md).  
  
#### <a name="do-not-install-untrusted-applications"></a>Não instale aplicativos não confiáveis.  
 O [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] não impõe permissões de segurança e invoca qualquer código de objeto de dados fornecido pelo usuário no processo, independentemente de ser ou não confiável. Verifique se a autenticação e a autorização do cliente são executadas pelo repositório de dados e por seu aplicativo.  
  
#### <a name="restrict-access-to-all-configuration-files"></a>Restrinja o acesso a todos os arquivos de configuração.  
 Um administrador deve restringir o acesso de gravação para o arquivo de configuração de aplicativo e de todos os arquivos que especificam a configuração de um aplicativo, incluindo Enterprisesec. config, Security. config, Machine. conf \< *aplicativo* >. exe.  
  
 O nome invariável do provedor pode ser modificado no arquivo app.config. O aplicativo cliente deve assumir a responsabilidade de acessar o provedor subjacente por meio do modelo padrão de fábrica do provedor usando um nome forte.  
  
#### <a name="restrict-permissions-to-the-model-and-mapping-files"></a>Restrinja permissões aos arquivos de modelo e de mapeamento.  
 Um administrador deve restringir o acesso para gravação nos arquivos de modelo e de mapeamento (.edmx, .csdl, .ssdl e .msl) somente aos usuários que alteram o modelo ou os mapeamentos. O [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] só requer acesso de leitura a esses arquivos em tempo de execução. Um administrador também deve restringir o acesso à camada de objeto e arquivos código-fonte pré-compilados do modo de exibição que são gerados pelas ferramentas do modelo de dados de entidade.  
  
## <a name="security-considerations-for-queries"></a>Considerações de segurança para consultas  
 As considerações de segurança a seguir se aplicam em consultas a um modelo conceitual. Essas considerações se aplicam a consultas [!INCLUDE[esql](../../../../../includes/esql-md.md)] usando EntityClient e a consultas de objeto usando LINQ, [!INCLUDE[esql](../../../../../includes/esql-md.md)] e métodos de construtor de consultas.  
  
#### <a name="prevent-sql-injection-attacks"></a>Evite ataques de injeção de SQL.  
 Os aplicativos normalmente obtêm entrada externa (de um usuário ou de outro agente externo) e executam ações com base nessa entrada. Qualquer entrada que seja derivada direta ou indiretamente do usuário ou de um agente externo pode ter conteúdo que usa a sintaxe da linguagem de destino para executar ações não autorizadas. Quando o idioma de destino é uma linguagem SQL (Structured Query), como Transact-SQL, essa manipulação é conhecida como um ataque de injeção de SQL. Um usuário mal-intencionado pode injetar comandos diretamente na consulta e remover uma tabela de banco de dados, causar uma negação de serviço ou alterar a natureza da operação que está sendo executada.  
  
- Ataques de injeção de [!INCLUDE[esql](../../../../../includes/esql-md.md)]:  
  
     Os ataques de injeção de SQL podem ser executados em [!INCLUDE[esql](../../../../../includes/esql-md.md)] fornecendo entrada mal-intencionada para valores que são usados em um predicado de consulta e em nomes de parâmetro. Para evitar o risco de injeção de SQL, você nunca deve combinar a entrada do usuário com o texto de comando de [!INCLUDE[esql](../../../../../includes/esql-md.md)].  
  
     As consultas [!INCLUDE[esql](../../../../../includes/esql-md.md)] aceitam parâmetros em todas as partes onde literais são aceitos. Você deve usar consultas parametrizadas, em vez de injetar literais de um agente externo diretamente na consulta. Você também deve considerar o uso [métodos de construtor de consulta](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896238(v=vs.100)) para construir o Entity SQL com segurança.  
  
- LINQ a ataques de injeção de entidades:  
  
     Embora a composição de consultas seja possível em LINQ to Entities, ela é executada por meio da API de modelo de objeto. Ao contrário de [!INCLUDE[esql](../../../../../includes/esql-md.md)] consultas, consultas LINQ to Entities não são compostas por meio da manipulação de cadeia de caracteres ou concatenação, e eles não são suscetíveis a tradicionais ataques de injeção de SQL.  
  
#### <a name="prevent-very-large-result-sets"></a>Evite conjuntos de resultados muito grandes.  
 Um conjunto de resultados muito grande pode fazer com que o sistema cliente seja desligado se o cliente estiver executando operações que consomem recursos proporcionais ao tamanho do conjunto de resultados. Conjuntos de resultados inesperadamente grandes podem ocorrer nas seguintes condições:  
  
- Em consultas a um banco de dados grande que não incluem as condições apropriadas de filtragem.  
  
- Em consultas que criam junções cartesianas no servidor.  
  
- Em consultas [!INCLUDE[esql](../../../../../includes/esql-md.md)] aninhadas.  
  
 Ao aceitar a entrada do usuário, verifique se a entrada não pode fazer com que os conjuntos de resultados se tornem maiores do que o sistema pode manipular. Você também pode usar o <xref:System.Linq.Queryable.Take%2A> método em LINQ to Entities ou o [limite](../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) operador em [!INCLUDE[esql](../../../../../includes/esql-md.md)] para limitar o tamanho do conjunto de resultados.  
  
#### <a name="avoid-returning-iqueryable-results-when-exposing-methods-to-potentially-untrusted-callers"></a>Evite retornar resultados IQueryable ao expor métodos a chamadores potencialmente não confiáveis.  
 Evite retornar tipos <xref:System.Linq.IQueryable%601> de métodos expostos a chamadores potencialmente não confiáveis pelos seguintes motivos:  
  
- Um consumidor de uma consulta que expõe um tipo <xref:System.Linq.IQueryable%601> pode chamar métodos no resultado que expõem dados seguros ou aumentam o tamanho do conjunto de resultados. Por exemplo, considere a seguinte assinatura de método:  
  
    ```  
    public IQueryable<Customer> GetCustomer(int customerId)  
    ```  
  
     Um consumidor dessa consulta pode chamar `.Include("Orders")` em `IQueryable<Customer>` retornado para recuperar os dados que a consulta não pretende expor. Para evitar isso, é possível alterar o tipo de retorno do método para <xref:System.Collections.Generic.IEnumerable%601> e chamar um método (como `.ToList()`) que materialize os resultados.  
  
- Como as consultas <xref:System.Linq.IQueryable%601> são executadas quando os resultados são iterados, um consumidor de uma consulta que expõe um tipo <xref:System.Linq.IQueryable%601> pode capturar exceções geradas. As exceções podem conter informações não dirigidas ao consumidor.  
  
## <a name="security-considerations-for-entities"></a>Considerações de segurança para entidades  
 As considerações de segurança a seguir se aplicam ao gerar e trabalhar com tipos de entidade.  
  
#### <a name="do-not-share-an-objectcontext-across-application-domains"></a>Não compartilhe um ObjectContext entre domínios do aplicativo.  
 O compartilhamento de um <xref:System.Data.Objects.ObjectContext> com mais de um domínio do aplicativo pode expor informações na cadeia de conexão. Em vez disso, transfira objetos serializados ou grafos de objetos para o outro domínio do aplicativo e depois anexe esses objetos a um <xref:System.Data.Objects.ObjectContext> nesse domínio do aplicativo. Para obter mais informações, consulte [serializar objetos](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738446(v=vs.100)).  
  
#### <a name="prevent-type-safety-violations"></a>Evite violações de segurança de tipos.  
 Se a segurança de tipo for violada, o [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] não poderá garantir a integridade dos dados em objetos. As violações de segurança de tipo podem ocorrer se você permitir que aplicativos não confiáveis sejam executados com segurança de acesso do código de confiança total.  
  
#### <a name="handle-exceptions"></a>Trate exceções.  
 Acesse métodos e propriedades de um <xref:System.Data.Objects.ObjectContext> dentro de um bloco try-catch. A captura de exceções impede que exceções não tratadas exponham entradas no <xref:System.Data.Objects.ObjectStateManager> ou informações de modelo (como nomes de tabela) aos usuários do seu aplicativo.  
  
## <a name="security-considerations-for-aspnet-applications"></a>Considerações de segurança para aplicativos ASP.NET  

Você deve considerar o seguinte ao trabalhar com caminhos em aplicativos ASP.NET.  
  
#### <a name="verify-whether-your-host-performs-path-checks"></a>Confira se o host executa verificações de caminho.  
 Quando o `|DataDirectory|` (delimitado por símbolos de pipe) é usada a cadeia de caracteres de substituição, ADO.NET verifica que o caminho resolvido é suportado. Por exemplo, ".." não é permitido atrás de `DataDirectory`. Essa mesma verificação para resolver o operador raiz do aplicativo Web (`~`) é executada pelo processo de hospedagem do ASP.NET. O IIS executa essa verificação; No entanto, os hosts que não seja o IIS não podem verificar que o caminho resolvido é suportado. Você deve conhecer o comportamento do host no qual implantar um aplicativo [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
#### <a name="do-not-make-assumptions-about-resolved-path-names"></a>Não faça suposições sobre nomes de caminho resolvidos.  
 Embora os valores para os quais o operador raiz (`~`) e a cadeia de caracteres de substituição `DataDirectory` são resolvidos devam permanecer constantes durante o tempo de execução do aplicativo, o [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] não impede que o host modifique esses valores.  
  
#### <a name="verify-the-path-length-before-deployment"></a>Verifique o comprimento do caminho antes da implantação.  
 Antes de implantar um aplicativo [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)], verifique se os valores do operador raiz (~) e da cadeia de caracteres de substituição `DataDirectory` não excedem os limites de comprimento de caminho no sistema operacional. Provedores de dados ADO.NET não garantem que o comprimento do caminho esteja dentro dos limites válidos.  
  
## <a name="security-considerations-for-adonet-metadata"></a>Considerações de segurança para metadados ADO.NET  
 As considerações de segurança a seguir se aplicam ao gerar e trabalhar com arquivos de modelo e de mapeamento.  
  
#### <a name="do-not-expose-sensitive-information-through-logging"></a>Não exponha informações confidenciais em logs.  
Componentes de serviço de metadados ADO.NET não faça qualquer informação particular. Se houver resultados que não possam ser retornados devido às restrições de acesso, os sistemas de gerenciamento de bancos de dados e os sistemas de arquivos retornarão um número zero de resultados, em vez de gerar uma exceção que possa conter informações confidenciais.  
  
#### <a name="do-not-accept-metadataworkspace-objects-from-untrusted-sources"></a>Não aceite objetos MetadataWorkspace de fontes não confiáveis.  
 Os aplicativos não devem aceitar instâncias da classe <xref:System.Data.Metadata.Edm.MetadataWorkspace> de fontes não confiáveis. Em vez disso, você deve construir e popular explicitamente um workspace como fonte.  
  
## <a name="see-also"></a>Consulte também

- [Securing ADO.NET Applications](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md) (Protegendo aplicativos ADO.NET)
- [Considerações de implantação](../../../../../docs/framework/data/adonet/ef/deployment-considerations.md)
- [Considerações sobre migração](../../../../../docs/framework/data/adonet/ef/migration-considerations.md)
