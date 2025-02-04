---
title: XmlDocument inseriu a XslTransform
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 97115892-410a-4657-ab47-1e14dfba73f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c80cb772f280c064e420e83a99b5f7ce41fe05e3
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170823"
---
# <a name="xmldocument-input-to-xsltransform"></a>XmlDocument inseriu a XslTransform
A classe de <xref:System.Xml.XmlDocument> fornece recursos de edição de um documento XML. Se o XML precisa ser editado ou alterado antes de ser enviado para o método de <xref:System.Xml.Xsl.XslTransform.Transform%2A> , carregar XML em <xref:System.Xml.XmlDocument>, editá-lo, e enviá-lo na <xref:System.Xml.Xsl.XslTransform>.  
  
> [!NOTE]
>  A classe <xref:System.Xml.Xsl.XslTransform> está obsoleta no .NET Framework 2.0. Você pode executar a linguagem XSL Transformations (XSLT) usando a classe <xref:System.Xml.Xsl.XslCompiledTransform>. Confira [Usar a classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrar da classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md) para saber mais.  
  
 <xref:System.Xml.XmlDocument> implementa a interface de <xref:System.Xml.XPath.IXPathNavigable> , o documento pode ser passado para o método de <xref:System.Xml.Xsl.XslTransform.Transform%2A> após editar.  
  
 Devido ao recurso de <xref:System.Xml.XmlDocument>, use a classe de <xref:System.Xml.XmlDocument> como entrada uma transformação é mais lento do que usar <xref:System.Xml.XPath.XPathDocument> para o idioma extensível de folha de estilos para transformações de transformações (XSLT), porque <xref:System.Xml.XPath.XPathDocument> é otimizado para consultas de idioma do caminho de XML (XPath) devido ao armazenamento interno.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como <xref:System.Xml.XmlDocument> pode ser fornecido para <xref:System.Xml.Xsl.XslTransform>, com a saída enviadas a <xref:System.Xml.XmlReader>.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.Load("books.xml")  
Dim trans As XslTransform = new XslTransform()  
trans.Load("book.xsl")  
Dim rdr As XmlReader = trans.Transform(doc, Nothing, Nothing)  
while (rdr.Read())  
end while  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
XslTransform trans = new XslTransform();  
trans.Load("book.xsl");  
XmlReader rdr = trans.Transform(doc, null, null);  
while (rdr.Read()) {}  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.XmlDocument>
- [Transformações XSLT com a classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)
- [A classe XslTransform implementa o processador XSLT](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
- [XPathNavigator em transformações](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)
- [XPathNodeIterator em transformações](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)
- [Entrada de XPathDocument para XslTransform](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)
- [Entrada de XmlDataDocument para XslTransform](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)
