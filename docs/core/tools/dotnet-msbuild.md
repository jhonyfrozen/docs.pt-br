---
title: Comando dotnet msbuild
description: O comando dotnet msbuild fornece acesso à linha de comando MSBuild.
ms.date: 12/03/2018
ms.openlocfilehash: 983fae6f4ecf875da0b155a668009984b5df50de
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632024"
---
# <a name="dotnet-msbuild"></a>dotnet msbuild

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>Nome

`dotnet msbuild` – Compila um projeto e todas as suas dependências.

## <a name="synopsis"></a>Sinopse

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>Descrição

O comando `dotnet msbuild` permite o acesso a um MSBuild totalmente funcional.

O comando tem exatamente os mesmos recursos do cliente de linha de comando existente do MSBuild somente para projetos no estilo SDK. As opções são todas iguais. Para obter mais informações sobre as opções disponíveis, confira a [Referência de linha de comando do MSBuild](/visualstudio/msbuild/msbuild-command-line-reference).

O comando [dotnet build](dotnet-build.md) é equivalente ao comando `dotnet msbuild -restore -target:Build`. `dotnet build` é mais comumente usado na criação de projetos, mas `dotnet msbuild` oferece mais controle. Por exemplo, se houver um destino específico que você deseja executar (sem executar o destino do build), convém usar `dotnet msbuild`.

## <a name="examples"></a>Exemplos

* Compile um projeto e suas dependências:

  ```console
  dotnet msbuild
  ```

* Compile um projeto e suas dependências usando a configuração da Versão:

  ```console
  dotnet msbuild -p:Configuration=Release
  ```

* Execute o destino de publicação e publique para o RID `osx.10.11-x64`:

  ```console
  dotnet msbuild -t:Publish -p:RuntimeIdentifiers=osx.10.11-x64
  ```

* Confira o projeto inteiro com todos os destinos incluídos pelo SDK:

  ```console
  dotnet msbuild -pp
  ```
