---
title: Executar aplicativos do .NET Framework 1.1 no Windows 8, Windows 8.1 ou Windows 10
ms.date: 05/26/2017
helpviewer_keywords:
- Windows 8, running .NET Framework 1.1 apps
- .NET Framework 1.1, running on Windows 8
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3ad78c9a277af23eebe357ef986ea59d16bb444e
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833729"
---
# <a name="run-net-framework-11-apps-on-windows-8-windows-81-or-windows-10"></a>Executar aplicativos do .NET Framework 1.1 no Windows 8, Windows 8.1 ou Windows 10

O .NET Framework 1.1 não tem suporte nos sistemas operacionais [!INCLUDE[win8](../../../includes/win8-md.md)], [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] ou Windows 10. Em alguns casos, o .NET Framework 1.1 é especificamente identificado conforme necessário para um aplicativo ser executado. Nesses casos, entre em contato com seu ISV (fornecedor independente de software) para que o aplicativo seja atualizado para execução no .NET Framework 3.5 SP1 ou versões posteriores. Para saber mais, confira [Migrar do .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md).

## <a name="install-the-net-framework-11-from-a-cd-or-download-center"></a>Instalar o .NET Framework 1.1 de um CD ou do Centro de Download

Não é possível instalar manualmente o .NET Framework 1.1 no [!INCLUDE[win8](../../../includes/win8-md.md)], no [!INCLUDE[win81](../../../includes/win81-md.md)], no [!INCLUDE[winserver8](../../../includes/winserver8-md.md)], no [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] ou no Windows 10. Ele não é mais compatível. Se você tentar instalar o pacote, a seguinte mensagem de erro será exibida: "A instalação não pode continuar porque esta versão do .NET Framework é incompatível com uma instalada anteriormente." Para resolver esse problema, instale o [.NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22). Essa versão inclui o .NET Framework 2.0 (a versão após o .NET Framework 1.1), que tem suporte no [!INCLUDE[win8](../../../includes/win8-md.md)], no [!INCLUDE[win81](../../../includes/win81-md.md)] e no Windows 10. Você sempre deve tentar instalar o aplicativo primeiro para determinar se ele será atualizado automaticamente para uma versão posterior do .NET Framework. Caso contrário, entre em contato com seu ISV para obter uma atualização do aplicativo.

## <a name="see-also"></a>Consulte também

- [Migrando do .NET Framework 1.1](../../../docs/framework/migration-guide/migrating-from-the-net-framework-1-1.md)
- [Instalar o .NET Framework 3.5 no Windows 10, no Windows 8.1 e no Windows 8](../../../docs/framework/install/dotnet-35-windows-10.md)
