---
title: Permissões perigosas e administração de políticas
ms.date: 03/30/2017
helpviewer_keywords:
- permissions [.NET Framework], policy administration
- security [.NET Framework], dangerous permissions
- code security, dangerous permissions
- secure coding, dangerous permissions
- permissions [.NET Framework], dangerous
ms.assetid: 1929e854-23a0-4bb1-94be-e8aa3b609e32
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 17a596d9fc223dc53268ae9c91f7d02357b0a9b8
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489984"
---
# <a name="dangerous-permissions-and-policy-administration"></a>Permissões perigosas e administração de políticas
Várias operações protegidas para o qual o .NET Framework fornece permissões potencialmente podem permitir que o sistema de segurança seja contornado. Essas permissões perigosas devem ser dada apenas ao código confiável e, em seguida, somente quando necessário. Normalmente, há nenhuma defesa contra código mal-intencionado se ele tem essas permissões.  
  
> [!NOTE]
>  No .NET Framework 4, houve alterações importantes para o modelo de segurança do .NET Framework e a terminologia. Para obter mais informações sobre essas alterações, consulte [alterações de segurança](../../../docs/framework/security/security-changes.md).  
  
 Permissões perigosas são explicadas na tabela a seguir.  
  
|Permissão|Risco em potencial|  
|----------------|--------------------|  
|<xref:System.Security.Permissions.SecurityPermission>||  
|<xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode>|Permite que o código gerenciado chamar código não gerenciado, que geralmente é perigoso.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SkipVerification>|Sem a verificação, o código pode fazer qualquer coisa.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlEvidence>|Evidência invalidada pode enganar a diretiva de segurança.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPolicy>|A capacidade de modificar a política de segurança pode desativar a segurança.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter>|O uso da serialização pode desviar os mecanismos de acessibilidade. Para obter detalhes, consulte [segurança e serialização](../../../docs/framework/misc/security-and-serialization.md).|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPrincipal>|A capacidade de definir a atual entidade pode enganar segurança baseada em função.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlThread>|Manipulação de threads é perigosa devido ao estado de segurança associado a threads.|  
|<xref:System.Security.Permissions.ReflectionPermission>||  
|<xref:System.MemberAccessException>|Pode usar membros particulares para anular os mecanismos de acessibilidade.|  
  
## <a name="see-also"></a>Consulte também

- [Diretrizes de codificação segura](../../../docs/standard/security/secure-coding-guidelines.md)
