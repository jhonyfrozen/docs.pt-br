---
title: Método ICorDebug::CanLaunchOrAttach
ms.date: 03/30/2017
api_name:
- ICorDebug.CanLaunchOrAttach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CanLaunchOrAttach
helpviewer_keywords:
- ICorDebug::CanLaunchOrAttach method [.NET Framework debugging]
- CanLaunchOrAttach method [.NET Framework debugging]
ms.assetid: ca7723db-7c07-4cdd-bd92-fba34928b623
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c109bab2ecd14e2b698a9b24dace56e986ad5e58
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593529"
---
# <a name="icordebugcanlaunchorattach-method"></a>Método ICorDebug::CanLaunchOrAttach
Retorna um HRESULT que indica se iniciando um novo processo ou anexar ao processo especificado existente é possível dentro do contexto da configuração da máquina e o tempo de execução atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CanLaunchOrAttach (  
    [in] DWORD      dwProcessId,  
    [in] BOOL       win32DebuggingEnabled  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `dwProcessId`  
 [in] A ID de um processo existente.  
  
 `win32DebuggingEnabled`  
 [in] Passe `true` se você planeja iniciar com depuração de Win32 habilitada, ou anexar Win32 depuração habilitada; caso contrário, passe `false`.  
  
## <a name="return-value"></a>Valor de retorno  
 S_OK se os serviços de depuração determinam que iniciar um novo processo ou anexando ao processo determinado é possível, considerando as informações sobre a configuração de máquina e o tempo de execução atual. Os valores HRESULT possíveis são:  
  
- S_OK  
  
- CORDBG_E_DEBUGGING_NOT_POSSIBLE  
  
- CORDBG_E_KERNEL_DEBUGGER_PRESENT  
  
- CORDBG_E_KERNEL_DEBUGGER_ENABLED  
  
## <a name="remarks"></a>Comentários  
 Esse método é meramente informativo. A interface não irá parar de iniciar ou anexar a um processo, independentemente do valor retornado por `CanLaunchOrAttach`.  
  
 Se você planeja iniciar com depuração de Win32 habilitada ou anexar com Win32 depuração habilitada, passe `true` para `win32DebuggingEnabled`. O HRESULT retornado pela `CanLaunchOrAttach` podem ser diferentes se você usar essa opção.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
