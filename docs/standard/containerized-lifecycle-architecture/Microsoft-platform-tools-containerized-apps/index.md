---
title: Introdução à plataforma e ferramentas da Microsoft para aplicativos em contêineres
description: Conheça as ofertas da Microsoft para dar suporte ao ciclo de vida de aplicativos do Docker.
ms.date: 02/15/2019
ms.openlocfilehash: 6907528a5d7ff354a312e7575531b9c608cb479f
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/13/2019
ms.locfileid: "66195593"
---
# <a name="introduction-to-the-microsoft-platform-andtools-for-containerized-apps"></a>Introdução à plataforma e às ferramentas da Microsoft para aplicativos em contêineres

*Visão: criar um ciclo de vida de aplicativo em contêineres adaptável e de nível empresarial que amplie o desenvolvimento, as operações de TI e o gerenciamento de produção.*

A Figura 3-1 mostra os pilares principais no ciclo de vida de aplicativos do Docker classificados por tipo de trabalho entregue por várias equipes (desenvolvimento de aplicativos, processos de infraestrutura de DevOps e o gerenciamento e operações de TI). Normalmente na empresa, os perfis de "a pessoa" responsável para cada área são diferentes. Suas habilidades também são diferentes.

![Ferramentas da Microsoft. Para a carga de trabalho de Desenvolvimento/Projeto: Mecanismo do Docker para Windows, VS e VS Code, .NET Core e Serviço de Kubernetes do Azure. Para a carga de trabalho de Build/Teste/Remessa: Azure DevOps, Team Foundation Server, CLI do Docker e Serviço de Kubernetes do Azure. Para a carga de trabalho de Execução/Monitoramento/Gerenciamento: Azure Monitor, Serviço de Kubernetes do Azure do Portal do Azure, Service Fabric e outros orquestradores.](./media/image1.png)

**Figura 3-1.** Principais pilares do ciclo de vida de aplicativos do Docker em contêineres com a plataforma e as ferramentas da Microsoft

Um fluxo de trabalho do ciclo de vida do Docker em contêineres pode ser inicialmente prescritivo com base nas “opções padrão de produto”, tornando mais fácil para os desenvolvedores começar a trabalhar mais rapidamente; porém, é fundamental haver uma estrutura aberta nos bastidores para que o fluxo de trabalho seja flexível e tenha a capacidade de ajustar-se aos diferentes contextos de cada organização ou empresa. A infraestrutura de fluxo de trabalho (componentes e produtos) deve ser flexível o suficiente para abranger o ambiente que cada empresa terá no futuro, mesmo sendo capaz de trocar de desenvolvimento ou produtos de DevOps por outros. Essa flexibilidade, a abertura e a ampla variedade de tecnologias na plataforma e infraestrutura são precisamente as prioridades da Microsoft para aplicativos em contêineres do Docker, conforme explicado nos capítulos a seguir.

A Tabela 3-1 demonstra que a intenção do Microsoft DevOps com relação aos aplicativos em contêineres do Docker é fornecer um fluxo de trabalho de DevOps livre para que você possa escolher quais produtos usar para cada fase (da Microsoft ou de terceiros), proporcionando um fluxo de trabalho simplificado que fornece “produtos padrão” já conectados. Dessa forma, você pode começar rapidamente com o fluxo de trabalho de DevOps de nível corporativo para aplicativos do Docker.

**Tabela 3-1.** Fluxos de trabalho do DevOps abertos para qualquer tecnologia

| Host | Tecnologias da Microsoft | Terceiros — Conectável ao Azure |
| ---------------------------| ----------------------------------------------------| --------------------------------------------------------------------------------|
| Plataforma para aplicativos do Docker   | • Microsoft Visual Studio e Visual Studio Code<br /> • .NET<br /> • AKS (Serviço de Kubernetes do Microsoft Azure)<br /> • Azure Service Fabric<br /> • Registro de Contêiner do Azure<br /> | • Qualquer editor de código (por exemplo, Sublime)<br /> • Qualquer linguagem (Node.js, Java, Go, etc.)<br /> • Qualquer orquestrador e agendador<br /> • Qualquer registro do Docker<br /> |
| DevOps para aplicativos do Docker     | • Azure DevOps Services<br /> • Microsoft Team Foundation Server<br /> • AKS (Serviço de Kubernetes do Azure)<br /> • Azure Service Fabric<br /> | • GitHub, Git, Subversion, etc.<br /> • Jenkins, Chef, Puppet, Velocity, CircleCI, TravisCI, etc.<br /> • Docker Datacenter, Docker Swarm, Mesos DC/OS, Kubernetes, etc. local<br /> |
| Gerenciamento e monitoramento  | • Azure Monitor | • Marathon, Chronos, etc.<br />|

A plataforma Microsoft e ferramentas para aplicativos em contêineres do Docker, conforme definido na tabela 3-1, incluem os seguintes componentes:

