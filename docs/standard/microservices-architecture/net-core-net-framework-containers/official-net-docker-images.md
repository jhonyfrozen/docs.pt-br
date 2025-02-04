---
title: Imagens oficiais do .NET Docker
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Imagens oficiais do .NET Docker
ms.date: 01/07/2019
ms.openlocfilehash: b184e8f3606da8448a06a1cad90688958ecbce3a
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644320"
---
# <a name="official-net-docker-images"></a>Imagens oficiais do .NET Docker

As imagens oficiais do .NET Docker são imagens do Docker criadas e otimizadas pela Microsoft. Elas ficam publicamente disponíveis nos repositórios da Microsoft no [Hub do Docker](https://hub.docker.com/u/microsoft/). Cada repositório pode conter várias imagens, dependendo de versões do .NET e, dependendo do sistema operacional e das versões (Linux Debian, Linux Alpine, Windows Nano Server, Windows Server Core, etc.).

Desde o .NET Core 2.1, todas as imagens do .NET Core, inclusive para o ASP.NET Core, estão disponíveis no Docker Hub no repositório de imagens do .NET Core: https://hub.docker.com/_/microsoft-dotnet-core/

A maioria dos repositórios de imagens fornecem marcação extensiva para ajudar a selecionar não apenas uma versão de estrutura específica, mas também escolher um sistema operacional (distribuição Linux ou versão do Windows).

## <a name="net-core-and-docker-image-optimizations-for-development-versus-production"></a>Otimizações de imagem do .NET Core e do Docker para desenvolvimento versus produção

Ao criar imagens do Docker para desenvolvedores, a Microsoft se concentrava nos seguintes cenários principais:

- Imagens usadas para *desenvolver* e criar aplicativos .NET Core.

- Imagens usadas para *executar* aplicativos .NET Core.

Por que várias imagens? Ao desenvolver, criar e executar aplicativos em contêineres, você geralmente tem prioridades diferentes. Fornecendo diferentes imagens para essas tarefas separadas, a Microsoft ajuda a otimizar os processos separados de desenvolver, criar e implantar aplicativos.

### <a name="during-development-and-build"></a>Durante o desenvolvimento e o build

Durante o desenvolvimento, o que é importante é a velocidade em que é possível iterar alterações e a capacidade de depurá-las. O tamanho da imagem não é tão importante quanto a capacidade de fazer alterações em seu código e ver as alterações rapidamente. Algumas ferramentas e "contêineres de agentes de build" usam a imagem de desenvolvimento do .NET Core (*mcr.microsoft.com/dotnet/core/sdk:2.2*) durante o processo de build e desenvolvimento. Ao compilar dentro de um contêiner do Docker, os aspectos importantes são os elementos necessários a fim de compilar seu aplicativo. Isso inclui o compilador e quaisquer outras dependências do .NET.

Por que este tipo de imagem de build é importante? Você não implanta essa imagem em produção. Em vez disso, é uma imagem usada para criar o conteúdo inserido em uma imagem de produção. Essa imagem seria usada em seu ambiente de CI (integração contínua) ou no ambiente de build ao usar builds do Docker Multi-stage.

### <a name="in-production"></a>Em produção

O que é importante na produção é a rapidez com que é possível implantar e iniciar seus contêineres com base em uma imagem do .NET Core de produção. Portanto, a imagem somente em tempo de execução baseada em *mcr.microsoft.com/dotnet/core/aspnet:2.2* é pequena, de modo que ela consegue percorrer rapidamente a rede do Registro do Docker para os hosts do Docker. O conteúdo está pronto para ser executado, habilitando o tempo mais rápido possível da inicialização do contêiner ao processamento de resultados. No modelo do Docker, não há necessidade de compilação de código C\#, como há quando você executa dotnet build ou dotnet publish ao usar o contêiner de build.

Nesta imagem otimizada você colocar somente os binários e outro conteúdo necessário para executar o aplicativo. Por exemplo, o conteúdo criado pelo dotnet publish contém apenas os binários do .NET compilados, imagens e arquivos .js e .css. Ao longo do tempo, você verá imagens que contêm pacotes pré-compilados (compilação de IL para nativa que ocorre em tempo de execução).

Embora haja várias versões das imagens do .NET Core e do ASP.NET Core, todas elas compartilham uma ou mais camadas, incluindo a camada base. Portanto, a quantidade de espaço em disco necessário para armazenar uma imagem é pequena, ela é composta apenas pelo delta entre sua imagem personalizada e sua imagem de base. O resultado é que é rápido extrair a imagem do Registro.

Quando você explorar os repositórios de imagem do .NET no Hub do Docker, encontrará várias versões de imagem confidenciais ou marcadas. Essas marcas ajudam a decidir qual usar, dependendo da versão de que você precisa, como as que estão na tabela a seguir:

| Image                                       | Comentários                                                                                          |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| mcr.microsoft.com/dotnet/core/aspnet:**2.2** | ASP.NET Core, somente com tempo de execução e otimizações de ASP.NET Core, no Linux e no Windows (várias arquiteturas) |
| mcr.microsoft.com/dotnet/core/sdk:**2.2**    | .NET Core, com SDKs incluídos, no Linux e no Windows (várias arquiteturas)                                  |

> [!div class="step-by-step"]
> [Anterior](net-container-os-targets.md)
> [Próximo](../architect-microservice-container-applications/index.md)
