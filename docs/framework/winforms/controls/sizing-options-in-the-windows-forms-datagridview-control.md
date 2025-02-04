---
title: Dimensionando opções no controle DataGridView dos Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], row sizing
- data grids [Windows Forms], column sizing
- DataGridView control [Windows Forms], column sizing
- DataGridView control [Windows Forms], sizing options
- data grids [Windows Forms], row sizing
- data grids [Windows Forms], sizing options
ms.assetid: a5620a9c-0d06-41e3-8934-c25ddb16c9e6
ms.openlocfilehash: 1da98dfa58651eca2052f7d180912d1aa2898385
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651973"
---
# <a name="sizing-options-in-the-windows-forms-datagridview-control"></a>Dimensionando opções no controle DataGridView dos Windows Forms
<xref:System.Windows.Forms.DataGridView> linhas, colunas e cabeçalhos podem alterar o tamanho como resultado de muitas ocorrências diferentes. A tabela a seguir mostra essas ocorrências.  
  
|Ocorrência|Descrição|  
|----------------|-----------------|  
|Redimensionamento do usuário|Os usuários podem fazer ajustes de tamanho arrastando ou clicando duas vezes nos divisores de linha, coluna ou cabeçalho.|  
|Redimensionamento do controle|No modo de preenchimento de coluna, as larguras de coluna são alteradas quando a largura do controle é alterada. Por exemplo, quando o controle é encaixado em seu formulário pai e o usuário redimensiona o formulário.|  
|Alteração do valor da célula|Nos modos de dimensionamento automático baseado em conteúdo, os tamanhos são alterados para ajustar os novos valores de exibição.|  
|Chamada de método|O redimensionamento programático baseado em conteúdo permite que você faça ajustes de tamanho oportunos com base nos valores de célula no momento da chamada de método.|  
|Configuração de propriedade|Você também pode definir valores específicos de largura e altura.|  
  
 Por padrão, o redimensionamento do usuário está habilitado, o dimensionamento automático está desabilitado e os valores de células são mais largos do que o recorte de suas colunas.  
  
 A tabela a seguir mostra cenários que você pode usar para ajustar o comportamento padrão ou para usar opções específicas de dimensionamento para atingir efeitos específicos.  
  
