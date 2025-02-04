---
title: Introdução ao Docker
description: Este artigo fornece uma visão geral e introdução ao Docker no contexto de um aplicativo .NET Core.
ms.date: 03/20/2019
ms.custom: mvc, seodec18
ms.openlocfilehash: d0bce09d7acdcf474fbb8849c8fc82dae4a69598
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753298"
---
# <a name="introduction-to-net-and-docker"></a>Introdução ao .NET e ao Docker

O .NET Core pode ser facilmente executado em um contêiner do Docker. Os contêineres oferecem uma maneira leve de isolar seu aplicativo do restante do sistema do host, compartilhando apenas o kernel e usando os recursos fornecidos para seu aplicativo. Se você não estiver familiarizado com o Docker, é altamente recomendável ler a [documentação de visão geral](https://docs.docker.com/engine/docker-overview/) do Docker.

Para saber mais sobre como instalar o Docker, confira a página de download de [Docker Desktop: Community Edition](https://www.docker.com/products/docker-desktop).

## <a name="docker-basics"></a>Noções básicas do Docker

Há alguns conceitos que você deve conhecer. O cliente do Docker tem um programa de interface de linha de comando que você usa para gerenciar imagens e contêineres. Conforme mencionado anteriormente, você deve reservar algum tempo para ler a documentação de [visão geral do Docker](https://docs.docker.com/engine/docker-overview/). 

### <a name="images"></a>Imagens

Uma imagem é uma coleção ordenada de alterações no sistema de arquivos que formam a base de um contêiner. A imagem não tem um estado e é somente leitura. Na maior parte das vezes, uma imagem é baseada em outra imagem, mas com alguma personalização. Por exemplo, quando você cria uma nova imagem para o aplicativo, você a baseará em uma imagem existente que já contenha o tempo de execução do .NET Core.

Como os contêineres são criados de imagens, as imagens têm um conjunto de parâmetros de execução (como um executável inicial) que são executados quando o contêiner é iniciado.

### <a name="containers"></a>Contêineres

Um contêiner é uma instância executável de uma imagem. Enquanto cria a imagem, você implanta seu aplicativo e dependências. Em seguida, vários contêineres podem ser instanciados, cada um isolado um do outro. Cada instância de contêiner tem seu próprio sistema de arquivos, memória e interface de rede.

### <a name="registries"></a>Registros

Registros de contêiner são uma coleção de repositórios de imagens. Você pode basear suas imagens em uma imagem de registro. Você pode criar contêineres diretamente em uma imagem em um registro. A [relação entre contêineres, imagens e registros do Docker](../../standard/microservices-architecture/container-docker-introduction/docker-containers-images-registries.md) é um conceito importante ao [arquitetar e compilar aplicativos ou microsserviços em contêineres](../../standard/microservices-architecture/architect-microservice-container-applications/index.md). Essa abordagem reduz bastante o tempo entre o desenvolvimento e a implantação.

O Docker tem um registro público disponível hospedado no [Hub do Docker](https://hub.docker.com/). As [imagens relacionadas ao .NET core](https://hub.docker.com/_/microsoft-dotnet-core/) estão listadas no Hub do Docker. 

O MCR (Registro de Contêiner da Microsoft) é a fonte oficial de imagens de contêiner fornecidas pela Microsoft. O MCR baseia-se na CDN do Azure para fornecer imagens replicadas globalmente. No entanto, o MCR não tem um site voltado ao público e a principal maneira de aprender sobre imagens de contêiner fornecidas pela Microsoft é por meio das [páginas do Hub do Docker da Microsoft](https://hub.docker.com/_/microsoft-dotnet-core/).

### <a name="dockerfile"></a>Dockerfile

Um **Dockerfile** é um arquivo que define um conjunto de instruções que cria uma imagem. Cada instrução no **Dockerfile** cria uma camada na imagem. Geralmente, quando você recria a imagem, somente as camadas que foram alteradas são recriadas. O **Dockerfile** pode ser distribuído para outras pessoas e permite que elas recriem para criar uma nova imagem da mesma maneira como você a criou. Embora isso permita distribuir as *instruções* sobre a criação de uma imagem, a principal forma de distribuir sua imagem é publicando-a em um registro.

## <a name="net-core-images"></a>Imagens do .NET Core

As imagens oficiais do Docker do .NET Core são publicadas no MCR (Registro de Contêiner da Microsoft) e podem ser encontradas no [repositório do Hub do Docker do .NET Core da Microsoft](https://hub.docker.com/_/microsoft-dotnet-core/). Cada repositório contém imagens para diferentes combinações do .NET (SDK ou Runtime) e do sistema operacional que você pode usar. 

A Microsoft fornece imagens personalizadas para cenários específicos. Por exemplo, o [repositório do ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) fornece imagens que são criadas para a execução de aplicativos ASP.NET Core na produção.

## <a name="azure-services"></a>Serviços do Azure

Vários serviços do Azure oferecem suporte a contêineres. Crie uma imagem do Docker para seu aplicativo e implante-a em um dos seguintes serviços:

* [AKS (Serviço de Kubernetes do Azure)](https://azure.microsoft.com/services/kubernetes-service/)\
Dimensione e orquestre contêineres do Linux usando o Kubernetes.

* [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/containers/)\
Implante aplicativos Web ou APIs usando contêineres do Linux em um ambiente PaaS.

* [Instâncias de Contêiner do Azure](https://azure.microsoft.com/services/container-instances/)\
Hospede seu contêiner na nuvem sem qualquer serviço de gerenciamento de nível superior.

* [Lote do Azure](https://azure.microsoft.com/services/batch/)\
Execute trabalhos de computação repetitivos usando contêineres.

* [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)\
Levantar, deslocar e modernizar aplicativos .NET para microsserviços usando contêineres do Windows Server

* [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry/)\
Armazene e gerencie imagens de contêiner em todos os tipos de implantações do Azure.

## <a name="next-steps"></a>Próximas etapas

* [Saiba como colocar em contêiner um aplicativo .NET Core.](build-docker-netcore-container.md)
* [Aprenda a colocar em contêiner um aplicativo ASP.NET Core.](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
* [Experimente o tutorial Saiba mais sobre o Microsserviço do ASP.NET Core.](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
* [Saiba mais sobre as Ferramentas de Contêiner no Visual Studio](/visualstudio/containers/overview)
