---
ms.openlocfilehash: 3f3f60f9752b9bd36d76387102c202d88b39c3ca
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65672034"
---
| .NET Standard              | [1.0]  | [1.1]  | [1.2] | [1.3] | [1.4] | [1.5]              | [1.6]              | [2.0]               |
|----------------------------|--------|--------|-------|-------|-------|--------------------|--------------------|---------------------|
| .NET Core                  | 1.0    | 1.0    | 1.0   | 1.0   | 1.0   | 1.0                | 1.0                | 2.0                 |
| .NET Framework <sup>1</sup>| 4.5    | 4.5    | 4.5.1 | 4.6   | 4.6.1 | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup>  |
| Mono                       | 4.6    | 4.6    | 4.6   | 4.6   | 4.6   | 4.6                | 4.6                | 5.4                 |
| Xamarin.iOS                | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0               | 10.0               | 10.14               |
| Xamarin.Mac                | 3.0    | 3.0    | 3.0   | 3.0   | 3.0   | 3.0                | 3.0                | 3.8                 |
| Xamarin.Android            | 7.0    | 7.0    | 7.0   | 7.0   | 7.0   | 7.0                | 7.0                | 8.0                 |
| Plataforma Universal do Windows | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0.16299         | 10.0.16299         | 10.0.16299          |
| Unity                      | 2018.1 | 2018.1 | 2018.1| 2018.1| 2018.1| 2018.1             |  2018.1            | 2018.1              |

<sup>1 As versões listadas para o .NET Framework se aplicam ao SDK do .NET Core 2.0 e versões posteriores das ferramentas. Versões antigas usavam um mapeamento diferente para o .NET Standard 1.5 e superiores. Você pode [fazer o download das ferramentas do .NET Core para Visual Studio 2015](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md) se não puder atualizar para o Visual Studio 2017.</sup>

<sup>2 As versões listadas aqui representam as regras que o NuGet usa para determinar se uma alguma biblioteca do .NET Standard é aplicável. Embora o NuGet considere o .NET Framework 4.6.1 como compatível com o .NET Standard 1.5 a 2.0, há vários problemas com o consumo de bibliotecas do .NET Standard que foram criadas para essas versões de projetos do .NET Framework 4.6.1. Para projetos do .NET Framework que precisam usar essas bibliotecas, recomendamos que você atualize o projeto para o .NET Framework 4.7.2 ou superior.</sup>

- As colunas representam versões do .NET Standard. Cada célula de cabeçalho é um link para um documento que mostra quais APIs foram adicionadas a essa versão do .NET Standard.
- As linhas representam as diferentes implementações do .NET.
- O número de versão em cada célula indica a versão *mínima* da implementação de que você precisará para direcionar essa versão do .NET Standard.
- Para obter uma tabela interativa, consulte [Versões do .NET Standard](https://dotnet.microsoft.com/platform/dotnet-standard#versions).

[1.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.0.md
[1.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.1.md
[1.2]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.2.md
[1.3]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.3.md
[1.4]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.4.md
[1.5]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.5.md
[1.6]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.6.md
[2.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md
