---
title: 'Como: Ancorar e encaixar controles filho em um controle TableLayoutPanel'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- net.ComponentModel.StyleCollectionEditor.TLP.AnchorDock
helpviewer_keywords:
- layout [Windows Forms], child controls
- controls [Windows Forms], child
- child controls [Windows Forms], anchoring and docking
- TableLayoutPanel control [Windows Forms], child controls
ms.assetid: 0d267c35-25f1-49b8-8976-c64e8f0ddc0b
ms.openlocfilehash: 7adbf9a98b25b237ee49d2689154e903d8fc0b5a
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586180"
---
# <a name="how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control"></a>Como: Ancorar e encaixar controles filho em um controle TableLayoutPanel
O <xref:System.Windows.Forms.TableLayoutPanel> controlar dá suporte a <xref:System.Windows.Forms.Control.Anchor%2A> e <xref:System.Windows.Forms.Control.Dock%2A> propriedades em seus controles filho.  
  
### <a name="to-align-a-child-control-in-a-tablelayoutpanel-cell"></a>Alinhar um controle filho a uma célula TableLayoutPanel  
  
1. Criar um <xref:System.Windows.Forms.TableLayoutPanel> controle no formulário.  
  
2. Defina o valor da <xref:System.Windows.Forms.TableLayoutPanel> do controle <xref:System.Windows.Forms.TableLayoutPanel.ColumnCount%2A> e <xref:System.Windows.Forms.TableLayoutPanel.RowCount%2A> propriedades a serem **1**.  
  
3. Criar uma <xref:System.Windows.Forms.Button> no controlar o <xref:System.Windows.Forms.TableLayoutPanel> controle. O <xref:System.Windows.Forms.Button> ocupa o canto superior esquerdo da célula.  
  
4. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `Left`. O <xref:System.Windows.Forms.Button> controle se move para alinhar com a borda esquerda da célula.  
  
    > [!NOTE]
    >  Esse comportamento difere do comportamento de outras caixas de controles. Em outros controles de contêiner, o controle filho não se move quando a <xref:System.Windows.Forms.Control.Anchor%2A> estiver definida, e a distância entre o controle ancorado e limite do contêiner pai é determinada no momento o <xref:System.Windows.Forms.Control.Anchor%2A> propriedade está definida.  
  
5. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `Top, Left`. O <xref:System.Windows.Forms.Button> controle se move para ocupar o canto superior esquerdo da célula.  
  
6. Repita a etapa 5 com um valor de `Top, Right` para mover o <xref:System.Windows.Forms.Button> controle para o canto superior direito da célula. Repita com valores de `Bottom, Left` e `Bottom, Right`.  
  
### <a name="to-stretch-a-child-control-in-a-tablelayoutpanel-cell"></a>Alongar um controle filho em uma célula TableLayoutPanel  
  
1. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `Left, Right`. O <xref:System.Windows.Forms.Button> controle é redimensionado para alongar-se pela célula.  
  
    > [!NOTE]
    >  Esse comportamento difere do comportamento de outras caixas de controles. Em outros controles de contêiner, o controle filho não é redimensionado quando o <xref:System.Windows.Forms.Control.Anchor%2A> estiver definida como `Left, Right` ou `Top, Bottom`.  
  
2. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `Top, Bottom`. O <xref:System.Windows.Forms.Button> controle é redimensionado para alongar de cima para baixo até a parte inferior da célula.  
  
3. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `Top, Bottom, Left, Right`. O <xref:System.Windows.Forms.Button> controle é redimensionado para preencher a célula.  
  
4. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Anchor%2A> propriedade `None`. O <xref:System.Windows.Forms.Button> controle é redimensionado e centralizado na célula.  
  
5. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Dock%2A> propriedade <xref:System.Windows.Forms.DockStyle.Left>. O <xref:System.Windows.Forms.Button> controle se move para alinhar com a borda esquerda da célula. O <xref:System.Windows.Forms.Button> controle mantém sua largura, mas sua altura é redimensionada para preencher a célula verticalmente.  
  
    > [!NOTE]
    >  Esse é o mesmo comportamento que ocorre em outras caixas de controle.  
  
6. Altere o valor da <xref:System.Windows.Forms.Button> do controle <xref:System.Windows.Forms.Control.Dock%2A> propriedade <xref:System.Windows.Forms.DockStyle.Fill>. O <xref:System.Windows.Forms.Button> controle é redimensionado para preencher a célula.  
  
## <a name="example"></a>Exemplo  
 A ilustração a seguir mostra cinco botões ancorados em cinco separado <xref:System.Windows.Forms.TableLayoutPanel> células.  
  
 ![Ancoragem TableLayoutPanel](./media/vs-tlpanchor.gif "VS_TLPanchor")  
  
 A ilustração a seguir mostra quatro botões ancorados nos cantos de quatro separado <xref:System.Windows.Forms.TableLayoutPanel> células.  
  
 ![Ancoragem TableLayoutPanel](./media/vs-tlpanchor2.gif "VS_TLPanchor2")  
  
 A ilustração a seguir mostra três botões alongados com ancoragem em três separado <xref:System.Windows.Forms.TableLayoutPanel> células.  
  
 ![Ancoragem TableLayoutPanel](./media/vs-tlpanchor3.gif "VS_TLPAnchor3")  
  
 O exemplo de código a seguir demonstra todas as combinações de <xref:System.Windows.Forms.Control.Anchor%2A> valores de propriedades de um <xref:System.Windows.Forms.Button> de controle em um <xref:System.Windows.Forms.TableLayoutPanel> controle.  
  
 [!code-csharp[System.Windows.Forms.TableLayoutPanel.AnchorExampleForm#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.AnchorExampleForm/CS/TlpAnchorExampleForm.cs#1)]
 [!code-vb[System.Windows.Forms.TableLayoutPanel.AnchorExampleForm#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.AnchorExampleForm/VB/TlpAnchorExampleForm.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências aos assemblies System, System.Data, System.Drawing e System.Windows.Forms.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.TableLayoutPanel>
- [Controle TableLayoutPanel](tablelayoutpanel-control-windows-forms.md)
