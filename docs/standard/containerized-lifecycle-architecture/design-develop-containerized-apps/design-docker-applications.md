---
title: Criar aplicativos de Docker
description: Encontre aqui uma referência a um guia detalhado sobre a arquitetura de microsserviços, porque esse é um tópico que não é detalhado neste guia.
ms.date: 02/15/2019
ms.openlocfilehash: 535b6cefb7371014527032972ec27ebfe4b67ebc
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/13/2019
ms.locfileid: "65644636"
---
# <a name="design-docker-applications"></a>Criar aplicativos de Docker

O Capítulo 1 apresentou os conceitos fundamentais sobre contêineres e Docker. Essa informação é o nível básico de informações que você precisa para começar. Entretanto, os aplicativos empresariais podem ser complexos e são compostos de vários serviços e não de um único serviço ou contêiner. Para esses casos de uso opcionais, você precisa saber outras abordagens para design, como a SOA (Arquitetura Orientada a Serviços) e os conceitos de microsserviços mais avançados, bem como os conceitos de orquestração de contêiner. O escopo deste documento não é limitado aos microsserviços, mas para qualquer ciclo de vida do aplicativo Docker, portanto, ele não explora a arquitetura de microsserviços de modo aprofundado porque você também pode usar o Docker e os contêineres com trabalhos ou tarefas em segundo plano, SOA regular ou até mesmo com abordagens de implantação de aplicativo monolítico.

**Mais informações** Para saber mais sobre aplicativos empresariais e arquitetura de microsserviços em detalhes, leia o guia [Microsserviços NET: arquitetura para aplicativos .NET em contêineres](../../microservices-architecture/index.md) que você também pode baixar no <https://aka.ms/MicroservicesEbook>.

No entanto, antes de entrarmos no ciclo de vida do aplicativo e no DevOps, é importante saber como você pretende projetar e construir seu aplicativo e quais são suas opções de design.

>[!div class="step-by-step"]
>[Anterior](index.md)
>[Próximo](common-container-design-principles.md)