|Cenário|Implementação|  
|--------------|--------------------|  
|Use o modo de preenchimento de coluna para exibir dados de tamanhos semelhantes em um número relativamente pequeno de colunas que ocupem toda a largura do controle sem exibir a barra de rolagem horizontal.|Defina a propriedade <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> como <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>.|  
|Use o modo de preenchimento de coluna com valores de exibição de tamanhos variados.|Defina a propriedade <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> como <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>. Inicializar as larguras da coluna relativas, definindo a coluna <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> propriedades ou chamando o controle <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> método depois de preencher o controle com os dados.|  
|Use o modo de preenchimento de coluna com valores de importância variada.|Defina a propriedade <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> como <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>. Definir grande <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> valores para as colunas que sempre devem exibir alguns dos seus dados ou usar uma opção de dimensionamento diferente de preencher o modo para colunas específicas.|  
|Use o modo de preenchimento de coluna para evitar a exibição da tela de fundo do controle.|Defina as <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> propriedade da última coluna para <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill> e usar outras opções de dimensionamento para as outras colunas. Se as outras colunas usam muito o espaço disponível, defina o <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> propriedade da última coluna.|  
|Exiba uma coluna de largura fixa, como um ícone ou uma coluna de ID.|Definir <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> à <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.None> e <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> para <xref:System.Windows.Forms.DataGridViewTriState.False> para a coluna. Inicialize sua largura, definindo o <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> propriedade ou chamando o controle <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A> método depois de preencher o controle com os dados.|  
|Ajuste os tamanhos automaticamente sempre que o conteúdo da célula for alterado para evitar recorte e otimizar o uso de espaço.|Defina uma propriedade de dimensionamento automático para um valor que represente um modo de dimensionamento baseado em conteúdo. Para evitar uma penalidade de desempenho ao trabalhar com grandes quantidades de dados, use um modo de dimensionamento que calcule apenas as linhas exibidas.|  
|Ajuste os tamanhos para ajustar os valores nas linhas exibidas para evitar penalidades de desempenho ao trabalhar com várias linhas.|Use os valores de enumeração de modo de dimensionamento apropriados com o redimensionamento automático ou programático. Para ajustar os tamanhos para ajustar os valores nas linhas durante a rolagem, chamar um método de redimensionamento em um <xref:System.Windows.Forms.DataGridView.Scroll> manipulador de eventos. Para personalizar o usuário clique duas vezes em redimensionamento para que somente os valores nas linhas exibidas determinem os novos tamanhos, chamar um método de redimensionamento em um <xref:System.Windows.Forms.DataGridView.RowDividerDoubleClick> ou <xref:System.Windows.Forms.DataGridView.ColumnDividerDoubleClick> manipulador de eventos.|  
|Ajuste os tamanhos para ajustar o conteúdo da célula apenas em momentos específicos para evitar penalidades de desempenho ou permitir o redimensionamento do usuário.|Chame um método de redimensionamento baseado em conteúdo em um manipulador de eventos. Por exemplo, use o <xref:System.Windows.Forms.DataGridView.DataBindingComplete> evento para inicializar tamanhos após a associação e lidar com o <xref:System.Windows.Forms.DataGridView.CellValidated> ou <xref:System.Windows.Forms.DataGridView.CellValueChanged> eventos para ajustar os tamanhos para compensar as edições do usuário ou alterações na fonte de dados associados.|  
|Ajuste as alturas de linhas para conteúdo de célula multilinha.|Verifique se as larguras de coluna são apropriadas para a exibição de parágrafos de texto e use o dimensionamento de linhas baseado em conteúdo automático ou programático para ajustar as alturas. Também Certifique-se de que as células com conteúdo multilinha são exibidas usando um <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> valor de estilo de célula <xref:System.Windows.Forms.DataGridViewTriState.True>.<br /><br /> Normalmente, você usará o modo de dimensionamento automático de coluna para manter as larguras de coluna ou defini-las como larguras específicas antes que as alturas das linhas sejam ajustadas.|  
  
## <a name="resizing-with-the-mouse"></a>Redimensionando com o mouse  
 Por padrão, os usuários podem redimensionar linhas, colunas e cabeçalhos que não usam um modo de dimensionamento automático com base nos valores de célula. Para impedir que os usuários redimensionem com outros modos, como o modo de preenchimento de coluna, defina uma ou mais dos seguintes <xref:System.Windows.Forms.DataGridView> propriedades:  
  
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
 Você também pode impedir que os usuários redimensionem colunas ou linhas individuais, definindo suas <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> propriedades. Por padrão, o <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> o valor da propriedade se baseia o <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A> valor da propriedade de colunas e o <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A> valor da propriedade de linhas. Se você definir explicitamente <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> à <xref:System.Windows.Forms.DataGridViewTriState.True> ou <xref:System.Windows.Forms.DataGridViewTriState.False>, no entanto, o valor especificado substituirá o valor do controle é para que a linha ou coluna. Definir <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> para <xref:System.Windows.Forms.DataGridViewTriState.NotSet> para restaurar a herança.  
  
 Porque <xref:System.Windows.Forms.DataGridViewTriState.NotSet> restaura a herança de valor, o <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> propriedade nunca retornará uma <xref:System.Windows.Forms.DataGridViewTriState.NotSet> de valor, a menos que a linha ou coluna não foi adicionada a um <xref:System.Windows.Forms.DataGridView> controle. Se você precisar determinar se o <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> valor da propriedade de uma linha ou coluna é herdado, examine seu <xref:System.Windows.Forms.DataGridViewElement.State%2A> propriedade. Se o <xref:System.Windows.Forms.DataGridViewElement.State%2A> valor inclui o <xref:System.Windows.Forms.DataGridViewElementStates.ResizableSet> sinalizador, o <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A> valor da propriedade não é herdado.  
  
