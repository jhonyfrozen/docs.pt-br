---
title: <remove> elemento para NameValueSectionHandler e DictionarySectionHandler
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/remove
helpviewer_keywords:
- remove Element
- <remove> Element
ms.assetid: 8d8af7f5-26c9-4db9-bbe4-b2a4e6949568
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: 062aa3921d29cffd33db2d96096ef25c2b819030
ms.sourcegitcommit: 621a5f6df00152006160987395b93b5b55f7ffcd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66300694"
---
# <a name="remove-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<Remover > elemento para NameValueSectionHandler e DictionarySectionHandler

Remove uma configuração definida anteriormente.

[ **\<configuration>** ](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[ **\<sectionName>** ](~/docs/framework/configure-apps/file-schema/custom-element-2.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<remove>**

## <a name="syntax"></a>Sintaxe

```xml
<add remove="key" />
```

## <a name="attribute"></a>Atributo

|           | Descrição |
| --------- | ----------- |
| **key**   | Atributo obrigatório.<br><br>Especifica o nome da configuração a ser removido. |

## <a name="parent-element"></a>Elemento pai

| Elemento | Descrição |
| ------- | ------------|
| [ **\<sectionName >** elemento](~/docs/framework/configure-apps/file-schema/custom-element-2.md) | Define as configurações para seções de configuração personalizadas que usam o <xref:System.Configuration.NameValueSectionHandler> e <xref:System.Configuration.DictionarySectionHandler> classes. |

## <a name="child-elements"></a>Elementos filho

Nenhum

## <a name="remarks"></a>Comentários

Você pode usar o  **\<remover >** elemento para remover as configurações do aplicativo que foram definidos em um nível mais alto na hierarquia do arquivo de configuração.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como usar o  **\<remover >** elemento em um arquivo de configuração de aplicativo para remover as configurações previamente definidas no arquivo de configuração do computador.

O seguinte código de arquivo de configuração de máquina declara a seção  **\<mySection >** e adiciona duas configurações, `key1` e `key2`, a ele:

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="mySection" type="System.Configuration.NameValueSectionHandler,System" />
  </configSections>
  <mySection>
    <add key="key1" value="value1" />
    <add key="key2" value="value2" />
  </mySection>
</configuration>
```

O seguinte código de arquivo de configuração de aplicativo remove o `key2` definindo a partir  **\<mySection >** :

```xml
<!--Application configuration file -->
<configuration>
  <mySection>
    <remove key="key2" />
  </mySection>
</configuration>
```

## <a name="configuration-file"></a>arquivo de configuração

Esse elemento pode ser usado no arquivo de configuração do aplicativo, arquivo de configuração de máquina (*Machine. config*), e *Web. config* arquivos que não estão no nível de diretório do aplicativo.

## <a name="see-also"></a>Consulte também

- [Esquema de arquivo de configuração para o .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
