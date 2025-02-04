---
title: Método ICLRRuntimeInfo::GetVersionString
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetVersionString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetVersionString
helpviewer_keywords:
- ICLRRuntimeInfo::GetVersionString method [.NET Framework hosting]
- GetVersionString method, ICLRRuntimeInfo interface [.NET Framework hosting]
ms.assetid: 98b097ef-2276-4dd9-8551-b03c972e8179
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7c80b85171ac9dab270a267cf2dd33a9f1c23d60
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650306"
---
# <a name="iclrruntimeinfogetversionstring-method"></a>Método ICLRRuntimeInfo::GetVersionString
Obtém informações de versão de runtime (CLR) de linguagem comum associadas com um determinado [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) interface.  
  
 Esse método substitui as seguintes funções:  
  
- [GetRequestedRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)  
  
- [GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetVersionString(  
    [out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
    [in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `pwzBuffer`  
 [out] A versão de compilação do .NET Framework no formato "v*um*. *B*[. *X*] ". *Um*, *B*, e *X* são números decimais que correspondem da versão principal, a versão secundária e o número da compilação. *X* é opcional. Se *X* é não estiver presente, não há nenhum ponto à direita.  
  
> [!NOTE]
>  Esse parâmetro deve corresponder ao nome de diretório para a versão do .NET Framework, como ele aparece sob C:\Windows\Microsoft.NET\Framework.  
  
 Os valores de exemplo são "v1.0.3705", "v1.1.4322", "v2.0.50727" e "v4.0. *x*", onde *x* depende do número de compilação instalado. Observe que o prefixo "v" é obrigatório.  
  
 `pchBuffer`  
 [no, out] Especifica o tamanho do `pwzBuffer` para evitar estouros de buffer. Se `pwzBuffer` está `null`, `pchBuffer` retorna o tamanho necessário do `pwzBuffer` para permitir a pré-alocação.  
  
## <a name="return-value"></a>Valor de retorno  
 Esse método retorna os HRESULTs específicos a seguir, bem como o HRESULT erros que indicam falha do método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pwzBuffer` ou `pchBuffer` é nulo.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost.h  
  
 **Biblioteca:** Incluído como um recurso em mscoree. dll  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [Hospedagem de Interfaces](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [Interfaces de hospedagem CLR adicionadas ao .NET Framework 4 e 4.5](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [Hospedagem](../../../../docs/framework/unmanaged-api/hosting/index.md)
