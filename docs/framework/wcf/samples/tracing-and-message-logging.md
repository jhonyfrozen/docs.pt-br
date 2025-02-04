---
title: Registro de mensagem e rastreamento
ms.date: 03/30/2017
helpviewer_keywords:
- Tracing and logging
ms.assetid: a4f39bfc-3c5e-4d51-a312-71c5c3ce0afd
ms.openlocfilehash: 55fdb31310c62c5d0ac7e5d963309cb1b3fe2da4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64617527"
---
# <a name="tracing-and-message-logging"></a>Registro de mensagem e rastreamento
Este exemplo demonstra como habilitar o rastreamento e o registro de mensagem. Os rastreamentos resultantes e logs de mensagem são exibidos usando o [ferramenta de Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md). Este exemplo se baseia a [Introdução ao](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
> [!NOTE]
>  As instruções de procedimento e compilação de configuração para este exemplo estão localizadas no final deste tópico.  
  
## <a name="tracing"></a>Rastreamento  
 Windows Communication Foundation (WCF) usa o mecanismo de rastreamento definido na <xref:System.Diagnostics> namespace. Nesse modelo de rastreamento, dados de rastreamento são produzidos por fontes de rastreamento que implementam a aplicativos. Cada origem é identificada por um nome. Os consumidores de rastreamento criam ouvintes de rastreamento para as fontes de rastreamento para o qual deseja recuperar informações. Para receber dados de rastreamento, você deve criar um ouvinte para a origem de rastreamento. No WCF, isso pode ser feito adicionando o seguinte código ao arquivo de configuração do serviço ou do cliente, configurando a origem de rastreamento do modelo de serviço `switchValue`:  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-service.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>  
```  
  
 Para obter mais informações sobre as fontes de rastreamento, consulte a seção origem de rastreamento de [Configurando o rastreamento](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md) tópico.  
  
## <a name="activity-tracing-and-propagation"></a>Rastreamento de atividades e propagação  
 Tendo `ActivityTracing` habilitado e `propagateActivity` definido como `true` no `system.ServiceModel` origens de rastreamento para o cliente e o serviço fornecem a correlação de rastreamentos em unidades lógicas de processamento (atividades), entre as atividades dentro de pontos de extremidade ( por meio de transferências de atividades) e entre as atividades que abrangem vários pontos de extremidade (por meio de propagação de ID de atividade).  
  
 Esses três mecanismos (atividades, transferências e propagação) podem ajudá-lo a localizar a causa raiz de um erro mais rapidamente usando a ferramenta Visualizador de rastreamento de serviço. Para obter mais informações, consulte [usando o Visualizador de rastreamento de serviço para exibir rastreamentos correlacionados e soluções de problemas](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 É possível estender o rastreamento que é fornecido pelo ServiceModel Criando rastreamentos de atividade definida pelo usuário. Rastreamento de atividades definidos pelo usuário permite ao usuário criar atividades de rastreamento para:  
  
- Rastreamentos de grupo em unidades lógicas de trabalho.  
  
- Correlacione atividades por meio de transferências e propagação.  
  
- Diminui o custo de desempenho de rastreamento do WCF (por exemplo, o custo de espaço em disco de um arquivo de log).  
  
 Para obter mais informações sobre rastreamento de atividade definida pelo usuário, consulte o [estendendo rastreamento](../../../../docs/framework/wcf/samples/extending-tracing.md) exemplo.  
  
## <a name="message-logging"></a>Registro em log de mensagens  
 Log de mensagens pode ser habilitado tanto no cliente e o serviço de qualquer aplicativo WCF. Para habilitar o registro em log de mensagem, você deve adicionar o código a seguir para o cliente ou serviço:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <diagnostics>  
      <!-- Enable Message Logging here. -->  
      <!-- log all messages received or sent at the transport or service model levels -->  
      <messageLogging logEntireMessage="true"  
                      maxMessagesToLog="300"  
                      logMessagesAtServiceLevel="true"  
                      logMalformedMessages="true"  
                      logMessagesAtTransportLevel="true" />  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 Quando uma mensagem é gravada, o tipo de rastreamento depende se ela está sendo rastreada no cliente ou servidor. Por exemplo, uma mensagem de "Adicionar" é enviada a um cliente é rastreada sob a categoria "TransportWrite" no cliente, enquanto a mesma mensagem é rastreada sob a categoria "TransportRead" no serviço.  
  
 Configurar o ouvinte de rastreamento, adicionando o seguinte código para o <xref:System.Diagnostics> seção do arquivo de App. config do cliente ou do serviço Web. config:  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-client.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
```  
  
 As mensagens são registradas no formato XML no diretório de destino especificado no arquivo de configuração.  
  
> [!NOTE]
>  Arquivos de rastreamento não são criados sem criar inicialmente o diretório de log. Certifique-se de que o diretório C:\logs\ existe, ou especifique um diretório de log alternativo na configuração de ouvinte. Consulte as instruções de configuração inicial no final deste documento para obter mais informações.  
  
 Para obter mais informações sobre o log de mensagem, consulte a [Configurando o log de mensagens](../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md) tópico.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Certifique-se de que você tenha executado o [procedimento de configuração de uso único para os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Antes de executar o exemplo de rastreamento e registro em log de mensagem, crie o diretório C:\logs\ para o serviço para gravar os arquivos. svclog para. O nome desse diretório é definido no arquivo de configuração como o caminho para as mensagens a serem registrados e rastreamentos e pode ser alterado. Dar ao usuário acesso de gravação do serviço de rede para o diretório de logs.  
  
3. Para compilar a edição de c#, C++ ou Visual Basic .NET da solução, siga as instruções em [compilando os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4. Para executar o exemplo em uma configuração ou entre computadores, siga as instruções em [executando os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Se este diretório não existir, vá para [Windows Communication Foundation (WCF) e o Windows Workflow Foundation (WF) exemplos do .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\TracingAndLogging`  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](../../../../docs/framework/wcf/diagnostics/tracing/index.md)
- [AppFabric que monitora exemplos](https://go.microsoft.com/fwlink/?LinkId=193959)
