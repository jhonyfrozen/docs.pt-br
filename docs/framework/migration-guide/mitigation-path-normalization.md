---
title: 'Mitigação: Normalização de caminho'
ms.date: 03/30/2017
ms.assetid: 158d47b1-ba6d-4fa6-8963-a012666bdc31
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5b1c704113c8e05e493cdb3ef24f6376ab54b1cb
ms.sourcegitcommit: 26f4a7697c32978f6a328c89dc4ea87034065989
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66251122"
---
# <a name="mitigation-path-normalization"></a>Mitigação: Normalização de caminho
Começando com os aplicativos direcionados ao .NET Framework 4.6.2, a normalização do caminho no .NET Framework foi alterada.  
  
## <a name="what-is-path-normalization"></a>O que é normalização do caminho?  
 Normalizar um caminho envolve modificar a cadeia de caracteres que identifica um caminho ou arquivo para que ele esteja em conformidade com um caminho válido no sistema operacional de destino. Normalmente, a normalização envolve:  
  
- Padronização de separadores de diretório e componente.  
  
- Aplicação do diretório atual a um caminho relativo.  
  
- Avaliação do diretório relativo (`.`) ou do diretório pai (`..`) em um caminho.  
  
- Remoção de determinados caracteres.  
  
## <a name="the-changes"></a>As alterações  
 Começando com os aplicativos direcionados ao .NET Framework 4.6.2, a normalização do caminho foi alterada nos seguintes aspectos:  
  
- O tempo de execução atende à função [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) do sistema operacional para normalizar caminhos.  
  
- A normalização não envolve mais a remoção do fim dos segmentos do diretório (como um espaço no fim do nome de um diretório).  
  
- Suporte à sintaxe do caminho do dispositivo em confiança total, incluindo `\\.\` e, para APIs de E/S de arquivo em mscorlib.dll, `\\?\`.  
  
- O tempo de execução não valida caminhos de sintaxe do dispositivo.  
  
- Há suporte ao uso da sintaxe de dispositivo para acessar fluxos de dados alternados.  
  
## <a name="impact"></a>Impacto  

Para os aplicativos direcionados ao .NET Framework 4.6.2 ou posterior, essas alterações estão ativadas por padrão. Elas devem melhorar o desempenho e ao mesmo tempo permitir que os métodos acessem caminhos anteriormente inacessíveis.  
  
Os aplicativos direcionados ao .NET Framework 4.6.1 e versões anteriores, mas que são executados no .NET Framework 4.6.2 ou posteriores, não são afetados por essa alteração.  
  
## <a name="mitigation"></a>Redução  
 Aplicativos destinados ao .NET Framework 4.6.2 ou posteriores podem recusar essa alteração e usar a normalização herdada adicionando o seguinte à seção [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do arquivo de configuração de aplicativo:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
</runtime>  
```  
  
Aplicativos destinados ao .NET Framework 4.6.1 ou anteriores, mas que são executados no .NET Framework 4.6.2 ou posteriores podem habilitar as alterações na normalização de caminho adicionando a seguinte linha à seção [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) do arquivo de configuração de aplicativo:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=false" />    
</runtime>  
```  
  
## <a name="see-also"></a>Consulte também

- [Alterações de redirecionamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-2.md)
