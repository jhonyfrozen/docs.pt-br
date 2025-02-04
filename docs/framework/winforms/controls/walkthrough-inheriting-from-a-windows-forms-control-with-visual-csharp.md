---
title: 'Passo a passo: Herdando um controle do Windows Forms com Visual C#'
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], custom controls
- inheritance [Windows Forms], control
- Windows Forms controls, inheritance
- inheritance [Windows Forms], walkthroughs
- custom controls [Windows Forms], inheritance
ms.assetid: 09476da0-8d4c-4a4c-b969-649519dfb438
ms.openlocfilehash: dc9abbf520d3af79a2c64884adcdfa2f1066ce1b
ms.sourcegitcommit: 682c64df0322c7bda016f8bfea8954e9b31f1990
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2019
ms.locfileid: "65557994"
---
# <a name="walkthrough-inheriting-from-a-windows-forms-control-with-visual-c"></a>Passo a passo: Herdando um controle de formulários do Windows com o Visual C\#
Com o Visual C#, você pode criar controles personalizados avançados por meio *herança*. Com a herança, você é capaz de criar controles que mantêm todas as funcionalidades inerentes de controles padrão dos Windows Forms, mas também incorporam funcionalidades personalizadas. Neste passo a passo, você criará um controle herdado simples chamado `ValueButton`. Esse botão herdará funcionalidades do formulários padrão do Windows <xref:System.Windows.Forms.Button> controlar e exporá uma propriedade personalizada chamada `ButtonValue`.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
## <a name="creating-the-project"></a>Criando o Projeto  
 Quando cria um novo projeto, você especifica seu nome para definir o namespace raiz, o nome do assembly e o nome do projeto e para garantir que o componente padrão estará no namespace correto.  
  
#### <a name="to-create-the-valuebuttonlib-control-library-and-the-valuebutton-control"></a>Para criar a biblioteca de controle ValueButtonLib e o controle ValueButton  
  
1. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto** para abrir a caixa de diálogo **Novo Projeto**.  
  
2. Selecione o **biblioteca de controle do Windows Forms** modelo de projeto da lista de projetos do Visual c# e o tipo `ValueButtonLib` no **nome** caixa.  
  
     O nome do projeto, `ValueButtonLib`, também é atribuído ao namespace raiz por padrão. O namespace raiz é usado para qualificar os nomes dos componentes no assembly. Por exemplo, se dois assemblies fornecerem componentes chamados `ValueButton`, você poderá especificar o componente `ValueButton` usando `ValueButtonLib.ValueButton`. Para obter mais informações, consulte [Namespaces](../../../csharp/programming-guide/namespaces/index.md).  
  
3. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **UserControl1.cs** e escolha **Renomear** no menu de atalho. Altere o nome de arquivo para `ValueButton.cs`. Clique no botão **Sim** quando solicitado se desejar renomear todas as referências ao elemento de código '`UserControl1`'.  
  
4. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **ValueButton.cs** e selecione **Exibir Código**.  
  
5. Localize o `class` linha de demonstrativo `public partial class ValueButton`e altere o tipo do qual esse controle herda de <xref:System.Windows.Forms.UserControl> para <xref:System.Windows.Forms.Button>. Isso permite que o controle herdado herde toda a funcionalidade do <xref:System.Windows.Forms.Button> controle.  
  
6. No **Gerenciador de Soluções**, abra o nó **ValueButton.cs** para exibir o arquivo de código gerado pelo designer, **ValueButton.Designer.cs**. Abra esse arquivo no **Editor de Códigos**.  
  
7. Localize o `InitializeComponent` método e remova a linha que atribui o <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> propriedade. Essa propriedade não existe no <xref:System.Windows.Forms.Button> controle.  
  
8. No menu **Arquivo**, escolha **Salvar Tudo** para salvar o projeto.  
  
    > [!NOTE]
    >  Um designer visual não está mais disponível. Porque o <xref:System.Windows.Forms.Button> controle faz sua própria pintura, você não conseguir modificar sua aparência no designer. Sua representação visual será exatamente o mesmo que a classe herda de (ou seja, <xref:System.Windows.Forms.Button>), a menos que modificado no código. Você ainda pode adicionar componentes, que não têm uma interface do usuário, à superfície de design.  
  
## <a name="adding-a-property-to-your-inherited-control"></a>Adicionando uma propriedade ao controle herdado  
 Um uso possível dos controles herdados dos Windows Forms é a criação de controles que são idênticos em termos de aparência a controles padrão dos Windows Forms, mas que expõem propriedades personalizadas. Nesta seção, você adicionará uma propriedade chamada `ButtonValue` ao controle.  
  
