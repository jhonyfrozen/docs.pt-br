---
title: Compartilhando loops de mensagem entre Win32 e WPF
ms.date: 03/30/2017
helpviewer_keywords:
- Win32 code [WPF], sharing message loops
- message loops [WPF]
- sharing message loops [WPF]
- interoperability [WPF], Win32
ms.assetid: 39ee888c-e5ec-41c8-b11f-7b851a554442
ms.openlocfilehash: d2fe63ed4bdefc91e4847af799747219bd7b4a76
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64611721"
---
# <a name="sharing-message-loops-between-win32-and-wpf"></a>Compartilhando loops de mensagem entre Win32 e WPF
Este tópico descreve como implementar um loop de mensagem para interoperação com [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], usando existente de exposição de loop em mensagem <xref:System.Windows.Threading.Dispatcher> ou criando um loop de mensagem separado no [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] lado de seu código de interoperação.  
  
## <a name="componentdispatcher-and-the-message-loop"></a>ComponentDispatcher e o loop de mensagem  
 Um cenário comum para suporte de eventos de teclado e interoperação é implementar <xref:System.Windows.Interop.IKeyboardInputSink>, ou subclasses de classes que já implementam <xref:System.Windows.Interop.IKeyboardInputSink>, como <xref:System.Windows.Interop.HwndSource> ou <xref:System.Windows.Interop.HwndHost>. No entanto, o suporte ao coletor de teclado não trata de todas as necessidades de loop de mensagem possíveis que você pode ter ao enviar e receber mensagens entre os limites de interoperação. Para ajudar a formalizar uma arquitetura de loop de mensagem do aplicativo, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornece o <xref:System.Windows.Interop.ComponentDispatcher> classe, que define um protocolo simples para um loop de mensagem a seguir.  
  
 <xref:System.Windows.Interop.ComponentDispatcher> é uma classe estática que expõe diversos membros. O escopo de cada método é unido implicitamente ao thread de chamada. Um loop de mensagem precisa chamar algumas desses [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] em momentos críticos (conforme definido na próxima seção).  
  
 <xref:System.Windows.Interop.ComponentDispatcher> Fornece eventos que outros componentes (como o coletor de teclado) podem aguardar. O <xref:System.Windows.Threading.Dispatcher> classe chama todos os <xref:System.Windows.Interop.ComponentDispatcher> métodos em uma sequência apropriada. Se você estiver implementando seu próprio loop de mensagem, seu código é responsável por chamar <xref:System.Windows.Interop.ComponentDispatcher> métodos de maneira semelhante.  
  
 Chamar <xref:System.Windows.Interop.ComponentDispatcher> métodos em um thread invocará somente manipuladores de eventos que foram registrados naquele thread.  
  
## <a name="writing-message-loops"></a>Escrevendo loops de mensagem  
 A seguir está uma lista de verificação de <xref:System.Windows.Interop.ComponentDispatcher> membros que você usará se escrever seu próprio loop de mensagem:  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A>: seu loop de mensagem deve chamá-lo para indicar que o thread é modal.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A>: seu loop de mensagem deve chamá-lo para indicar que o thread foi revertido para não modal.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>: seu loop de mensagem deve chamá-lo para indicar que <xref:System.Windows.Interop.ComponentDispatcher> deve gerar o <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> eventos. <xref:System.Windows.Interop.ComponentDispatcher> não gerará <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> se <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A> é `true`, mas loops de mensagem poderão optar por chamar <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A> mesmo se <xref:System.Windows.Interop.ComponentDispatcher> não possa responder enquanto no estado modal.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A>: seu loop de mensagem deve chamá-lo para indicar que uma nova mensagem está disponível. O valor retornado indica se um ouvinte para um <xref:System.Windows.Interop.ComponentDispatcher> evento manipulado a mensagem. Se <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A> retorna `true` (tratado), o dispatcher deve fazer nada com a mensagem. Se o valor retornado for `false`, o despachante deverá chamar a função [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] de `TranslateMessage` e, em seguida, chamar `DispatchMessage`.  
  
