---
title: 'Passo a passo: hospedar conteúdo do WPF no Win32'
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- hosting WPF content in Win32 window [WPF]
ms.assetid: 38ce284a-4303-46dd-b699-c9365b22a7dc
ms.openlocfilehash: 9042548c52a7a82f75b4287323097655ffec48bf
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610430"
---
# <a name="walkthrough-hosting-wpf-content-in-win32"></a>Passo a passo: hospedar conteúdo do WPF no Win32
O [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornece um ambiente avançado para a criação de aplicativos. No entanto, quando você tem um investimento substancial em [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] código, ele pode ser mais eficiente adicionar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] funcionalidade ao seu aplicativo em vez de reescrever o código original. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Fornece um mecanismo simples para hospedar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela.  
  
 Este tutorial descreve como escrever um aplicativo de exemplo [hospedando conteúdo do WPF em uma amostra de janela Win32](https://go.microsoft.com/fwlink/?LinkID=160004), que hosts [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela. Você pode estender este exemplo para hospedar qualquer [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela. Porque envolve a mistura de código gerenciado e não gerenciado, o aplicativo é escrito em [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)].  

<a name="requirements"></a>   
## <a name="requirements"></a>Requisitos  
 Este tutorial pressupõe uma familiaridade básica com ambos [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] de programação. Para obter uma introdução básica [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de programação, consulte [Introdução](../getting-started/index.md). Para obter uma introdução [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] de programação, você deve fazer referência a qualquer um dos vários livros sobre o assunto, em particular *Programming Windows* por Charles Petzold.  
  
 Como a amostra que acompanha este tutorial é implementada no [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)], este tutorial pressupõe uma familiaridade com o uso de [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] ao programa o [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]programação de código gerenciado de API mais um entendimento dos. Familiaridade com [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] é útil, mas não são essenciais.  
  
> [!NOTE]
>  Este tutorial inclui vários exemplos de código da amostra associada. No entanto, para facilitar a leitura, não inclui o código de exemplo completo. Para o código de exemplo completo, consulte [hospedando conteúdo do WPF em uma amostra de janela Win32](https://go.microsoft.com/fwlink/?LinkID=160004).  
  
<a name="basic_procedure"></a>   
## <a name="the-basic-procedure"></a>O procedimento básico  
 Esta seção descreve o procedimento básico para host [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela. As outras seções explicam os detalhes de cada etapa.  
  
 A chave para hospedar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela é o <xref:System.Windows.Interop.HwndSource> classe. Essa classe encapsula o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela, permitindo que ele seja incorporado a seu [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] como uma janela filho. A abordagem a seguir combina o [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] e o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] em um único aplicativo.  
  
1. Implemente sua [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo como uma classe gerenciada.  
  
2. Implementar um aplicativo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] com [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)]. Se você estiver começando com um aplicativo existente e não gerenciados [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] código, você poderá geralmente habilitá-lo chamar código gerenciado alterando as configurações de projeto para incluir o `/clr` sinalizador do compilador.  
  
3. Defina o modelo de threading como STA (Single-Threaded Apartment).  
  
4. Lidar com o [WM_CREATE](/windows/desktop/winmsg/wm-create)notificação no seu procedimento de janela e faça o seguinte:  
  
    1. Criar um novo <xref:System.Windows.Interop.HwndSource> objeto com a janela pai como seu `parent` parâmetro.  
  
    2. Crie uma instância da sua classe de conteúdo do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
    3. Atribua uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] objeto de conteúdo para o <xref:System.Windows.Interop.HwndSource.RootVisual%2A> propriedade do <xref:System.Windows.Interop.HwndSource>.  
  
    4. Obtenha o HWND do conteúdo. O <xref:System.Windows.Interop.HwndSource.Handle%2A> propriedade do <xref:System.Windows.Interop.HwndSource> objeto contém o identificador de janela (HWND). Para obter um HWND que você possa usar na parte não gerenciada de seu aplicativo, transmita `Handle.ToPointer()` para um HWND.  
  
5. Implemente uma classe gerenciada que contém um campo estático para manter uma referência ao seu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. Essa classe permite que você obtenha uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo do seu [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] código.  
  
6. Atribuir o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo ao campo estático.  
  
7. Receber notificações do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo anexando um manipulador para um ou mais do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] eventos.  
  
8. Se comunicar com o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo usando a referência que você armazenou no campo estático para definir propriedades e assim por diante.  
  
