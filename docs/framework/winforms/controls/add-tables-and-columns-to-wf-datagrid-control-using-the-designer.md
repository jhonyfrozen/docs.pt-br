---
title: 'Como: Adicionar tabelas e colunas do controle DataGrid do Windows Forms usando o Designer'
ms.date: 03/30/2017
helpviewer_keywords:
- columns [Windows Forms], adding to DataGrid control
- tables [Windows Forms], adding to DataGrid control
- DataGrid control [Windows Forms], adding tables and columns
ms.assetid: 4a6d1b34-b696-476b-bf8a-57c6230aa9e1
ms.openlocfilehash: a5955840988cb747b21f32efbd5c6091a86f483a
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959522"
---
# <a name="how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control-using-the-designer"></a>Como: Adicionar tabelas e colunas do controle DataGrid do Windows Forms usando o Designer

> [!NOTE]
> O controle <xref:System.Windows.Forms.DataGridView> substitui e adiciona funcionalidade ao controle <xref:System.Windows.Forms.DataGrid>, no entanto, o controle <xref:System.Windows.Forms.DataGrid> é mantido para compatibilidade com versões anteriores e para uso futuro, se desejado. Para obter mais informações, consulte [Diferenças Entre o Windows Forms DataGridView e os Controles do DataGrid](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).

Você pode exibir dados em formulários do Windows <xref:System.Windows.Forms.DataGrid> controle em tabelas e colunas criando <xref:System.Windows.Forms.DataGridTableStyle> objetos e adicioná-los para o <xref:System.Windows.Forms.GridTableStylesCollection> objeto, que é acessado por meio de <xref:System.Windows.Forms.DataGrid> do controle <xref:System.Windows.Forms.DataGrid.TableStyles%2A> propriedade. Cada estilo de tabela exibe o conteúdo da tabela de dados é especificada na <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> propriedade do <xref:System.Windows.Forms.DataGridTableStyle>. Por padrão, um estilo de tabela sem estilos de coluna especificados exibirá todas as colunas dentro dessa tabela de dados. Você pode restringir quais colunas da tabela aparecem adicionando <xref:System.Windows.Forms.DataGridColumnStyle> objetos para o <xref:System.Windows.Forms.GridColumnStylesCollection>, que é acessado por meio de <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> propriedade de cada <xref:System.Windows.Forms.DataGridTableStyle>.

Os procedimentos a seguir exigem uma **aplicativo do Windows** projeto com um formulário que contenha um <xref:System.Windows.Forms.DataGrid> controle. Para obter informações sobre como configurar um projeto desse tipo, consulte [como: Criar um projeto de aplicativo do Windows Forms](/visualstudio/ide/step-1-create-a-windows-forms-application-project) e [como: Adicionar controles ao Windows Forms](how-to-add-controls-to-windows-forms.md). Por padrão no Visual Studio 2005, o <xref:System.Windows.Forms.DataGrid> controle não está na **caixa de ferramentas**. Para obter informações sobre como adicioná-lo, consulte [como: Adicionar itens à caixa de ferramentas](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100)).

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).

### <a name="to-add-a-table-to-the-datagrid-control-in-the-designer"></a>Para adicionar uma tabela ao controle DataGrid no designer

1. Para exibir dados na tabela, primeiro você deve associar o <xref:System.Windows.Forms.DataGrid> controle para um conjunto de dados. Para obter mais informações, confira [Como: Associar o controle DataGrid dos Windows Forms a uma fonte de dados usando o Designer](bind-wf-datagrid-control-to-a-data-source-using-the-designer.md).

2. Selecione o <xref:System.Windows.Forms.DataGrid> do controle <xref:System.Windows.Forms.DataGrid.TableStyles%2A> propriedade na janela Propriedades e, em seguida, clique no botão de reticências (![o botão (...) na janela Propriedades do Visual Studio.](./media/visual-studio-ellipsis-button.png)) ao lado da propriedade para exibir o **Editor de coleção DataGridTableStyle**.

3. No editor de coleção, clique em **Adicionar** para inserir um estilo de tabela.

4. Clique em **Okey** para fechar o editor de coleção e, em seguida, reabri-lo clicando no botão de reticências ao lado de <xref:System.Windows.Forms.DataGrid.TableStyles%2A> propriedade.

     Quando você reabrir o editor de coleção, nenhuma tabela de dados associada ao controle aparecerá na lista suspensa para o <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> propriedade do estilo de tabela.

5. Na caixa **Membros** do editor de coleção, clique no estilo de tabela.

6. No **propriedades** caixa do editor de coleção, selecione o <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> valor para a tabela que você deseja exibir.

### <a name="to-add-a-column-to-the-datagrid-control-in-the-designer"></a>Para adicionar uma coluna ao controle DataGrid no designer

1. Na caixa **Membros** do **Editor de Coleção DataGridTableStyle**, selecione o estilo de tabela adequado. No **propriedades** caixa do editor de coleção, selecione o <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> coleção e, em seguida, clique no botão de reticências (![botão do botão de reticências (...) na janela Propriedades do Visual Studio.](./media/visual-studio-ellipsis-button.png)) próximo a a propriedade para exibir o **Editor de coleção DataGridColumnStyle**.

2. No editor de coleção, clique em **Adicionar** para inserir um estilo de coluna ou clique na seta para baixo ao lado de **Adicionar** para especificar um tipo de coluna.

     Na caixa suspensa, você pode selecionar o <xref:System.Windows.Forms.DataGridTextBoxColumn> ou <xref:System.Windows.Forms.DataGridBoolColumn> tipo.

3. Clique em Okey para fechar o **Editor de coleção DataGridColumnStyle**e, em seguida, reabra-o clicando no botão de reticências ao lado de <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> propriedade.

     Quando você reabrir o editor de coleção, quaisquer colunas de dados na tabela de dados associada serão exibido na lista suspensa para o <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> propriedade do estilo de coluna.

4. Na caixa **Membros** do editor de coleção, clique no estilo de coluna.

5. No **propriedades** caixa do editor de coleção, selecione o <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> valor para a coluna que você deseja exibir.

## <a name="see-also"></a>Consulte também

- [Controle DataGrid](datagrid-control-windows-forms.md)
- [Como: Excluir ou ocultar colunas no controle DataGrid dos Windows Forms](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
