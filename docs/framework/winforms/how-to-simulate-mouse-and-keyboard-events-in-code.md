---
title: 'Como: simular eventos de mouse e teclado no código'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboards [Windows Forms], event simulation
- user input [Windows Forms], simulating
- SendKeys [Windows Forms], using
- mouse clicks [Windows Forms], simulating
- mouse [Windows Forms], event simulation
ms.assetid: 6abcb67e-3766-4af2-9590-bf5dabd17e41
ms.openlocfilehash: 1d2e837ec13e6a0b507d004cd75c2f77ae0008dc
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583396"
---
# <a name="how-to-simulate-mouse-and-keyboard-events-in-code"></a>Como: simular eventos de mouse e teclado no código
O Windows Forms fornece várias opções para simular programaticamente entradas do mouse e do teclado. Este tópico fornece uma visão geral dessas opções.  
  
## <a name="simulating-mouse-input"></a>Simulando entrada do mouse  
 A melhor maneira de simular eventos do mouse é chamar o método `On`*EventName* que gera o evento de mouse que você deseja simular. Essa opção é possível apenas dentro de controles e formulários personalizados, pois os métodos que geram eventos são protegidos e não podem ser acessados fora do controle ou do formulário. Por exemplo, as etapas a seguir ilustram como simular um clique no botão direito do mouse no código.  
  
#### <a name="to-programmatically-click-the-right-mouse-button"></a>Para clicar programaticamente no botão direito do mouse  
  
1. Criar uma <xref:System.Windows.Forms.MouseEventArgs> cujos <xref:System.Windows.Forms.MouseEventArgs.Button%2A> estiver definida como o <xref:System.Windows.Forms.MouseButtons.Right?displayProperty=nameWithType> valor.  
  
2. Chame o <xref:System.Windows.Forms.Control.OnMouseClick%2A> método com este <xref:System.Windows.Forms.MouseEventArgs> como o argumento.  
  
 Para obter mais informações sobre controles personalizados, consulte [Desenvolvendo Controles dos Windows Forms no Tempo de Design](./controls/developing-windows-forms-controls-at-design-time.md).  
  
 Existem outras maneiras de simular a entrada do mouse. Por exemplo, você pode definir uma propriedade de controle que representa um estado que normalmente é definido por meio de entrada do mouse por meio de programação (como o <xref:System.Windows.Forms.CheckBox.Checked%2A> propriedade do <xref:System.Windows.Forms.CheckBox> controle), ou você pode chamar diretamente o representante que é anexado ao evento você você deseja simular.  
  
## <a name="simulating-keyboard-input"></a>Simulando Entrada do Teclado  
 Embora você possa simular a entrada do teclado usando as estratégias discutidas acima para a entrada do mouse, Windows Forms também fornece o <xref:System.Windows.Forms.SendKeys> classe para enviar pressionamentos de teclas para o aplicativo ativo.  
  
> [!CAUTION]
>  Se seu aplicativo se destina para uso internacional com diversos teclados, o uso de <xref:System.Windows.Forms.SendKeys.Send%2A?displayProperty=nameWithType> pode produzir resultados imprevisíveis e deve ser evitado.  
  