## <a name="using-componentdispatcher-and-existing-message-handling"></a>Usando ComponentDispatcher e manipulando mensagens existentes  
 A seguir está uma lista de verificação <xref:System.Windows.Interop.ComponentDispatcher> membros que você usará se você depender inerente [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] loop de mensagem.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A>: Retorna se o aplicativo se tornou modal (por exemplo, um loop de mensagem modal foi introduzido). <xref:System.Windows.Interop.ComponentDispatcher> pode controlar este estado porque a classe mantém uma contagem dos <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A> e <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A> chamadas a partir do loop de mensagem.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> e <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> eventos seguem as regras padrão para invocações de delegados. Representantes são invocados em ordem não especificada e todos os representantes são invocados, mesmo que o primeiro marca a mensagem como tratada.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>: indica um momento apropriado e eficiente para fazer o processamento ocioso (não há nenhuma mensagem pendente para o thread). <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> não será gerado se o thread é modal.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>: gerado para todas as mensagens que processa a bomba de mensagens.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>: gerado para todas as mensagens que não foram tratadas durante <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>.  
  
 Uma mensagem é considerada tratada se depois de <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> evento ou <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> evento, o `handled` parâmetro passado por referência nos dados de evento é `true`. Manipuladores de evento devem ignorar a mensagem se `handled` for `true`, pois isso significa que o manipulador diferente a tratou primeiro. Manipuladores de eventos dos dois eventos podem modificar a mensagem. O despachante deve despachar a mensagem modificada e não a mensagem original inalterada. <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> é entregue a todos os ouvintes, mas a intenção arquitetural é que somente a janela de nível superior que contém o HWND no qual as mensagens direcionadas devem invocar código em resposta à mensagem.  
  
## <a name="how-hwndsource-treats-componentdispatcher-events"></a>Como HwndSource trata eventos de ComponentDispatcher  
 Se o <xref:System.Windows.Interop.HwndSource> é uma janela de nível superior (sem um HWND pai), ele registrará com <xref:System.Windows.Interop.ComponentDispatcher>. Se <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> é gerado, e se a mensagem destina-se para o <xref:System.Windows.Interop.HwndSource> ou janelas filho, <xref:System.Windows.Interop.HwndSource> chamadas seu <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TranslateAccelerator%2A>, <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A>, <xref:System.Windows.Interop.IKeyboardInputSink.OnMnemonic%2A> sequência de coletor de teclado.  
  
 Se o <xref:System.Windows.Interop.HwndSource> não é uma janela de nível superior (tiver um HWND pai), não haverá nenhum tratamento. Somente a janela de nível superior deve realizar o tratamento e espera-se que haja uma janela de nível superior com suporte para coletor de teclado como parte de qualquer cenário de interoperação.  
  
 Se <xref:System.Windows.Interop.HwndHost.WndProc%2A> em um <xref:System.Windows.Interop.HwndSource> é chamado sem um método de coletor de teclado apropriado seja chamado primeiro, seu aplicativo receberá os eventos de teclado de nível superiores, como <xref:System.Windows.UIElement.KeyDown>. No entanto, nenhum método de coletor de teclado será chamado, o que contorna recursos de modelo de entrada do teclado desejáveis, como suporte para chave de acesso. Isso pode acontecer porque o loop de mensagem não notificou adequadamente o thread relevante no <xref:System.Windows.Interop.ComponentDispatcher>, ou porque o HWND pai não invocou as respostas de coletor de teclado apropriadas.  
  
 Uma mensagem que vai para o coletor de teclado não pode ser enviada ao HWND se você tiver adicionado ganchos para aquela mensagem usando o <xref:System.Windows.Interop.HwndSource.AddHook%2A> método. A mensagem pode ser sido tratada no nível de bomba de mensagens diretamente e não enviada para a função `DispatchMessage`.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Interop.ComponentDispatcher>
- <xref:System.Windows.Interop.IKeyboardInputSink>
- [Interoperação do WPF e do Win32](wpf-and-win32-interoperation.md)
- [Modelo de threading](threading-model.md)
- [Visão geral da entrada](input-overview.md)
