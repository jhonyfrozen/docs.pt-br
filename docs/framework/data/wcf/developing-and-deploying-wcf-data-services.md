---
title: Desenvolvendo e implantando WCF Data Services
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- deploying [WCF Data Services
- developing applications [WCF Data Services]
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
ms.openlocfilehash: ef38bacfd129033aab41f5f516b96b95fac7913f
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65880002"
---
# <a name="develop-and-deploy-wcf-data-services"></a>Desenvolva e implante o WCF Data Services

Este tópico fornece informações sobre como desenvolver e implantando WCF Data Services. Para obter mais informações sobre o WCF Data Services, consulte [guia de Introdução](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md) e [visão geral](../../../../docs/framework/data/wcf/wcf-data-services-overview.md).

## <a name="develop-wcf-data-services"></a>Desenvolver um WCF Data Services

Quando você usa o WCF Data Services para criar um serviço de dados que oferece suporte a [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)], você deve executar as seguintes tarefas básicas durante o desenvolvimento:

1. **Definir o modelo de dados**

     WCF Data Services dá suporte a uma variedade de provedores de serviço de dados que permitem que você definir um modelo de dados com base nos dados de uma variedade de fontes de dados, de bancos de dados relacionais a tipos de dados de associação tardia. Para obter mais informações, consulte [provedores de serviços de dados](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md).

2. **Criar o serviço de dados**

     O serviço de dados mais básico expõe uma classe herdada da classe <xref:System.Data.Services.DataService%601>, com um tipo `T` que é o nome qualificado para namespace do contêiner de entidade. Para obter mais informações, consulte [definindo o WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md).

3. **Configurar o serviço de dados**

     Por padrão, o WCF Data Services desabilita o acesso aos recursos que são expostos por um contêiner de entidade. O <xref:System.Data.Services.DataServiceConfiguration> interface permite que você configure o acesso aos recursos e operações de serviço, especifique a versão compatível do OData e para definir outros comportamentos de serviços, como comportamentos de lote ou o número máximo de entidades que podem ser retornados em um feed de resposta única. Para obter mais informações, consulte [Configurando o serviço de dados](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md).

Este tópico aborda primeiramente o desenvolvimento e implantação dos serviços de dados usando o Visual Studio. Para obter informações sobre a flexibilidade fornecida pelo WCF Data Services para expor seus dados como feeds OData, consulte [definindo o WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md).

### <a name="choose-a-development-web-server"></a>Escolha um servidor Web de desenvolvimento

Ao desenvolver um WCF Data Service como um aplicativo ASP.NET ou site da Web ASP.NET usando o Visual Studio 2015, você tem a opção de servidores Web no qual executar o serviço de dados durante o desenvolvimento. Os seguintes servidores Web integram ao Visual Studio para torná-lo mais fácil de testar e depurar seus serviços de dados no computador local.

1. **Servidor IIS local**

     Quando você cria um serviço de dados é um aplicativo ASP.NET ou site da Web do ASP.NET que é executado no Internet Information Services (IIS), é recomendável que você desenvolva e teste seu serviço de dados usando o IIS no computador local. Executar o serviço de dados no IIS facilita o rastreamento de solicitações HTTP durante a depuração. Isso também permite que você predetermine os direitos necessários exigidos pelo IIS para acessar arquivos, bancos de dados e outros recursos necessários pelo serviço de dados. Para executar seu serviço de dados no IIS, você deve torna-se de que o IIS e o Windows Communication Foundation (WCF) são instalados e configurados corretamente e conceder acesso às contas do IIS no sistema de arquivos e bancos de dados. Para obter mais informações, confira [Como: Desenvolver um WCF Data Service em execução no IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md).

    > [!NOTE]
    > Você deve executar o Visual Studio com direitos de administrador para permitir que o ambiente de desenvolvimento para configurar o servidor IIS local.

