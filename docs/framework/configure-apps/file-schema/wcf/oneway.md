---
title: <oneWay>
ms.date: 03/30/2017
ms.assetid: 00e67e0e-77c0-4695-9138-c0997b0e5f3c
ms.openlocfilehash: 2458cdd4d593637c2025047d5dd510f0f89b2a0f
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67423082"
---
# <a name="oneway"></a>\<oneWay>
Habilita o roteamento de pacotes e o uso de métodos unidirecionais para uma associação personalizada.  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<oneWay>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<oneWay packetRoutable="Boolean">
  <channelPoolSettings idleTimeout="TimeSpan"
                       leaseTimeout="TimeSpan"
                       maxOutboundConnectionsPerEndpoint="Integer" />
</oneWay>
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`packetRoutable`|Um valor booliano que especifica se o roteamento de pacotes está habilitado. O padrão é `false`.|  
|`MaxAcceptedChannels`|Um inteiro que especifica o número máximo de canais que podem ser aceitos.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<channelPoolSettings>](../../../../../docs/framework/configure-apps/file-schema/wcf/channelpoolsettings.md)|Um <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement> objeto que contém as propriedades do pool de canal para o canal atual.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|Define todos os recursos de associação de associação personalizada.|  
  
## <a name="remarks"></a>Comentários  
 Para habilitar o roteamento de pacotes, uma camada de conversão unidirecional é necessária, que fornece esse elemento. Um usuário pode criar uma ligação personalizada que esta associação de camadas em um transporte para torná-lo pacote roteável de reconhecimento de sessão ou de solicitação-resposta. Esse elemento também é útil quando você deseja expor métodos unidirecionais de forma mais nativa. Mais transformações podem ser aplicadas nessa camada, como Duplex composto e sistema de mensagens confiável.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Channels.OneWayBindingElement>
- <xref:System.ServiceModel.Configuration.OneWayElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [Associações](../../../../../docs/framework/wcf/bindings.md)
- [Estendendo associações](../../../../../docs/framework/wcf/extending/extending-bindings.md)
- [Associações personalizadas](../../../../../docs/framework/wcf/extending/custom-bindings.md)
- [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
