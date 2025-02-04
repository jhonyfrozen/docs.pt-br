---
title: Elemento <clear> para <configSections>
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 77f1d761-ff45-4001-8f36-3a3e5c41fa63
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: e79def513637937262d00b0edb1b0f7676fd120b
ms.sourcegitcommit: 621a5f6df00152006160987395b93b5b55f7ffcd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66300800"
---
# <a name="clear-element-for-configsections"></a>\<Limpar > elemento para \<configSections >

Limpa todas as seções definidas anteriormente e grupos de seções.

[ **\<configuration>** ](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear>**

## <a name="syntax"></a>Sintaxe

```xml
<clear/>
```

## <a name="attribute"></a>Atributo

|           | Descrição |
| --------- | ----------- |
| **name**  | Atributo obrigatório.<br><br>Especifica o nome da seção ou grupo da seção a ser removido. |

## <a name="parent-element"></a>Elemento pai

|     | Descrição |
| --- | ----------- |
| [ **\<configSections>** Element](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) | Contém as declarações de namespace e a seção de configuração. |

## <a name="child-elements"></a>Elementos filho

Nenhum

## <a name="remarks"></a>Comentários

O  **\<limpar >** elemento remove todas as seções e grupos de seções do seu aplicativo que foram definidos anteriormente no arquivo de configuração atual ou em um nível mais alto na hierarquia do arquivo de configuração.

## <a name="example"></a>Exemplo

Este exemplo define um arquivo de configuração do computador e um arquivo de configuração de aplicativo e mostra como usar o  **\<limpar >** elemento em um arquivo de configuração de aplicativo para limpar as seções definidas anteriormente no arquivo de configuração do computador.

O seguinte código de arquivo de configuração de máquina declara duas seções,  **\<sampleSection >** e  **\<anotherSampleSection >** , que são lidos antes que o aplicativo arquivo de configuração:

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
    <section name="anotherSampleSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

O seguinte código de arquivo de configuração de aplicativo limpa todas as seções declaradas anteriormente. O aplicativo não pode usar ou recuperar as configurações em qualquer uma das seções que foram declaradas no arquivo de configuração do computador. No entanto, ele pode usar as configurações do  **\<anotherSection >** porque ele vem após o  **\<limpar >** elemento.

```xml
<!-- Application configuration file -->
<configuration>
  <configSections>
    <clear/>
    <section name="anotherSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <anotherSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>arquivo de configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo, arquivo de configuração de máquina (*Machine. config*), e *Web. config* arquivos que não estão no nível de diretório do aplicativo.

## <a name="see-also"></a>Consulte também

- [Esquema de arquivo de configuração para o .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
