---
title: Implementando comunicação baseada em evento entre microsserviços (eventos de integração)
description: Arquitetura de microsserviços .NET para aplicativos .NET em contêineres | Entender eventos de integração para implementar comunicação baseada em evento entre microsserviços.
ms.date: 10/02/2018
ms.openlocfilehash: 8a5cfa280063da742dc1693905fc44cf870c1fcc
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640728"
---
# <a name="implementing-event-based-communication-between-microservices-integration-events"></a>Implementando comunicação baseada em evento entre microsserviços (eventos de integração)

Conforme descrito anteriormente, quando você usa comunicação baseada em evento, um microsserviço publica um evento quando algo importante acontece, como quando ele atualiza uma entidade de negócios. Outros microsserviços assinam esses eventos. Quando um microsserviço recebe um evento, ele pode atualizar suas próprias entidades de negócios, o que pode levar à publicação de mais eventos. Essa é a essência do conceito de consistência eventual. Este sistema de publicação/assinatura normalmente é executado por meio de uma implementação de um barramento de evento. O barramento de evento pode ser criado como uma interface com a API necessária para assinar e cancelar a assinatura de eventos e eventos de publicação. Também pode ter uma ou mais implementações com base em qualquer comunicação de mensagens ou entre processos, como uma fila de mensagens ou um barramento de serviço que seja compatível com a comunicação assíncrona e um modelo de publicação/assinatura.

Você pode usar eventos para implementar transações comerciais que abranjam vários serviços, o que lhe dá consistência eventual entre esses serviços. Uma transação eventualmente consistente consiste em uma série de ações distribuídas. Em cada ação, o microsserviço atualiza uma entidade de negócios e publica um evento que dispara a próxima ação.

![O microsserviço Catálogo usando comunicação controlada por eventos por meio de um barramento de eventos, a fim de obter uma consistência eventual com Carrinho de compras e outros microsserviços.](./media/image19.png)

**Figura 6-18**. Comunicação controlada por evento com base em um barramento de evento

Esta seção descreve como você faz para implementar esse tipo de comunicação com o .NET usando uma interface de barramento de evento genérica, conforme mostra a Figura 6-18. Há várias implementações possíveis, cada uma usando uma tecnologia ou infraestrutura diferente, como RabbitMQ, Barramento de Serviço do Azure ou qualquer outro software livre de terceiros ou barramento de serviço comercial.

## <a name="using-message-brokers-and-services-buses-for-production-systems"></a>Usando agentes de mensagem e barramentos de serviços para sistemas de produção

Conforme observado na seção de arquitetura, você pode escolher entre várias tecnologias de mensagem para implementar o barramento do evento abstrato. Porém, essas tecnologias estão em diferentes níveis. Por exemplo, RabbitMQ, um transporte de agente de mensagens, está em um nível inferior a produtos comerciais, como o Barramento de Serviço do Azure, o NServiceBus, o MassTransit ou o Brighter. A maioria desses produtos pode operar sobre RabbitMQ ou Barramento de Serviço do Azure. Sua escolha do produto depende de quantos recursos e quanta escalabilidade imediata você precisa para seu aplicativo.

Para implementar apenas uma prova de conceito de barramento de evento para seu ambiente de desenvolvimento, como fizemos no exemplo de eShopOnContainers, pode ser suficiente uma implementação simples sobre RabbitMQ em execução como um contêiner. Porém, para sistemas críticos e de produção que precisam de alta escalabilidade, talvez você queira avaliar e usar o Barramento de Serviço do Azure.

