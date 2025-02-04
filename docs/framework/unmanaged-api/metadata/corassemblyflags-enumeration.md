---
title: Enumeração CorAssemblyFlags
ms.date: 03/30/2017
api_name:
- CorAssemblyFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorAssemblyFlags
helpviewer_keywords:
- CorAssemblyFlags enumeration [.NET Framework metadata]
ms.assetid: bb8db3b6-d81d-49fc-b74c-dbc908a9eab9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 43bfec471fbcfc481e178f6610e0318e9538ee34
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025776"
---
# <a name="corassemblyflags-enumeration"></a>Enumeração CorAssemblyFlags
Contém valores que descrevem os metadados aplicados a uma compilação do assembly.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef enum CorAssemblyFlags {  
  
    afPublicKey             =   0x0001,  
    afPA_None               =   0x0000,  
    afPA_MSIL               =   0x0010,  
    afPA_x86                =   0x0020,  
    afPA_IA64               =   0x0030,  
    afPA_AMD64              =   0x0040,  
    afPA_ARM                =   0x0050,  
    afPA_NoPlatform         =   0x0070,  
    afPA_Specified          =   0x0080,  
    afPA_Mask               =   0x0070,  
    afPA_FullMask           =   0x00F0,  
    afPA_Shift              =   0x0004,  
  
    afEnableJITcompileTracking  =   0x8000,  
    afDisableJITcompileOptimizer=   0x4000,  
  
    afRetargetable          =   0x0100,  
    afContentType_Default        =   0x0000,  
    afContentType_WindowsRuntime =   0x0200,  
    afContentType_Mask           =   0x0E00,  
  
} CorAssemblyFlags;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Descrição|  
|------------|-----------------|  
|`afPublicKey`|Indica que a referência de assembly retém a chave pública completa, sem hash.|  
|`afPA_None`|Indica que a arquitetura do processador é especificada.|  
|`afPA_MSIL`|Indica que a arquitetura do processador é neutra (PE32).|  
|`afPA_x86`|Indica que a arquitetura de processador x86 (PE32).|  
|`afPA_IA64`|Indica que a arquitetura do processador Itanium (PE32 +).|  
|`afPA_AMD64`|Indica que a arquitetura do processador AMD X64 (PE32 +).|  
|`afPA_ARM`|Indica que a arquitetura do processador ARM (PE32).|  
|`afPA_NoPlatform`|Indica que o assembly é um assembly de referência; ou seja, ele se aplica a qualquer arquitetura, mas não pode ser executado em qualquer arquitetura. Portanto, o sinalizador é o mesmo que `afPA_Mask`.|  
|`afPA_Specified`|Indica que os sinalizadores de arquitetura de processador devem ser propagados para o `AssemblyRef` registro.|  
|`afPA_Mask`|Uma máscara que descreve a arquitetura do processador.|  
|`afPA_FullMask`|Especifica que a descrição da arquitetura de processador está incluída.|  
|`afPA_Shift`|Indica uma contagem de shift os sinalizadores de arquitetura do processador de e para o índice.|  
|`afEnableJITcompileTracking`|Indica o valor correspondente do <xref:System.Diagnostics.DebuggableAttribute.DebuggingModes> do <xref:System.Diagnostics.DebuggableAttribute>.|  
|`afDisableJITcompileOptimizer`|Indica o valor correspondente do <xref:System.Diagnostics.DebuggableAttribute.DebuggingModes> do <xref:System.Diagnostics.DebuggableAttribute>.|  
|`afRetargetable`|Indica que o assembly pode ser redirecionado em tempo de execução a um assembly de um outro editor.|  
|`afContentType_Mask`|Uma máscara que descreve o tipo de conteúdo.|  
|`afContentType_Default`|Indica o tipo de conteúdo padrão.|  
|`afContentType_WindowsRuntime`|Indica o tipo de conteúdo de tempo de execução do Windows.|  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorHdr.h  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de metadados](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
