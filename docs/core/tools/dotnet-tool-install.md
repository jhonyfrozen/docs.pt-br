---
title: Comando dotnet tool install – CLI do .NET Core
description: O comando dotnet tool install instala no computador a Ferramenta Global do .NET Core especificada.
author: mairaw
ms.author: mairaw
ms.date: 05/29/2018
ms.openlocfilehash: f3068848910d6672a10ecfb639bac8e18a72818d
ms.sourcegitcommit: bbf70abe6b46073148f78cbf0619de6092b5800c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34697281"
---
# <a name="dotnet-tool-install"></a><span data-ttu-id="78906-103">dotnet tool install</span><span class="sxs-lookup"><span data-stu-id="78906-103">dotnet tool install</span></span>

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="name"></a><span data-ttu-id="78906-104">Nome</span><span class="sxs-lookup"><span data-stu-id="78906-104">Name</span></span>

<span data-ttu-id="78906-105">`dotnet tool install` – instala a [Ferramenta Global do .NET Core](global-tools.md) especificada no computador.</span><span class="sxs-lookup"><span data-stu-id="78906-105">`dotnet tool install` - Installs the specified [.NET Core Global Tool](global-tools.md) on your machine.</span></span>

## <a name="synopsis"></a><span data-ttu-id="78906-106">Sinopse</span><span class="sxs-lookup"><span data-stu-id="78906-106">Synopsis</span></span>

```
dotnet tool install <PACKAGE_NAME> <-g|--global> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <PACKAGE_NAME> <--tool-path> [--add-source] [--configfile] [--framework] [-v|--verbosity] [--version]
dotnet tool install <-h|--help>
```

## <a name="description"></a><span data-ttu-id="78906-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="78906-107">Description</span></span>

<span data-ttu-id="78906-108">O comando `dotnet tool install` fornece uma maneira de instalar no computador as Ferramentas Globais do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="78906-108">The `dotnet tool install` command provides a way for you to install .NET Core Global Tools on your machine.</span></span> <span data-ttu-id="78906-109">Para usar o comando, você precisa especificar que deseja uma instalação de todos os usuários usando a opção `--global` ou especificar um caminho para instalá-la usando a opção `--tool-path`.</span><span class="sxs-lookup"><span data-stu-id="78906-109">To use the command, you either have to specify that you want a user-wide installation using the `--global` option or you specify a path to install it using the `--tool-path` option.</span></span>

<span data-ttu-id="78906-110">As Ferramentas Globais são instaladas nos seguintes diretórios por padrão quando você especifica a opção `-g` (ou `--global`):</span><span class="sxs-lookup"><span data-stu-id="78906-110">Global Tools are installed in the following directories by default when you specify the `-g` (or `--global`) option:</span></span>

| <span data-ttu-id="78906-111">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="78906-111">OS</span></span>          | <span data-ttu-id="78906-112">Caminho</span><span class="sxs-lookup"><span data-stu-id="78906-112">Path</span></span>                          |
|-------------|-------------------------------|
| <span data-ttu-id="78906-113">Linux/macOS</span><span class="sxs-lookup"><span data-stu-id="78906-113">Linux/macOS</span></span> | `$HOME/.dotnet/tools`         |
| <span data-ttu-id="78906-114">Windows</span><span class="sxs-lookup"><span data-stu-id="78906-114">Windows</span></span>     | `%USERPROFILE%\.dotnet\tools` |

## <a name="arguments"></a><span data-ttu-id="78906-115">Arguments</span><span class="sxs-lookup"><span data-stu-id="78906-115">Arguments</span></span>

`PACKAGE_NAME`

<span data-ttu-id="78906-116">Nome/ID do pacote NuGet que contém a Ferramenta Global do .NET Core a ser instalada.</span><span class="sxs-lookup"><span data-stu-id="78906-116">Name/ID of the NuGet package that contains the .NET Core Global Tool to install.</span></span>

## <a name="options"></a><span data-ttu-id="78906-117">Opções</span><span class="sxs-lookup"><span data-stu-id="78906-117">Options</span></span>

`--add-source <SOURCE>`

<span data-ttu-id="78906-118">Adiciona outra origem do pacote NuGet a ser usada durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="78906-118">Adds an additional NuGet package source to use during installation.</span></span>

`--configfile <FILE>`

<span data-ttu-id="78906-119">O arquivo de configuração do NuGet (*nuget.config*) a ser usado.</span><span class="sxs-lookup"><span data-stu-id="78906-119">The NuGet configuration (*nuget.config*) file to use.</span></span>

`--framework <FRAMEWORK>`

<span data-ttu-id="78906-120">Especifica a [estrutura de destino](../../standard/frameworks.md) para a qual instalar a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="78906-120">Specifies the [target framework](../../standard/frameworks.md) to install the tool for.</span></span> <span data-ttu-id="78906-121">Por padrão, o SDK do .NET Core tenta escolher a estrutura de destino mais apropriada.</span><span class="sxs-lookup"><span data-stu-id="78906-121">By default, the .NET Core SDK tries to choose the most appropriate target framework.</span></span>