Se você precisar de abstrações de alto nível e os recursos mais avançados, como [Sagas](https://docs.particular.net/nservicebus/sagas/), para processos de execução longa que facilitam o desenvolvimento distribuído barramentos, valerá a pena avaliar outros barramentos de serviço comerciais e de software livre como NServiceBus, MassTransit e Brighter. Nesse caso, as abstrações e a API a serem usadas em geral serão seriam diretamente aquelas fornecidas por esses barramentos de serviço de alto nível, em vez das suas próprias abstrações (como [abstrações de barramento de evento simples fornecidas no eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/BuildingBlocks/EventBus/EventBus/Abstractions/IEventBus.cs)). Para isso, você pode pesquisar o [eShopOnContainers bifurcado usando NServiceBus](https://go.particular.net/eShopOnContainers) (amostra derivada adicional implementada pelo Software Específico)

Obviamente, você sempre pode criar seus próprios recursos de barramento de serviço sobre tecnologias de nível inferior, como RabbitMQ e o Docker, mas o trabalho necessário para "reinventar a roda" pode ser muito alto para um aplicativo empresarial personalizado.

Para reiterar: as abstrações do barramento de evento de exemplo e a implementação apresentada no exemplo do eShopOnContainers devem ser usados apenas como uma prova de conceito. Quando decidir que deseja ter comunicação assíncrona e controlada por evento, conforme explicado na seção atual, você deve escolher o produto de barramento de serviço que melhor atenda às suas necessidades de produção.

## <a name="integration-events"></a>Eventos de integração

Eventos de integração são usados para colocar o estado de domínio em sincronia entre vários microsserviços ou sistemas externos. Isso é feito ao publicar eventos de integração fora do microsserviço. Quando um evento é publicado para vários microsserviços receptores (para tantos microsserviços quantos assinarem o evento de integração), o manipulador de eventos apropriado em cada microsserviço receptor manipulará o evento.

Um evento de integração é basicamente uma classe de retenção de dados, como no exemplo a seguir:

```csharp
public class ProductPriceChangedIntegrationEvent : IntegrationEvent
{
    public int ProductId { get; private set; }
    public decimal NewPrice { get; private set; }
    public decimal OldPrice { get; private set; }

    public ProductPriceChangedIntegrationEvent(int productId, decimal newPrice,
        decimal oldPrice)
    {
        ProductId = productId;
        NewPrice = newPrice;
        OldPrice = oldPrice;
    }
}
```

Os eventos de integração podem ser definidos no nível do aplicativo de cada microsserviço, assim, estão separados de outros microsserviços, de modo comparável a como os ViewModels são definidos no cliente e servidor. O que não é recomendável é compartilhar uma biblioteca de eventos de integração comum com vários microsserviços; fazer isso seria acoplar esses microsserviços a uma única biblioteca de dados de definição de evento. Você não deseja fazer isso pelos mesmos motivos que não deseja compartilhar um modelo de domínio comum entre vários microsserviços: os microsserviços deve ser completamente autônomos.

Há apenas alguns tipos de bibliotecas que você deve compartilhar entre microsserviços. Um são as bibliotecas que são blocos de aplicativo finais, como [API cliente do Barramento de Evento](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/BuildingBlocks/EventBus), conforme mostrado em eShopOnContainers. Outra vantagem são as bibliotecas que constituem ferramentas que também podem ser compartilhadas como componentes do NuGet, como serializadores JSON.

## <a name="the-event-bus"></a>O barramento de evento

Um barramento de evento permite comunicação no estilo publicar/assinar entre microsserviços sem a necessidade de os componentes explicitamente estarem cientes uns dos outros, como mostra a Figura 6-19.

![Padrão básico pub/sub, o Microsserviço A publica no Barramento de Evento, que distribui para os microsserviços B e C assinantes, sem que o publicador saiba quem são os assinantes.](./media/image20.png)

**Figura 6-19**. Noções básicas sobre publicação/assinatura com um barramento de evento

O barramento de evento está relacionado ao padrão Observador e ao padrão de publicação/assinatura.

### <a name="observer-pattern"></a>Padrão do observador

No [padrão Observador](https://en.wikipedia.org/wiki/Observer_pattern), seu objeto primário (conhecido como o Observável) notifica outros objetos de interessados (conhecidos como Observadores) com informações relevantes (eventos).

### <a name="publishsubscribe-pubsub-pattern"></a>Padrão Pub/Sub (Publicar/Assinar)

O objetivo do [padrão Publicar/Assinar](https://docs.microsoft.com/previous-versions/msp-n-p/ff649664(v=pandp.10)) é o mesmo que o padrão Observador: você deseja notificar outros serviços quando determinados eventos ocorrem. Mas há uma diferença importante entre os padrões de Observador e Pub/Sub. No padrão de observador, a difusão é executada diretamente do observável para os observadores, de modo que eles "conhecem" uns aos outros. Porém, ao usar um padrão Pub/Sub, há um terceiro componente, chamado de agente, agente de mensagem ou barramento de evento, que é conhecido tanto pelo publicador quanto pelo assinante. Portanto, ao usar o padrão Pub/Sub, o publicador e os assinantes são precisamente desacoplados graças ao agente de mensagem ou barramento de evento mencionado.

### <a name="the-middleman-or-event-bus"></a>O barramento de evento ou intermediário

Como você obtém anonimato entre publicador e assinante? Uma maneira fácil é permitir que um intermediário cuide de toda a comunicação. Um barramento de evento é um intermediário.

Um barramento de evento normalmente é composto por duas partes:

- A abstração ou interface.

- Uma ou mais implementações.

Na Figura 6-19, você pode ver como, de um ponto de vista de aplicativo, o barramento de evento é nada mais que um canal Pub/Sub. A maneira como você implementa essa comunicação assíncrona pode variar. Eles podem ter várias implementações, assim, você pode alternar entre elas, dependendo dos requisitos do ambiente (por exemplo, produção versus ambientes de desenvolvimento).

Na Figura 6-20, você pode ver uma abstração de um barramento de evento com várias implementações baseadas nas tecnologias de mensagem de infraestrutura, como RabbitMQ, Barramento de Serviço do Azure ou outro agente de mensagem/evento.

![É bom ter o barramento de evento definido por meio de uma interface para que ele possa ser implementado com várias tecnologias, como o Barramento de Serviço do Azure, o RabbitMQ ou outros.](./media/image21.png)

**Figura 6- 20.** Várias implementações de um barramento de evento

No entanto, conforme mencionado anteriormente, usar suas próprias abstrações (a interface de barramento do evento) será bom somente se você precisar de recursos de barramento de evento básicos compatíveis com as suas abstrações. Se você precisar de recursos mais avançados de barramento de serviço, provavelmente deverá usar a API e as abstrações fornecidas pelo seu barramento de serviço comercial preferido, em vez das suas próprias abstrações.

### <a name="defining-an-event-bus-interface"></a>Definir uma interface de barramento de evento

Vamos começar com algum código de implementação para a interface de barramento de evento e possíveis implementações para fins de exploração. A interface deve ser genérica e simples, como na interface a seguir.

```csharp
public interface IEventBus
{
    void Publish(IntegrationEvent @event);

    void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>;

    void SubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void UnsubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void Unsubscribe<T, TH>()
        where TH : IIntegrationEventHandler<T>
        where T : IntegrationEvent;
}
```

O método `Publish` é simples. O barramento de evento difundirá o evento de integração passado a ele para qualquer microsserviço ou até mesmo um aplicativo externo, que assine esse evento. Esse método é usado pelo microsserviço que está publicando o evento.

Os métodos `Subscribe` (você pode ter várias implementações, dependendo dos argumentos) são usados pelos microsserviços que desejam receber eventos. Esse método tem dois argumentos. O primeiro é o evento de integração a assinar (`IntegrationEvent`). O segundo argumento é o manipulador de eventos de integração (ou método de retorno de chamada), denominado `IIntegrationEventHandler<T>`, a ser executado quando o microsserviço receptor obtiver essa mensagem de evento de integração.

> [!div class="step-by-step"]
> [Anterior](database-server-container.md)
> [Próximo](rabbitmq-event-bus-development-test-environment.md)
