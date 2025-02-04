---
title: 'Passo a passo: organizar controles do Windows Forms no WPF'
ms.date: 04/03/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- arranging controls [WPF]
ms.assetid: a1db8049-15c7-45d6-ae3d-36a6735cb848
ms.openlocfilehash: 88b360d8445a743e2be5f16919b0c5d637ca46d7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64620720"
---
# <a name="walkthrough-arranging-windows-forms-controls-in-wpf"></a>Passo a passo: organizar controles do Windows Forms no WPF
Este passo a passo mostra como usar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] recursos de layout para organizar [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controles em um aplicativo híbrido.  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
- Criar o projeto.  
  
- Usando as configurações padrão de layout.  
  
- Dimensionando o conteúdo.  
  
- Usando o posicionamento absoluto.  
  
- Especificando o tamanho explicitamente.  
  
- Definindo propriedades de layout.  
  
- Noções básicas sobre limitações da ordem z.  
  
- Encaixe.  
  
- Definindo a visibilidade.  
  
- Hospedando um controle que não se alonga.  
  
- Dimensionamento.  
  
- Girando.  
  
- Margens e preenchimento de configuração.  
  
- Usando contêineres de layout dinâmico.  
  
 Para obter uma listagem de código completa das tarefas ilustradas neste passo a passo, consulte [Organizando controles do Windows Forms no WPF de exemplo](https://go.microsoft.com/fwlink/?LinkID=159971).  
  
 Quando tiver terminado, você terá um entendimento dos [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] recursos de layout no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-com base em aplicativos.  
  
## <a name="prerequisites"></a>Pré-requisitos  

É necessário o Visual Studio para concluir este passo a passo.
  
## <a name="creating-the-project"></a>Criando o Projeto  
  
#### <a name="to-create-and-set-up-the-project"></a>Criar e configurar o projeto  
  
1. Crie um projeto de aplicativo WPF chamado `WpfLayoutHostingWf`.  
  
2. No Gerenciador de Soluções, adicione referências aos assemblies a seguir.  
  
    - WindowsFormsIntegration  
  
    - System.Windows.Forms  
  
    - System.Drawing  
  
3. Clique duas vezes em MainWindow.xaml para abri-lo no modo de exibição XAML.  
  
4. No <xref:System.Windows.Window> elemento, adicione o seguinte [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] mapeamento de namespace.  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5. No <xref:System.Windows.Controls.Grid> conjunto de elementos a <xref:System.Windows.Controls.Grid.ShowGridLines%2A> propriedade `true` e defina cinco linhas e três colunas.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#2)]  
  
## <a name="using-default-layout-settings"></a>Usando as configurações padrão de layout  
 Por padrão, o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento manipula o layout para hospedado [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle.  
  
#### <a name="to-use-default-layout-settings"></a>Para usar as configurações padrão de layout  
  
1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#3)]  
  
2. Pressione F5 para compilar e executar o aplicativo. O [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.Button?displayProperty=nameWithType> controle aparece no <xref:System.Windows.Controls.Canvas>. O controle hospedado é dimensionado com base em seu conteúdo e o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento é dimensionado para acomodar o controle hospedado.  
  
## <a name="sizing-to-content"></a>Dimensionando para o conteúdo  
 O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento garante que o controle hospedado é dimensionado para exibir seu conteúdo corretamente.  
  
#### <a name="to-size-to-content"></a>Para dimensionar para o Conteúdo  
  
1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#4)]  
  
2. Pressione F5 para compilar e executar o aplicativo. Os dois novos controles de botão são dimensionados para exibir a sequência de texto mais longa e maior tamanho de fonte corretamente e o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elementos são redimensionados para acomodar os controles hospedados.  
  
## <a name="using-absolute-positioning"></a>Usando o posicionamento absoluto  
 Você pode usar posicionamento absoluto para colocar o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento em qualquer lugar na interface do usuário (IU).  
  
#### <a name="to-use-absolute-positioning"></a>Para usar posicionamento absoluto  
  
1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#5](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#5)]  
  
2. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento é colocado a 20 pixels do lado superior da célula da grade e 20 pixels da esquerda.  
  
## <a name="specifying-size-explicitly"></a>Especificando o tamanho explicitamente  
 Você pode especificar o tamanho do <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento usando o <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> propriedades.  
  
#### <a name="to-specify-size-explicitly"></a>Para especificar o tamanho explicitamente  
  
1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#6](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#6)]  
  
2. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> é definido como um tamanho de 50 pixels de largura por 70 pixels de altura, que é menor do que as configurações de layout padrão. O conteúdo a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle é reorganizado adequadamente.  
  
## <a name="setting-layout-properties"></a>Definindo propriedades de layout  
 Sempre defina propriedades relacionadas ao layout no controle hospedado usando as propriedades do <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento. Definindo propriedades de layout diretamente no controle hospedado produzirá resultados indesejados.  
  
 Definição de propriedades relacionadas ao layout no controle hospedado em [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] não tem nenhum efeito.  
  
#### <a name="to-see-the-effects-of-setting-properties-on-the-hosted-control"></a>Para ver os efeitos da definição das propriedades no controle hospedado  
  
1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#7](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#7)]  
  
2. No Gerenciador de Soluções, clique duas vezes em MainWindow.xaml. Abrir vb ou MainWindow.xaml.cs no Editor de códigos.  
  
3. Copie o seguinte código para o `MainWindow` definição de classe.  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#101)]
     [!code-vb[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#101)]

4. Pressione F5 para compilar e executar o aplicativo.

5. Clique o **Click me** botão. O `button1_Click` conjuntos de manipulador de eventos do <xref:System.Windows.Forms.Control.Top%2A> e <xref:System.Windows.Forms.Control.Left%2A> propriedades no controle hospedado. Isso faz com que o controle hospedado seja reposicionado dentro do <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento. O host mantém a mesma área da tela, mas o controle hospedado é cortado. Em vez disso, o controle hospedado sempre deve preencher o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento.

## <a name="understanding-z-order-limitations"></a>Noções básicas sobre limitações da ordem z
 Visível <xref:System.Windows.Forms.Integration.WindowsFormsHost> elementos sempre são desenhados sobre outros elementos do WPF, e eles não são afetados pela ordem z. Para ver esse comportamento da ordem z, faça o seguinte:

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#8](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#8)]

2. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento é pintado sobre o elemento de rótulo.

## <a name="docking"></a>Encaixe
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> dá suporte ao elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] encaixe. Defina as <xref:System.Windows.Controls.DockPanel.Dock%2A> propriedade anexada para encaixar o controle hospedado em um <xref:System.Windows.Controls.DockPanel> elemento.

#### <a name="to-dock-a-hosted-control"></a>Para encaixar o controle hospedado

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#9](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#9)]

2. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> é encaixado à direita do elemento a <xref:System.Windows.Controls.DockPanel> elemento.

## <a name="setting-visibility"></a>Definindo a visibilidade
 Você pode fazer sua [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle invisível ou recolhê-lo definindo o <xref:System.Windows.UIElement.Visibility%2A> propriedade no <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento. Quando um controle estiver invisível, ele não será exibido, mas ocupa espaço de layout. Quando um controle estiver recolhido, ele não será exibido, mas também não ocupa espaço de layout.

#### <a name="to-set-the-visibility-of-a-hosted-control"></a>Para definir a visibilidade de um controle hospedado

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#10](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#10)]

2. Em MainWindow.xaml.vb ou MainWindow.xaml.cs, copie o código a seguir para a definição de classe.

     [!code-csharp[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#102)]
     [!code-vb[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#102)]

3. Pressione F5 para compilar e executar o aplicativo.

4. Clique o **clique para tornar invisíveis** botão para fazer o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento invisível.

5. Clique o **clique para recolher** botão para ocultar o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento do layout completamente. Quando o [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle estiver recolhido, os elementos adjacentes serão reorganizados para ocupar o seu espaço.

## <a name="hosting-a-control-that-does-not-stretch"></a>Hospedando um controle que não se alonga
 Alguns [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controles têm um tamanho fixo e não se esticam para preencher o espaço disponível no layout. Por exemplo, o <xref:System.Windows.Forms.MonthCalendar> controle exibe um mês em um espaço fixo.

#### <a name="to-host-a-control-that-does-not-stretch"></a>Para hospedar um controle que não se alonga

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#11)]

2. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento é centralizado na linha de grade, mas ele não é alongado para preencher o espaço disponível. Se a janela é grande o suficiente, você poderá ver duas ou mais meses exibidos pelo hospedado <xref:System.Windows.Forms.MonthCalendar> controle, mas eles são centralizados na linha. O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mecanismo de layout centraliza os elementos que não podem ser dimensionados para preencher o espaço disponível.

## <a name="scaling"></a>Dimensionamento
 Diferentemente dos elementos do WPF, a maioria dos controles de formulários do Windows não são escalonáveis continuamente. Para fornecer dimensionamento personalizado, você deve substituir o <xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A?displayProperty=nameWithType> método.

#### <a name="to-scale-a-hosted-control-by-using-the-default-behavior"></a>Para dimensionar um controle hospedado usando o comportamento padrão

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#12)]

2. Pressione F5 para compilar e executar o aplicativo. O controle hospedado e seus elementos adjacentes são dimensionados por um fator de 0,5. No entanto, a fonte do controle hospedada não é redimensionada.

<!-- This could use an example of custom scaling. -->

## <a name="rotating"></a>Girando
 Diferentemente dos elementos do WPF, controles dos Windows Forms não oferecem suporte a rotação. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento não gira com outros elementos do WPF quando uma transformação de rotação é aplicada. Qualquer valor de rotação diferente de 180 graus gera o <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> eventos.

#### <a name="to-see-the-effect-of-rotation-in-a-hybrid-application"></a>Para ver o efeito de rotação em um aplicativo híbrido

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#13)]

2. Pressione F5 para compilar e executar o aplicativo. O controle hospedado não é girado, mas seus elementos adjacentes são girados por um ângulo de 180 graus. Você terá que redimensionar a janela para ver os elementos.

## <a name="setting-padding-and-margins"></a>Margens e preenchimento de configuração
 Preenchimento e margens em [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] layout são semelhantes a preenchimento e margens em [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]. Basta definir a <xref:System.Windows.Controls.Control.Padding%2A> e <xref:System.Windows.FrameworkElement.Margin%2A> propriedades sobre o <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento.

#### <a name="to-set-padding-and-margins-for-a-hosted-control"></a>Para definir o preenchimento e margens de um controle hospedado

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#14)]
    [!code-xaml[WpfLayoutHostingWfWithXaml#15](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#15)]

2. Pressione F5 para compilar e executar o aplicativo. As configurações de preenchimento e margem são aplicadas para hospedado [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controles da mesma maneira que seriam aplicadas em [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].

## <a name="using-dynamic-layout-containers"></a>Usando contêineres de layout dinâmico
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] fornece dois contêineres de layout dinâmico <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel>. Você também pode usar esses contêineres em [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] layouts.

#### <a name="to-use-a-dynamic-layout-container"></a>Para usar um contêiner de layout dinâmico

1. Copie o seguinte XAML para o <xref:System.Windows.Controls.Grid> elemento.

     [!code-xaml[WpfLayoutHostingWfWithXaml#16](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#16)]

2. Em MainWindow.xaml.vb ou MainWindow.xaml.cs, copie o código a seguir para a definição de classe.

     [!code-csharp[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#103)]
     [!code-vb[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#103)]

3. Adicione uma chamada para o `InitializeFlowLayoutPanel` método no construtor.

     [!code-csharp[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#104)]
     [!code-vb[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#104)]  
  
4. Pressione F5 para compilar e executar o aplicativo. O <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento preenche os <xref:System.Windows.Controls.DockPanel>, e <xref:System.Windows.Forms.FlowLayoutPanel> organiza seus controles filho no padrão <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Criar o XAML no Visual Studio](/visualstudio/designers/designing-xaml-in-visual-studio)
- [Considerações sobre o layout do elemento WindowsFormsHost](layout-considerations-for-the-windowsformshost-element.md)
- [Organizar o Windows Forms a controles no WPF de exemplo](https://go.microsoft.com/fwlink/?LinkID=159971)
- [Passo a passo: Hospedando um controle composto do Windows Forms no WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [Passo a passo: Hospedando um controle composto do WPF nos Windows Forms](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
