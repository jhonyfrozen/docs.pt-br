---
title: Estender quadro com efeito de transparência em um aplicativo WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], extending glass frames into
- graphics [WPF], extending glass frames into applications
- extending glass frames into applications [WPF]
- glass frames [WPF], extending into applications
ms.assetid: 74388a3a-4b69-4a9d-ba1f-e107636bd660
ms.openlocfilehash: 1c3316fa88d3024af4e81072cbe64c13cfbdb18e
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610291"
---
# <a name="extend-glass-frame-into-a-wpf-application"></a>Estender quadro com efeito de transparência em um aplicativo WPF

Este tópico demonstra como estender o [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] quadro de vidro na área do cliente de um aplicativo Windows Presentation Foundation (WPF).

> [!NOTE]
> Este exemplo só funcionará em um computador [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] que executa o DWM (Gerenciador de Janelas da Área de Trabalho) com efeito de transparência habilitado. O [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] Home Basic edition não dá suporte ao efeito de transparência. Áreas que normalmente seriam renderizadas com efeito de transparência nas outras edições do [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] são renderizadas opacas.

## <a name="example"></a>Exemplo

A imagem a seguir ilustra o quadro com efeito de transparência estendido em barra de endereços do Internet Explorer 7:

![Captura de tela mostrando o quadro com efeito de transparência estendido por trás da barra de endereços do IE7.](./media/extend-glass-frame-into-a-wpf-application/internet-explorer-glass-frame-extended-address-bar.png)

Para estender o quadro com efeito de transparência em um aplicativo [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], é necessário obter acesso ao [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] não gerenciado. O exemplo de código a seguir faz uma invocação de plataforma (pinvoke) para a API de dois necessárias para estender o quadro para a área de cliente. Cada uma dessas APIs são declarados em uma classe chamada **NonClientRegionAPI**.

```csharp
[StructLayout(LayoutKind.Sequential)]
public struct MARGINS
{
    public int cxLeftWidth;      // width of left border that retains its size
    public int cxRightWidth;     // width of right border that retains its size
    public int cyTopHeight;      // height of top border that retains its size
    public int cyBottomHeight;   // height of bottom border that retains its size
};

[DllImport("DwmApi.dll")]
public static extern int DwmExtendFrameIntoClientArea(
    IntPtr hwnd,
    ref MARGINS pMarInset);
```

```vb
<StructLayout(LayoutKind.Sequential)>
Public Structure MARGINS
    Public cxLeftWidth As Integer ' width of left border that retains its size
    Public cxRightWidth As Integer ' width of right border that retains its size
    Public cyTopHeight As Integer ' height of top border that retains its size
    Public cyBottomHeight As Integer ' height of bottom border that retains its size
End Structure

<DllImport("DwmApi.dll")>
Public Shared Function DwmExtendFrameIntoClientArea(ByVal hwnd As IntPtr, ByRef pMarInset As MARGINS) As Integer
End Function
```

[DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea) é a função de DWM que estende o quadro para a área de cliente. Ela recebe dois parâmetros: um identificador de janela e uma estrutura [MARGINS](/windows/desktop/api/uxtheme/ns-uxtheme-_margins). [MARGINS](/windows/desktop/api/uxtheme/ns-uxtheme-_margins) é usado para instruir o DWM sobre quanto a mais o quadro deve ser estendido para a área de cliente.

## <a name="example"></a>Exemplo

Para usar a função [DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea), é necessário obter um identificador de janela. Na [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], o identificador de janela pode ser obtido de <xref:System.Windows.Interop.HwndSource.Handle%2A> propriedade de um <xref:System.Windows.Interop.HwndSource>. No exemplo a seguir, o quadro é estendido para a área de cliente sobre o <xref:System.Windows.FrameworkElement.Loaded> eventos da janela.

```csharp
void OnLoaded(object sender, RoutedEventArgs e)
{
   try
   {
      // Obtain the window handle for WPF application
      IntPtr mainWindowPtr = new WindowInteropHelper(this).Handle;
      HwndSource mainWindowSrc = HwndSource.FromHwnd(mainWindowPtr);
      mainWindowSrc.CompositionTarget.BackgroundColor = Color.FromArgb(0, 0, 0, 0);

      // Get System Dpi
      System.Drawing.Graphics desktop = System.Drawing.Graphics.FromHwnd(mainWindowPtr);
      float DesktopDpiX = desktop.DpiX;
      float DesktopDpiY = desktop.DpiY;

      // Set Margins
      NonClientRegionAPI.MARGINS margins = new NonClientRegionAPI.MARGINS();

      // Extend glass frame into client area
      // Note that the default desktop Dpi is 96dpi. The  margins are
      // adjusted for the system Dpi.
      margins.cxLeftWidth = Convert.ToInt32(5 * (DesktopDpiX / 96));
      margins.cxRightWidth = Convert.ToInt32(5 * (DesktopDpiX / 96));
      margins.cyTopHeight = Convert.ToInt32(((int)topBar.ActualHeight + 5) * (DesktopDpiX / 96));
      margins.cyBottomHeight = Convert.ToInt32(5 * (DesktopDpiX / 96));

      int hr = NonClientRegionAPI.DwmExtendFrameIntoClientArea(mainWindowSrc.Handle, ref margins);
      //
      if (hr < 0)
      {
         //DwmExtendFrameIntoClientArea Failed
      }
   }
   // If not Vista, paint background white.
   catch (DllNotFoundException)
   {
      Application.Current.MainWindow.Background = Brushes.White;
   }
}
```

## <a name="example"></a>Exemplo

O exemplo a seguir mostra uma janela simples em que o quadro é estendido para a área de cliente. O quadro é estendido por trás da borda superior que contém os dois <xref:System.Windows.Controls.TextBox> objetos.

```xaml
<Window x:Class="SDKSample.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Extended Glass in WPF" Height="300" Width="400"
    Loaded="OnLoaded" Background="Transparent"
    >
  <Grid ShowGridLines="True">
    <DockPanel Name="mainDock">
      <!-- The border is used to compute the rendered height with margins.
           topBar contents will be displayed on the extended glass frame.-->
      <Border Name="topBar" DockPanel.Dock="Top" >
        <Grid Name="grid">
          <Grid.ColumnDefinitions>
            <ColumnDefinition MinWidth="100" Width="*"/>
            <ColumnDefinition Width="Auto"/>
          </Grid.ColumnDefinitions>
          <TextBox Grid.Column="0" MinWidth="100" Margin="0,0,10,5">Path</TextBox>
          <TextBox Grid.Column="1" MinWidth="75" Margin="0,0,0,5">Search</TextBox>
        </Grid>
      </Border>
      <Grid DockPanel.Dock="Top" >
        <Grid.ColumnDefinitions>
          <ColumnDefinition/>
        </Grid.ColumnDefinitions>
        <TextBox Grid.Column="0" AcceptsReturn="True"/>
      </Grid>
    </DockPanel>
  </Grid>
</Window>
```

A imagem a seguir ilustra o quadro com efeito de transparência estendido em um [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] aplicativo:

![Captura de tela mostrando um quadro com efeito de transparência estendido em um aplicativo WPF.](./media/extend-glass-frame-into-a-wpf-application/glass-frame-extended-wpf-application.png)

## <a name="see-also"></a>Consulte também

- [Visão geral do Gerenciador de janelas da área de trabalho](/windows/desktop/dwm/dwm-overview)
- [Visão geral de desfoque do Gerenciador de janelas da área de trabalho](/windows/desktop/dwm/blur-ovw)
- [DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea)
