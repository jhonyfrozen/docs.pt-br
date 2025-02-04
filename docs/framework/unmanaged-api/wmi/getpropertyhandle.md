---
title: Função GetPropertyHandle (referência de API não gerenciada)
description: A função GetPropertyHandle retorna um identificador exclusivo que identifica uma propriedade.
ms.date: 11/06/2017
api_name:
- GetPropertyHandle
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetPropertyHandle
helpviewer_keywords:
- GetPropertyHandle function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d1397188b38066bac6375da0c76e7d66724a75d7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65636238"
---
# <a name="getpropertyhandle-function"></a>Função GetPropertyHandle

Retorna um identificador exclusivo que reconhece uma propriedade.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPropertyHandle (
   [in] int                  vFunc,
   [in] IWbemObjectAccess*   ptr,
   [in] LPCWSTR              wszPropertyName,
   [out] CIMTYPE*            pType,
   [out] long*               pHandle
);
```

## <a name="parameters"></a>Parâmetros

`vFunc`\
[in] Esse parâmetro é usado.

`ptr`\
[in] Um ponteiro para um [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) instância.

`wszPropertyName`\
[in] Uma terminação nula cadeia de caracteres codificada em UTF16 que contém o nome da propriedade.

`pType`\
[out] Um ponteiro para um [ `CIMTYPE` ](/windows/desktop/api/wbemcli/ne-wbemcli-tag_cimtype_enumeration) membro de enumeração que representa o tipo CIM da propriedade.

`pHandle`\
[out] Um ponteiro para um inteiro que contém o identificador de propriedade.

## <a name="return-value"></a>Valor retornado

Os seguintes valores retornados por essa função são definidos na *WbemCli.h* arquivo de cabeçalho, ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | Nome da propriedade especificada não foi encontrado. |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um parâmetro não é válido. |
|`WBEM_E_NOT_SUPPORTED` | 0x8004100c | A propriedade solicitada é do tipo são `CIM_OBJECT` ou `CIM_ARRAY`. |
|`WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |

## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o [IWbemClassObject::GetPropertyHandle](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-getpropertyhandle) método.

Você pode usar esse identificador para identificar as propriedades ao usar [IWbemObjectAccess](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess) métodos para ler ou gravar valores de propriedade.

Identificadores podem ser recuperados para propriedades de todos os tipos de dados diferente de `CIM_OBJECT` e `CIM_ARRAY`. Retornou o trabalho de identificadores em todas as instâncias de uma classe.

## <a name="requirements"></a>Requisitos

**Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).

**Cabeçalho:** WMINet_Utils.idl

**Versões do .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Consulte também

- [WMI e contadores de desempenho (referência de API não gerenciada)](index.md)
