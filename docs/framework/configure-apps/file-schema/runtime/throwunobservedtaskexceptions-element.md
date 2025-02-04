---
title: Elemento <ThrowUnobservedTaskExceptions>
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ThrowUnobservedTaskExceptions element
- <ThrowUnobservedTaskExceptions> element
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9647297bf976d26a97be0da8807d607789e8a065
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489579"
---
# <a name="throwunobservedtaskexceptions-element"></a>\<ThrowUnobservedTaskExceptions > elemento
Especifica se as exceções de tarefas sem tratamento devem encerrar um processo em execução.  
  
 \<configuration>  
\<runtime>  
\<ThrowUnobservedTaskExceptions>  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`enabled`|Atributo obrigatório.<br /><br /> Especifica se as exceções de tarefa sem tratamento devem encerrar o processo em execução.|  
  
## <a name="enabled-attribute"></a>Atributo habilitado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`false`|Não encerra o processo em execução para uma exceção de tarefa sem tratamento. Esse é o padrão.|  
|`true`|Encerra o processo em execução para uma exceção de tarefa sem tratamento.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`configuration`|O elemento raiz em cada arquivo de configuração usado pelos aplicativos do Common Language Runtime e .NET Framework.|  
|`runtime`|Contém informações sobre opções de inicialização do tempo de execução.|  
|||  
  
## <a name="remarks"></a>Comentários  
 Se uma exceção que está associada com um <xref:System.Threading.Tasks.Task> não foi observado, não há nenhuma <xref:System.Threading.Tasks.Task.Wait%2A> operação, o pai não estiver anexada e o <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> propriedade não foi lido a exceção de tarefa é considerada não observado.  
  
 No .NET Framework 4, por padrão, se um <xref:System.Threading.Tasks.Task> que tem um observada exceção é coletado como lixo, o finalizador lança uma exceção e finaliza o processo. O encerramento do processo é determinado pela medição de tempo de coleta de lixo e finalização.  
  
 Para tornar mais fácil para os desenvolvedores escrevam código assíncrono com base em tarefas, o .NET Framework 4.5 altera esse comportamento padrão para exceções não observadas que. Exceções não observadas ainda fazer com que o <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> evento seja acionado, mas por padrão, o processo não encerra. Em vez disso, a exceção é ignorada após o evento é gerado, independentemente se um manipulador de eventos observa a exceção.  
  
 No .NET Framework 4.5, você pode usar o [ \<ThrowUnobservedTaskExceptions > elemento](../../../../../docs/framework/configure-apps/file-schema/runtime/throwunobservedtaskexceptions-element.md) em um arquivo de configuração de aplicativo para habilitar o comportamento do .NET Framework 4 de lançar uma exceção.  
  
 Você também pode especificar o comportamento de exceção em uma das seguintes maneiras:  
  
- Definindo a variável de ambiente `COMPlus_ThrowUnobservedTaskExceptions` (`set COMPlus_ThrowUnobservedTaskExceptions=1`).  
  
- Definindo o DWORD do registro valor ThrowUnobservedTaskExceptions = 1 em que a chave HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\. Chave NETFramework.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como habilitar a geração de exceções em tarefas usando um arquivo de configuração do aplicativo.  
  
```xml  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como uma exceção não observada é gerada a partir de uma tarefa. O código deve ser executado como um programa lançado para funcionar corretamente.  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Esquema de configurações do tempo de execução](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)
- [Esquema de arquivos de configuração](../../../../../docs/framework/configure-apps/file-schema/index.md)
