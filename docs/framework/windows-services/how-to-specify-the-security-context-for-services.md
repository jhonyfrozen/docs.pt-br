---
title: 'Como: Especificar o contexto de segurança para serviços'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, security
- security [Visual Studio], contexts
- contexts, Visual Studio security
- security [Visual Studio], service applications
- ServiceProcessInstaller class, security context
- services, security
- ServiceInstaller class, security context
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
author: ghogen
ms.openlocfilehash: 633d378b2336b3ee166375a923252e0477e75127
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64591662"
---
# <a name="how-to-specify-the-security-context-for-services"></a>Como: Especificar o contexto de segurança para serviços
Por padrão, os serviços são executados em um contexto de segurança diferente do que o usuário que fez logon. Os serviços são executados no contexto da conta padrão do sistema, chamada `LocalSystem`, que oferece a eles privilégios de acesso a recursos do sistema diferentes que os do usuário. Você pode alterar esse comportamento para especificar outra conta de usuário diferente com a qual o serviço deverá ser executado.  
  
 Você define o contexto de segurança manipulando a propriedade <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> para o processo no qual o serviço é executado. Essa propriedade permite que você defina o serviço para uma entre quatro tipos de conta:  
  
- `User`, que faz com que o sistema solicite um nome de usuário e uma senha válidos quando o serviço é instalado e executado no contexto de uma conta especificada por um único usuário na rede;  
  
- `LocalService`, que é executado no contexto de uma conta que age como um usuário sem privilégios no computador local e apresenta credenciais anônimas para qualquer servidor remoto;  
  
- `LocalSystem`, que é executado no contexto de uma conta que fornece privilégios locais abrangentes e apresenta as credenciais do computador para qualquer servidor remoto;  
  
- `NetworkService`, que é executado no contexto de uma conta que age como um usuário sem privilégios no computador local e apresenta as credenciais do computador para qualquer servidor remoto.  
  
 Para obter mais informações, consulte a enumeração <xref:System.ServiceProcess.ServiceAccount>.  
  
### <a name="to-specify-the-security-context-for-a-service"></a>Para especificar o contexto de segurança de um serviço  
  
1. Depois de criar o serviço, adicione os instaladores necessários para ele. Para obter mais informações, confira [Como: Adicionar instaladores ao aplicativo de serviço](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
2. No designer, acesse a classe `ProjectInstaller` e clique no instalador do processo de serviço para o serviço com o qual você está trabalhando.  
  
    > [!NOTE]
    >  Para cada aplicativo de serviço, há pelo menos dois componentes de instalação na classe `ProjectInstaller` – um que instala os processos para todos os serviços no projeto e um instalador para cada serviço que o aplicativo contém. Nesse caso, você desejará selecionar <xref:System.ServiceProcess.ServiceProcessInstaller>.  
  
3. Na janela **Propriedades**, defina a <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> para o valor apropriado.  
  
## <a name="see-also"></a>Consulte também

- [Introdução aos Aplicativos de Serviço Windows](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
- [Como: adicionar instaladores ao aplicativo de serviço](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)
- [Como: criar serviços do Windows](../../../docs/framework/windows-services/how-to-create-windows-services.md)