2. **Visual Studio Development Server**

     Visual Studio inclui um servidor Web interno, o Visual Studio Development Server, que é o servidor de Web padrão para projetos do ASP.NET. Esse servidor Web foi projetado para executar projetos do ASP.NET no computador local durante o desenvolvimento. O [início rápido do WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) mostra como criar um serviço de dados que é executado no Visual Studio Development Server.

     Quando você usa o Visual Studio Development Server para desenvolver o serviço de dados, você deve estar ciente das seguintes limitações:

    - Este servidor só pode ser acessado no computador local.

    - Este servidor escuta no `localhost` e em uma porta específica, não na porta 80, que é a porta padrão para mensagens HTTP. Para obter mais informações, consulte [Servidores Web no Visual Studio para projetos Web ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/58wxa9w5(v=vs.120)).

    - Este servidor executa o serviço de dados no contexto de sua conta de usuário atual. Por exemplo, se você estiver executando como um usuário de nível de administrador, um serviço de dados em execução no Visual Studio Development Server terá privilégios de administrador. Isso pode fazer o serviço de dados ser capaz de acessar recursos que ele não tem os direitos de acesso quando implantado em um servidor IIS.

    - Este servidor não inclui os recursos adicionais do IIS, como autenticação.

    - Este servidor não pode manipular fluxos HTTP em partes, que é enviado ser padrão pelo cliente do WCF Data Services ao acessar dados binários grandes do serviço de dados. Para obter mais informações, consulte [provedor de Streaming](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md).

    - Este servidor tem problemas com o período de processamento (`.`) de caracteres em uma URL, mesmo que esse caractere tenha suporte pelo WCF Data Services nos valores de chave.

    > [!TIP]
    > Mesmo que você pode usar o Visual Studio Development Server para testar seus serviços de dados durante o desenvolvimento, você deve testá-los novamente após implantar em um servidor Web que está executando o IIS.