`-g|--global`

<span data-ttu-id="78906-122">Especifica que a instalação é de todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="78906-122">Specifies that the installation is user wide.</span></span> <span data-ttu-id="78906-123">Não pode ser combinada com a opção `--tool-path`.</span><span class="sxs-lookup"><span data-stu-id="78906-123">Can't be combined with the `--tool-path` option.</span></span> <span data-ttu-id="78906-124">Se você não especificar essa opção, especifique a opção `--tool-path`.</span><span class="sxs-lookup"><span data-stu-id="78906-124">If you don't specify this option, you must specify the `--tool-path` option.</span></span>

`-h|--help`

<span data-ttu-id="78906-125">Imprime uma ajuda breve para o comando.</span><span class="sxs-lookup"><span data-stu-id="78906-125">Prints out a short help for the command.</span></span>

`--tool-path <PATH>`

<span data-ttu-id="78906-126">Especifica o local do qual a Ferramenta Global será instalada.</span><span class="sxs-lookup"><span data-stu-id="78906-126">Specifies the location where to install the Global Tool.</span></span> <span data-ttu-id="78906-127">PATH pode ser absoluto ou relativo.</span><span class="sxs-lookup"><span data-stu-id="78906-127">PATH can be absolute or relative.</span></span> <span data-ttu-id="78906-128">Se PATH não existir, o comando tentará criá-lo.</span><span class="sxs-lookup"><span data-stu-id="78906-128">If PATH doesn't exist, the command tries to create it.</span></span> <span data-ttu-id="78906-129">Não pode ser combinada com a opção `--global`.</span><span class="sxs-lookup"><span data-stu-id="78906-129">Can't be combined with the `--global` option.</span></span> <span data-ttu-id="78906-130">Se você não especificar essa opção, especifique a opção `--global`.</span><span class="sxs-lookup"><span data-stu-id="78906-130">If you don't specify this option, you must specify the `--global` option.</span></span>

`-v|--verbosity <LEVEL>`

<span data-ttu-id="78906-131">Define o nível de detalhes do comando.</span><span class="sxs-lookup"><span data-stu-id="78906-131">Sets the verbosity level of the command.</span></span> <span data-ttu-id="78906-132">Os valores permitidos são `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.</span><span class="sxs-lookup"><span data-stu-id="78906-132">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span>

`--version <VERSION_NUMBER>`

<span data-ttu-id="78906-133">A versão da ferramenta a ser instalada.</span><span class="sxs-lookup"><span data-stu-id="78906-133">The version of the tool to install.</span></span> <span data-ttu-id="78906-134">Por padrão, a última versão estável do pacote é instalada.</span><span class="sxs-lookup"><span data-stu-id="78906-134">By default, the latest stable package version is installed.</span></span> <span data-ttu-id="78906-135">Use essa opção para instalar a versão prévia ou versões mais antigas da ferramenta.</span><span class="sxs-lookup"><span data-stu-id="78906-135">Use this option to install preview or older versions of the tool.</span></span>

## <a name="examples"></a><span data-ttu-id="78906-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="78906-136">Examples</span></span>

<span data-ttu-id="78906-137">Instala a Ferramenta Global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) na localização padrão:</span><span class="sxs-lookup"><span data-stu-id="78906-137">Installs the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool in the default location:</span></span>

`dotnet tool install -g dotnetsay`

<span data-ttu-id="78906-138">Instala a Ferramenta Global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) em uma pasta específica do Windows:</span><span class="sxs-lookup"><span data-stu-id="78906-138">Installs the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool on a specific Windows folder:</span></span>

`dotnet tool install dotnetsay --tool-path c:\global-tools`

<span data-ttu-id="78906-139">Instala a Ferramenta Global [dotnetsay](https://www.nuget.org/packages/dotnetsay/) em uma pasta específica do Linux/macOS:</span><span class="sxs-lookup"><span data-stu-id="78906-139">Installs the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool on a specific Linux/macOS folder:</span></span>

`dotnet tool install dotnetsay --tool-path ~/bin`

<span data-ttu-id="78906-140">Instala a versão 2.0.0 da Ferramenta Global [dotnetsay](https://www.nuget.org/packages/dotnetsay/):</span><span class="sxs-lookup"><span data-stu-id="78906-140">Installs version 2.0.0 of the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) Global Tool:</span></span>

`dotnet tool install -g dotnetsay --version 2.0.0`

## <a name="see-also"></a><span data-ttu-id="78906-141">Consulte também</span><span class="sxs-lookup"><span data-stu-id="78906-141">See also</span></span>

[<span data-ttu-id="78906-142">Ferramentas Globais do .NET Core</span><span class="sxs-lookup"><span data-stu-id="78906-142">.NET Core Global Tools</span></span>](global-tools.md)