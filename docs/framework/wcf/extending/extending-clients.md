---
title: Estendendo clientes
ms.date: 03/30/2017
helpviewer_keywords:
- proxy extensions [WCF]
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
ms.openlocfilehash: 48e6177e7098f8131d2a0fd62bda9c505fa8bcc9
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662811"
---
# <a name="extending-clients"></a>Estendendo clientes
Em um aplicativo de chamada, a camada de modelo de serviço é responsável por converter as invocações de método no código do aplicativo em mensagens de saída, enviá-los para os canais subjacentes, converter os resultados de volta em valores de retorno e parâmetros out em o código do aplicativo e retornando os resultados de volta ao chamador. Extensões do modelo de serviço modificarem ou implementam a execução ou o comportamento de comunicação e recursos que envolvem a funcionalidade de cliente ou dispatcher, comportamentos personalizados, mensagem e interceptação de parâmetro e outras funcionalidades de extensibilidade.  
  
 Este tópico descreve como usar o <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.ClientOperation> classes em um aplicativo de cliente do Windows Communication Foundation (WCF) para modificar o comportamento de execução padrão de um cliente WCF para interceptar ou modificar as mensagens, parâmetros, ou valores de retorno antes ou após enviar ou recuperá-los da camada de canal. Para obter mais informações sobre como estender o tempo de execução do serviço, consulte [estendendo Dispatchers](../../../../docs/framework/wcf/extending/extending-dispatchers.md). Para obter mais informações sobre os comportamentos que modificam e inserir objetos de personalização em tempo de execução do cliente, consulte [Configurando e estendendo o tempo de execução com comportamentos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="clients"></a>Clientes  
 Em um cliente, um canal de cliente ou objeto de cliente do WCF converte as invocações de método em mensagens de saída e mensagens de entrada para os resultados da operação que são retornados ao aplicativo de chamada. (Para obter mais informações sobre os tipos de cliente, consulte [arquitetura de cliente WCF](../../../../docs/framework/wcf/feature-details/client-architecture.md).)  
  
 Tipos de cliente WCF têm tipos de tempo de execução que lidar com essa funcionalidade de nível de operação e de ponto de extremidade. Quando um aplicativo chama uma operação, o <xref:System.ServiceModel.Dispatcher.ClientOperation> converte os objetos de saída em uma mensagem, processa os interceptadores, confirma que a chamada de saída está em conformidade com o contrato de destino e todas as mensagens de saída para o <xref:System.ServiceModel.Dispatcher.ClientRuntime>, que é responsável por criar e gerenciar canais de saída (e canais de entrada no caso de serviços duplex), lidar com mensagem de saída adicional de processamento (por exemplo, a modificação de cabeçalho), os interceptadores de mensagem em ambas as direções de processamento e roteamento de entrada duplex chamadas para o lado do cliente apropriado <xref:System.ServiceModel.Dispatcher.DispatchRuntime> objeto. Tanto a <xref:System.ServiceModel.Dispatcher.ClientOperation> e <xref:System.ServiceModel.Dispatcher.ClientRuntime> fornecem serviços semelhantes quando as mensagens (inclusive falhas) são retornadas ao cliente.  
  
 Essas duas classes de tempo de execução são a extensão do principal para personalizar o processamento de objetos de cliente WCF e canais. O <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe permite que os usuários interceptar e estender a execução do cliente em todas as mensagens no contrato. O <xref:System.ServiceModel.Dispatcher.ClientOperation> classe permite que os usuários interceptar e estender a execução do cliente para todas as mensagens em uma determinada operação.  
  
 Modificando as propriedades ou inserindo as personalizações são feitas usando o contrato, ponto de extremidade e comportamentos de operação. Para obter mais informações sobre como usar esses tipos de comportamentos para executar personalizações de tempo de execução do cliente, consulte [Configurando e estendendo o tempo de execução com comportamentos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="scenarios"></a>Cenários  
 Há uma série de motivos para estender o sistema cliente, incluindo:  
  
- Validação de mensagem personalizada. Um usuário talvez queira impor que uma mensagem é válida para um determinado esquema. Isso pode ser feito com a implementação de <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> interface e atribuindo a implementação para o <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A> propriedade. Para ver mais exemplos, veja [Como: Inspecionar ou modificar as mensagens no cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md) e [como: Inspecionar ou modificar as mensagens no cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
- Registro em log de mensagem personalizada. Um usuário talvez queira inspecionar e um conjunto de mensagens de aplicativo por meio de um ponto de extremidade de fluxo de log. Isso também pode ser feito com as interfaces de interceptador de mensagem.  
  
- Transformações de mensagens personalizadas. Em vez de modificar o código do aplicativo, o usuário talvez queira aplicar determinadas transformações para a mensagem no tempo de execução (por exemplo, para controle de versão). Isso pode ser feito, novamente, com as interfaces de interceptador de mensagem.  
  
- Modelo de dados personalizado. Um usuário pode querer ter um modelo de serialização ou de dados não suportados por padrão no WCF (ou seja, <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>, <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>, e <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> objetos). Isso pode ser feito ao implementar as interfaces de formatador de mensagem. Para obter mais informações, consulte <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType> e o <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=nameWithType> propriedade.  
  
- Validação de parâmetro personalizado. Um usuário talvez queira impor que os parâmetros de tipo são válidos (em vez de XML). Isso pode ser feito usando as interfaces do Inspetor de parâmetro. Para obter um exemplo, consulte [ Inspecionar ou modificar os parâmetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md) ou [validação do cliente](../../../../docs/framework/wcf/samples/client-validation.md).  
  
### <a name="using-the-clientruntime-class"></a>Usando a classe ClientRuntime  
 O <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe é um ponto de extensibilidade para que você pode adicionar objetos de extensão que interceptam mensagens e estendem o comportamento do cliente. Objetos de interceptação podem processar todas as mensagens em um determinado contrato, processar apenas mensagens para operações específicas, executar a inicialização de canal personalizado e implementar outros comportamentos de aplicativo personalizadas do cliente.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> propriedade retorna o objeto de tempo de execução de expedição para clientes de retorno de chamada iniciados pelo serviço.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> propriedade aceita um objeto de seletor de operação personalizado.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> propriedade permite a adição de um inicializador de canal que pode inspecionar ou modificar o canal do cliente.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> propriedade obtém uma coleção de <xref:System.ServiceModel.Dispatcher.ClientOperation> objetos aos quais você pode adicionar interceptores de mensagem personalizada que fornecem funcionalidade específica para as mensagens dessa operação.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> propriedade permite que um aplicativo desativar alguns cabeçalhos de endereçamento automático para controlar o endereçamento diretamente.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> propriedade define o valor do destino da mensagem no nível de transporte para dar suporte a outros cenários e intermediários.  
  
- O <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> propriedade obtém uma coleção de <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> objetos aos quais você pode adicionar interceptores de mensagem personalizada para todas as mensagens viajando através de um cliente do WCF.  
  
 Além disso, há uma série de outras propriedades que recuperar as informações de contrato:  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 Se o cliente do WCF é um cliente duplex do WCF, as propriedades a seguir também recuperar informações do cliente WCF o retorno de chamada:  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 Para estender a execução de cliente do WCF em um cliente WCF inteira, examine as propriedades disponíveis no <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe para ver se a modificação de uma propriedade ou implementar uma interface e adicioná-lo a uma propriedade criam a funcionalidade que você está procurando. Depois de ter escolhido uma extensão específica para criar, insira sua extensão apropriada <xref:System.ServiceModel.Dispatcher.ClientRuntime> propriedade com a implementação de um comportamento do cliente que fornece acesso para o <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe quando invocado.  
  
 Você pode inserir objetos de extensão personalizada em uma coleção usando um comportamento de operação (um objeto que implementa <xref:System.ServiceModel.Description.IOperationBehavior>), um comportamento de contrato (um objeto que implementa <xref:System.ServiceModel.Description.IContractBehavior>), ou um comportamento de ponto de extremidade (um objeto que implementa <xref:System.ServiceModel.Description.IEndpointBehavior> ). O objeto de comportamento de instalação é adicionado à coleção de comportamentos apropriada por meio de programação, declarativamente (Implementando um atributo personalizado), ou implementando um personalizado <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> objeto para habilitar o comportamento a ser inserido usando um arquivo de configuração do aplicativo. Para obter detalhes, consulte [Configurando e estendendo o tempo de execução com comportamentos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para obter exemplos que demonstram a intercepção entre um cliente WCF, consulte [como: Inspecionar ou modificar as mensagens no cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
### <a name="using-the-clientoperation-class"></a>Usando a classe ClientOperation  
 O <xref:System.ServiceModel.Dispatcher.ClientOperation> classe é o local para modificações de tempo de execução do cliente e a inserção de ponto para extensões personalizadas que estão no escopo para apenas uma operação de serviço. (Para modificar o comportamento de tempo de execução do cliente para todas as mensagens em um contrato, use o <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe.)  
  
 Use o <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> propriedade para localizar o <xref:System.ServiceModel.Dispatcher.ClientOperation> objeto que representa uma operação de serviço específico. As propriedades a seguir permitem que você inserir objetos personalizados no sistema de cliente do WCF:  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> propriedade para inserir um personalizado <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> implementação para uma operação ou modificar o formatador atual.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> propriedade para inserir um personalizado <xref:System.ServiceModel.Dispatcher.IParameterInspector> implementação ou para modificar o atual.  
  
 As propriedades a seguir permitem que você modifique o sistema de interação com o formatador e inspetores de parâmetro personalizado:  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> propriedade para controlar a serialização de uma mensagem de saída.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> propriedade para controlar a desserialização de uma mensagem de entrada.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> propriedade para controlar a ação WS-Addressing da mensagem de solicitação.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A> e <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> para especificar quais métodos de cliente do WCF são associados uma operação assíncrona.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> como o tipo de detalhe de falhas de propriedade para obter uma coleção que contém os tipos que podem aparecer em SOAP.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> e <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> propriedades para controlar se uma sessão é iniciada ou interrompida para baixo, respectivamente, quando a operação é chamada.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> propriedade para controlar se a operação é uma operação unidirecional.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> propriedade para obter o contendo <xref:System.ServiceModel.Dispatcher.ClientRuntime> objeto.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> propriedade para obter o nome da operação.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> propriedade para controlar qual método é mapeado para a operação.  
  
 Para estender a execução de cliente do WCF em apenas uma operação de serviço, examine as propriedades disponíveis no <xref:System.ServiceModel.Dispatcher.ClientOperation> classe para ver se a modificação de uma propriedade ou implementar uma interface e adicioná-lo a uma propriedade criam a funcionalidade que você está procurando. Depois de ter escolhido uma extensão específica para criar, insira sua extensão apropriada <xref:System.ServiceModel.Dispatcher.ClientOperation> propriedade com a implementação de um comportamento do cliente que fornece acesso para o <xref:System.ServiceModel.Dispatcher.ClientOperation> classe quando invocado. Dentro desse comportamento, em seguida, você pode modificar o <xref:System.ServiceModel.Dispatcher.ClientRuntime> propriedade para atender às suas necessidades.  
  
 Normalmente, implementar um comportamento de operação (um objeto que implementa o <xref:System.ServiceModel.Description.IOperationBehavior> interface) é suficiente, mas você também pode usar comportamentos de ponto de extremidade e comportamentos para realizar a mesma coisa com a localização de contrato a <xref:System.ServiceModel.Description.OperationDescription> para um determinado operação e anexando o comportamento de lá. Para obter detalhes, consulte [Configurando e estendendo o tempo de execução com comportamentos](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para usar o comportamento personalizado de configuração, instale seu comportamento usando um manipulador de seção de configuração de comportamento personalizado. Você também pode instalar seu comportamento com a criação de um atributo personalizado.  
  
 Para obter exemplos que demonstram a intercepção entre um cliente WCF, consulte [como: Inspecionar ou modificar parâmetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Dispatcher.ClientRuntime>
- <xref:System.ServiceModel.Dispatcher.ClientOperation>
- [Como: Inspecionar ou modificar as mensagens no cliente](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)
- [Como: Inspecionar ou modificar parâmetros](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)
