---
title: 'Como: Capturar erros de análise (C#)'
ms.date: 07/20/2015
ms.assetid: bfb612d4-5605-48ef-8c93-915cf9d5dcfb
ms.openlocfilehash: 094485b24cdccee7898bd0344aa7c100e26bf4e9
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66487479"
---
# <a name="how-to-catch-parsing-errors-c"></a>Como: Capturar erros de análise (C#)
Este tópico mostra como detectar XML mal formado ou inválido.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] é implementado usando <xref:System.Xml.XmlReader>. Se malformado ou XML válido é passado para [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], a classe subjacente de <xref:System.Xml.XmlReader> irá acionar uma exceção. Os vários métodos que analisam XML, tais como <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>, não capturam a exceção; a exceção pode ser capturada por seu aplicativo.  
  
## <a name="example"></a>Exemplo  
 O código a seguir tenta analisar XML válido:  
  
```csharp  
try {  
    XElement contacts = XElement.Parse(  
        @"<Contacts>  
            <Contact>  
                <Name>Jim Wilson</Name>  
            </Contact>  
          </Contcts>");  
  
    Console.WriteLine(contacts);  
}  
catch (System.Xml.XmlException e)  
{  
    Console.WriteLine(e.Message);  
}  
```  
  
 Quando você executa esse código, gerencie a seguinte exceção:  
  
```  
The 'Contacts' start tag on line 1 does not match the end tag of 'Contcts'. Line 5, position 13.  
```  
  
 Para obter informações sobre as exceções que você pode esperar <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>, <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>, <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>, e métodos de <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType> lançar, consulte a documentação de <xref:System.Xml.XmlReader> .  
  