- **Plataforma para desenvolvimento de aplicativos de Docker** O desenvolvimento de um serviço ou coleção de serviços que compõem um “aplicativo”. A plataforma de desenvolvimento fornece todo o trabalho exigido pelos desenvolvedores antes de efetuar push do código para um repositório de código compartilhado. Os serviços de desenvolvimento, implantados como contêineres, são semelhantes ao desenvolvimento dos mesmos aplicativos ou serviços sem o Docker. Você continua a usar sua linguagem (.NET, Node.js, Go, etc.) e editor favoritos ou um IDE como o Visual Studio ou o Visual Studio Code. No entanto, em vez de considerar o Docker como um destino de implantação, você pode desenvolver seus serviços no ambiente do Docker. Você compila, executa, testa e depura o código em contêineres localmente, fornecendo o ambiente de destino no tempo de desenvolvimento. Ao fornecer o ambiente de destino localmente, os contêineres do Docker configuram o que ajudará a melhorar drasticamente seu ciclo de vida de DevOps. O Visual Studio e o Visual Studio Code têm extensões para integrar com contêineres do Docker em seu processo de desenvolvimento.

- **DevOps para aplicativos do Docker** Os desenvolvedores que criam aplicativos do Docker podem usar o [Azure DevOps Services](https://azure.microsoft.com/services/devops/) ou qualquer outro produto de terceiros, como o Jenkins, para criar um ALM (gerenciamento de ciclo de vida de aplicativos) automatizado e abrangente.

  Com o Azure DevOps Services, os desenvolvedores podem criar DevOps voltado para contêineres para um processo iterativo rápido que abrange o controle de código-fonte de qualquer lugar (Azure DevOps Services-Git, GitHub, qualquer repositório Git remoto ou Subversion), CI (Integração Contínua), testes de unidade interna, testes entre contêineres/de integração do serviço, CD (Entrega Contínua) e RM (gerenciamento de versão). Os desenvolvedores também podem automatizar suas versões de aplicativo do Docker dentro do AKS (Serviço de Kubernetes do Azure), desde o desenvolvimento até os ambientes de preparo e produção.

- **Gerenciamento e Monitoramento** O time de TI pode gerenciar e monitorar aplicativos e serviços de produção de várias maneiras, integrando ambas as perspectivas em uma experiência consolidada.

  - **Portal do Azure** Se você estiver usando orquestradores de open-source, o AKS (Serviço de Kubernetes do Azure), o Service Fabric e outros orquestradores o ajudam a configurar e manter seus ambientes do Docker. Se você estiver usando o Azure Service Fabric, a ferramenta Service Fabric Explorer possibilita visualizar e configurar o cluster.

  - **Ferramentas do Docker** Você pode gerenciar seus aplicativos de contêiner usando ferramentas familiares. Não é necessário alterar suas práticas de gerenciamento existentes do Docker para mover cargas de trabalho do contêiner para a nuvem. Use as ferramentas de gerenciamento de aplicativo com as quais você já está familiarizado e conecte-se por meio de pontos de extremidade de API padrão ao orquestrador de sua escolha. Você também pode usar outras ferramentas de terceiros para gerenciar seus aplicativos do Docker, como Docker Datacenter ou até mesmo as ferramentas do Docker CLI. 

    Mesmo que você esteja familiarizado com os comandos do Linux, você pode gerenciar seus aplicativos de contêiner usando o Microsoft Windows e o PowerShell com uma linha de comando de subsistema do Linux e os produtos (Docker, Kubernetes...) clientes executando nessa funcionalidade de Subsistema do Linux. Você verá mais sobre como usar essas ferramentas no Subsistema do Linux usando seu SO favorito do Microsoft Windows mais adiante neste livro.

  - **Ferramentas de open-source** Como o AKS expõe os pontos de extremidade de API padrão para o mecanismo de orquestração, as ferramentas mais populares são compatíveis com o AKS e, na maioria dos casos, funcionarão de imediato – incluindo visualizadores, monitoramento, ferramentas de linha de comando e até mesmo ferramentas futuras à medida que forem disponibilizadas.

  - **Azure Monitor** É a solução do Azure para monitorar todos os aspectos do seu ambiente de produção. Você pode monitorar aplicativos do Docker de produção apenas configurando seu SDK nos seus serviços de forma a obter dos aplicativos dados de log gerados pelo sistema.

Dessa forma, a Microsoft oferece uma base completa para um ciclo de vida de ponta a ponta para aplicativos do Docker em contêineres. No entanto, é *uma coleção de produtos e tecnologias que permitem que você, opcionalmente, selecione e se integre a ferramentas e processos existentes*. A flexibilidade de uma abordagem ampla junto com a força da profundidade dos recursos colocam a Microsoft em uma forte posição para desenvolvimento de aplicativos em contêineres do Docker.

>[!div class="step-by-step"]
>[Anterior](../Docker-application-lifecycle/containers-foundation-for-devops-collaboration.md)
>[Próximo](../design-develop-containerized-apps/index.md)
