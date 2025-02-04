---
title: Função SetSecurity (referência de API não gerenciada)
description: A função SetSecurity recupera o token de representação do thread atual.
ms.date: 11/06/2017
api_name:
- SetSecurity
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SetSecurity
helpviewer_keywords:
- SetSecurity function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5cecd8538b8f2b5d04cb9f1822751661ce9f8728
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636212"
---
# <a name="setsecurity-function"></a>Função SetSecurity

Recupera o token de representação associado ao thread atual. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe

```
HRESULT SetSecurity (
   [out] boolean* pNeedToReset, 
   [out] HANDLE* pCurrentThreadToken
); 
```

## <a name="parameters"></a>Parâmetros

`pNeedToReset`\
[out] Quando a função retorna, contém um ponteiro para um `boolean` que indica se o token deve ser redefinido por meio da chamada a [ResetSecurity](resetsecurity.md) função.

`token`\
[out] Quando a função retornar, contém um ponteiro para o identificador do token de representação associado ao thread atual. Seu valor pode ser `null` se não houver nenhum token associado ao thread atual. 

## <a name="return-value"></a>Valor retornado

Se a função for bem-sucedida, o valor retornado é `S_OK` (0).

Se a função falhar, o valor de retorno é um código de erro diferente de zero. Para obter outras informações de erro, chame o [GetErrorInfo](geterrorinfo.md) função.

## <a name="requirements"></a>Requisitos

 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).

 **Cabeçalho:** WMINet_Utils.idl

 **Versões do .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Consulte também

- [WMI e contadores de desempenho (referência de API não gerenciada)](index.md)
