---
title: Как создать Часовые пояса с правилами коррекции
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], creating
- time zones [.NET Framework], and adjustment rules
- adjustment rule [.NET Framework]
ms.assetid: c52ef192-13a9-435f-8015-3b12eae8c47c
ms.openlocfilehash: 4ef3d93746c5688dc15fc7e45d9be054dcfba4c8
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132556"
---
# <a name="how-to-create-time-zones-with-adjustment-rules"></a>Как создать Часовые пояса с правилами коррекции

Точные сведения о часовом поясе, необходимые для приложения, могут отсутствовать в определенной системе по нескольким причинам:

- Часовой пояс никогда не был определен в реестре локальной системы.

- Данные о часовом поясе были изменены или удалены из реестра.

- Часовой пояс не содержит точных сведений о корректировках часового пояса для определенного исторического периода.

В таких случаях можно вызвать метод <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>, чтобы определить часовой пояс, необходимый для приложения. Перегрузки этого метода можно использовать для создания часового пояса с правилами коррекции или без них. Если часовой пояс поддерживает переход на летнее время, можно определить корректировки с помощью фиксированных или плавающих правил коррекции. (Определения этих терминов см. в подразделе «терминология часовых поясов» раздела « [Общие сведения о часовом поясе](../../../docs/standard/datetime/time-zone-overview.md)».)

> [!IMPORTANT]
> Пользовательские часовые пояса, созданные путем вызова метода <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>, не добавляются в реестр. Вместо этого доступ к ним можно получить только через ссылку на объект, возвращенную вызовом метода <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>.

В этом разделе показано, как создать часовой пояс с правилами коррекции. Сведения о создании часового пояса, не поддерживающего правила коррекции перехода на летнее время, см. [в разделе как создавать Часовые пояса без правил коррекции](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md).

### <a name="to-create-a-time-zone-with-floating-adjustment-rules"></a>Создание часового пояса с плавающими правилами коррекции

1. Для каждой корректировки (т. е. для каждого перехода на зимнее и обратное время в течение определенного интервала времени) выполните следующие действия.

    1. Определите начальное время перехода для коррекции часового пояса.

       Необходимо вызвать метод <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType> и передать ему значение <xref:System.DateTime>, которое определяет время перехода, целочисленное значение, определяющее месяц перехода, целочисленное значение, определяющее неделю, в которой происходит переход, и <xref:System.DayOfWeek> значение, определяющее день недели, в который происходит переход. Этот вызов метода создает объект <xref:System.TimeZoneInfo.TransitionTime>.

    2. Укажите время окончания перехода для коррекции часового пояса. Для этого требуется еще один вызов метода <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType>. Этот вызов метода создает экземпляр второго объекта <xref:System.TimeZoneInfo.TransitionTime>.

    3. Вызовите метод <xref:System.TimeZoneInfo.AdjustmentRule.CreateAdjustmentRule%2A> и передайте ему действующие даты начала и окончания корректировки, объект <xref:System.TimeSpan>, определяющий время перехода, и два <xref:System.TimeZoneInfo.TransitionTime> объектов, которые определяют, когда происходит переход на летнее время и обратно. Этот вызов метода создает объект <xref:System.TimeZoneInfo.AdjustmentRule>.

    4. Назначьте объект <xref:System.TimeZoneInfo.AdjustmentRule> массиву объектов <xref:System.TimeZoneInfo.AdjustmentRule>.

2. Определите отображаемое имя часового пояса. Отображаемое имя соответствует довольно стандартному формату, в котором смещение часового пояса относительно времени в формате UTC заключено в круглые скобки. за ним следует строка, определяющая часовой пояс, один или несколько городов в часовом поясе или один или несколько из КАУ. нтриес или регионы в часовом поясе.

3. Определите имя стандартного времени часового пояса. Как правило, эта строка также используется в качестве идентификатора часового пояса.

4. Определите название часового пояса (лето).

5. Если вы хотите использовать другой идентификатор, отличный от стандартного имени часового пояса, определите идентификатор часового пояса.

6. Создайте экземпляр объекта <xref:System.TimeSpan>, который определяет смещение часового пояса относительно времени в формате UTC. Часовые пояса со временем, превышающим время UTC, имеют положительное смещение. Часовые пояса со временем, предшествующим UTC, имеют отрицательное смещение.

7. Вызовите метод <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType>, чтобы создать экземпляр нового часового пояса.

## <a name="example"></a>Пример

В следующем примере определяется центральный стандартный часовой пояс для США, включающий правила коррекции для различных временных интервалов от 1918 до текущего.

[!code-csharp[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#5)]
[!code-vb[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#5)]

Часовой пояс, созданный в этом примере, имеет несколько правил коррекции. Необходимо соблюдать осторожность, чтобы гарантировать, что действующие даты начала и окончания всех правил коррекции не перекрываются с датами другого правила коррекции. При наложении возникает исключение <xref:System.InvalidTimeZoneException>.

Для правил коррекции с плавающей запятой значение 5 передается в параметр `week` метода <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A>, чтобы указать, что переход выполняется в последнюю неделю конкретного месяца.

При создании массива объектов <xref:System.TimeZoneInfo.AdjustmentRule>, которые будут использоваться в вызове метода <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType>, код может инициализировать массив до размера, который требуется для создания часового пояса. Вместо этого этот пример кода вызывает метод <xref:System.Collections.Generic.List%601.Add%2A>, чтобы добавить каждое правило коррекции к универсальной коллекции <xref:System.Collections.Generic.List%601> объектов <xref:System.TimeZoneInfo.AdjustmentRule>. Затем код вызывает метод <xref:System.Collections.Generic.List%601.CopyTo%2A>, чтобы скопировать члены этой коллекции в массив.

В примере также используется метод <xref:System.TimeZoneInfo.TransitionTime.CreateFixedDateRule%2A> для определения корректировок фиксированной даты. Это аналогично вызову метода <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A>, за исключением того, что ему требуется только время, месяц и день параметров перехода.

Пример можно протестировать с помощью следующего кода:

[!code-csharp[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#7)]
[!code-vb[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#7)]

## <a name="compiling-the-code"></a>Компиляция кода

Для этого примера требуются:

- Для импорта следующих пространств имен:

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a>См. также

- [Даты, время и часовые пояса](../../../docs/standard/datetime/index.md)
- [Общие сведения о часовых поясах](../../../docs/standard/datetime/time-zone-overview.md)
- [Практическое руководство. Создание часовых поясов без правил коррекции](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)