## <a name="automatic-sizing"></a>Dimensionamento automático  
 Há dois tipos de dimensionamento automático no <xref:System.Windows.Forms.DataGridView> controle: modo de preenchimento de coluna e dimensionamento automático baseado em conteúdo.  
  
 O modo de preenchimento de coluna faz com que as colunas visíveis no controle preencham a largura da área de exibição do controle. Para obter mais informações sobre esse modo, consulte [Modo de preenchimento da coluna no controle DataGridView dos Windows Forms](column-fill-mode-in-the-windows-forms-datagridview-control.md).  
  
 Você também pode configurar as linhas, as colunas e os cabeçalhos para ajustar automaticamente seus tamanhos a fim de ajustar o conteúdo de suas células. Nesse caso, o ajuste de tamanho ocorre sempre que o conteúdo da célula é alterado.  
  
> [!NOTE]
>  Se você mantiver os valores de célula em um cache de dados personalizados usando o modo virtual, o dimensionamento automático ocorre quando o usuário edita o valor de uma célula, mas não ocorrerá quando você altera um valor em cache fora de um <xref:System.Windows.Forms.DataGridView.CellValuePushed> manipulador de eventos. Nesse caso, chamar o <xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A> método para forçar o controle a atualizar a exibição de célula e aplicar os modos de dimensionamento automático atual.  
  
 Se o dimensionamento automático baseado em conteúdo estiver habilitado para apenas uma dimensão — ou seja, para linhas mas não colunas ou colunas, mas não para linhas — e <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> também é habilitada, o tamanho de ajuste também ocorre sempre que a outra dimensão for alterado. Por exemplo, se as linhas, mas não colunas são configuradas para dimensionamento automático e <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> é habilitado, os usuários podem arrastar divisores de coluna para alterar a largura de uma coluna e as alturas das linhas se ajustará automaticamente para que o conteúdo da célula ainda seja totalmente exibido.  
  
 Se você configurar as linhas e colunas para dimensionamento automático baseado em conteúdo e <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A> estiver habilitado, o <xref:System.Windows.Forms.DataGridView> controle ajustará os tamanhos sempre que o conteúdo da célula alterado e usará uma razão de altura e largura do ideal da célula ao calcular novos tamanhos.  
  
 Para configurar o modo de dimensionamento para cabeçalhos e linhas e colunas que não substituem o valor do controle, defina uma ou mais dos seguintes <xref:System.Windows.Forms.DataGridView> propriedades:  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A>  
  
 Para substituir o modo de dimensionamento de coluna do controle para uma coluna individual, defina suas <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> propriedade para um valor diferente de <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet>. O modo de dimensionamento para uma coluna, na verdade, é determinado pelo seu <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> propriedade. O valor dessa propriedade é baseado na coluna de <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> valor de propriedade, a menos que seja <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet>, caso em que o controle <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> valor é herdado.  
  
 Use o redimensionamento automático baseado em conteúdo com cuidado ao trabalhar com grandes quantidades de dados. Para evitar penalidades de desempenho, use os modos de dimensionamento automático que calculam tamanhos base apenas nas linhas exibidas em vez de analisar cada linha no controle. Para obter o desempenho máximo, use o redimensionamento programático para que você possa redimensionar em momentos específicos, como imediatamente depois que novos dados são carregados.  
  
 Modos de dimensionamento automático baseado em conteúdo não afetam linhas, colunas ou cabeçalhos que você ocultou Configurando a linha ou coluna <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> propriedade ou o controle <xref:System.Windows.Forms.DataGridView.RowHeadersVisible%2A> ou <xref:System.Windows.Forms.DataGridView.ColumnHeadersVisible%2A> propriedades a serem `false`. Por exemplo, se uma coluna for ocultada depois de ser dimensionada automaticamente para ajustar um valor de célula grande, a coluna oculta não mudará seu tamanho se a linha que contém o valor da célula grande for excluída. O dimensionamento automático não ocorre quando a visibilidade é alterado, portanto, alterar a coluna <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> propriedade de volta para `true` não forçará a recalcular seu tamanho com base no conteúdo atual.  
  
 O redimensionamento programático baseado em conteúdo afeta colunas, linhas e cabeçalhos independentemente da visibilidade.  
  
