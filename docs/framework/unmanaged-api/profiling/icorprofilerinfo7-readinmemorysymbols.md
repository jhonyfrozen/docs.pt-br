---
title: ICorProfilerInfo7::ReadInMemorySymbols
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo7.ReadInMemorySymbols
api_location:
- CorProf.idl
- CorProf.h
- CorGuids.lib
api_type:
- COM
ms.assetid: 1745a0b9-8332-4777-a670-b549bff3b901
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c3df5324e23ebeded38f3aa9843f81701f7fd333
ms.sourcegitcommit: 26f4a7697c32978f6a328c89dc4ea87034065989
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66251057"
---
# <a name="icorprofilerinfo7readinmemorysymbols"></a>ICorProfilerInfo7::ReadInMemorySymbols
[Com suporte no .NET Framework 4.6.1 e versões posteriores]  
  
 Lê os bytes do fluxo símbolo na memória.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ReadInMemorySymbols(  
        [in] ModuleID moduleId,  
        [in] DWORD symbolsReadOffset,  
        [out] BYTE* pSymbolBytes,  
        [in] DWORD countSymbolBytes,  
        [out] DWORD* pCountSymbolBytesRead  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `moduleId`  
 [in] O identificador do módulo que contém o fluxo de memória.  
  
 `symbolsReadOffset`  
 [in] O deslocamento dentro do fluxo de memória no qual iniciar a leitura dos bytes.  
  
 `pSymbolBytes`  
 [out] Um ponteiro para o buffer no qual os dados serão copiados. O buffer deve ter `countSymbolBytes` de espaço disponível.  
  
 `countSymbolBytes`  
 [in] O número de bytes a serem copiados.  
  
 `pCountSymbolBytesRead`  
 [out] Quando o método retorna, contém o número real de bytes lidos.  
  
## <a name="return-value"></a>Valor de retorno  
 `S_OK`, se um número diferente de zero de bytes foram lidos.  
  
 `CORPROF_E_MODULE_IS_DYNAMIC`, se o módulo foi criado usando <xref:System.Reflection.Emit>.  
  
## <a name="remarks"></a>Comentários  
 O `ReadInMemorySymbols` método tenta ler `countSymbolBytes` dos dados começando no deslocamento `symbolsReadOffset` dentro do fluxo de memória. Os dados são copiados para `pSymbolBytes`, que deve ter `countSymbolBytes` de espaço disponível.     `pCountSymbolsBytesRead` contém o número real de bytes lidos, que pode ser menor do que `countSymbolBytes` se o final do fluxo for atingido.  
  
> [!NOTE]
>  A implementação atual não oferece suporte a Reflection. Emit. Se o módulo foi criado usando Reflection. Emit, o método retorna `CORPROF_E_MODULE_IS_DYNAMIC`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorProf.idl, CorProf.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICorProfilerInfo7](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)