3. **Ambiente de desenvolvimento do Azure do Windows**

     Ferramentas do Windows Azure para Visual Studio inclui um conjunto integrado de ferramentas para desenvolvimento de serviços do Windows Azure no Visual Studio. Com essas ferramentas, você pode desenvolver um serviço de dados que pode ser implantado no Microsoft Azure e você pode testar o serviço de dados no computador local antes da implantação. Use essas ferramentas ao usar o Visual Studio para desenvolver um serviço de dados que é executado na plataforma Windows Azure. Você pode baixar ferramentas do Windows Azure para Visual Studio a partir de [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=201848). Para obter mais informações sobre como desenvolver um serviço de dados que é executado no Windows Azure, consulte a postagem [Implantando um OData Service no Windows Azure](https://go.microsoft.com/fwlink/?LinkId=201847).

### <a name="development-tips"></a>Dicas de desenvolvimento

Você deve considerar o seguinte ao desenvolver um serviço de dados:

- Determinar os requisitos de segurança de seu serviço de dados, se planejar autenticar usuários ou restringir o acesso para usuários específicos. Para obter mais informações, consulte [protegendo o WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md).

- Um programa de inspeção de HTTP pode ser muito útil ao depurar um serviço de dados permitindo que você inspecione o conteúdo de mensagens de solicitação e resposta. Qualquer analisador de pacote de rede que possa exibir pacotes brutos pode ser usado para inspecionar solicitações HTTP para e respostas do serviço de dados.

- Quando estiver depurando um serviço de dados, você talvez queira obter mais informações sobre o erro do serviço de dados que, durante a operação normal. Você pode obter informações de erro adicionais do serviço de dados definindo a propriedade <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> no <xref:System.Data.Services.DataServiceConfiguration> para `true` e definindo a propriedade <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> do atributo <xref:System.ServiceModel.Description.ServiceDebugBehavior> na classe de serviço de dados como `true`. Para obter mais informações, consulte a postagem [depuração WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=201868). Você também pode habilitar o rastreamento do WCF para exibir as exceções geradas na camada de mensagens HTTP. Para obter mais informações, consulte [Configurando o rastreamento](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).

- Um serviço de dados é geralmente desenvolvido como um projeto de aplicativo do ASP.NET, mas você também pode criar a você o serviço de dados como um projeto de site da Web do ASP.NET no Visual Studio. Para obter informações sobre as diferenças entre os dois tipos de projetos, consulte [projetos de aplicativos Web versus projetos de Site da Web no Visual Studio](https://docs.microsoft.com/previous-versions/aspnet/dd547590(v=vs.110)).

- Quando você cria um serviço de dados usando o **Adicionar Novo Item** caixa de diálogo no Visual Studio, o serviço de dados é hospedada pelo ASP.NET no IIS. Embora o ASP.NET e IIS seja o host padrão para um serviço de dados, há suporte para outras opções de hospedagem. Para obter mais informações, consulte [que hospeda o serviço de dados](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md).

## <a name="deploy-wcf-data-services"></a>Implantar o WCF Data Services

O WCF Data Service fornece flexibilidade na escolha do processo que hospeda o serviço de dados. Você pode usar o Visual Studio para implantar um serviço de dados para as seguintes plataformas:

- **IIS-Hosted Web Server**

    Quando um serviço de dados é desenvolvido como um projeto do ASP.NET, ele pode ser implantado em um servidor Web do IIS usando os processos de implantação padrão do ASP.NET.  Visual Studio fornece as seguintes tecnologias de implantação para o ASP.NET, dependendo do tipo de projeto do ASP.NET que hospeda o serviço de dados que você está implantando.

  - **Tecnologias de implantação para aplicativos Web do ASP.NET**

    - [Como: Criar um pacote de implantação da Web no Visual Studio](https://docs.microsoft.com/previous-versions/aspnet/dd465323(v=vs.110))

    - [Como: Implantar uma Web de publicação de projeto usando um único clique no Visual Studio](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))

  - **Tecnologias de implantação para Sites da Web ASP.NET**

    - [Como: Copiar arquivos de Site da Web com a ferramenta Copy Web Site](https://docs.microsoft.com/previous-versions/aspnet/c95809c0(v=vs.100))

    - [Como: Publicar Sites da Web](https://docs.microsoft.com/previous-versions/aspnet/20yh9f1b(v=vs.100))

    - [Passo a passo: Implantando um aplicativo Web ASP.NET usando XCOPY](https://docs.microsoft.com/previous-versions/aspnet/f735abw9(v=vs.100))

     Para obter mais informações sobre as opções de implantação para um aplicativo ASP.NET, consulte [visão geral de implantação da Web para Visual Studio e o ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/dd394698(v=vs.110)).

    > [!TIP]
    > Antes de tentar implantar o serviço de dados para o IIS, verifique se você testou a implantação para um servidor Web que esteja executando o IIS. Para obter mais informações, confira [Como: Desenvolver um WCF Data Service em execução no IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md).

- **Windows Azure**

     Você pode implantar um serviço de dados para o Windows Azure usando ferramentas do Windows Azure para Visual Studio. Você pode baixar ferramentas do Windows Azure para Visual Studio a partir de [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=201848). Para obter mais informações sobre como implantar um serviço de dados para o Windows Azure, consulte a postagem [Implantando um OData Service no Windows Azure](https://go.microsoft.com/fwlink/?LinkId=201847).

### <a name="deployment-considerations"></a>Considerações de implantação

Você deve considerar o seguinte ao implantar um serviço de dados:

- Quando você implanta um serviço de dados que usa o provedor do [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] para acessar um banco de dados do SQL Server, você também pode ter que propagar as estruturas de dados, os dados ou ambos com a implantação do serviço de dados. Visual Studio pode criar automaticamente scripts (arquivos. SQL) para fazer isso no banco de dados de destino, e esses scripts podem ser incluídos no pacote de implantação da Web de um aplicativo ASP.NET. Para obter mais informações, confira [Como: Implantar um banco de dados com um projeto de aplicativo Web](https://docs.microsoft.com/previous-versions/dd465343(v=vs.100)). Para um site da Web do ASP.NET, você pode fazer isso usando o **Assistente de publicação de banco de dados** no Visual Studio. Para obter mais informações, consulte [publicando um banco de dados SQL](https://docs.microsoft.com/previous-versions/aspnet/bb907585(v=vs.100)).

- Como o WCF Data Services inclui uma implementação básica do WCF, você pode usar o Windows Server AppFabric para monitorar um serviço de dados implantado no IIS em execução no Windows Server. Para obter mais informações sobre como usar o Windows Server AppFabric para monitorar um serviço de dados, consulte a postagem [rastreamento do WCF Data Services com o Windows Server AppFabric](https://go.microsoft.com/fwlink/?LinkID=202005).

## <a name="see-also"></a>Consulte também

- [Hospedagem o serviço de dados](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)
- [Protegendo o WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)
- [Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md) (Definindo o WCF Data Services)
