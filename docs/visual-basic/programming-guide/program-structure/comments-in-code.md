---
title: Comentários no código (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Uncomment button
- REM statement [Visual Basic]
- comments [Visual Basic], in code
- comments [Visual Basic], Visual Basic code
- Comment button
- buttons [Visual Basic], Uncomment
- buttons [Visual Basic], Comment
- code comments [Visual Basic], Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
ms.openlocfilehash: 2737d9494fb4cd2f0cfaec4da1bca69003c6bad7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753748"
---
# <a name="comments-in-code-visual-basic"></a>Comentários no código (Visual Basic)
À medida que você lê os exemplos de código, você encontra geralmente o símbolo de comentário (`'`). Esse símbolo diz ao compilador do Visual Basic para ignorar o texto a seguir, ou o *comentário*. Os comentários são uma breve explicação e/ou anotações adicionadas ao código para o benefício de quem os lê.  
  
 É uma prática de programação recomendável iniciar todos os procedimentos com um breve comentário descrevendo as características do procedimento e sua funcionalidade (o que ele faz). Isso é um benefício para o programador e é vantajoso para qualquer pessoa que examinar o código. Você deve separar os detalhes de implementação (como o procedimento faz isso) dos comentários que descrevem as características funcionais. Quando você incluir detalhes da implementação na descrição, lembre-se de atualizá-los quando você atualizar a função.  
  
 Comentários podem seguir uma instrução na mesma linha ou ocupar uma linha inteira. Ambos são ilustrados no código a seguir.  
  
 [!code-vb[VbVbcnConventions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#16)]  
  
 Se seu comentário exigir mais de uma linha, use o símbolo de comentário em cada linha, como o exemplo a seguir mostra.  
  
 [!code-vb[VbVbcnConventions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#17)]  
  
## <a name="commenting-guidelines"></a>Diretrizes de comentários  
 A tabela a seguir fornece diretrizes gerais para os tipos de comentários que podem preceder uma seção de código. Esses são sugestões; Visual Basic não impõe regras para adicionar comentários. Escreva o que funciona melhor, tanto para você quanto para qualquer outra pessoa que leia seu código.  
  
|||  
|---|---|  
|Tipo de comentário|Descrição do comentário|  
|Finalidade|Descreve o que o procedimento faz (não como ele faz)|  
|Suposições|Lista cada variável externa, controle, arquivo aberto ou outro elemento acessado pelo procedimento|  
|Efeitos|Listas cada variável externa, controle ou arquivo afetado, e o efeito que ele tem (somente se não for óbvio)|  
|Entradas|Especifica a finalidade do argumento|  
|Retorna|Explica os valores retornados pelo procedimento|  
  
 Lembre-se dos seguintes pontos:  
  
- Cada declaração de variável importante deve ser precedida por um comentário sobre o uso da variável sendo declarada.  
  
- Variáveis, controles e procedimentos devem ser chamados claramente o bastante para que os comentários sejam necessários somente para detalhes de implementação complexos.  
  
- Os comentários não podem seguir uma sequência de continuação de linha na mesma linha.  
  
 Você pode adicionar ou remover símbolos de comentário de um bloco de código, selecionando uma ou mais linhas de código e escolhendo a **comentário** (![botão o comentário do Visual Basic no Visual Studio.](./media/comments-in-code/visual-basic-comment-button.gif)) e **Remover comentário**  (![Botão descomente o do Visual Basic no Visual Studio.](./media/comments-in-code/visual-basic-uncomment-button.gif)) botões a **editar** barra de ferramentas.  
  
> [!NOTE]
>  Você também pode adicionar comentários ao código precedendo o texto com a palavra-chave `REM`. No entanto, o `'` símbolo e o **comentário**/**Remover comentário** botões são mais fáceis de usar e exigem menos espaço e memória.  
  
## <a name="see-also"></a>Consulte também

- [Instintos básicos - documentando seu código com comentários XML](https://msdn.microsoft.com/magazine/dd722812.aspx)
- [Como: Criar documentação XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
- [Marcações de Comentário XML](../../../visual-basic/language-reference/xmldoc/index.md)
- [Estrutura do Programa e Convenções de Código](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [Instrução REM](../../../visual-basic/language-reference/statements/rem-statement.md)
