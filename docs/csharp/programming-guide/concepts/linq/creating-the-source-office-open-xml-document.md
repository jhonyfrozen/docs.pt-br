---
title: Criando o documento do Office Open XML de origem (C#)
ms.date: 07/20/2015
ms.assetid: 653c8cdb-73be-4dc2-927f-924cfb4ed9ed
ms.openlocfilehash: 024b6c80cdedf38fd2dcee77562c0105df7bd033
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690101"
---
# <a name="creating-the-source-office-open-xml-document-c"></a>Criando o documento do Office Open XML de origem (C#)

Este tópico mostra como criar o documento do Office Open XML WordprocessingML que os outros exemplos neste tutorial uso. Se você segue essas declarações, a saída corresponderão a saída fornecida em cada exemplo.

No entanto, os exemplos neste tutorial funcionarão com qualquer documento válido de WordprocessingML.

Para criar o documento que este tutorial usa, você precisa ter o Microsoft Office 2007 ou posterior instalado ou precisa ter o Microsoft Office 2003 com o Microsoft Office Compatibility Pack para formatos de arquivo do Word, Excel e PowerPoint 2007.

## <a name="creating-the-wordprocessingml-document"></a>Criando o documento de WordprocessingML

#### <a name="to-create-the-wordprocessingml-document"></a>Para criar o documento de WordprocessingML

1. Crie um novo documento Microsoft Word.

2. Cole o seguinte texto no novo documento:

    ```
    Parsing WordprocessingML with LINQ to XML

    The following example prints to the console.

    using System;

    class Program {
        public static void Main(string[] args) {
            Console.WriteLine("Hello World");
        }
    }

    This example produces the following output:

    Hello World
    ```

3. Formatar a primeira linha com o estilo que dirige “1 ".

4. Selecione as linhas que contêm o código em c. A primeira linha começa com a palavra-chave `using` . A última linha é a chave da última. Formatar as linhas com a fonte de correio. Formatar-los com um novo estilo, e nomeie o novo estilo “código”.

5. Finalmente, selecione a linha inteira que contém a saída, e formatar-la com o estilo de `Code` .

6. Salve o documento, e denomine-o SampleDoc.docx.

    > [!NOTE]
    > Se você estiver usando o Microsoft Word 2003, selecione **Documento do Word 2007** na lista suspensa **Salvar como tipo**.
