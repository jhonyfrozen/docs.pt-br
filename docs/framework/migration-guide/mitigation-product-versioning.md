---
title: 'Mitigação: Controle de versão do produto'
ms.date: 03/30/2017
ms.assetid: 1c4de9d7-9aba-427a-8f38-0ab9bfb8f85e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d76615b5bd4d140917b84a52f7d1c251ca32302f
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489992"
---
# <a name="mitigation-product-versioning"></a>Mitigação: Controle de versão do produto
Na .NET Framework 4.6 e posterior, o controle de versão do produto foi alterado em relação às versões anteriores do .NET Framework (o .NET Framework 4, 4,5, 4.5.1 e 4.5.2).  
  
## <a name="product-versioning-changes"></a>Alterações no controle de versão de produto  
 Veja a seguir as alterações em detalhes:  
  
- O valor da entrada `Version` na chave `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` foi alterado para `4.6.`*xxxxx* para o .NET Framework 4.6 e suas versões pontuais, e para `4.7.`*xxxxx* para o .NET Framework 4.7. No .NET Framework 4.5, 4.5.1 e 4.5.2, ele tinha o formato `4.5.`*xxxxx*.  
  
- O controle de versão de arquivo e produto para arquivos do .NET Framework foi alterado do esquema de controle de versão anterior de `4.0.30319.x` para o de `4.6.X.0` para o .NET Framework 4.6 e suas versões pontuais, e para o de `4.7.X.0` para o .NET Framework 4.7 e suas versões pontuais. Você pode ver esses novos valores quando exibe as **Propriedades** do arquivo depois de clicar com o botão direito do mouse em um arquivo.  
  
- Os atributos <xref:System.Reflection.AssemblyFileVersionAttribute> e <xref:System.Reflection.AssemblyInformationalVersionAttribute> para assemblies gerenciados têm valores de <xref:System.Version> no formulário `4.6.X.0` para o .NET Framework 4.6 e suas versões pontuais, e `4.7.X.0` para o .NET Framework 4.7.  
  
- A partir do .NET Framework 4.6, a propriedade <xref:System.Environment.Version%2A?displayProperty=nameWithType> retorna a cadeia de caracteres de versão fixa `4.0.30319.42000`. No .NET Framework 4, 4.5, 4.5.1 e 4.5.2, ela retorna as cadeias de caracteres de versão no formato `4.0.30319.xxxxx`, em que `xxxxx` é menor que 42000 (por exemplo, "4.0.30319.18010"). Não é recomendável criar nova dependência de código de aplicativo na propriedade <xref:System.Environment.Version%2A?displayProperty=nameWithType>.
  
### <a name="handling-the-product-versioning-changes"></a>Como lidar com as alterações de controle de versão de produto  
 Em geral, os aplicativos devem depender das técnicas recomendadas para detecção de itens como a versão de tempo de execução do .NET Framework e o diretório de instalação:  
  
- Para detectar a versão de tempo de execução do .NET Framework, confira [Como: Determinar quais versões do .NET Framework estão instaladas](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md).  
  
- Para determinar o caminho de instalação do .NET Framework, use o valor da entrada `InstallPath` na chave `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`.  
  
    > [!IMPORTANT]
    >  O nome da subchave é `NET Framework Setup`, e não `.NET Framework Setup`.  
  
- Para determinar o caminho do diretório do Common Language Runtime do .NET Framework, chame o método <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory%2A?displayProperty=nameWithType>.  
  
- Para obter a versão do CLR, chame o método <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion%2A?displayProperty=nameWithType>.   Para o .NET Framework 4 e suas versões pontuais (o .NET Framework 4.5, 4.5.1, 4.5.2 e o .NET Framework 4.6, 4.6.1, 4.6.2 e 4.7), ele retorna a cadeia de caracteres `v4.0.30319`.  
  
## <a name="see-also"></a>Consulte também

- [Alterações no tempo de execução](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)
