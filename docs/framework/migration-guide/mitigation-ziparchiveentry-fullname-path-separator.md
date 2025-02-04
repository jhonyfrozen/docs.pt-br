---
title: 'Mitigação: Separador de caminho ZipArchiveEntry.FullName'
ms.date: 03/30/2017
helpviewer_keywords:
- application compatibility
- ',NET Framework application compatibility'
- .NET Framework 4.6.1
- .NET Framework 4.6.1 retargeting changes
- retargeting changes
ms.assetid: 8d575722-4fb6-49a2-8a06-f72d62dc3766
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 908ac7c441dbb7f6c70b9fafc701d403fc153222
ms.sourcegitcommit: 26f4a7697c32978f6a328c89dc4ea87034065989
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66251081"
---
# <a name="mitigation-ziparchiveentryfullname-path-separator"></a>Mitigação: Separador de caminho ZipArchiveEntry.FullName
Começando com aplicativos direcionados ao .NET Framework 4.6.1, o separador de caminho usado na propriedade <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> foi alterado da barra invertida ("\\") usada nas versões anteriores do .NET Framework para uma barra ("/").   Os objetos <xref:System.IO.Compression.ZipArchiveEntry?displayProperty=nameWithType> são criados chamando uma das sobrecargas do método <xref:System.IO.Compression.ZipFile.CreateFromDirectory%2A?displayProperty=nameWithType>.  
  
## <a name="impact"></a>Impacto  
 A alteração traz a implementação do .NET em conformidade com a seção 4.4.17.1 da [Especificação de formato de arquivo .ZIP](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT) e permite que arquivamentos .ZIP sejam descompactados em sistemas não Windows.  
  
 A descompactação de um arquivo zip criado por um aplicativo que se destina a uma versão anterior do .NET Framework em sistemas operacionais não Windows, como o Macintosh, falha na preservação da estrutura de diretório. Por exemplo, no Macintosh, ela cria um conjunto de arquivos cujo nome de arquivo concatena o caminho do diretório com qualquer caractere de barra invertida ("\\") e o nome do arquivo. Consequentemente, a estrutura do diretório de arquivos descompactados não é preservada.  
  
 O impacto dessa alteração em arquivos .ZIP que são descompactados no sistema operacional Windows por APIs no namespace <xref:System.IO> do .NET Framework deve ser mínimo, uma vez que as APIs podem lidar perfeitamente com uma barra ("/") ou uma barra invertida ("\\") como o caractere separador de caminho.  
  
## <a name="mitigation"></a>Redução  
 Se esse comportamento for indesejável, você poderá recusar adicionando uma definição de configuração à seção [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do seu arquivo de configuração de aplicativo. Veja a seguir a seção `<runtime>` e a opção de recusa.  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=true" />  
</runtime>  
```  
  
 Além disso, os aplicativos destinados a versões anteriores do .NET Framework, mas estão sendo executados no .NET Framework 4.6.1 e versões posteriores, podem aceitar esse comportamento adicionando uma definição de configuração à seção [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do arquivo de configuração de aplicativo. Veja a seguir a seção `<runtime>` e a opção de aceitação.  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IO.Compression.ZipFile.UseBackslash=false" />  
</runtime>  
```  
  
## <a name="see-also"></a>Consulte também

- [Alterações de redirecionamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-1.md)
- [Compatibilidade de aplicativos na versão 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)
