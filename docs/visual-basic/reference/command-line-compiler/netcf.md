---
title: -netcf
ms.date: 03/13/2018
f1_keywords:
- /netcf
- -netcf
helpviewer_keywords:
- -netcf compiler option [Visual Basic]
- netcf compiler option [Visual Basic]
- /netcf compiler option [Visual Basic]
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
ms.openlocfilehash: 028fa148d0e5622648a5fdfff1789c3d0bfde057
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268285"
---
# <a name="-netcf"></a>-netcf

Define o compilador para ter como destino o .NET Compact Framework.

## <a name="syntax"></a>Sintaxe

```
-netcf
```

## <a name="remarks"></a>Comentários

O `-netcf` opção faz com que o compilador do Visual Basic para ter como destino o .NET Compact Framework, em vez do .NET Framework completo. Funcionalidades de linguagem que estão presentes apenas no .NET Framework completo está desabilitada.

O `-netcf` opção é projetada para ser usada com [- sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md). Os recursos de linguagem desabilitados por `-netcf` são os mesmos recursos de idioma não está presentes nos arquivos de destino com `-sdkpath`.

> [!NOTE]
> O `-netcf` opção não está disponível no ambiente de desenvolvimento do Visual Studio; ele está disponível somente durante a compilação da linha de comando. O `-netcf` opção é definida quando um projeto de dispositivo do Visual Basic é carregado.

O `-netcf` opção altera os seguintes recursos de idioma:

- O [final \<palavra-chave > demonstrativo](../../../visual-basic/language-reference/statements/end-keyword-statement.md) palavra-chave, que finaliza a execução de um programa, está desabilitado. O programa a seguir compila e executa sem `-netcf` , mas falhar no tempo de compilação com `-netcf`.

  [!code-vb[VbVbalrCompiler#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/netcf.vb#34)]

- Associação tardia em todos os formulários, está desabilitado. Erros de tempo de compilação são gerados quando os cenários de associação tardia reconhecidos são encontrados. O programa a seguir compila e executa sem `-netcf` , mas falhar no tempo de compilação com `-netcf`.

  [!code-vb[VbVbalrCompiler#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#35)]

- O [automática](../../../visual-basic/language-reference/modifiers/auto.md), [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md), e [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) modificadores estão desabilitados. A sintaxe do [instrução Declare](../../../visual-basic/language-reference/statements/declare-statement.md) instrução também será modificada para `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`. O código a seguir mostra o efeito de `-netcf` em uma compilação.

  [!code-vb[VbVbalrCompiler#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#36)]

- Usando o Visual Basic 6.0 as palavras-chave que foram removidas do Visual Basic gera um erro diferente quando `-netcf` é usado. Isso afeta as mensagens de erro para as seguintes palavras-chave:

  - `Open`

  - `Close`

  - `Put`

  - `Print`

  - `Write`

  - `Input`

  - `Lock`

  - `Unlock`

  - `Seek`

  - `Width`

  - `Name`

  - `FreeFile`

  - `EOF`

  - `Loc`

  - `LOF`

  - `Line`

## <a name="example"></a>Exemplo

O seguinte código compila `Myfile.vb` com o .NET Compact Framework, usando as versões de mscorlib. dll e VisualBasic seja localizado no diretório de instalação padrão do .NET Compact Framework na unidade C. Normalmente, você poderia usar a versão mais recente do .NET Compact Framework.

```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb
```

## <a name="see-also"></a>Consulte também

- [Compilador de linha de comando do Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)
- [Linhas de Comando de Compilação de Exemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
