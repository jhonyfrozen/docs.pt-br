---
title: Referências fracas
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- weak references, short
- weak references, using
- weak references, long
- garbage collection, weak references
ms.assetid: 6a600fe5-3af3-4c64-82da-10a0a8e2d79b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f2e2fd6f46a430424e6010adbe0662b5bd3db7ea
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622649"
---
# <a name="weak-references"></a>Referências fracas
O coletor de lixo não pode coletar um objeto em uso por um aplicativo enquanto o código do aplicativo pode acessar esse objeto. O aplicativo tem uma referência forte para o objeto.  
  
 Uma referência fraca permite que o coletor de lixo colete o objeto enquanto ainda permite que o aplicativo o acesse. Uma referência fraca é válida somente durante o período indeterminado até que o objeto seja coletado quando não há nenhuma referência forte. Quando você usa uma referência fraca, o aplicativo ainda pode obter uma referência forte para o objeto, o que impede que ele seja coletado. No entanto, sempre há o risco de o coletor de lixo obter o objeto primeiro antes de uma referência forte ser restabelecida.  
  
 As referências fracas são úteis para objetos que usam muita memória, mas podem ser facilmente recriados se forem recuperados pela coleta de lixo.  
  
 Suponha que um modo de exibição de árvore em um aplicativo do Windows Forms exiba uma escolha hierárquica complexa de opções para o usuário. Se os dados subjacentes forem grandes, manter a árvore na memória é ineficiente quando o usuário está envolvido com outra coisa no aplicativo.  
  
 Quando o usuário alterna para outra parte do aplicativo, você pode usar a classe <xref:System.WeakReference> para criar uma referência fraca para a árvore e destruir todas as referências fortes. Quando o usuário alterna de volta para a árvore, o aplicativo tenta obter uma referência forte para a árvore e, se tiver êxito, evita a reconstrução da árvore.  
  
 Para estabelecer uma referência fraca com um objeto, você cria uma <xref:System.WeakReference> usando a instância do objeto a ser rastreada. Em seguida, você deve define a propriedade <xref:System.WeakReference.Target%2A> para aquele objeto e define a referência original para o objeto como `null`. Para obter um exemplo de código, consulte <xref:System.WeakReference> na biblioteca de classes.  
  
## <a name="short-and-long-weak-references"></a>Referências fracas curtas e longas  
 Você pode criar uma referência fraca curta ou uma referência fraca longa:  
  
- Abreviado  
  
     O destino de uma referência fraca curta se torna `null` quando o objeto é recuperado pela coleta de lixo. A referência fraca é um objeto gerenciado e está sujeita à coleta de lixo assim como qualquer outro objeto gerenciado.  Uma referência fraca curta é o construtor padrão para <xref:System.WeakReference>.  
  
- Long  
  
     Uma referência fraca longa é mantida após o método <xref:System.Object.Finalize%2A> do objeto ter sido chamado. Isso permite que o objeto seja recriado, mas o estado do objeto permanece imprevisível. Para usar uma referência longa, especifique `true` no construtor <xref:System.WeakReference>.  
  
     Se o tipo de objeto não tiver um método <xref:System.Object.Finalize%2A>, a funcionalidade de referência fraca curta é aplicada e a referência fraca é válida apenas até o destino ser coletado, o que pode ocorrer a qualquer momento após o finalizador ser executado.  
  
 Para estabelecer uma referência forte e usar o objeto novamente, converta a propriedade <xref:System.WeakReference.Target%2A> de um <xref:System.WeakReference> para o tipo do objeto. Se a propriedade <xref:System.WeakReference.Target%2A> retornar `null`, o objeto terá sido coletado, caso contrário, continue usando o objeto, pois o aplicativo recuperou uma referência forte para ele.  
  
## <a name="guidelines-for-using-weak-references"></a>Diretrizes para usar referências fracas  
 Use referências fracas longas somente quando necessário, uma vez que o estado do objeto é imprevisível após a finalização.  
  
 Evite usar referências fracas para objetos pequenos, pois o ponteiro em si pode ser tão grande quanto ou maior.  
  
 Evite usar referências fracas como uma solução automática para problemas de gerenciamento de memória. Em vez disso, desenvolva uma política de cache efetiva para lidar com os objetos do seu aplicativo.  
  
## <a name="see-also"></a>Consulte também

- [Coleta de lixo](../../../docs/standard/garbage-collection/index.md)
