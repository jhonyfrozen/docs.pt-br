---
title: Aplicando abordagens CQRS e CQS em um microsserviço DDD em eShopOnContainers
description: Arquitetura de Microsserviços .NET para aplicativos .NET em contêineres | Entenda como a CQRS é implementada no microsserviço de pedidos no eShopOnContainers.
ms.date: 10/08/2018
ms.openlocfilehash: 0380e759595e8a159e89f858a5ced4dacfa4e9b4
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875906"
---
# <a name="apply-cqrs-and-cqs-approaches-in-a-ddd-microservice-in-eshoponcontainers"></a>Aplicar abordagens CQRS e CQS em um microsserviço DDD em eShopOnContainers

O design do microsserviço de ordenação no aplicativo de referência eShopOnContainers é baseado nos princípios CQRS. No entanto, ele usa a abordagem mais simples, que está separando as consultas dos comandos e usando o mesmo banco de dados para ambas as ações.

A essência desses padrões e o ponto importante aqui é que as consultas são idempotentes: não importa quantas vezes você consulte um sistema, o estado desse sistema não será alterado. Em outras palavras, as consultas não têm efeito colateral.

Portanto, você pode usar um modelo de dados de "leituras" diferente do que o modelo de domínio “gravações” de lógica transacional, mesmo que os microsserviços de pedidos estejam usando o mesmo banco de dados. Portanto, essa é uma abordagem de CQRS simplificada.

Por outro lado, comandos, que disparam transações e atualizações de dados, alteram o estado no sistema. Com os comandos, é necessário ter cuidado ao lidar com a complexidade e com regras de negócio em constante mudança. É o local em que você deseja aplicar as técnicas DDD para ter um sistema modelado melhor.

Os padrões DDD apresentados neste guia não devem ser aplicados universalmente. Eles apresentam restrições em seu design. Essas restrições oferecem benefícios como maior qualidade com o tempo, principalmente em comandos e outro código que modifica o estado do sistema. No entanto, essas restrições adicionam complexidade com menos benefícios para ler e consultar dados.

Um desses padrões é o padrão de agregação, que examinaremos mais nas seções posteriores. Resumidamente, no padrão de agregação, você trata muitos objetos de domínio como uma única unidade como resultado de sua relação no domínio. Você nem sempre pode obter vantagens desse padrão em consultas; ele pode aumentar a complexidade da lógica de consulta. Para consultas somente leitura, você não obtém as vantagens de tratar vários objetos como uma única agregação. Você somente obtém a complexidade.

Conforme mostrado na Figura 7-2, este guia sugere usar padrões DDD apenas na área transacional/de atualizações do seu microsserviço (ou seja, como disparado por comandos). As consultas podem seguir uma abordagem mais simples e devem estar separadas de comandos, seguindo uma abordagem CQRS.

Para implementar o "lado das consultas", é possível escolher entre muitas abordagens, do seu ORM completo como EF Core, projeções do AutoMapper, procedimentos armazenados, exibições, exibições materializadas ou um micro ORM.

Neste guia e nos eShopOnContainers (principalmente o microsserviço de ordenação), escolhemos implementar consultas diretas usando um micro ORM como o [Dapper](https://github.com/StackExchange/dapper-dot-net). Isso permite a você implementar qualquer consulta com base em instruções SQL para obter o melhor desempenho, graças à estrutura leve com muito pouca sobrecarga.

Observe que, quando você usa essa abordagem, as atualizações em seu modelo que afetam como as entidades são persistentes em um Banco de Dados SQL também precisam de atualizações separadas em consultas SQL usadas pelo Dapper ou por quaisquer outras abordagens separadas (que não são do EF) para consultar.

## <a name="cqrs-and-ddd-patterns-are-not-top-level-architectures"></a>Os padrões CQRS e DDD não são arquiteturas de nível superior

É importante entender que os padrões CQRS e a maioria dos padrões DDD (como camadas DDD ou um modelo de domínio com agregações) não são estilos de arquitetura, mas apenas padrões de arquitetura. Microsserviços, SOA e EDA (arquitetura orientada a eventos) são exemplos de estilos de arquitetura. Eles descrevem um sistema de muitos componentes, como muitos microsserviços. Os padrões CQRS e DDD descrevem algo dentro de um único sistema ou componente; nesse caso, algo dentro de um microsserviço.

Diferentes BCs (Contextos limitados) empregarão diferentes padrões. Eles têm diferentes responsabilidades, e isso leva a diferentes soluções. Vale destacar que forçar o mesmo padrão em todos os lugares leva a uma falha. Não use padrões CQRS nem DDD em todos os lugares. Muitos subsistemas, BCs ou microsserviços são mais simples e podem ser implementados mais facilmente usando serviços CRUD simples ou outra abordagem.

Há apenas uma arquitetura de aplicativo: a arquitetura do sistema ou o aplicativo de ponta a ponta que você está criando (por exemplo, a arquitetura de microsserviços). No entanto, o design de cada Contexto limitado ou microsserviço dentro desse aplicativo reflete suas próprias compensações e decisões de design interno em um nível de padrões de arquitetura. Não tente aplicar os mesmos padrões de arquitetura como CQRS ou DDD em todos os lugares.

### <a name="additional-resources"></a>Recursos adicionais

- **Martin Fowler. CQRS** \
  <https://martinfowler.com/bliki/CQRS.html>

- **Greg Young. Documentos CQRS** \
  <https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf>

- **Udi Dahan. CQRS esclarecida** \
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

>[!div class="step-by-step"]
>[Anterior](apply-simplified-microservice-cqrs-ddd-patterns.md)
>[Próximo](cqrs-microservice-reads.md)
