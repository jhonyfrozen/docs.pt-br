---
title: Trabalhar com calendários
ms.date: 04/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- globalization [.NET], calendars
- calendars, global applications
- global applications, calendars
- world-ready applications, calendars
- international applications [.NET], calendars
- culture, calendars
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed276d8026201af94a0259c4258d5c50fa67c0f3
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053238"
---
# <a name="working-with-calendars"></a>Trabalhar com calendários

Embora um valor de data e hora representem um momento, sua representação de cadeia de caracteres depende da cultura e também das convenções usadas para exibir valores de data e hora por uma cultura específica e do calendário usado por essa cultura. Este tópico explora o suporte para os calendários no .NET e discute o uso das classes de calendário ao trabalhar com valores de data.

## <a name="calendars-in-net"></a>Calendários no .NET

Todos os calendários no .NET derivam o <xref:System.Globalization.Calendar?displayProperty=nameWithType> classe, que fornece a implementação do calendário base. Uma das classes que herda da classe <xref:System.Globalization.Calendar> é a classe <xref:System.Globalization.EastAsianLunisolarCalendar>, a qual é a classe base para todos os calendários lunissolares. O .NET inclui as seguintes implementações de calendar:

* <xref:System.Globalization.ChineseLunisolarCalendar>, que representa o calendário lunissolar chinês.

* <xref:System.Globalization.GregorianCalendar>, que representa o calendário gregoriano. Esse calendário é particionado em subtipos adicionais (como árabe e francês do Oriente Médio) que são definidos pela enumeração <xref:System.Globalization.GregorianCalendarTypes?displayProperty=nameWithType>. A propriedade <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=nameWithType> especifica o subtipo do calendário gregoriano.

* <xref:System.Globalization.HebrewCalendar>, que representa o calendário hebraico.

* <xref:System.Globalization.HijriCalendar>, que representa o calendário islâmico.

* <xref:System.Globalization.JapaneseCalendar>, que representa o calendário japonês.

* <xref:System.Globalization.JapaneseLunisolarCalendar>, que representa o calendário lunissolar japonês.

* <xref:System.Globalization.JulianCalendar>, que representa o calendário juliano.

* <xref:System.Globalization.KoreanCalendar>, que representa o calendário coreano.

* <xref:System.Globalization.KoreanLunisolarCalendar>, que representa o calendário lunissolar coreano.

* <xref:System.Globalization.PersianCalendar>, que representa o calendário persa.

* <xref:System.Globalization.TaiwanCalendar>, que representa o calendário de Taiwan.

* <xref:System.Globalization.TaiwanLunisolarCalendar>, que representa o calendário lunissolar de Taiwan.

* <xref:System.Globalization.ThaiBuddhistCalendar>, que representa o calendário tailandês budista.

* <xref:System.Globalization.UmAlQuraCalendar>, que representa o calendário Um Al Qura.

Um calendário pode ser usado em uma de duas formas:

* Como o calendário usado por uma cultura específica. Cada objeto <xref:System.Globalization.CultureInfo> contém um calendário atual, que é o calendário que o objeto está usando no momento. As representações de cadeia de caracteres de todos os valores de data e hora refletem automaticamente a cultura e seu calendário atual. Normalmente, o calendário atual é o calendário padrão da cultura. <xref:System.Globalization.CultureInfo> objetos também têm calendários opcionais, que incluem os calendários adicionais que a cultura pode usar.

* Como calendário autônomo independente de uma cultura específica. Nesse caso, os métodos <xref:System.Globalization.Calendar> são usados para expressar datas como os valores que refletem o calendário.

Observe que seis classes de calendário – <xref:System.Globalization.ChineseLunisolarCalendar>, <xref:System.Globalization.JapaneseLunisolarCalendar>, <xref:System.Globalization.JulianCalendar>, <xref:System.Globalization.KoreanLunisolarCalendar>, <xref:System.Globalization.PersianCalendar> e <xref:System.Globalization.TaiwanLunisolarCalendar> – podem ser usadas apenas como calendários autônomos. Elas não são usadas por nenhuma cultura, seja como o calendário padrão ou como um calendário opcional.

## <a name="calendars-and-cultures"></a>Calendários e culturas

