---
title: Enumeração EClrFailure
ms.date: 03/30/2017
api_name:
- EClrFailure
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrFailure
helpviewer_keywords:
- EClrFailure enumeration [.NET Framework hosting]
ms.assetid: 37b95cce-9bfb-4ecf-a00b-33dcba782c67
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cb19f950122f7b0db66830e9ed5dff44ccd370c2
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490430"
---
# <a name="eclrfailure-enumeration"></a>Enumeração EClrFailure
Descreve o conjunto de falhas para o qual um host pode definir ações de política.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum {  
    FAIL_NonCriticalResource,  
    FAIL_CriticalResource,  
    FAIL_FatalRuntime,  
    FAIL_OrphanedLock  
    FAIL_StackOverflow  
    FAIL_AccessViolation  
    FAIL_CodeContract  
} EClrFailure;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|`FAIL_NonCriticalResource`|Ocorreu uma falha durante uma tentativa de alocar um recurso (por exemplo, um thread, um bloco de memória ou um bloqueio) em uma região não-críticas do código.|  
|`FAIL_CriticalResource`|Ocorreu uma falha durante uma tentativa de alocar um recurso (por exemplo, um thread, um bloco de memória ou um bloqueio) em uma região crítica de código.|  
|`FAIL_FatalRuntime`|O common language runtime (CLR) não é mais capaz de executar código gerenciado no processo. Daqui em diante, chamadas para hospedagem todas as funções retornam um valor HRESULT HOST_E_CLRNOTAVAILABLE.|  
|`FAIL_OrphanedLock`|Um thread falhou ao liberar um bloqueio após o retorno de um <xref:System.AppDomain> objeto. O host não é possível definir essa falha para fazer com que um thread anular.|  
|`FAIL_StackOverflow`|Ocorreu um estouro de pilha.|  
|`FAIL_AccessViolation`|Foi feita uma tentativa para ler ou gravar memória protegida. Não tem suporte no .NET Framework 4.|  
|`FAIL_CodeContract`|Ocorreu uma falha de contrato de código. Ver [contratos de código](../../../../docs/framework/debug-trace-profile/code-contracts.md).|  
  
## <a name="remarks"></a>Comentários  
 Consulte a [ICLRPolicyManager:: SetActionOnFailure](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactiononfailure-method.md) método para obter uma lista de [EPolicyAction](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md) valores host pode ser usados para especificar as ações de política para condições de falha. Para obter mais informações sobre as regiões críticas e não-críticas do código, consulte [EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md).  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE.h  
  
 **Biblioteca:** MSCorEE.dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRPolicyManager](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [Método SetActionOnFailure](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactiononfailure-method.md)
- [Interface IHostPolicyManager](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [Enumerações de hospedagem](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
