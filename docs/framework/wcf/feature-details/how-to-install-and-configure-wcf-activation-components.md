---
title: 'Como: instalar e configurar componentes de ativação do WCF'
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: 1141bd8344887990ddd8646eba9d25c5d9a4287d
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487059"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>Como: instalar e configurar componentes de ativação do WCF
Este tópico descreve as etapas necessárias para configurar o serviço de ativação de processos do Windows (também conhecido como WAS) em [!INCLUDE[wv](../../../../includes/wv-md.md)] para hospedar o Windows Communication Foundation (WCF) protocolos de rede de serviços que não se comunicam por HTTP. As seções a seguir descrevem as etapas para essa configuração:  
  
- Instalar (ou confirmar a instalação do) os componentes de ativação do WCF.  
  
- Configure o WAS para dar suporte a um protocolo não HTTP. O procedimento a seguir configura [!INCLUDE[wv](../../../../includes/wv-md.md)] para ativação de TCP.  
  
 Depois de instalar e configurar o WAS, consulte [como: Hospedar um serviço WCF no WAS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md) para os procedimentos para criar um serviço WCF que expõe um ponto de extremidade HTTP não emprega o WAS.  
  
### <a name="to-install-the-wcf-non-http-activation-components"></a>Para instalar os componentes de ativação não HTTP do WCF  
  
1. Clique o **inicie** botão e, em seguida, clique em **painel de controle**.  
  
2. Clique em **programas**e, em seguida, clique em **programas e recursos**.  
  
3. Sobre o **tarefas** menu, clique em **ou desativar recursos do Windows ativar**.  
  
4. Localize o nó do WinFX, selecione e expanda-o.  
  
5. Selecione o **componentes de ativação não Http WCF** caixa e salvar a configuração.  
  
### <a name="to-configure-the-was-to-support-tcp-activation"></a>Para configurar o WAS para dar suporte à ativação TCP  
  
1. Para dar suporte à ativação de NET. TCP, o site padrão primeiro deve ser associado a uma porta NET. TCP. Você pode fazer isso usando Appcmd.exe, que é instalado com o conjunto de ferramentas de gerenciamento do IIS 7.0. Em uma janela de Prompt de comando com nível de administrador, execute o comando a seguir.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Esse comando é uma única linha de texto. Este comando adiciona uma associação de site do NET. TCP para o site padrão escuta na porta TCP 808 com qualquer nome de host.  
  
2. Embora todos os aplicativos dentro de um site compartilham uma associação comum de NET. TCP, cada aplicativo pode habilitar o suporte do NET. TCP individualmente. Para habilitar o NET. TCP para o aplicativo, execute o seguinte comando em um prompt de comando com nível de administrador.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app   
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp  
    ```  
  
    > [!NOTE]
    >  Esse comando é uma única linha de texto. Este comando habilita o /\<*aplicativo WCF*> aplicativo seja acessado usando ambos `http://localhost/<WCF Application>` e `net.tcp://localhost/<WCF Application>`.
  
     Remova a associação de site do NET. TCP que é adicionado para este exemplo.  
  
     Como uma conveniência, as duas etapas a seguir são implementadas em um arquivo em lotes chamado RemoveNetTcpSiteBinding.cmd localizado no diretório de exemplo.  
  
    1. Remova o NET. TCP da lista de protocolos habilitados, executando o seguinte comando em uma janela de Prompt de comando com nível de administrador.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
        ```  
  
        > [!NOTE]
        >  Esse comando é uma única linha de texto.  
  
    2. Remova a associação do site NET. TCP, executando o seguinte comando em uma janela elevada de Prompt de comando:  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
        --bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!NOTE]
        >  Esse comando é uma única linha de texto.  
  
### <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>Para remover o NET. TCP da lista de protocolos habilitados  
  
1. Para remover o NET. TCP da lista de protocolos habilitados, execute o seguinte comando em uma janela de Prompt de comando com nível de administrador.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
    ```  
  
    > [!NOTE]
    >  Esse comando é uma única linha de texto.  
  
### <a name="to-remove-the-nettcp-site-binding"></a>Para remover a associação de site do NET. TCP  
  
1. Para remover o site do NET. TCP associação execute o seguinte comando em uma janela de Prompt de comando com nível de administrador.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
    -bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Esse comando é uma única linha de texto.  
  
## <a name="see-also"></a>Consulte também

- [Ativação TCP](../../../../docs/framework/wcf/samples/tcp-activation.md)
- [Ativação de MSMQ](../../../../docs/framework/wcf/samples/msmq-activation.md)
- [NamedPipe Activation](../../../../docs/framework/wcf/samples/namedpipe-activation.md)
- [Recursos de hospedagem do Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkId=201276)
