---
title: 'Como: Personalizar a formatação de dados no controle DataGridView do Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting data
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], changing colors in DataGridView control [Windows Forms]
- colors [Windows Forms], changing in DataGridView control [Windows Forms]
- data [Windows Forms], formatting in DataGridView control
- DataGridView control [Windows Forms], cell customization
- DataGridView control [Windows Forms], changing cell colors
- Windows Forms, changing colors of DataGridView cells
- DataGridView control [Windows Forms], substituting cell values for display
- data grids [Windows Forms], formatting data
ms.assetid: a6e72c70-ce18-425f-828d-d57be6f96ab6
ms.openlocfilehash: 948e9bf485b42b445491a4da9f8de7ae7974075c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592828"
---
# <a name="how-to-customize-data-formatting-in-the-windows-forms-datagridview-control"></a>Como: Personalizar a formatação de dados no controle DataGridView do Windows Forms
O exemplo de código a seguir demonstra como implementar um manipulador para o <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> evento que altera como as células são exibidas, dependendo de suas colunas e valores.  
  
 Células no `Balance` coluna que contêm números negativos são fornecidos a um plano de fundo vermelho. Você também pode formatar essas células como moeda para exibir valores negativos entre parênteses. Para obter mais informações, confira [Como: Formatar dados no Windows Forms DataGridView Control](how-to-format-data-in-the-windows-forms-datagridview-control.md).  
  
 Células no `Priority` valores de célula de imagens de exibição de coluna no lugar de correspondente textual. O <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> propriedade do <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> é usado para obter o valor de célula textual e para definir o valor de exibição de imagem correspondente.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/cs/customFormatting.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewCustomizeDataFormatting#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewCustomizeDataFormatting/vb/customFormatting.vb#00)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências aos assemblies System, System.Drawing e System.Windows.Forms.  
  
- <xref:System.Drawing.Bitmap> imagens denominadas `highPri.bmp`, `mediumPri.bmp`, e `lowPri.bmp` que residem no mesmo diretório que o arquivo executável.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Drawing.Bitmap>
- [Exibindo dados no controle DataGridView do Windows Forms](displaying-data-in-the-windows-forms-datagridview-control.md)
- [Como: Formatar dados no Windows Forms DataGridView Control](how-to-format-data-in-the-windows-forms-datagridview-control.md)
- [Estilos de célula no controle DataGridView do Windows Forms](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Formatação de dados no controle DataGridView dos Windows Forms](data-formatting-in-the-windows-forms-datagridview-control.md)