## <a name="programmatic-resizing"></a>Redimensionamento programático  
 Quando o dimensionamento automático está desabilitado, você pode definir programaticamente a largura ou a altura exata de linhas, colunas ou cabeçalhos usando as propriedades a seguir:  
  
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>  
  
 Você também pode redimensionar de forma programática as linhas, as colunas e os cabeçalhos para que se ajustem ao conteúdo usando os seguintes métodos:  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>  
  
- <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A>  
  
 Esses métodos redimensionarão as linhas, as colunas ou os cabeçalhos uma única vez em vez de configurá-los para redimensionamento contínuo. Os novos tamanhos são calculados automaticamente para exibir todo o conteúdo da célula sem recorte. Quando você redimensiona programaticamente colunas que tenham <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> valores de propriedade de <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill>, no entanto, as larguras de baseado em conteúdo calculadas são usadas para ajustar proporcionalmente a coluna <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> valores de propriedade e a coluna, na verdade, são de larguras em seguida, calculado de acordo com essas novas proporções para que todas as colunas preencham a área de exibição disponível do controle.  
  
 O redimensionando programático é útil para evitar penalidades de desempenho com o redimensionamento contínuo. Ele também é útil para fornecer os tamanhos inicias de cabeçalhos, colunas e linhas redimensionáveis pelo usuário e para o modo de preenchimento de coluna.  
  
 Normalmente, você chamará os métodos de redimensionamento programáticos em momentos específicos. Por exemplo, você pode redimensionar de forma programática todas as colunas imediatamente após o carregamento de dados ou redimensionar de forma programática uma linha específica depois que um valor de célula específico foi modificado.  
  
## <a name="customizing-content-based-sizing-behavior"></a>Personalizando o comportamento de dimensionamento baseado em conteúdo  
 Você pode personalizar os comportamentos de dimensionamento ao trabalhar com derivada <xref:System.Windows.Forms.DataGridView> tipos de célula, linha e coluna, substituindo o <xref:System.Windows.Forms.DataGridViewCell.GetPreferredSize%2A?displayProperty=nameWithType>, <xref:System.Windows.Forms.DataGridViewRow.GetPreferredHeight%2A?displayProperty=nameWithType>, ou <xref:System.Windows.Forms.DataGridViewColumn.GetPreferredWidth%2A?displayProperty=nameWithType> métodos ou chamando sobrecargas de método de redimensionamento em um derivado de protegidos <xref:System.Windows.Forms.DataGridView> controle. As sobrecargas de método de redimensionamento protegidas são projetadas para funcionar em pares para atingir uma razão ideal de altura para largura da célula, evitando células excessivamente altas ou largas. Por exemplo, se você chamar o `AutoResizeRows(DataGridViewAutoSizeRowsMode,Boolean)` sobrecarga da <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A> método e passar um valor de `false` para o <xref:System.Boolean> parâmetro, a sobrecarga calculará as alturas ideais e larguras de células na linha, mas ele se ajustará as alturas de linha somente. Em seguida, você deve chamar o <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> método para ajustar as larguras da coluna para o ideal calculado.  
  
## <a name="content-based-sizing-options"></a>Opções de dimensionamento baseado em conteúdo  
 As enumerações usadas pelos métodos e propriedades de dimensionamento têm valores semelhantes para dimensionamento baseado em conteúdo. Com esses valores, você pode limitar quais células são usadas para calcular o tamanho preferencial. Para todas as enumerações de dimensionamento, valores com nomes que se referem a células exibidas limitam seus cálculos para células em linhas exibidas. Excluir linhas é útil para evitar uma penalidade de desempenho ao trabalhar com uma grande quantidade de linhas. Você também pode restringir os cálculos para valores de célula nas células de cabeçalho ou que não sejam de cabeçalho.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>
- <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>
- <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>
- [Redimensionando colunas e linhas no controle DataGridView dos Windows Forms](resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
- [Modo de preenchimento de coluna no controle DataGridView dos Windows Forms](column-fill-mode-in-the-windows-forms-datagridview-control.md)
- [Como: Definir os modos de dimensionamento do controle DataGridView dos Windows Forms](how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)