Cada cultura tem um calendário padrão, o qual é definido pela propriedade <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType>. A propriedade <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> retorna uma matriz de objetos <xref:System.Globalization.Calendar> que especifica todos os calendários suportados por uma cultura específica, inclusive o calendário padrão da cultura.

O exemplo a seguir ilustra as propriedades <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> e <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>. Ele cria objetos `CultureInfo` para as culturas Tailandês (Tailândia) e Japonês (Japão) e exibe seus calendários padrão e opcionais. Observe que, em ambos os casos, o calendário padrão da cultura também é incluído na coleção <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>.

[!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
[!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]

O calendário em uso no momento por um objeto <xref:System.Globalization.CultureInfo> específico é definido pela propriedade <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> da cultura. O objeto <xref:System.Globalization.DateTimeFormatInfo> de uma cultura é retornado pela propriedade <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType>. Quando uma cultura é criada, o valor padrão é o mesmo valor da propriedade <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType>. No entanto, você pode mudar o calendário atual da cultura para qualquer calendário contido na matriz retornada pela propriedade <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>. Se você tentar definir o calendário atual como um calendário que não está incluído no valor da propriedade <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>, uma <xref:System.ArgumentException> será gerada.

O exemplo a seguir altera o calendário usado pela cultura Árabe (Arábia Saudita). Ele primeiro cria uma instância de um valor <xref:System.DateTime> e o exibe usando a cultura atual – que, nesse caso, é Inglês (Estados Unidos) – e o calendário atual da cultura (que, nesse caso, é o calendário gregoriano). Em seguida, ele muda a cultura atual para Árabe (Arábia Saudita) e exibe a data usando seu calendário padrão Um Al Qura. Finalmente, ele chama o método `CalendarExists` para determinar se o calendário islâmico é suportado pela cultura Árabe (Arábia Saudita). Como o calendário é suportado, ele muda o calendário atual para Hijri e, novamente, exibe a data. Observe que, em cada caso, a data é exibida usando o calendário atual da cultura atual.

[!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
[!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]

## <a name="dates-and-calendars"></a>Datas e calendários

Com exceção dos construtores que incluem um parâmetro de tipo <xref:System.Globalization.Calendar> e permitem que os elementos de uma data (ou seja, mês, dia e ano), reflitam valores em um calendário designado, os valores de <xref:System.DateTime> e <xref:System.DateTimeOffset> sempre são baseados no calendário gregoriano. Isso significa, por exemplo, que a propriedade <xref:System.DateTime.Year%2A?displayProperty=nameWithType> retorna o ano no calendário gregoriano e que a propriedade <xref:System.DateTime.Day%2A?displayProperty=nameWithType> retorna o dia do mês no calendário gregoriano.

> [!IMPORTANT]
> É importante lembrar que há uma diferença entre um valor de data e sua representação de cadeia de caracteres. O primeiro baseia-se no calendário gregoriano; o último baseia-se no calendário atual de uma determinada cultura.

O exemplo a seguir ilustra a diferença entre as propriedades <xref:System.DateTime> e seus métodos <xref:System.Globalization.Calendar> correspondentes. No exemplo, a cultura atual é Árabe (Egito), e o calendário atual é Um Al Qura. Um valor de <xref:System.DateTime> é definido como o décimo quinto dia do sétimo mês de 2011. Está claro que esse é interpretado como uma data gregoriana, pois esses mesmos valores são retornados pelo método <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> quando as convenções da cultura invariável são usadas. A representação de cadeia de caracteres da data que é formatada usando as convenções de cultura atual é 14/08/32, que é a data equivalente no calendário Um Al Qura. Em seguida, membros de `DateTime` e `Calendar` são usados para retornar o dia, mês e o ano do valor de <xref:System.DateTime>. Em cada caso, os valores retornados pelos membros de <xref:System.DateTime> refletem os valores do calendário gregoriano, enquanto que os valores retornados pelos membros de <xref:System.Globalization.UmAlQuraCalendar> refletem os valores do calendário Um Al Qura.

[!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
[!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]

### <a name="instantiating-dates-based-on-a-calendar"></a>Criando instâncias datas com base em um calendário

Como os valores <xref:System.DateTime> e <xref:System.DateTimeOffset> baseiam-se no calendário gregoriano, você deve chamar um construtor sobrecarregado que inclua um parâmetro do tipo <xref:System.Globalization.Calendar> para criar uma instância de um valor de data se você quiser usar os valores de dia, mês ou ano em um calendário diferente. Você também pode chamar uma das sobrecargas do método <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=nameWithType> de um calendário específico para criar uma instância de um objeto <xref:System.DateTime> com base nos valores de um calendário específico.

O exemplo a seguir cria uma instância de um valor de <xref:System.DateTime> ao passar um objeto <xref:System.Globalization.HebrewCalendar> para um construtor de <xref:System.DateTime> e cria uma instância de um segundo valor <xref:System.DateTime> ao chamar o método <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>. Como os dois valores são criados com valores idênticos do calendário hebraico, a chamada ao método <xref:System.DateTime.Equals%2A?displayProperty=nameWithType> mostra que os dois valores de <xref:System.DateTime> são iguais.

[!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
[!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]

### <a name="representing-dates-in-the-current-calendar"></a>Representando datas no calendário atual

Os métodos de formatação de data e hora sempre usam o calendário atual ao converter datas em cadeias de caracteres. Isso significa que a representação de cadeia de caracteres do ano, mês e dia do mês reflete o calendário atual, e não necessariamente o calendário gregoriano.

O exemplo a seguir mostra como o calendário atual afeta a representação de cadeia de caracteres de uma data. Ele muda a cultura atual de Chinês (Tradicional, Taiwan) e cria uma instância de um valor de data. Ele então exibe o calendário e a data atuais, altera o calendário atual para <xref:System.Globalization.TaiwanCalendar> e exibe o calendário e a data atuais mais uma vez. Na primeira vez que a data é exibida, ela é representada como uma data no calendário gregoriano. Na segunda vez que a data é exibida, ela é representada como uma data no calendário de Taiwan.

[!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
[!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]

### <a name="representing-dates-in-a-non-current-calendar"></a>Representando datas em um calendário diferente do atual

Para representar uma data usando um calendário que não é o calendário atual de uma cultura específica, você deve chamar métodos do objeto <xref:System.Globalization.Calendar>. Por exemplo, os métodos <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> e <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> convertem o ano, o mês e o dia para valores que refletem um calendário específico.

> [!WARNING]
> Como alguns calendários são calendários não opcionais de qualquer cultura, representar datas nesses calendários sempre exige que você chame métodos de calendário. Isso é verdadeiro para todos os calendários que derivam das classes <xref:System.Globalization.EastAsianLunisolarCalendar>, de <xref:System.Globalization.JulianCalendar> e <xref:System.Globalization.PersianCalendar>.

O exemplo a seguir usa um objeto <xref:System.Globalization.JulianCalendar> para criar uma instância de uma data, 9 de janeiro de 1905, no calendário juliano. Quando essa data é exibida no calendário gregoriano (padrão), ela é representada como 22 de janeiro de 1905. Chamadas para métodos <xref:System.Globalization.JulianCalendar> individuais permitem que a data seja representada no calendário juliano.

[!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
[!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]

### <a name="calendars-and-date-ranges"></a>Calendários e intervalos de datas

A data mais antiga suportada por um calendário é indicada pela propriedade <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=nameWithType> desse calendário. Para a classe <xref:System.Globalization.GregorianCalendar>, essa data é 1º de janeiro de 0001. C.E. A maioria dos outros calendários no .NET dão suporte a uma data posterior. Tentar trabalhar com um valor de data e hora que antecedem a data com suporte mais antiga de um calendário gerará uma exceção <xref:System.ArgumentOutOfRangeException>.

Porém, há uma exceção importante. O valor padrão (não inicializado) de um objeto <xref:System.DateTime> e um objeto <xref:System.DateTimeOffset> é igual ao valor de <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=nameWithType>. Se você tentar formatar essa data em um calendário que não oferece suporte a 1 de janeiro de 0001. C.E. e você não fornecer um especificador de formato, o método de formatação usa o especificador de formato "s" (padrão de data/hora classificável) em vez do especificador de formato "G" (padrão de data/hora geral). Como resultado, a operação de formatação não gerará uma exceção <xref:System.ArgumentOutOfRangeException>. Em vez disso, retornará uma data sem suporte. Isso é ilustrado no exemplo a seguir, que exibe o valor de <xref:System.DateTime.MinValue?displayProperty=nameWithType> quando a cultura atual é configurada para Japonês (Japão) com o calendário japonês, e para Árabe (Egito) com o calendário Um Al Qura. Ela também define a cultura atual como Inglês (Estados Unidos) e chama o método <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType> com cada um desses objetos <xref:System.Globalization.CultureInfo>. Em cada caso, a data é exibida usando o padrão classificável de data/hora.

[!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
[!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]

## <a name="working-with-eras"></a>Trabalhando com eras

Os calendários normalmente dividem as datas em eras. No entanto, o <xref:System.Globalization.Calendar> classes no .NET não dão suporte a cada era definida por um calendário e a maioria do <xref:System.Globalization.Calendar> classes dão suporte a uma única era. Somente as classes <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar> oferecem suporte a várias eras.

> [!IMPORTANT]
>  A era Reiwa, uma nova era na <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar>, começa em 1 de maio de 2019. Essa alteração afeta todos os aplicativos que usam esses calendários. Consulte os seguintes artigos para obter mais informações:
> - [Tratamento de uma nova era no calendário japonês no .NET](https://devblogs.microsoft.com/dotnet/handling-a-new-era-in-the-japanese-calendar-in-net/), que documenta os recursos adicionados ao .NET para dar suporte a calendários com eras vários e discute as práticas recomendadas para usar ao lidar com era vários calendários.
> - [Preparar seu aplicativo para que a alteração era japonesa](/windows/uwp/design/globalizing/japanese-era-change), que fornece informações sobre como testar seus aplicativos em Windows para garantir que a preparação para a alteração era.
> - [Resumo da nova Era de japonês atualiza para o .NET Framework](https://support.microsoft.com/help/4477957/new-japanese-era-updates-for-net-framework), que lista as atualizações do .NET Framework para versões individuais do Windows que estão relacionadas a nova era de calendário japonês, notas de novos recursos do .NET Framework para suporte a várias eras e inclui Você deve procurar em testar seus aplicativos.

Uma época na maioria dos calendários denota um período de tempo extremamente longo. No calendário gregoriano, por exemplo, a era atual abrange mais de dois milênios. Para o <xref:System.Globalization.JapaneseCalendar> e o <xref:System.Globalization.JapaneseLunisolarCalendar>, os dois calendários que dão suporte a várias eras, isso não for o caso. Uma era corresponde ao período de Reino do Imperador um. Suporte a várias eras, especialmente quando o limite superior de era atual é desconhecido, apresenta desafios. 

### <a name="eras-and-era-names"></a>Eras e nomes de eras

No .NET, inteiros que representam as eras com suporte por uma implementação específica do calendário são armazenados em ordem inversa no <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> matriz. A era atual (que é a era com o intervalo de tempo mais recente) está no índice zero e <xref:System.Globalization.Calendar> classes que oferecem suporte a várias eras, cada índice sucessivo reflete a era anterior. A propriedade estática <xref:System.Globalization.Calendar.CurrentEra?displayProperty=nameWithType> define o índice de era atual na matriz <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> ; ela é uma constante cujo valor é sempre zero. As classes <xref:System.Globalization.Calendar> individuais também incluem os campos estáticos que retornam o valor da era atual. Elas são listadas na tabela a seguir.

| Classe do calendário                                        | Campo de era atual                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------------- |
| <xref:System.Globalization.ChineseLunisolarCalendar>  | <xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>   |
| <xref:System.Globalization.GregorianCalendar>         | <xref:System.Globalization.GregorianCalendar.ADEra>               |
| <xref:System.Globalization.HebrewCalendar>            | <xref:System.Globalization.HebrewCalendar.HebrewEra>              |
| <xref:System.Globalization.HijriCalendar>             | <xref:System.Globalization.HijriCalendar.HijriEra>                |
| <xref:System.Globalization.JapaneseLunisolarCalendar> | <xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra> |
| <xref:System.Globalization.JulianCalendar>            | <xref:System.Globalization.JulianCalendar.JulianEra>              |
| <xref:System.Globalization.KoreanCalendar>            | <xref:System.Globalization.KoreanCalendar.KoreanEra>              |
| <xref:System.Globalization.KoreanLunisolarCalendar>   | <xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>  |
| <xref:System.Globalization.PersianCalendar>           | <xref:System.Globalization.PersianCalendar.PersianEra>            |
| <xref:System.Globalization.ThaiBuddhistCalendar>      | <xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>  |
| <xref:System.Globalization.UmAlQuraCalendar>          | <xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>          |

O nome que corresponde a um número de era específico não pode ser recuperado com a passagem do número da era para o método <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> ou <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=nameWithType>. O exemplo a seguir chama esses métodos para recuperar informações sobre o suporte a eras na classe <xref:System.Globalization.GregorianCalendar>. Ele exibe a data do calendário gregoriano que corresponde a 1º de janeiro do ano segundo da era atual, bem como a data do calendário gregoriano que corresponde a 1º de janeiro do ano segundo da era cada calendário japonês com suporte.

[!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs)]
[!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb)]

Além disso, a cadeia de caracteres de formato de data e hora personalizado "g" inclui o nome da era na representação de cadeia de caracteres de uma data e hora. Para obter mais informações, consulte [cadeias de caracteres de formato de data e hora personalizado](../../../docs/standard/base-types/custom-date-and-time-format-strings.md).

### <a name="instantiating-a-date-with-an-era"></a>Criando uma instância de uma data com uma época

Para os dois <xref:System.Globalization.Calendar> classes que oferecem suporte a várias eras, uma data que consiste em um determinado ano, mês e dia do valor de mês pode ser ambígua. Por exemplo, todas as eras com suporte a <xref:System.Globalization.JapaneseCalendar> ter anos cujo número é 1. Normalmente, se uma era não é especificada, os métodos de data e hora e calendário assumem que os valores pertencem à era atual. Isso é verdadeiro para o <xref:System.DateTime.%23ctor%2A> e <xref:System.DateTimeOffset.%23ctor%2A> construtores que incluem parâmetros de tipo <xref:System.Globalization.Calendar>, bem como o [JapaneseCalendar.ToDateTime](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) e [JapaneseLunisolarCalendar.ToDateTime ](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) métodos. O exemplo a seguir cria uma instância de uma data que representa 1 de janeiro do segundo ano de uma época não especificado. Se você executar o exemplo de quando a era Reiwa é era atual, a data é interpretada como o segundo ano da era Reiwa. Era, 令和, precede o ano na cadeia de caracteres retornada pelo <xref:System.DateTime.ToString(System.String,System.IFormatProvider)?displayProperty=nameWithType> método e corresponde a 1º de janeiro de 2020 no calendário gregoriano. (A era Reiwa começa no ano de 2019 do calendário gregoriano).

[!code-csharp[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/cs/program.cs)]
[!code-vb[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/vb/program.vb)]

No entanto, se a era for alterado, a intenção desse código se torna ambígua. A data serve para representar um segundo ano de era atual ou ele serve para representar o segundo ano da era Heisei? Há duas maneiras de evitar essa ambiguidade:

- O valor de data e hora usando o padrão de criar uma instância <xref:System.Globalization.GregorianCalendar> classe. Em seguida, você pode usar o calendário japonês ou o calendário Lunissolar japonês para a representação de cadeia de caracteres de datas, como mostra o exemplo a seguir.

   [!code-csharp[Insantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/cs/program.cs)]
   [!code-vb[Instantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/vb/program.vb)]

- Chame um método de data e hora que especifica explicitamente uma era. Isso inclui os seguintes métodos:

   - O <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)> método da <xref:System.Globalization.JapaneseCalendar> ou <xref:System.Globalization.JapaneseLunisolarCalendar> classe.

   - Um <xref:System.DateTime> ou <xref:System.DateTimeOffset> tais como o método, de análise <xref:System.DateTime.Parse%2A>, <xref:System.DateTime.TryParse%2A>, <xref:System.DateTime.ParseExact%2A>, ou <xref:System.DateTime.TryParseExact%2A>, que inclui a cadeia de caracteres a ser analisada e, opcionalmente, um <xref:System.Globalization.DateTimeStyles> argumento se a cultura atual é Japão japonês (" ja-JP") e o calendário da cultura é o <xref:System.Globalization.JapaneseCalendar>. A cadeia de caracteres a ser analisada deve incluir a era.

   - Um <xref:System.DateTime> ou <xref:System.DateTimeOffset> análise do método inclui um `provider` parâmetro do tipo <xref:System.IFormatProvider>. `provider` deve ser um <xref:System.Globalization.CultureInfo> objeto que representa a cultura de japonês-Japão ("ja-JP") cujo calendário atual é <xref:System.Globalization.JapaneseCalendar> ou um <xref:System.Globalization.DateTimeFormatInfo> do objeto cuja <xref:System.Globalization.DateTimeFormatInfo.Calendar> é de propriedade <xref:System.Globalization.JapaneseCalendar>. A cadeia de caracteres a ser analisada deve incluir a era.

   O exemplo a seguir usa três desses métodos para instanciar uma data e hora na era Meiji, que iniciou em 8 de setembro de 1868 e foi encerrado em 29 de julho de 1912. 

   [!code-csharp[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/cs/program.cs)]
   [!code-vb[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/vb/program.vb)]

> [!TIP]
> Quando estiver trabalhando com calendários que dão suporte a várias eras, *sempre* use a data no calendário gregoriano para instanciar uma data, ou especifique a era quando você instancia uma data e hora com base no calendário.

Especificar uma era para o <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)> método, você fornece o índice da era do calendário <xref:System.Globalization.Calendar.Eras> propriedade. Para os calendários cujos eras estão sujeitos a alterações, porém, esses índices não são valores de constante; a era atual está no índice 0 e a era mais antiga está no índice `Eras.Length - 1`. Quando uma nova era é adicionada a um calendário, os índices das eras anteriores aumentam em um. Você pode fornecer o índice de era apropriado da seguinte maneira:

- Para datas na era atual, use sempre o calendário <xref:System.Globalization.Calendar.CurrentEra> propriedade.

- Para datas em uma era especificada, use o <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> método para recuperar o índice que corresponde a um nome da era especificada. Isso requer que o <xref:System.Globalization.JapaneseCalendar> ser o calendário atual do <xref:System.Globalization.CultureInfo> objeto que representa a cultura ja-JP.  (Essa técnica funciona para o <xref:System.Globalization.JapaneseLunisolarCalendar> Além disso, já que ele suporta as mesmas eras como o <xref:System.Globalization.JapaneseCalendar>.) O exemplo anterior ilustra essa abordagem.

### <a name="calendars-eras-and-date-ranges-relaxed-range-checks"></a>Calendários, eras e intervalos de datas: Verificações de intervalo reduzida

Muito parecida com a calendários individuais têm suporte para intervalos de datas, eras na <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar> classes também têm suporte para intervalos. .NET usado anteriormente, era estrito intervalo verifica para garantir que uma data de era específico foi dentro do intervalo de nessa época. Ou seja, se uma data está fora do intervalo da era especificada, o método gerará uma <xref:System.ArgumentOutOfRangeException>. Atualmente, .NET usa a verificação de intervalos reduzida por padrão. Atualizações para todas as versões do .NET introduziram era reduzida de intervalo verificações; a tentativa de instanciar uma data de era específico que está fora do intervalo da era especificada "estoura" para a era a seguir, e nenhuma exceção é lançada.

O exemplo a seguir tenta criar uma instância de uma data no ano 65th da era Imperador Showa, que iniciou em 25 de dezembro de 1926 e terminou em 7 de janeiro de 1989. Essa data corresponde ao dia 9 de janeiro de 1990, que está fora do intervalo da era Imperador Showa no <xref:System.Globalization.JapaneseCalendar>. Como ilustra a saída do exemplo, a data exibida pelo exemplo é 9 de janeiro de 1990, no segundo ano da era Heisei do calendário.

   [!code-csharp[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/cs/program.cs)]
   [!code-vb[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/vb/program.vb)]

Se as verificações de intervalo reduzida indesejáveis, você pode restaurar verificações de intervalo estrita de várias maneiras, dependendo da versão do .NET que está executando seu aplicativo:

- **.NET core:** Você pode adicionar o seguinte para o *. netcore.runtime.json* arquivo de configuração:

   ```json
   "runtimeOptions": {
      "configProperties": {
         "Switch.System.Globalization.EnforceJapaneseEraYearRanges": true
      } 
   }
   ```

- **.NET framework 4.6 ou posterior:** Você pode definir a opção de AppContext a seguir:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <runtime>
       <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceJapaneseEraYearRanges=true" />
     </runtime>
   </configuration>
   ```

- **.NET framework 4.5.2 ou anterior:** Você pode definir o valor do registro:

   |  |  |
   |--|--|
   |Chave | HKEY_LOCAL_MACHINE\Software\Microsoft.NETFramework\AppContext |
   |Nome | Switch.System.Globalization.EnforceJapaneseEraYearRanges |
   |Tipo | REG_SZ |
   |Valor | 1 |

Com verificações de intervalo estrito habilitadas, o exemplo anterior gera um <xref:System.ArgumentOutOfRangeException> e exibe a seguinte saída:

```console
Unhandled Exception: System.ArgumentOutOfRangeException: Valid values are between 1 and 64, inclusive.
Parameter name: year
   at System.Globalization.GregorianCalendarHelper.GetYearOffset(Int32 year, Int32 era, Boolean throwOnError)
   at System.Globalization.GregorianCalendarHelper.ToDateTime(Int32 year, Int32 month, Int32 day, Int32 hour, Int32 minute, Int32 second, Int32 millisecond, Int32 era)
   at Example.Main()
```

### <a name="representing-dates-in-calendars-with-multiple-eras"></a>Representando datas em calendários com eras vários

Se um objeto <xref:System.Globalization.Calendar> oferece suporte a eras e é o calendário atual de um objeto <xref:System.Globalization.CultureInfo>, a era está incluída na representação de cadeia de caracteres de um valor de data e hora para os padrões de data e hora completa, data completa e data abreviada. O exemplo a seguir exibe esses padrões de data quando a cultura atual é Japão (japanese) e o calendário atual é o calendário japonês.

[!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
[!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]

> [!WARNING]
> O <xref:System.Globalization.JapaneseCalendar> classe é a única classe de calendário no .NET que ambos os oferece suporte a datas em mais de uma era e que pode ser o calendário atual de um <xref:System.Globalization.CultureInfo> objeto – especificamente, de um <xref:System.Globalization.CultureInfo> objeto que representa a cultura japonês (Japão).

Para todos os calendários, o especificador de formato personalizado “g” inclui a era na cadeia de caracteres de resultado. O exemplo a seguir usa a cadeia de caracteres de formato personalizado "MM-dd-aaaa g" para incluir a era na cadeia de caracteres de resultado quando o calendário atual é o calendário gregoriano.

[!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
[!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]

Em casos em que a representação de cadeia de caracteres de uma data é expressa em um calendário que não é o calendário atual, a classe <xref:System.Globalization.Calendar> inclui um método <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=nameWithType> que pode ser usado junto com <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> e os métodos <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> para indicar inequivocamente uma data e a era à qual ela pertence. O exemplo a seguir usa a classe <xref:System.Globalization.JapaneseLunisolarCalendar> para fornecer uma ilustração. No entanto, observe que incluir um nome ou abreviação significativa em vez de um inteiro para a era na cadeia de caracteres de resultado exige que você crie uma instância de um objeto <xref:System.Globalization.DateTimeFormatInfo> e faça de <xref:System.Globalization.JapaneseCalendar> o calendário atual. (O calendário <xref:System.Globalization.JapaneseLunisolarCalendar> não pode ser o calendário atual de qualquer cultura, mas, nesse caso, os dois calendários compartilham as mesmas eras.)

[!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
[!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]

O primeiro ano de uma época nos calendários japonês, é chamado de Gannen (元年). Por exemplo, em vez de 1 Heisei do calendário, o primeiro ano da era Heisei do calendário pode ser descrito como Heisei Gannen. .NET adota essa convenção na formatação de operações para datas e horários formatada com o seguinte padrão ou personalizada formato de data e hora em cadeias de caracteres quando eles são usados com um <xref:System.Globalization.CultureInfo> objeto que representa a cultura de japonês-Japão ("ja-JP") com o <xref:System.Globalization.JapaneseCalendar> classe:

- [O padrão de data por extenso](../base-types/standard-date-and-time-format-strings.md#LongDate), indicado pela "D" data e hora de cadeia de caracteres de formato padrão.
- [A hora longa de data completa padrão](../base-types/standard-date-and-time-format-strings.md#FullDateLongTime), indicado pela "F" data e hora de cadeia de caracteres de formato padrão.
- [O padrão de curto período de tempo de data completa](../base-types/standard-date-and-time-format-strings.md#FullDateShortTime), indicado pela "f" data e hora de cadeia de caracteres de formato padrão.
- [O padrão de ano/mês](../base-types/standard-date-and-time-format-strings.md#YearMonth), indicado pelo Y "ou"y"padrão de data e hora de cadeia de caracteres de formato.
- [O "ggy '年'" ou "ggy年" [cadeia de caracteres de formato de data e hora personalizado](../base-types/custom-date-and-time-format-strings.md).

Por exemplo, o exemplo a seguir exibe uma data no primeiro ano da era Heisei do calendário no <xref:System.Globalization.JapaneseCalendar> .

   [!code-csharp[gannen](~/samples/snippets/standard/datetime/calendars/gannen/cs/program.cs)]
   [!code-vb[gannen](~/samples/snippets/standard/datetime/calendars/gannen/vb/gannen-fmt.vb)]

Se esse comportamento for indesejável em operações de formatação, você pode restaurar o comportamento anterior, o que sempre representa o primeiro ano de uma época como "1" em vez de "Gannen", fazendo o seguinte, dependendo da versão do .NET:

- **.NET core:** Você pode adicionar o seguinte para o *. netcore.runtime.json* arquivo de configuração:

   ```json
   "runtimeOptions": {
      "configProperties": {
         "Switch.System.Globalization.FormatJapaneseFirstYearAsANumber": true
      } 
   }
   ```

- **.NET framework 4.6 ou posterior:** Você pode definir a opção de AppContext a seguir:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <runtime>
       <AppContextSwitchOverrides value="Switch.System.Globalization.FormatJapaneseFirstYearAsANumber=true" />
     </runtime>
   </configuration>
   ```

- **.NET framework 4.5.2 ou anterior:** Você pode definir o valor do registro:

   |  |  |
   |--|--|
   |Chave | HKEY_LOCAL_MACHINE\Software\Microsoft.NETFramework\AppContext |
   |Nome | Switch.System.Globalization.FormatJapaneseFirstYearAsANumber |
   |Tipo | REG_SZ |
   |Valor | 1 |

Com o suporte de gannen em operações desabilitadas de formatação, o exemplo anterior exibe a seguinte saída:

```console
Japanese calendar date: 平成1年8月18日 (Gregorian: Friday, August 18, 1989)
```

.NET também foi atualizado para que a data e hora em operações de análise de cadeias de caracteres que contêm o ano representado como "1" ou Gannen dão suporte. Embora você não deve precisar fazer isso, você pode restaurar o comportamento anterior ao reconhece apenas "1" como o primeiro ano de uma época. Você pode fazer isso da seguinte maneira, dependendo da versão do .NET:

- **.NET core:** Você pode adicionar o seguinte para o *. netcore.runtime.json* arquivo de configuração:

   ```json
   "runtimeOptions": {
      "configProperties": {
         "Switch.System.Globalization.EnforceLegacyJapaneseDateParsing": true
      } 
   }
   ```

- **.NET framework 4.6 ou posterior:** Você pode definir a opção de AppContext a seguir:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <runtime>
       <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceLegacyJapaneseDateParsing=true" />
     </runtime>
   </configuration>
   ```

- **.NET framework 4.5.2 ou anterior:** Você pode definir o valor do registro:

   |  |  |
   |--|--|  
   |Chave | HKEY_LOCAL_MACHINE\Software\Microsoft.NETFramework\AppContext |
   |Nome | Switch.System.Globalization.EnforceLegacyJapaneseDateParsing |
   |Tipo | REG_SZ |
   |Valor | 1 | 

## <a name="see-also"></a>Consulte também

- [Como: Exibir datas em calendários não gregorianos](../../../docs/standard/base-types/how-to-display-dates-in-non-gregorian-calendars.md)
- [Exemplo: Utilitário de intervalo de semana de calendário](https://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)
- [Classe de calendário](xref:System.Globalization.Calendar)