> [!NOTE]
>  Você também pode usar [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] para implementar seu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. No entanto, você precisará compilá-lo separadamente como um [!INCLUDE[TLA#tla_dll](../../../../includes/tlasharptla-dll-md.md)] e fazer referência a ele [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] de seu [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] aplicativo. O restante do procedimento é semelhante ao descrito acima.

<a name="implementing_the_application"></a>
## <a name="implementing-the-host-application"></a>Implementando o aplicativo host
 Esta seção descreve como hospedar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo em um basic [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] aplicativo. O conteúdo em si é implementado em [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] como uma classe gerenciada. Geralmente, é simples [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de programação. Os principais aspectos da implementação de conteúdo são discutidos [Implementando o conteúdo do WPF](#implementing_the_wpf_page).

<a name="autoNestedSectionsOUTLINE1"></a>
- [O aplicativo básico](#the_basic_application)

- [Hospedando o conteúdo do WPF](#hosting_the_wpf_page)

- [Mantendo uma referência ao conteúdo do WPF](#holding_a_reference)

- [Comunicando com o conteúdo do WPF](#communicating_with_the_page)

<a name="the_basic_application"></a>
### <a name="the-basic-application"></a>O aplicativo básico
 O ponto de partida para o aplicativo host era criar um modelo do Visual Studio 2005.

1. Abra o Visual Studio 2005 e, em seguida, selecione **novo projeto** da **arquivo** menu.

2. Selecione **Win32** na lista de [!INCLUDE[TLA2#tla_visualcpp](../../../../includes/tla2sharptla-visualcpp-md.md)] tipos de projeto. Se o idioma padrão não for [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)], você encontrará esses tipos de projeto sob **outras linguagens**.

3. Selecione uma **projeto Win32** modelo, atribua um nome ao projeto e clique em **Okey** para iniciar o **Assistente de aplicativo Win32**.

4. Aceite as configurações padrão do assistente e clique em **concluir** para iniciar o projeto.

 O modelo cria um basic [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] aplicativo, incluindo:

- Um ponto de entrada do aplicativo.

- Uma janela, com um procedimento de janela associado (WndProc).

- Um menu com **arquivo** e **ajudar** títulos. O **arquivo** menu tem um **sair** item que fecha o aplicativo. O **ajudar** menu tem um **sobre** item que inicia uma caixa de diálogo simples.

 Antes de começar a escrever código para hospedar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo, você precisa fazer duas modificações no modelo básico.

 A primeira é compilar o projeto como um código gerenciado. Por padrão, o projeto é compilado como um código não gerenciado. No entanto, porque [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] é implementado no código gerenciado, o projeto deve ser compilado de acordo.

1. Clique com botão direito no nome do projeto no **Gerenciador de soluções** e selecione **propriedades** no menu de contexto para iniciar o **páginas de propriedade** caixa de diálogo.

2. Selecione **propriedades de configuração** da exibição em árvore no painel esquerdo.

3. Selecione **Common Language Runtime** suporte das **padrões de projeto** lista no painel direito.

4. Selecione **Common Language Runtime Support (/ clr)** na caixa de listagem suspensa.

> [!NOTE]
>  Esse sinalizador de compilação permite que você use um código gerenciado no aplicativo, mas o código não gerenciado continuará sendo compilado como antes.

 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa o modelo de threading STA (Single-Threaded Apartment). Para funcionar adequadamente com o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] código de conteúdo, você deve definir o modelo de threading do aplicativo como STA aplicando um atributo para o ponto de entrada.

 [!code-cpp[Win32HostingWPFPage#WinMain](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#winmain)]

<a name="hosting_the_wpf_page"></a>
### <a name="hosting-the-wpf-content"></a>Hospedando o conteúdo do WPF
 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo é um aplicativo de entrada de endereço simples. Ele consiste em vários <xref:System.Windows.Controls.TextBox> controles para levar o nome de usuário, endereço e assim por diante. Também há dois <xref:System.Windows.Controls.Button> controles **Okey** e **Cancelar**. Quando o usuário clica **Okey**, o botão <xref:System.Windows.Controls.Primitives.ButtonBase.Click> manipulador de eventos coleta os dados das <xref:System.Windows.Controls.TextBox> controla, atribui a propriedades correspondentes e aciona um evento personalizado, `OnButtonClicked`. Quando o usuário clica **cancele**, o manipulador apenas aciona `OnButtonClicked`. O objeto de argumento de evento para `OnButtonClicked` contém um campo booleano que indica qual botão foi clicado.

 O código para hospedar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo é implementado em um manipulador para o [WM_CREATE](/windows/desktop/winmsg/wm-create) notificação na janela do host.

 [!code-cpp[Win32HostingWPFPage#WMCreate](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcreate)]

 O `GetHwnd` método usa as informações de tamanho e posição mais pai identificador de janela e retorna o identificador de janela de hospedado [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo.

> [!NOTE]
>  Não é possível usar um `#using` diretiva para o `System::Windows::Interop` namespace. Isso cria uma colisão de nomes entre o <xref:System.Windows.Interop.MSG> nesse namespace e a estrutura MSG declarada em winuser. h. Em vez disso, use nomes totalmente qualificados para acessar o conteúdo desse namespace.

 [!code-cpp[Win32HostingWPFPage#GetHwnd](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#gethwnd)]

 Você não pode hospedar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo diretamente na janela do aplicativo. Em vez disso, primeiro crie uma <xref:System.Windows.Interop.HwndSource> objeto para encapsular o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. Este objeto é basicamente uma janela projetada para hospedar um [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. Você hospedar o <xref:System.Windows.Interop.HwndSource> objeto na janela pai criando-o como um filho de um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela que é parte do seu aplicativo. O <xref:System.Windows.Interop.HwndSource> parâmetros do construtor contêm basicamente as mesmas informações que você passaria para CreateWindow ao criar um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] janela filho.

 Depois que você cria uma instância da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] objeto de conteúdo. Nesse caso, o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo é implementado como uma classe separada, `WPFPage`, usando [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)]. Você também pode implementar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo com [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. No entanto, para fazer isso você precisa configurar um projeto separado e construir o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo como um [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]. Você pode adicionar uma referência a esse [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] ao seu projeto e usá-la para criar uma instância da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo.

 Você exibir o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo na sua janela filho atribuindo uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo para o <xref:System.Windows.Interop.HwndSource.RootVisual%2A> propriedade do <xref:System.Windows.Interop.HwndSource>.

 A próxima linha de código anexa um manipulador de eventos `WPFButtonClicked`, para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo `OnButtonClicked` eventos. Esse manipulador é chamado quando o usuário clica o **Okey** ou **Cancelar** botão. Ver [conteúdo do communicating_with_the_WPF](#communicating_with_the_page) para mais informações sobre esse manipulador de eventos.

 A linha final do código mostrado retorna o identificador de janela (HWND) que está associado com o <xref:System.Windows.Interop.HwndSource> objeto. Você pode usar este identificador de seu [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] código para enviar mensagens para a janela hospedada, embora o exemplo não fazê-lo. O <xref:System.Windows.Interop.HwndSource> objeto gera um evento sempre que receber uma mensagem. Para processar as mensagens, chame o <xref:System.Windows.Interop.HwndSource.AddHook%2A> método anexar um manipulador de mensagens e, em seguida, processar as mensagens no manipulador.

<a name="holding_a_reference"></a>
### <a name="holding-a-reference-to-the-wpf-content"></a>Mantendo uma referência ao conteúdo do WPF
 Para muitos aplicativos, você desejará se comunicar com o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de conteúdo mais tarde. Por exemplo, você talvez queira modificar os [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] propriedades do conteúdo ou fazer com que o <xref:System.Windows.Interop.HwndSource> host de objeto diferente [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. Para fazer isso, você precisa de uma referência para o <xref:System.Windows.Interop.HwndSource> objeto ou o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. O <xref:System.Windows.Interop.HwndSource> objeto e seus respectivos [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo permanecer na memória até que você destrua o identificador de janela. No entanto, a variável que você atribuir ao <xref:System.Windows.Interop.HwndSource> objeto sairá do escopo assim que você retornar do procedimento de janela. A maneira habitual de resolver esse problema com [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] aplicativos é usar uma variável global ou estática. Infelizmente, não é possível atribuir um objeto gerenciado a esses tipos de variáveis. Você pode atribuir um identificador de janela associado <xref:System.Windows.Interop.HwndSource> do objeto a uma variável global ou estática, mas que não fornece acesso ao próprio objeto.

 A solução mais simples para esse problema é implementar uma classe gerenciada que contém um conjunto de campos estáticos para manter referências a todos os objetos gerenciados aos quais você precisa ter acesso. O exemplo usa o `WPFPageHost` classe para manter uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo, mais os valores iniciais de um número de suas propriedades que podem ser alteradas posteriormente pelo usuário. Isso é definido no cabeçalho.

 [!code-cpp[Win32HostingWPFPage#WPFPageHost](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.h#wpfpagehost)]

 A última parte do `GetHwnd` função atribui valores a esses campos para uso posterior, enquanto `myPage` ainda está no escopo.

<a name="communicating_with_the_page"></a>
### <a name="communicating-with-the-wpf-content"></a>Comunicando com o conteúdo do WPF
 Há dois tipos de comunicação com o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. O aplicativo recebe informações do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de conteúdo quando o usuário clica o **Okey** ou **Cancelar** botões. O aplicativo também possui um [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] que permite ao usuário alterar várias [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] propriedades, tais como o tamanho de fonte de cor ou padrão do plano de fundo do conteúdo.

 Conforme mencionado acima, quando o usuário clica em um dos botões do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo gera um `OnButtonClicked` eventos. O aplicativo anexa um manipulador a esse evento para receber essas notificações. Se o **Okey** botão foi clicado, o manipulador obterá as informações do usuário a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] de conteúdo e o exibe em um conjunto de controles estáticos.

 [!code-cpp[Win32HostingWPFPage#WPFButtonClicked](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wpfbuttonclicked)]

 O manipulador recebe um objeto de argumento de evento personalizado do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo, `MyPageEventArgs`. O objeto `IsOK` estiver definida como `true` se o **Okey** botão foi clicado, e `false` se a **Cancelar** botão foi clicado.

 Se o **Okey** botão foi clicado, o manipulador obterá uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo da classe de contêiner. Depois, ele coletará as informações do usuário que são mantidas pelo associado [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] propriedades de conteúdo e usará controles estáticos para exibir as informações na janela pai. Porque o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dados de conteúdo estão na forma de uma cadeia de caracteres gerenciada, ele deve ser empacotado para uso por um [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] controle. Se o **Cancelar** botão foi clicado, o manipulador limpará os dados dos controles estáticos.

 O aplicativo [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] fornece um conjunto de botões de opção que permitem ao usuário modificar a cor de fundo a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo e várias propriedades relacionadas a fonte. O exemplo a seguir é um trecho do procedimento de janela (WndProc) do aplicativo e sua manipulação de mensagens que define várias propriedades em diferentes mensagens, incluindo a cor da tela de fundo. As outras são semelhantes e não são mostradas. Consulte a amostra completa para obter detalhes e o contexto.

 [!code-cpp[Win32HostingWPFPage#WMCommandToBG](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcommandtobg)]

 Para definir a cor do plano de fundo, obtenha uma referência para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo (`hostedPage`) de `WPFPageHost` e defina a propriedade de cor do plano de fundo para a cor apropriada. A amostra usa três opções de cores: a cor original, verde-claro e salmão-claro. A cor de plano de fundo original é armazenada como um campo estático no `WPFPageHost` classe. Para ver as outras duas, crie um novo <xref:System.Windows.Media.SolidColorBrush> do objeto e passar um valor de cor estática para o construtor de <xref:System.Windows.Media.Colors> objeto.

<a name="implementing_the_wpf_page"></a>
## <a name="implementing-the-wpf-page"></a>Implementando a página do WPF
 Você pode hospedar e usar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo sem qualquer conhecimento da implementação real. Se o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo tiver sido empacotado em um separado [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)], poderá ter sido criado em qualquer [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] idioma. A seguir está um breve passo a passo o [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] implementação que é usada no exemplo. Esta seção contém as subseções a seguir.

<a name="autoNestedSectionsOUTLINE2"></a>
- [Layout](#page_layout)

- [Retornando os dados à janela do host](#returning_data_to_window)

- [Definindo as propriedades do WPF](#set_page_properties)

<a name="page_layout"></a>
### <a name="layout"></a>Layout
 O [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] elementos em de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo consistem em cinco <xref:System.Windows.Controls.TextBox> controla, às associada <xref:System.Windows.Controls.Label> controles: Nome, endereço, cidade, estado e CEP. Também há dois <xref:System.Windows.Controls.Button> controles **Okey** e **Cancelar**

 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo é implementado de `WPFPage` classe. Layout é tratado com um <xref:System.Windows.Controls.Grid> elemento de layout. A classe herda de <xref:System.Windows.Controls.Grid>, que torna o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elemento raiz do conteúdo.

 O [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo construtor usa a largura e altura e tamanhos a <xref:System.Windows.Controls.Grid> adequadamente. Em seguida, define o layout básico criando um conjunto de <xref:System.Windows.Controls.ColumnDefinition> e <xref:System.Windows.Controls.RowDefinition> objetos e adicioná-los para o <xref:System.Windows.Controls.Grid> objeto base <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> e <xref:System.Windows.Controls.Grid.RowDefinitions%2A> coleções, respectivamente. Isso define uma grade de cinco linhas e sete colunas, com as dimensões determinadas pelo conteúdo das células.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorToGridDef](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortogriddef)]

 Em seguida, o construtor adiciona os [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] elementos para o <xref:System.Windows.Controls.Grid>. O primeiro elemento é o texto do título, que é um <xref:System.Windows.Controls.Label> controle centralizado na primeira linha da grade.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorTitle](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortitle)]

 A próxima linha contém o nome <xref:System.Windows.Controls.Label> controle e seus respectivos <xref:System.Windows.Controls.TextBox> controle. Como o mesmo código é usado para cada par rótulo/caixa de texto, ele é colocado em um par de métodos particulares e usado para todos os cinco pares de rótulo/caixa de texto. Os métodos criam apropriado de controle e, em seguida, chamar o <xref:System.Windows.Controls.Grid> classe estática <xref:System.Windows.Controls.Grid.SetColumn%2A> e <xref:System.Windows.Controls.Grid.SetRow%2A> métodos para colocar os controles na célula apropriada. Depois que o controle é criado, o exemplo chama o <xref:System.Windows.Controls.UIElementCollection.Add%2A> método em de <xref:System.Windows.Controls.Panel.Children%2A> propriedade do <xref:System.Windows.Controls.Grid> para adicionar o controle à grade. O código para adicionar os pares de rótulo/caixa de texto restantes é semelhante. Consulte o código de exemplo para obter detalhes.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorName](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorname)]

 A implementação dos dois métodos ocorre da seguinte forma:

 [!code-cpp[Win32HostingWPFPage#WPFPageCreateHelpers](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagecreatehelpers)]

 Por fim, o exemplo adiciona o **Okey** e **Cancelar** botões e anexa um manipulador de eventos para seus <xref:System.Windows.Controls.Primitives.ButtonBase.Click> eventos.

 [!code-cpp[Win32HostingWPFPage#WPFPageCtorButtonsEvents](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorbuttonsevents)]

<a name="returning_data_to_window"></a>
### <a name="returning-the-data-to-the-host-window"></a>Retornando os dados à janela do host
 Quando qualquer botão é clicado, seu <xref:System.Windows.Controls.Primitives.ButtonBase.Click> é gerado. A janela de host poderia simplesmente anexar manipuladores para esses eventos e obter os dados diretamente a partir de <xref:System.Windows.Controls.TextBox> controles. O exemplo usa uma abordagem um pouco menos direta. Ele lida com o <xref:System.Windows.Controls.Primitives.ButtonBase.Click> dentro de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] , conteúdo e, em seguida, gera um evento personalizado `OnButtonClicked`, para notificar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo. Isso permite que o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo fazer alguma validação de parâmetro antes de notificar o host. O manipulador obtém o texto do <xref:System.Windows.Controls.TextBox> controla e o atribui a propriedades públicas, do qual o host pode recuperar as informações.

 A declaração de evento, em WPFPage.h:

 [!code-cpp[Win32HostingWPFPage#WPFPageEventDecl](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpageeventdecl)]

 O <xref:System.Windows.Controls.Primitives.ButtonBase.Click> manipulador de eventos, em WPFPage. cpp:

 [!code-cpp[Win32HostingWPFPage#WPFPageButtonClicked](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagebuttonclicked)]

<a name="set_page_properties"></a>
### <a name="setting-the-wpf-properties"></a>Definindo as propriedades do WPF
 O [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] host permite ao usuário alterar várias [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] propriedades do conteúdo. Do [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] lado, é simplesmente uma questão de alterar as propriedades. A implementação no [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] classe de conteúdo é um pouco mais complicado, porque não há nenhuma propriedade global que controla as fontes para todos os controles. Em vez disso, a propriedade apropriada de cada controle é alterada nos acessadores set das propriedades. O exemplo a seguir mostra o código para o `DefaultFontFamily` propriedade. Definindo a propriedade chama um método particular que por sua vez define o <xref:System.Windows.Controls.Control.FontFamily%2A> propriedades de vários controles.

 Em WPFPage.h:

 [!code-cpp[Win32HostingWPFPage#WPFPageFontFamilyProperty](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpagefontfamilyproperty)]

 Em WPFPage.cpp:

 [!code-cpp[Win32HostingWPFPage#WPFPageSetFontFamily](~/samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagesetfontfamily)]

## <a name="see-also"></a>Consulte também

- <xref:System.Windows.Interop.HwndSource>
- [Interoperação do WPF e do Win32](wpf-and-win32-interoperation.md)
