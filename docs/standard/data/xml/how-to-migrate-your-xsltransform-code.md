---
title: 'Como: Migrar o código de XslTransform'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 910beb2f-cfb3-4e8e-9936-f7e0c5f4064a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 67cf4636a8b947bc6ad0ce0475c53bc25cd0f678
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647920"
---
# <a name="how-to-migrate-your-xsltransform-code"></a>Como: Migrar o código de XslTransform
As novas classes XSLT foram criadas para ser muito semelhantes às classes existentes. A classe de <xref:System.Xml.Xsl.XslCompiledTransform> substitui a classe de <xref:System.Xml.Xsl.XslTransform> . As folhas de estilos são criadas usando o método de <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> . Transforms é executado usando o método <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> . Os procedimentos a seguir mostram tarefas comuns XSLT, e comparam o código usando a classe de <xref:System.Xml.Xsl.XslTransform> contra a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
### <a name="to-transform-a-file-and-output-to-a-uri"></a>Para transformar um arquivo e uma saída para o URI  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#9](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#9)]
     [!code-vb[XML_Migration#9](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#9)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
     [!code-csharp[XML_Migration#10](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#10)]
     [!code-vb[XML_Migration#10](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#10)]  
  
### <a name="to-compile-a-style-sheet-and-use-a-resolver-with-default-credentials"></a>Para criar uma folha de estilos e usar um resolvedor com credenciais padrão  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#11)]
     [!code-vb[XML_Migration#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#11)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
     [!code-csharp[XML_Migration#12](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#12)]
     [!code-vb[XML_Migration#12](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#12)]  
  
### <a name="to-use-an-xslt-parameter"></a>Para usar um parâmetro XSLT  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#13](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#13)]
     [!code-vb[XML_Migration#13](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#13)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
     [!code-csharp[XML_Migration#14](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#14)]
     [!code-vb[XML_Migration#14](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#14)]  
  
### <a name="to-enable-xslt-scripting"></a>Para habilitar scripts XSLT  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#15](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#15)]
     [!code-vb[XML_Migration#15](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#15)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
     [!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
     [!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]  
  
### <a name="to-load-the-results-into-a-dom-object"></a>Para carregar os resultados nos objetos DOM  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#19](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#19)]
     [!code-vb[XML_Migration#19](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#19)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
    > [!NOTE]
    >  A classe de <xref:System.Xml.Xsl.XslCompiledTransform> não tem um método que retorna os resultados da transformação XSLT como um objeto de <xref:System.Xml.XmlReader> . No entanto, você pode dar saída a um arquivo XML e carregar o arquivo XML em outro objeto.  
  
     [!code-csharp[XML_Migration#20](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#20)]
     [!code-vb[XML_Migration#20](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#20)]  
  
### <a name="to-stream-the-results-into-another-data-store"></a>Para passar os resultados em outro armazenamento de dados  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslTransform> .  
  
     [!code-csharp[XML_Migration#17](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#17)]
     [!code-vb[XML_Migration#17](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#17)]  
  
- Código usando a classe de <xref:System.Xml.Xsl.XslCompiledTransform> .  
  
     [!code-csharp[XML_Migration#18](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#18)]
     [!code-vb[XML_Migration#18](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#18)]  
  
## <a name="see-also"></a>Consulte também

- [Migrando da classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)
- [Usando a classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)
