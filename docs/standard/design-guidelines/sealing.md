---
title: Selar
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- limiting extensibility
- classes [.NET Framework], sealing
- preventing customization
- sealed classes
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
author: KrzysztofCwalina
ms.openlocfilehash: f25573c0fef29ef54dc04c5287757903429d89d4
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615208"
---
# <a name="sealing"></a>Selar
Um dos recursos das estruturas orientada a objeto é que os desenvolvedores podem estender e personalizá-los de maneiras não previstas pelos designers do framework. Isso é a potência e o perigo de design extensível. Quando você projeta sua estrutura, ele é, portanto, muito importante para projetar cuidadosamente para extensibilidade quando ele for desejado e para limitar a extensibilidade quando é perigoso.  
  
 Um mecanismo poderoso que impede a extensibilidade é lacrar. Você pode lacre a classe ou a membros individuais. Lacrar uma classe impede que os usuários herdando da classe. Lacrar um membro impede que os usuários a substituição de um membro específico.  
  
 **X DO NOT** lacrar classes sem ter uma boa razão para isso.  
  
 Lacrar uma classe, porque você não é possível pensar em um cenário de extensibilidade não é um bom motivo. Usuários da estrutura, como herdar de classes por vários motivos nonobvious, como adicionar membros de conveniência. Ver [Classes não seladas](../../../docs/standard/design-guidelines/unsealed-classes.md) para obter exemplos dos motivos nonobvious usuários desejam herdar de um tipo.  
  
 Bons motivos para lacrar uma classe incluem o seguinte:  
  
- A classe é uma classe estática. Ver [Design de classe estática](../../../docs/standard/design-guidelines/static-class.md).  
  
- A classe armazena os segredos confidenciais de segurança em membros protegidos herdados.  
  
- A classe herda muitos membros virtuais e o custo de lacrá-los individualmente seria superam os benefícios de deixar a classe sem lacre.  
  
- A classe é um atributo que requer tempo de execução muito rápida pesquisa. Atributos lacrados têm um pouco mais altos níveis de desempenho que aqueles sem lacre. ver [atributos](../../../docs/standard/design-guidelines/attributes.md).  
  
 **X DO NOT** declarar membros virtuais ou protegidos em tipos lacrados.  
  
 Por definição, tipos lacrados não podem ser herdados de. Isso significa que membros protegidos em tipos lacrados não podem ser chamados e métodos virtuais em tipos lacrados não podem ser substituídos.  
  
 **✓ CONSIDER** lacrar membros que você substituir.  
  
 Problemas que podem resultar de introduzir membros virtuais (discutidos [membros virtuais](../../../docs/standard/design-guidelines/virtual-members.md)) se aplicam a substituições Além disso, embora a um nível um pouco menor. Selando uma substituição protege você contra esses problemas a partir desse ponto na hierarquia de herança.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*  
  
 *Reimpresso com permissão da Pearson Education, Inc. de [as diretrizes de Design do Framework: As convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008 pela Addison-Wesley Professional, como parte da série de desenvolvimento do Microsoft Windows.*  
  
## <a name="see-also"></a>Consulte também

- [Diretrizes de design do Framework](../../../docs/standard/design-guidelines/index.md)
- [Designer voltado para extensibilidade](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [Classes não seladas](../../../docs/standard/design-guidelines/unsealed-classes.md)
