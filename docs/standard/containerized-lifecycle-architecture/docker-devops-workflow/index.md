---
title: Fluxo de trabalho de DevOps de aplicativos do Docker com as ferramentas da Microsoft
description: Ciclo de vida de aplicativo do Docker em contêineres com a plataforma e as ferramentas da Microsoft, o fluxo de trabalho do DevOps e as ferramentas da Microsoft
ms.date: 02/15/2019
ms.openlocfilehash: 6b138301a7e6794ce0a7b15957684b3b73e9f89f
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/13/2019
ms.locfileid: "65644815"
---
# <a name="docker-application-devops-workflow-with-microsoft-tools"></a>Fluxo de trabalho de DevOps de aplicativos do Docker com as ferramentas da Microsoft

*O Microsoft Visual Studio, o Azure DevOps Services, o Team Foundation Server e o Azure Monitor fornecem um ecossistema abrangente para desenvolvimento e operações de TI que proporciona à sua equipe as ferramentas para gerenciar projetos e compilar, testar e implantar aplicativos em contêineres com rapidez.*

Com o Visual Studio e o Azure DevOps Services na nuvem, juntamente com o Team Foundation Server local, as equipes de desenvolvimento podem compilar, testar e liberar de forma produtiva aplicativos em contêineres para Windows ou Linux.

As ferramentas da Microsoft podem automatizar o pipeline para implementações específicas de aplicativos em contêineres – Docker, .NET Core ou qualquer combinação com outras plataformas – desde compilações globais e CI (Integração Contínua) e testes com o Azure DevOps Services ou o Team Foundation Server, até CD (Implantação Contínua) para ambientes do Docker (Desenvolvimento, Processo de Preparo, Produção) e transmissão de informações de análise sobre os serviços para a equipe de desenvolvimento por meio do Azure Monitor. Cada confirmação de código pode iniciar uma compilação (CI) e implantar automaticamente os serviços em ambientes em contêineres específicos (CD).

Os desenvolvedores e testadores podem provisionar ambientes de desenvolvimento e teste semelhante à produção com rapidez e facilidade baseados no Docker usando modelos no Microsoft Azure.

A complexidade do desenvolvimento de aplicativos em contêineres aumenta de maneira estável dependendo das necessidades de complexidade e escalabilidade do negócio. Um bom exemplo dessa complexidade são os aplicativos baseados em arquiteturas de microsserviços. Para ter êxito nesse ambiente, o projeto precisa automatizar todo o ciclo de vida – não apenas o build e a implantação, mas também deve gerenciar versões juntamente com a coleção de telemetria. O Azure DevOps Services e o Azure oferecem as seguintes funcionalidades:

- Gerenciamento de código-fonte do Azure DevOps Services/Team Foundation Server (baseado no Git ou no Controle de Versão do Team Foundation), planejamento do Agile (com suporte para Agile, Scrum e CMMI), CI, gerenciamento de versão e outras ferramentas para equipes do Agile.

- O Azure DevOps Services e o Team Foundation Server incluem um ecossistema avançado e crescente de extensões internas e de terceiros com as quais você pode facilmente construir um pipeline de CI, build, teste, entrega e gerenciamento de versão para microsserviços.

- Execute testes automatizados como parte do seu pipeline de build no Azure DevOps Services.

- O Azure DevOps Services pode aprimorar o ciclo de vida do DevOps com entrega para vários ambientes, não apenas para ambientes de produção, mas também para teste, incluindo experimentação A/B, [versões canário](https://martinfowler.com/bliki/CanaryRelease.html) e assim por diante.

- As organizações podem provisionar com facilidade contêineres do Docker com base em imagens privadas armazenadas no Registro de Contêiner do Azure, juntamente com as dependências de componentes do Azure (Dados, PaaS, etc.) usando modelos do Azure Resource Manager com ferramentas com as quais elas já estão familiarizadas.

>[!div class="step-by-step"]
>[Anterior](../design-develop-containerized-apps/build-aspnet-core-applications-linux-containers-aks-kubernetes.md)
>[Próximo](docker-application-outer-loop-devops-workflow.md)
