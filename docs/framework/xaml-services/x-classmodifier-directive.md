---
title: Diretiva x:ClassModifier
ms.date: 03/30/2017
f1_keywords:
- xClassModifier
- x:ClassModifier
- ClassModifier
helpviewer_keywords:
- XAML [XAML Services], x:ClassModifier attribute
- x:ClassModifier attribute [XAML Services]
- ClassModifier attribute in XAML [XAML Services]
ms.assetid: ef30ab78-d334-4668-917d-c9f66c3b6aea
ms.openlocfilehash: 8f90f56a595fa175d5c48a929fc19ceb81ab0d63
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64617113"
---
# <a name="xclassmodifier-directive"></a>Diretiva x:ClassModifier
Modifica o comportamento de compilação XAML quando `x:Class` também é fornecido. Especificamente, em vez de criar um parcial `class` que tem um `Public` (o padrão), do nível de acesso fornecido `x:Class` é criada com um `NotPublic` nível de acesso. Esse comportamento afeta o nível de acesso para a classe em que os assemblies gerados.  
  
## <a name="xaml-attribute-usage"></a>Uso do Atributo XAML  
  
```  
<object x:Class="namespace.classname" x:ClassModifier="NotPublic">  
   ...  
</object>  
```  
  
## <a name="xaml-values"></a>Valores XAML  
  
|||  
|-|-|  
|*NotPublic*|A cadeia de caracteres exata para passar para especificar <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> versus <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> varia, dependendo da linguagem de programação de lógica que você usar. Consulte Observações.|  
  
## <a name="dependencies"></a>Dependências  
 [X:Class](x-class-directive.md) também deve ser fornecido no mesmo elemento, e esse elemento deve ser o elemento raiz em uma página. Para obter mais informações, consulte [ \[MS-XAML\] seção 4.3.1.8](https://go.microsoft.com/fwlink/?LinkId=114525).  
  
## <a name="remarks"></a>Comentários  
 O valor de `x:ClassModifier` nos serviços de XAML do .NET Framework uso varia de acordo com a linguagem de programação. A cadeia de caracteres a ser usado depende de como cada linguagem implementa sua <xref:System.CodeDom.Compiler.CodeDomProvider> e os conversores de tipo, ele retorna para definir os significados para <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> e <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>, e se esse idioma é diferencia maiusculas de minúsculas.  
  
- Para c#, a cadeia de caracteres para passar para designar <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> é `internal`.  
  
- Para o Microsoft Visual Basic .NET, a cadeia de caracteres para passar para designar <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> é `Friend`.  
  
- Para [!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)], nenhum destino existe que dão suporte à compilação de XAML; portanto, o valor passado não está especificado.  
  
 Você também pode especificar <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> (`public` em c#, `Public` no Visual Basic); no entanto, especificando <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> raramente é feito porque <xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType> já é o comportamento padrão.  
  
 Outros valores com o código de usuário equivalente nível de acesso restrições, como `private` em c#, não são relevantes `x:ClassModifier` porque não há suporte para referências de classe aninhada em XAML e, portanto, o <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> modificador tem o mesmo efeito.  
  
## <a name="security-notes"></a>Observações sobre segurança  
 O nível de acesso, como declarado na `x:ClassModifier` ainda está sujeito à interpretação de determinadas estruturas e seus recursos. O WPF inclui recursos para carregar e instanciar tipos em que `x:ClassModifier` é `internal`, se essa classe é referenciada em um recurso WPF por meio de um pacote de referência de URI. Como consequência neste caso e potencialmente outras como ela é implementada por outras estruturas, não dependa exclusivamente nas `x:ClassModifier` para bloquear a instanciação de todos os possíveis tentativas.  
  
## <a name="see-also"></a>Consulte também

- [Diretiva x:Class](x-class-directive.md)
- [Code-behind e XAML no WPF](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [Diretiva x:FieldModifier](x-fieldmodifier-directive.md)
- [Segurança (WPF)](../wpf/security-wpf.md)
- [Tipos migrados do WPF para System.Xaml](types-migrated-from-wpf-to-system-xaml.md)