#### <a name="to-add-the-value-property"></a>Para adicionar a propriedade de valor  
  
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **ValueButton.cs** e, depois, clique em **Exibir Código** no menu de atalho.  
  
2. Localize a instrução `class`. Cole o código a seguir imediatamente depois de `{`:  
  
    ```csharp  
    // Creates the private variable that will store the value of your   
    // property.  
    private int varValue;  
    // Declares the property.  
    public int ButtonValue  
    {  
       // Sets the method for retrieving the value of your property.  
       get  
       {  
          return varValue;  
       }  
       // Sets the method for setting the value of your property.  
       set  
       {  
          varValue = value;  
       }  
    }  
    ```  
  
     Esse código define os métodos segundo os quais a propriedade `ButtonValue` é armazenada e recuperada. A instrução `get` define o valor retornado como o valor que é armazenado na variável particular `varValue` e a instrução `set` define o valor da variável particular usando a palavra-chave `value`.  
  
3. No menu **Arquivo**, escolha **Salvar Tudo** para salvar o projeto.  
  
## <a name="testing-your-control"></a>Testando seu controle  
 Controles não são projetos autônomos; eles devem ser hospedados em um contêiner. Para testar seu controle, você precisa fornecer um projeto de teste em que ele será executado. Você também precisa tornar seu controle acessível para o projeto de teste compilando-o. Nesta seção, você compilará seu controle e o testará em um Windows Form.  
  
#### <a name="to-build-your-control"></a>Para compilar seu controle  
  
1. No menu **Compilar**, clique em **Compilar Solução**.  
  
     O build deve ser bem-sucedido, sem avisos ou erros do compilador.  
  
#### <a name="to-create-a-test-project"></a>Para criar um projeto de teste  
  
1. No menu **Arquivo**, aponte para **Adicionar** e clique em **Novo Projeto** para abrir a caixa de diálogo **Adicionar Novo Projeto**.  
  
2. Selecione o nó **Windows**, abaixo de **Visual C#** e clique em **Aplicativo dos Windows Forms**.  
  
3. Na caixa **Nome**, digite `Test`.  
  
4. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Referências** de seu projeto de teste e selecione **Adicionar Referência** no menu de atalho para exibir a caixa de diálogo **Adicionar Referência**.  
  
5. Clique na guia rotulada como **Projetos**. O projeto `ValueButtonLib` estará listado em **Nome do Projeto**. Clique duas vezes no projeto para adicionar a referência ao projeto de teste.  
  
6. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Testar** e selecione **Compilar**.  
  
#### <a name="to-add-your-control-to-the-form"></a>Para adicionar o controle ao formulário  
  
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Form1.cs** e selecione **Designer de Modo de Exibição** no menu de atalho.  
  
2. Na **Caixa de Ferramentas**, clique em **Componentes de ValueButtonLib**. Clique duas vezes em **ValueButton**.  
  
     Um **ValueButton** aparece no formulário.  
  
3. Clique com o botão direito do mouse em **ValueButton** e selecione **Propriedades** no menu de atalho.  
  
4. Na janela **Propriedades**, examine as propriedades desse controle. Observe que elas são idênticas às propriedades expostas por um botão padrão, exceto pelo fato de que há uma propriedade adicional, `ButtonValue`.  
  
5. Defina a propriedade `ButtonValue` como `5`.  
  
6. No **todos os Windows Forms** guia da **caixa de ferramentas**, clique duas vezes em **rótulo** para adicionar um <xref:System.Windows.Forms.Label> controle ao seu formulário.  
  
7. Reposicione o rótulo no centro do formulário.  
  
8. Clique duas vezes em `valueButton1`.  
  
     O **Editor de Códigos** é aberto no evento `valueButton1_Click`.  
  
9. Insira a seguinte linha de código.  
  
    ```csharp  
    label1.Text = valueButton1.ButtonValue.ToString();  
    ```  
  
10. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Teste** e escolha **Definir como Projeto de Inicialização** no menu de atalho.  
  
11. No menu **Depuração**, selecione **Iniciar Depuração**.  
  
     `Form1` é exibido.  
  
12. Clique em `valueButton1`.  
  
     O numeral "5" é exibido em `label1`, demonstrando que a propriedade `ButtonValue` de seu controle herdado foi passada para `label1` por meio do método `valueButton1_Click`. Portanto, seu controle `ValueButton` herda todas as funcionalidades do botão padrão dos Windows Forms, mas expõe uma propriedade adicional personalizada.  
  
## <a name="see-also"></a>Consulte também

- [Como: Exibir um controle na caixa de diálogo de itens de caixa de ferramentas de escolha](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)
- [Passo a passo: Criando um controle composto com VisualC#](walkthrough-authoring-a-composite-control-with-visual-csharp.md)