> [!NOTE]
>  O <xref:System.Windows.Forms.SendKeys> classe foi atualizado para o .NET Framework 3.0 habilitar seu uso em aplicativos executados no Windows Vista. A segurança avançada do Windows Vista (conhecida como Controle de Conta de Usuário ou UAC) impede que a implementação anterior funcione conforme o esperado.  
>   
>  O <xref:System.Windows.Forms.SendKeys> classe é suscetível a problemas de atraso, alguns desenvolvedores tiveram que contornar. A implementação atualizada ainda está suscetível a problemas de atraso, mas é ligeiramente mais rápida e pode exigir alterações para as soluções alternativas. O <xref:System.Windows.Forms.SendKeys> classe tenta usar a implementação anterior primeiro e, se isso falhar, usa a nova implementação. Como resultado, o <xref:System.Windows.Forms.SendKeys> classe pode ter um comportamento diferente em diferentes sistemas operacionais. Além disso, quando o <xref:System.Windows.Forms.SendKeys> classe usa a nova implementação, o <xref:System.Windows.Forms.SendKeys.SendWait%2A> método não aguardará por mensagens a serem processadas quando elas são enviadas para outro processo.  
>   
>  Se seu aplicativo depender de comportamento consistente independentemente do sistema operacional, você pode forçar o <xref:System.Windows.Forms.SendKeys> classe para usar a nova implementação adicionando a seguinte configuração de aplicativo ao seu arquivo App. config.  
>   
>  `<appSettings>`  
>   
>  `<add key="SendKeys" value="SendInput"/>`  
>   
>  `</appSettings>`  
>   
>  Para forçar o <xref:System.Windows.Forms.SendKeys> classe para usar a implementação anterior, use o valor `"JournalHook"` em vez disso.  
  
#### <a name="to-send-a-keystroke-to-the-same-application"></a>Para enviar um pressionamento de tecla para o mesmo aplicativo  
  
1. Chame o <xref:System.Windows.Forms.SendKeys.Send%2A> ou <xref:System.Windows.Forms.SendKeys.SendWait%2A> método o <xref:System.Windows.Forms.SendKeys> classe. Os pressionamentos de teclas especificados serão recebidos pelo controle ativo do aplicativo. O seguinte exemplo de código usa <xref:System.Windows.Forms.SendKeys.Send%2A> para simular o pressionamento da tecla ENTER quando o usuário clica duas vezes a superfície do formulário. Este exemplo pressupõe um <xref:System.Windows.Forms.Form> com um único <xref:System.Windows.Forms.Button> controle que tem um índice de tabulação 0.  
  
     [!code-cpp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#10)]
     [!code-csharp[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#10)]
     [!code-vb[System.Windows.Forms.SimulateKeyPress#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#10)]  
  
#### <a name="to-send-a-keystroke-to-a-different-application"></a>Para enviar um pressionamento de tecla para um aplicativo diferente  
  
1. Ativar a janela do aplicativo que receberá os pressionamentos de tecla e, em seguida, chame o <xref:System.Windows.Forms.SendKeys.Send%2A> ou <xref:System.Windows.Forms.SendKeys.SendWait%2A> método. Como não há nenhum método gerenciado para ativar outro aplicativo, você deve usar métodos nativos do Windows para forçar foco em outros aplicativos. A seguinte código exemplo usa invocação de plataforma para chamar o `FindWindow` e `SetForegroundWindow` métodos para ativar a janela do aplicativo Calculadora e, em seguida, chama <xref:System.Windows.Forms.SendKeys.SendWait%2A> para emitir uma série de cálculos para o aplicativo Calculadora.  
  
    > [!NOTE]
    >  Os parâmetros corretos da chamada `FindWindow` que localiza o aplicativo Calculadora variam de acordo com sua versão do Windows.  O código a seguir localiza o aplicativo Calculadora em [!INCLUDE[win7](../../../includes/win7-md.md)]. Em [!INCLUDE[windowsver](../../../includes/windowsver-md.md)], altere o primeiro parâmetro para "SciCalc". Você pode usar a ferramenta Spy++, incluída no Visual Studio, para determinar os parâmetros corretos.  
  
     [!code-cpp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.SimulateKeyPress#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#5)]  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir é o aplicativo completo para os exemplos de código anteriores.  
  
 [!code-cpp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/cpp/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.SimulateKeyPress#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SimulateKeyPress/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências aos assemblies System, System.Drawing e System.Windows.Forms.  
  
## <a name="see-also"></a>Consulte também

- [Entrada do usuário nos Windows Forms](user-input-in-windows-forms.md)
