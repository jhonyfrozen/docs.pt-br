---
title: Método IGCHost::SetGCStartupLimits
ms.date: 03/30/2017
api_name:
- IGCHost.SetGCStartupLimits
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SetGCStartupLimits
helpviewer_keywords:
- SetGCStartupLimits method, IGCHost interface [.NET Framework hosting]
- IGCHost::SetGCStartupLimits method [.NET Framework hosting]
ms.assetid: cae53926-82ac-4d1d-b297-0bde0bd1bebb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e65a83d1da0580436babd15e4f27e2db7a698668
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66377606"
---
# <a name="igchostsetgcstartuplimits-method"></a>Método IGCHost::SetGCStartupLimits
Define o tamanho do segmento e o tamanho máximo para a geração 0.  
  
> [!IMPORTANT]
>  Começando com o .NET Framework 4.5, você pode definir tamanho do segmento e o tamanho máximo de geração 0 para valores maior `DWORD` usando o [IGCHost2::SetGCStartupLimitsEx](../../../../docs/framework/unmanaged-api/hosting/igchost2-setgcstartuplimitsex-method.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetGCStartupLimits (  
    [in] DWORD SegmentSize,  
    [in] DWORD MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `SegmentSize`  
 [in] O tamanho do segmento usado pelo sistema de coleta de lixo.  
  
 `MaxGen0Size`  
 [in] O tamanho máximo para a geração 0.  
  
## <a name="remarks"></a>Comentários  
 O `SetGCStartupLimits` método pode ser chamado apenas uma vez. Esses valores não podem ser alterados posteriormente.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** GCHost.idl, GCHost.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IGCHost](../../../../docs/framework/unmanaged-api/hosting/igchost-interface.md)
