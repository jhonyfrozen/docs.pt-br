---
title: Literal CDATA XML (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralCdata
helpviewer_keywords:
- CDATA literal [Visual Basic]
- XML CDATA literal [Visual Basic]
- XML literals [Visual Basic], CDATA
ms.assetid: 9eafb6a4-dd9d-4866-85e8-0654c65abc44
ms.openlocfilehash: 889ec7f93d0503edac51652dda217c6a9f654f9b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64621429"
---
# <a name="xml-cdata-literal-visual-basic"></a>Literal CDATA XML (Visual Basic)
Um valor literal que representa um <xref:System.Xml.Linq.XCData> objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<![CDATA[content]]>  
```  
  
## <a name="parts"></a>Partes  
 `<![CDATA[`  
 Necessário. Indica o início da seção CDATA do XML.  
  
 `content`  
 Necessário. Conteúdo do texto seja exibido na seção CDATA do XML.  
  
 `]]>`  
 Necessário. Indica o fim da seção.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto <xref:System.Xml.Linq.XCData>.  
  
## <a name="remarks"></a>Comentários  
 As seções CDATA XML contêm o texto não processado que deve ser incluído, mas não analisado com o XML que o contém. Uma seção CDATA XML pode conter qualquer texto. Isso inclui caracteres XML reservados. A seção CDATA XML termina com a sequência "]] >". Isso significa que os seguintes pontos:  
  
- Você não pode usar uma expressão inserida em um literal XML CDATA porque os delimitadores de expressão incorporada são conteúdo XML CDATA válido.  
  
- As seções CDATA XML não podem ser aninhadas, porque `content` não pode conter o valor "]] >".  
  
 Você pode atribuir um literal XML CDATA a uma variável ou incluí-lo em um elemento XML literal.  
  
> [!NOTE]
>  Um literal XML pode abranger várias linhas, mas não usa caracteres de continuação de linha. Isso permite que você copie o conteúdo de um documento XML e colá-lo diretamente em um programa Visual Basic.  
  
 O compilador do Visual Basic converte o literal XML CDATA em uma chamada para o <xref:System.Xml.Linq.XCData.%23ctor%2A> construtor.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria uma seção CDATA que contém o texto "pode conter literal \<XML > marcas".  
  
 [!code-vb[VbXMLSamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#23)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XCData>
- [Literal do Elemento XML](../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
- [Literais XML](../../../visual-basic/language-reference/xml-literals/index.md)
- [Criando XML no Visual Basic](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
