---
title: função declarada por modelo
ms.date: 03/30/2017
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
ms.openlocfilehash: a0bea36693122c77d9c1abdf4484ee8e68627a0c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645868"
---
# <a name="model-declared-function"></a>função declarada por modelo
Um *função declarada modelo* é uma função que é declarada em um modelo conceitual, mas não está definida no modelo conceitual. A função pode ser definida no ambiente de hospedagem ou de armazenamento. Por exemplo, uma função o declarada pode ser mapeada para uma função que está definida em uma base de dados, bem expõe a funcionalidade do lado do modelo conceitual.  
  
 A declaração de uma função declarada modelo contém as informações a seguir:  
  
- O nome da função. (Necessário)  
  
- O tipo do valor de retorno. (Opcional)  
  
    > [!NOTE]
    >  Se nenhum valor de retorno for especificado, o tipo de retorno é vago.  
  
- Informações de parâmetro, incluindo o nome do parâmetro e o tipo. (Opcional)  
  
## <a name="example"></a>Exemplo  
 O [ADO.NET Entity Framework](./ef/index.md) usa uma linguagem específica de domínio (DSL) chamada linguagem de definição de esquema conceitual ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) para definir modelos conceituais. Em CSDL, uma implementação de uma função declarada por modelo é uma importação de função (usando o [elemento FunctionImport](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#functionimport-element-csdl)). CSDL seguir define um contêiner de entidade com uma definição de importação de função. Observe que o tipo de retorno da função é vago desde que nenhum tipo de retorno é especificado.  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## <a name="see-also"></a>Consulte também

- [Principais conceitos do Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model.md)
