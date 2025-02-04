---
title: Interação da política de cache – idade máxima e desatualização máxima
ms.date: 03/30/2017
helpviewer_keywords:
- maximum staleness
- freshness of cached resources
- time, cached resources
- maximum age policy
- staleness of cached resources
- age of cached resources
ms.assetid: 7f775925-89a1-4956-ba90-c869c1749a94
ms.openlocfilehash: 3819882fe4a93016b25c10daa198a24fe7b0e951
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624681"
---
# <a name="cache-policy-interactionmaximum-age-and-maximum-staleness"></a>Interação da política de cache – idade máxima e desatualização máxima
Para ajudar a garantir que o conteúdo mais atualizado é retornado para o aplicativo cliente, a interação dos requisitos de revalidação do servidor e da política de cache de cliente sempre resulta na política de cache mais conservadora. Todos os exemplos deste tópico ilustram a política de cache para um recurso que é armazenado em cache em 1º de janeiro e expira em 4 de janeiro.  
  
 Nos seguintes exemplos, o valor máximo de desatualização (`maxStale`) é usado em conjunto com uma idade máxima (`maxAge`):  
  
- Se a política de cache definir `maxAge` = 5 dias e não especificar um valor `maxStale`, de acordo com o valor `maxAge`, o conteúdo será utilizável até 6 de janeiro. No entanto, de acordo com os requisitos de revalidação do servidor, o conteúdo expirará em 4 de janeiro. Como a data de expiração do conteúdo é mais conservadora (anterior), ela terá precedência sobre a política `maxAge`. Portanto, o conteúdo expirará em 4 de janeiro e deverá ser revalidado, embora sua idade máxima não tenha sido atingida.  
  
- Se a política de cache definir `maxAge` = 5 dias e `maxStale` = 3 dias, de acordo com o valor `maxAge`, o conteúdo será utilizável até 6 de janeiro. De acordo com o valor `maxStale`, o conteúdo será utilizável até 7 de janeiro. Portanto, o conteúdo será revalidado em 6 de janeiro.  
  
- Se a política de cache definir `maxAge` = 5 dias e `maxStale` = 1 dia, de acordo com o valor `maxAge`, o conteúdo será utilizável até 6 de janeiro. De acordo com o valor `maxStale`, o conteúdo será utilizável até 5 de janeiro. Portanto, o conteúdo será revalidado em 5 de janeiro.  
  
 Quando a idade máxima for menor que a data de expiração do conteúdo, o comportamento de cache mais conservador sempre prevalecerá e o valor máximo de desatualização não terá nenhum efeito. Os seguintes exemplos ilustram o efeito de definir um valor máximo de desatualização (`maxStale`) quando a idade máxima (`maxAge`) for atingida antes da expiração do conteúdo:  
  
- Se a política de cache definir `maxAge` = 1 dia e não especificar um valor para o valor `maxStale`, o conteúdo será revalidado em 2 de janeiro, mesmo que não tenha expirado.  
  
- Se a política de cache definir `maxAge` = 1 dia e `maxStale` = 3 dias, o conteúdo será revalidado em 2 de janeiro para impor a configuração de política mais conservadora.  
  
- Se a política de cache definir `maxAge` = 1 dia e `maxStale` = 1 dia, o conteúdo será revalidado em 2 de janeiro.  
  
## <a name="see-also"></a>Consulte também

- [Gerenciamento de cache para aplicativos de rede](../../../docs/framework/network-programming/cache-management-for-network-applications.md)
- [Política de cache](../../../docs/framework/network-programming/cache-policy.md)
- [Políticas de cache baseadas na localização](../../../docs/framework/network-programming/location-based-cache-policies.md)
- [Políticas de cache baseadas em tempo](../../../docs/framework/network-programming/time-based-cache-policies.md)
- [Configurando o cache em aplicativos de rede](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)
- [Interação da política de cache – idade máxima e atualização mínima](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-minimum-freshness.md)
