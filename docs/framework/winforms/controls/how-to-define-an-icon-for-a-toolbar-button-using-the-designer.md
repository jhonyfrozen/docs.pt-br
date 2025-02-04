---
title: 'Como: Definir um ícone para um botão de barra de ferramentas usando o Designer'
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms], adding icons to buttons
- examples [Windows Forms], toolbars
- images [Windows Forms], toolbar buttons
- buttons [Windows Forms], images
- icons [Windows Forms], toolbar buttons
- ToolBar control [Windows Forms], adding icons to buttons
ms.assetid: d848f38e-67f2-49d4-8e88-01c845c06c02
ms.openlocfilehash: 04b4b2ddeadf5a86bd191d5a173659032461dfc5
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65960208"
---
# <a name="how-to-define-an-icon-for-a-toolbar-button-using-the-designer"></a>Como: Definir um ícone para um botão de barra de ferramentas usando o Designer

> [!NOTE]
> O controle <xref:System.Windows.Forms.ToolStrip> substitui e adiciona funcionalidade ao controle <xref:System.Windows.Forms.ToolBar>, no entanto, o controle <xref:System.Windows.Forms.ToolBar> é mantido para compatibilidade com versões anteriores e para uso futuro, se desejado.

<xref:System.Windows.Forms.ToolBar> botões são capazes de exibir ícones dentro deles para facilitar a identificação pelos usuários. Isso é feito pela adição de imagens para o <xref:System.Windows.Forms.ImageList> componente e associá-lo com o <xref:System.Windows.Forms.ToolBar> controle.

O procedimento a seguir exige um **aplicativo do Windows** projeto com um formulário que contém uma <xref:System.Windows.Forms.ToolBar> controle e um <xref:System.Windows.Forms.ImageList> componente. Para obter informações sobre como configurar um projeto desse tipo, consulte [como: Criar um projeto de aplicativo do Windows Forms](/visualstudio/ide/step-1-create-a-windows-forms-application-project) e [como: Adicionar controles ao Windows Forms](how-to-add-controls-to-windows-forms.md).

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).

### <a name="to-set-an-icon-for-a-toolbar-button-at-design-time"></a>Para definir um ícone para um botão de barra de ferramentas em tempo de design

1. Adicionar imagens para o <xref:System.Windows.Forms.ImageList> componente. Para obter mais informações, confira [Como: Adicionar ou remover imagens ImageList com o Designer](how-to-add-or-remove-imagelist-images-with-the-designer.md).

2. Selecione o <xref:System.Windows.Forms.ToolBar> controle no formulário.

3. No **propriedades** janela, defina as <xref:System.Windows.Forms.ToolBar> do controle <xref:System.Windows.Forms.ToolBar.ImageList%2A> propriedade para o <xref:System.Windows.Forms.ImageList> componente.

4. Clique o <xref:System.Windows.Forms.ToolBar> do controle <xref:System.Windows.Forms.ToolBar.Buttons%2A> propriedade para selecioná-lo e, em seguida, clique nas reticências (![o botão (...) na janela Propriedades do Visual Studio.](./media/visual-studio-ellipsis-button.png)) para abrir o **coleção ToolBarButton Editor de**.

5. Use o **Add** botão para adicionar botões a serem o <xref:System.Windows.Forms.ToolBar> controle.

6. No **propriedades** janela que aparece no painel à direita do **Editor de coleção ToolBarButton**, defina o <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> propriedade de cada botão de barra de ferramentas para um dos valores na lista, que é desenhada entre as imagens que você adicionou ao <xref:System.Windows.Forms.ImageList> componente.

## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.ToolBar>
- [Como: Disparar eventos de Menu para botões da barra de ferramentas](how-to-trigger-menu-events-for-toolbar-buttons.md)
- [Controle de barra de ferramentas](toolbar-control-windows-forms.md)
- [Componente ImageList](imagelist-component-windows-forms.md)
