---
title: 'Como: Popular uma árvore XML com um XmlWriter (LINQ to XML) (C#)'
ms.date: 07/20/2015
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
ms.openlocfilehash: 6e121b246729b2b671d0d07dfed6a31602bfe565
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66485222"
---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>Como: Popular uma árvore XML com um XmlWriter (LINQ to XML) (C#)
Uma maneira de preencher uma árvore XML é usar <xref:System.Xml.Linq.XContainer.CreateWriter%2A> para criar um <xref:System.Xml.XmlWriter> e escrever no <xref:System.Xml.XmlWriter>. A árvore XML é preenchida com todos os nós que são escritos no <xref:System.Xml.XmlWriter>.  
  
 Você normalmente usa este método quando usa [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] com outra classe que espera escrever em um <xref:System.Xml.XmlWriter>, por exemplo, <xref:System.Xml.Xsl.XslCompiledTransform>.  
  
## <a name="example"></a>Exemplo  
 Um uso possível para <xref:System.Xml.Linq.XContainer.CreateWriter%2A> é ao chamar uma transformação XSLT. Este exemplo cria uma árvore XML, cria <xref:System.Xml.XmlReader> da árvore XML, cria um novo documento e, em seguida, cria <xref:System.Xml.XmlWriter> para gravar no novo documento. Ele então chama a transformação XSLT, passando no <xref:System.Xml.XmlReader> e no <xref:System.Xml.XmlWriter>. Depois que a transformação for concluída com êxito, a nova árvore XML será preenchida com os resultados da transformação.  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
    <xsl:template match='/Parent'>  
        <Root>  
            <C1>  
            <xsl:value-of select='Child1'/>  
            </C1>  
            <C2>  
            <xsl:value-of select='Child2'/>  
            </C2>  
        </Root>  
    </xsl:template>  
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter())  
{  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 Este exemplo gera a seguinte saída:  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A>
- <xref:System.Xml.XmlWriter>
- <xref:System.Xml.Xsl.XslCompiledTransform>
- [Criando árvores XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md)
