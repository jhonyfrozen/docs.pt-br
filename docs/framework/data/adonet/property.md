---
title: propriedade
ms.date: 03/30/2017
ms.assetid: a941c53f-fc97-42c2-8832-0fb9f1d55c06
ms.openlocfilehash: 97bb41305bd9b736fd67b51d77ee15ad9efa3f29
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645231"
---
# <a name="property"></a>propriedade
*As propriedades* são os blocos de construção fundamentais [tipos de entidade](../../../../docs/framework/data/adonet/entity-type.md) e [tipos complexos](../../../../docs/framework/data/adonet/complex-type.md). As propriedades definem a forma e as características de dados que uma instância do tipo de entidade ou a instância do tipo complexo conterão. As propriedades em um modelo conceitual são análogas as propriedades definidas em uma classe. Da mesma forma que as propriedades em uma classe definem a forma da classe e transportam informações sobre objetos, as propriedades em um modelo conceitual definem a forma de um tipo de entidade e transportam informações sobre as instâncias dos tipos de entidade.  
  
> [!NOTE]
>  As propriedades, como descrito neste tópico, são diferentes de propriedades de navegação. Para obter mais informações, consulte [propriedades de navegação](../../../../docs/framework/data/adonet/navigation-property.md).  
  
 Uma definição de propriedade contém as informações a seguir:  
  
- Um nome de propriedade. (Necessário)  
  
- Um tipo de propriedade. (Necessário)  
  
- Um conjunto de [facetas](../../../../docs/framework/data/adonet/facet.md). (Opcional)  
  
 Uma propriedade pode conter dados primitivos (como uma cadeia de caracteres, um número inteiro ou um valor booliano) ou dados estruturados (como um tipo complexo). As propriedades que são do tipo primitivo também são chamadas propriedades escalares. Para obter mais informações, consulte [modelo de dados de entidade: Tipos de dados primitivos](../../../../docs/framework/data/adonet/entity-data-model-primitive-data-types.md).  
  
> [!NOTE]
>  Um tipo complexo pode, em si, para ter as propriedades que são tipos complexos.  
  
## <a name="example"></a>Exemplo  
 O diagrama a seguir mostra um modelo conceitual com três tipos de entidade: `Book`, `Publisher`, e `Author`. Cada tipo de entidade tem várias propriedades, embora as informações de tipo para cada propriedade não é transmitida no diagrama. As propriedades que são [chaves de entidade](../../../../docs/framework/data/adonet/entity-key.md) são denotadas com (chave).  
  
 ![Modelo de exemplo com três tipos de entidade](./media/property/example-model-three-entity-types.gif)  
  
 O [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa uma linguagem específica de domínio (DSL) chamada linguagem de definição de esquema conceitual ([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)) para definir modelos conceituais. CSDL seguir define o tipo de entidade de `Book` (conforme mostrado no diagrama anterior) e indica o tipo e o nome de cada propriedade usando atributos XML. Um aspecto opcional, `Nullable`, também é definida usando um atributo XML.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 É possível que uma das propriedades mostradas no diagrama é uma propriedade do tipo complexo. Por exemplo, a propriedade de `Address` no tipo de entidade de `Publisher` pode ser uma propriedade do tipo complexo composto de várias propriedades escalares, como `StreetAddress`, `City`, `StateOrProvince`, `Country`, e `PostalCode`. A representação de CSDL de um tipo complexo seria como segue:  
  
 [!code-xml[EDM_Example_Model#ComplexTypeExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#complextypeexample)]  
  
## <a name="see-also"></a>Consulte também

- [Principais conceitos do Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)
- [Modelo de Dados de Entidade](../../../../docs/framework/data/adonet/entity-data-model.md)
