---
title: Elemento <NetFx40_LegacySecurityPolicy>
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_LegacySecurityPolicy> element
- NetFx40_LegacySecurityPolicy element
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e5bfa5449ece1b24d4f47fe3e77e36b26bbe430c
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66689837"
---
# <a name="netfx40legacysecuritypolicy-element"></a>\<NetFx40_LegacySecurityPolicy > elemento

Especifica se o tempo de execução usa a política de CAS (Segurança de Acesso do Código) herdada.

\<configuration>\
\<runtime>\
\<NetFx40_LegacySecurityPolicy>

## <a name="syntax"></a>Sintaxe

```xml
<NetFx40_LegacySecurityPolicy
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Atributo obrigatório.<br /><br /> Especifica se o tempo de execução usa a política CAS herdada.|

## <a name="enabled-attribute"></a>Atributo habilitado

|Valor|Descrição|
|-----------|-----------------|
|`false`|O tempo de execução não usa a política CAS herdada. Esse é o padrão.|
|`true`|O tempo de execução usa a política CAS herdada.|

### <a name="child-elements"></a>Elementos filho

nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|
|`runtime`|Contém informações sobre opções de inicialização do tempo de execução.|

## <a name="remarks"></a>Comentários

No .NET Framework versão 3.5 e versões anteriores, a política de CAS está sempre em vigor. No .NET Framework 4, a política de CAS deve estar habilitada.

Política de CAS é específico da versão. As políticas personalizadas do CAS que existem nas versões anteriores do .NET Framework devem ser especificadas novamente no .NET Framework 4.

Aplicando o `<NetFx40_LegacySecurityPolicy>` não afeta o elemento a um assembly do .NET Framework 4 [código transparente de segurança](../../../../../docs/framework/misc/security-transparent-code.md); as regras de transparência ainda se aplicam.

> [!IMPORTANT]
> Aplicando o `<NetFx40_LegacySecurityPolicy>` elemento pode resultar em penalidades de desempenho significativos para os assemblies de imagem nativa criados pelo [gerador de imagem nativa (Ngen.exe)](../../../../../docs/framework/tools/ngen-exe-native-image-generator.md) que não estão instaladas no [cache de assembly global ](../../../../../docs/framework/app-domains/gac.md). A degradação do desempenho é causada pela incapacidade do tempo de execução para carregar os assemblies como imagens nativas, quando o atributo é aplicado, resultando em seus que está sendo carregado assemblies como just-in-time.

> [!NOTE]
> Se você especificar uma versão do .NET Framework de destino que é anterior ao .NET Framework 4, nas configurações do projeto para o seu projeto do Visual Studio, política de CAS será habilitada, incluindo as políticas personalizadas de CAS especificado para essa versão. No entanto, você não poderá usar os novos tipos do .NET Framework 4 e membros. Você também pode especificar uma versão anterior do .NET Framework usando o [ \<supportedRuntime > elemento](../../../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) no esquema de configurações de inicialização em seu [arquivo de configuração de aplicativo](../../../../../docs/framework/configure-apps/index.md).

> [!NOTE]
> Sintaxe do arquivo de configuração diferencia maiusculas de minúsculas. Você deve usar a sintaxe conforme fornecidos nas seções de sintaxe e exemplo.

## <a name="configuration-file"></a>Arquivo de Configuração

Esse elemento pode ser usado apenas no arquivo de configuração do aplicativo.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como habilitar a política CAS herdada para um aplicativo.

```xml
<configuration>
   <runtime>
      <NetFx40_LegacySecurityPolicy enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>Consulte também

- [Esquema de configurações do tempo de execução](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [Esquema de arquivos de configuração](../../../../../docs/framework/configure-apps/file-schema/index.md)
