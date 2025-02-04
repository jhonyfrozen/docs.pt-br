---
title: Mapear restrições de esquema XML (XSD) keyref para restrições de DataSet
ms.date: 03/30/2017
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
ms.openlocfilehash: 4cc4cb530b7252f35469fd4bb43bf6da9c1a3e24
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64604030"
---
# <a name="map-keyref-xml-schema-xsd-constraints-to-dataset-constraints"></a>Mapear restrições de esquema XML (XSD) keyref para restrições de DataSet
O **keyref** elemento permite estabelecer links entre elementos dentro de um documento. Isso é semelhante a uma relação de chave estrangeira no banco de dados relacional. Se um esquema Especifica a **keyref** elemento, o elemento é convertido durante o processo de mapeamento de esquema para uma restrição de chave estrangeira correspondente nas colunas nas tabelas da <xref:System.Data.DataSet>. Por padrão, o **keyref** elemento também gera uma relação com o **ParentTable**, **ChildTable**, **ParentColumn**e  **ChildColumn** propriedades especificadas na relação.  
  
 A tabela a seguir descreve o **msdata** atributos que você pode especificar o **keyref** elemento.  
  
|Nome do atributo|Descrição|  
|--------------------|-----------------|  
|**msdata:ConstraintOnly**|Se **ConstraintOnly = "true"** for especificado na **keyref** elemento no esquema, uma restrição é criada, mas nenhuma relação é criada. Se esse atributo não for especificado (ou é definido como **falsos**), a restrição e a relação são criados na **conjunto de dados**.|  
|**msdata:ConstraintName**|Se o **ConstraintName** atributo for especificado, seu valor é usado como o nome da restrição. Caso contrário, o **nome** atributo da **keyref** elemento no esquema fornece o nome da restrição no **conjunto de dados**.|  
|**msdata:UpdateRule**|Se o **UpdateRule** atributo é especificado no **keyref** elemento no esquema, seu valor é atribuído para o **UpdateRule** propriedade restrição no  **Conjunto de dados**. Caso contrário, o **UpdateRule** estiver definida como **Cascade**.|  
|**msdata:DeleteRule**|Se o **DeleteRule** atributo é especificado no **keyref** elemento no esquema, seu valor é atribuído para o **DeleteRule** propriedade restrição no  **Conjunto de dados**. Caso contrário, o **DeleteRule** estiver definida como **Cascade**.|  
|**msdata:AcceptRejectRule**|Se o **AcceptRejectRule** atributo é especificado no **keyref** elemento no esquema, seu valor é atribuído para o **AcceptRejectRule** propriedade restrição no  **Conjunto de dados**. Caso contrário, o **AcceptRejectRule** estiver definida como **None**.|  
  
 O exemplo a seguir contém um esquema que especifica o **chave** e **keyref** relações entre as **OrderNumber** elemento filho do **ordem**  elemento e o **OrderNo** elemento filho do **OrderDetail** elemento.  
  
 No exemplo, o **OrderNumber** elemento filho do **OrderDetail** elemento refere-se ao **OrderNo** elemento chave filho do **ordem**elemento.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 O processo de mapeamento de esquema de linguagem XSD do esquema XML definição produz a seguinte **conjunto de dados** com duas tabelas:  
  
```  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 Além disso, o **conjunto de dados** define as seguintes restrições:  
  
- Uma restrição exclusiva na **ordem** tabela.  
  
    ```  
              Table: Order  
    Columns: OrderNumber   
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
- Uma relação entre o **ordem** e **OrderDetail** tabelas. O **Nested** estiver definida como **falso** porque os dois elementos não estão aninhados no esquema.  
  
    ```  
              ParentTable: Order  
    ParentColumns: OrderNumber   
    ChildTable: OrderDetail  
    ChildColumns: OrderNo   
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
- Uma restrição de chave estrangeira na **OrderDetail** tabela.  
  
    ```  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo   
    RelatedTable: Order  
    RelatedColumns: OrderNumber   
    ```  
  
## <a name="see-also"></a>Consulte também

- [Mapeamento de restrições de esquema XML (XSD) exclusivos para restrições de conjunto de dados](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Gerando relações de conjunto de dados do esquema XML (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET Managed Providers and DataSet Developer Center](https://go.microsoft.com/fwlink/?LinkId=217917) (Central de desenvolvedores do DataSet e de provedores gerenciados do ADO.NET)
