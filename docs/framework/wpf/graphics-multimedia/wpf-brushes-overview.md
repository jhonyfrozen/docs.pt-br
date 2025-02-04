---
title: Visão geral de pincéis do WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], about brushes
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
ms.openlocfilehash: a0de8aee53c5db63952e4baa72827a92c47ccce0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593384"
---
# <a name="wpf-brushes-overview"></a>Visão geral de pincéis do WPF
Tudo o que é visível na tela é visível porque foi pintado por um pincel. Por exemplo, um pincel é usado para descrever a tela de fundo de um botão, o primeiro plano do texto e o preenchimento de uma forma. Este tópico apresenta os conceitos de pintura com pincéis [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e fornece exemplos. Os pincéis permitem que você pinte objetos [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] com qualquer coisa, desde cores simples e sólidas a conjuntos complexos de padrões e imagens.  
  
<a name="paintingwithbrush"></a>   
## <a name="painting-with-a-brush"></a>Pintando com um pincel  
 Um <xref:System.Windows.Media.Brush> "pinta" uma área com sua saída. Pincéis diferentes têm tipos diferentes de saída. Alguns pincéis pintam uma área com uma cor sólida, outros com um gradiente, um padrão, uma imagem ou um desenho. A ilustração a seguir mostra exemplos de cada um dos diferentes <xref:System.Windows.Media.Brush> tipos.  
  
 ![Tipos de pincel](./media/graphicsmm-brushtypes.jpg "graphicsmm_brushtypes")  
Exemplos de pincel  
  
 A maioria dos objetos visuais permite especificar como eles são pintados. A tabela a seguir lista alguns objetos comuns e a propriedades com o qual você pode usar um <xref:System.Windows.Media.Brush>.  
  
|Classe|Propriedades do pincel|  
|-----------|----------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 As seções a seguir descrevem as diferentes <xref:System.Windows.Media.Brush> tipos e fornecem um exemplo de cada um.  
  
<a name="paintwithsolidcolorbrush"></a>   
## <a name="paint-with-a-solid-color"></a>Pintar com uma cor sólida  
 Um <xref:System.Windows.Media.SolidColorBrush> pinta uma área com uma sólida <xref:System.Windows.Media.Color>. Há uma variedade de maneiras para especificar o <xref:System.Windows.Media.SolidColorBrush.Color%2A> de um <xref:System.Windows.Media.SolidColorBrush>: por exemplo, você pode especificar seus canais alfabéticos, vermelhos, azuis e verdes ou usar uma das cores predefinidas fornecidas pelo <xref:System.Windows.Media.Colors> classe.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.SolidColorBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado usando um SolidColorBrush](./media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm_brush_ovw_solidcolorbrush")  
Um retângulo pintado usando um SolidColorBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.SolidColorBrush> classe, consulte [pintura com cores sólidas e gradientes Overview](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithlineargradientbrush"></a>   
## <a name="paint-with-a-linear-gradient"></a>Pintar com um gradiente linear  
 Um <xref:System.Windows.Media.LinearGradientBrush> pinta uma área com um gradiente linear. Um gradiente linear combina duas ou mais cores em uma linha, o eixo de gradiente. Você usa <xref:System.Windows.Media.GradientStop> objetos para especificar as cores no gradiente, bem como suas posições.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.LinearGradientBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado usando um LinearGradientBrush](./media/graphicsmm-brush-ovw-lineargradientbrush.jpg "graphicsmm_brush_ovw_lineargradientbrush")  
Um retângulo pintado usando um LinearGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.LinearGradientBrush> classe, consulte [pintura com cores sólidas e gradientes Overview](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithradialgradientbrush"></a>   
## <a name="paint-with-a-radial-gradient"></a>Pintar com um gradiente radial  
 Um <xref:System.Windows.Media.RadialGradientBrush> pinta uma área com um gradiente radial. Um gradiente radial combina duas ou mais cores em um círculo. Assim como acontece com o <xref:System.Windows.Media.LinearGradientBrush> classe, use <xref:System.Windows.Media.GradientStop> objetos para especificar as cores no gradiente, bem como suas posições.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.RadialGradientBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado usando um RadialGradientBrush](./media/graphicsmm-brush-ovw-radialgradientbrush.jpg "graphicsmm_brush_ovw_radialgradientbrush")  
Um retângulo pintado usando um RadialGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.RadialGradientBrush> classe, consulte [pintura com cores sólidas e gradientes Overview](painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithimage"></a>   
## <a name="paint-with-an-image"></a>Pintar com uma imagem  
 Uma <xref:System.Windows.Media.ImageBrush> pinta uma área com um <xref:System.Windows.Media.ImageSource>.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.ImageBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado por um ImageBrush](./media/graphicsmm-brush-ovw-imagebrush.jpg "graphicsmm_brush_ovw_imagebrush")  
Um retângulo pintado usando uma imagem  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.ImageBrush> classe, consulte [pintando com imagens, desenhos e visuais](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithdrawing"></a>   
## <a name="paint-with-a-drawing"></a>Pintar com um desenho  
 Um <xref:System.Windows.Media.DrawingBrush> pinta uma área com um <xref:System.Windows.Media.Drawing>. Um <xref:System.Windows.Media.Drawing> pode conter formas, imagens, texto e mídia.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.DrawingBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado usando um DrawingBrush](./media/graphicsmm-brush-ovw-drawingbrush.jpg "graphicsmm_brush_ovw_drawingbrush")  
Um retângulo pintado usando um DrawingBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.DrawingBrush> classe, consulte [pintando com imagens, desenhos e visuais](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithvisual"></a>   
## <a name="paint-with-a-visual"></a>Pintar com um visual  
 Um <xref:System.Windows.Media.VisualBrush> pinta uma área com um <xref:System.Windows.Media.Visual> objeto. Exemplos de objetos visuais <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Page>, e <xref:System.Windows.Controls.MediaElement>. Um <xref:System.Windows.Media.VisualBrush> também permite projetar conteúdo de uma parte de seu aplicativo em outra área; ele é muito útil para criar efeitos de reflexão e ampliar partes da tela.  
  
 O exemplo a seguir usa uma <xref:System.Windows.Media.VisualBrush> para pintar o <xref:System.Windows.Shapes.Shape.Fill%2A> de um <xref:System.Windows.Shapes.Rectangle>. A ilustração a seguir mostra o retângulo pintado.  
  
 ![Um retângulo pintado usando um VisualBrush](./media/graphicsmm-brush-ovw-visualbrush.jpg "graphicsmm_brush_ovw_visualbrush")  
Um retângulo pintado usando um VisualBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 Para obter mais informações sobre o <xref:System.Windows.Media.VisualBrush> classe, consulte [pintando com imagens, desenhos e visuais](painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## <a name="paint-using-predefined-and-system-brushes"></a>Pintar usando pincéis do sistema e predefinidos  
 Para sua conveniência, o Windows Presentation Foundation (WPF) fornece predefinido de um conjunto de pincéis do sistema e que você pode usar para pintar objetos.  
  
- Para obter uma lista dos pincéis predefinidos disponíveis, consulte o <xref:System.Windows.Media.Brushes> classe. Para ver um exemplo que mostra como usar um pincel predefinido, consulte [Pintar uma área com uma cor sólida](how-to-paint-an-area-with-a-solid-color.md).  
  
- Para obter uma lista de pincéis do sistema disponíveis, consulte o <xref:System.Windows.SystemColors> classe. Para ver um exemplo, consulte [Pintar uma área com um pincel de sistema](how-to-paint-an-area-with-a-system-brush.md).  
  
<a name="commonbrushfeatures"></a>   
## <a name="common-brush-features"></a>Recursos comuns de pincel  
 <xref:System.Windows.Media.Brush> objetos fornecem um <xref:System.Windows.Media.Brush.Opacity%2A> propriedade que pode ser usada para deixar um pincel transparente ou parcialmente transparente. Uma <xref:System.Windows.Media.Brush.Opacity%2A> valor igual a 0 deixa o pincel completamente transparente, enquanto um <xref:System.Windows.Media.Brush.Opacity%2A> valor igual a 1 deixa o pincel completamente opaco. O exemplo a seguir usa o <xref:System.Windows.Media.Brush.Opacity%2A> propriedade para tornar um <xref:System.Windows.Media.SolidColorBrush> 25 por cento opaco.  
  
 [!code-xaml[BrushOverviewExamples_snip#OpacityExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 Se o pincel contiver cores parcialmente transparentes, o valor da opacidade da cor será combinado por multiplicação com o valor da opacidade do pincel. Por exemplo, se um pincel tiver um valor de opacidade de 0,5 e uma cor usada no pincel também tiver um valor de opacidade de 0,5, a cor de saída terá o valor de opacidade de 0,25.  
  
> [!NOTE]
>  É mais eficiente para alterar o valor de opacidade de um pincel do que alterar a opacidade de um elemento inteiro usando sua <xref:System.Windows.UIElement.Opacity%2A?displayProperty=nameWithType> propriedade.  
  
 Girar, dimensionar, inclinar e converter o conteúdo do pincel usando suas <xref:System.Windows.Media.Brush.Transform%2A> ou <xref:System.Windows.Media.Brush.RelativeTransform%2A> propriedades. Para obter mais informações, veja [Visão geral da transformação de pincel](brush-transformation-overview.md).  
  
 Por estarem <xref:System.Windows.Media.Animation.Animatable> objetos, <xref:System.Windows.Media.Brush> objetos podem ser animados. Para obter mais informações, consulte [Visão geral de animação](animation-overview.md).  
  
<a name="freezable_features"></a>   
### <a name="freezable-features"></a>Recursos congeláveis  
 Porque ele herda o <xref:System.Windows.Freezable> classe, o <xref:System.Windows.Media.Brush> classe fornece vários recursos especiais: <xref:System.Windows.Media.Brush> objetos podem ser declarados como [recursos](../advanced/xaml-resources.md), compartilhados entre vários objetos e clonados. Além disso, todos os <xref:System.Windows.Media.Brush> tipos exceto <xref:System.Windows.Media.VisualBrush> pode ser somente leitura para melhorar o desempenho e transformados em thread-safe.  
  
 Para obter mais informações sobre os diferentes recursos fornecidos pelo <xref:System.Windows.Freezable> objetos, consulte [visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md).  
  
 Para obter mais informações sobre por que <xref:System.Windows.Media.VisualBrush> objetos não podem ser congelados, consulte o <xref:System.Windows.Media.VisualBrush> página de tipo.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.Brushes>
- [Visão geral da pintura com cores sólidas e gradientes](painting-with-solid-colors-and-gradients-overview.md)
- [Pintando com imagens, desenhos e visuais](painting-with-images-drawings-and-visuals.md)
- [Visão geral de objetos congeláveis](../advanced/freezable-objects-overview.md)
- [Exemplo de pincéis](https://go.microsoft.com/fwlink/?LinkID=159973)
- [Exemplo de ImageBrush](https://go.microsoft.com/fwlink/?LinkID=160005)
- [Exemplo de VisualBrush](https://go.microsoft.com/fwlink/?LinkID=160049)
- [Tópicos de instruções](brushes-how-to-topics.md)
- [Outras recomendações de desempenho](../advanced/optimizing-performance-other-recommendations.md)
