---
title: Método ISOSDacInterface::GetMethodDescData
ms.date: 01/16/2019
api.name:
- ISOSDacInterface::GetMethodDescData Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface::GetMethodDescData Method
helpviewer.keywords:
- ISOSDacInterface::GetMethodDescData Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: cdbf662c664d6c87b2fa17bcb10d735b0f573dd2
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632313"
---
# <a name="isosdacinterfacegetmethoddescdata-method"></a>Método ISOSDacInterface::GetMethodDescData

Obtém os dados para o ponteiro de MethodDesc determinado.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>Sintaxe

```
HRESULT GetMethodDescData(
    CLRDATA_ADDRESS            methodDesc,
    CLRDATA_ADDRESS            ip,
    DacpMethodDescData *data,
    ULONG                      cRevertedRejitVersions,
    DacpReJitData      *rgRevertedRejitData,
    void                      *pcNeededRevertedRejitData
);
```

## <a name="parameters"></a>Parâmetros

`methodDesc`\
[in] O endereço do MethodDesc.

`ip`\
[in] O endereço IP do método.

`data`\
[out] Os dados associados a MethodDesc conforme retornado pelo APIs internas.

`cRevertedRejitVersions`\
[out] O número de versões do rejit revertido.

`rgRevertedRejitData`\
[out] Os dados associados com as versões do rejit revertido como retornado pelo APIs internas.

`pcNeededRevertedRejitData`\
[out] O número de bytes necessários para armazenar os dados associados com as versões do ReJit revertidas.

## <a name="remarks"></a>Comentários

O método fornecido é parte do `ISOSDacInterface` de interface e corresponde ao slot de 20 anos da tabela de método virtual. Para poder usá-los [ `CLRDATA_ADDRESS` ](../common-data-types-unmanaged-api-reference.md) deve ser definido como um inteiro sem sinal de 64 bits.

## <a name="requirements"></a>Requisitos

**Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
**Cabeçalho:** Nenhum  
**Biblioteca:** Nenhum  
**Versões do .NET Framework:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>Consulte também

- [Depuração](index.md)
- [ISOSDacInterface Interface](isosdacinterface-interface.md)
