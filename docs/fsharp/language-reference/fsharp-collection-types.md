---
title: Типы коллекций
description: Сведения о F# типах коллекций и их отличиях от типов коллекций в .NET Framework.
ms.date: 05/16/2016
ms.openlocfilehash: e5735efbffb1010f3886f3b32800a61e2d3b0d36
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75344573"
---
# <a name="f-collection-types"></a>Типы коллекций F#

Изучив этот раздел, можно определить, какой F# тип коллекции лучше подходит для конкретной потребности. Эти типы коллекций отличаются от типов коллекций в .NET Framework, например, в пространстве имен `System.Collections.Generic`, в том, что типы F# коллекций спроектированы с точки зрения функционального программирования, а не объектно-ориентированной перспективы. В частности, только коллекция массивов содержит изменяемые элементы. Таким образом, при изменении коллекции создается экземпляр измененной коллекции вместо изменения исходной коллекции.

Типы коллекций также отличаются в типе структуры данных, в которой хранятся объекты. Структуры данных, такие как хэш-таблицы, связанные списки и массивы, имеют различные характеристики производительности и разные наборы доступных операций.

## <a name="f-collection-types"></a>Типы коллекций F#

В следующей таблице показаны F# типы коллекций.

|Тип|Описание|Связанные ссылки|
|----|-----------|-------------|
|[List](https://msdn.microsoft.com/library/c627b668-477b-4409-91ed-06d7f1b3e4a7)|Упорядоченная, неизменяемая серия элементов одного и того же типа. Реализуется как связанный список.|[Списки](lists.md)<br /><br />[Модуль List](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)|
|[массив](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1).|Изменяемая коллекция последовательных элементов данных с фиксированным размером, начинающимся с нуля, которые имеют одинаковый тип.|[Массивы](arrays.md)<br /><br />[Модуль Array](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1)<br /><br />[Модуль Array2D](https://msdn.microsoft.com/library/ae1a9746-7817-4430-bcdb-a79c2411bbd3)<br /><br />[Модуль Array3D](https://msdn.microsoft.com/library/c8355e2d-add8-48a4-8aa6-1c57ae74c560)|
|[порядк](https://msdn.microsoft.com/library/2f0c87c6-8a0d-4d33-92a6-10d1d037ce75)|Логический ряд элементов одного типа. Последовательности особенно полезны при наличии большой упорядоченной коллекции данных, но не обязательно должны использовать все элементы. Отдельные элементы последовательности вычисляются только по мере необходимости, поэтому последовательность может выполняться лучше, чем список, если не все элементы используются. Последовательности представлены типом `seq<'T>`, который является псевдонимом для `IEnumerable<T>`. Таким образом, в качестве последовательности можно использовать любой тип .NET Framework, реализующий `System.Collections.Generic.IEnumerable<'T>`.|[Последовательности](sequences.md)<br /><br />[Seq, модуль](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684)|
|[Карта](https://msdn.microsoft.com/library/975316ea-55e3-4987-9994-90897ad45664)|Неизменяемый словарь элементов. Доступ к элементам осуществляется по ключу.|[Модуль Map](https://msdn.microsoft.com/library/bfe61ead-f16c-416f-af98-56dbcbe23e4f)|
|[Set](https://msdn.microsoft.com/library/50cebdce-0cd7-4c5c-8ebc-f3a9e90b38d8)|Неизменяемый набор, основанный на двоичных деревьях, где сравнение F# является структурной функцией сравнения, которая потенциально использует реализации интерфейса `System.IComparable` в значениях ключа.|[Задать модуль](https://msdn.microsoft.com/library/61efa732-d55d-4c32-993f-628e2f98e6a0)|

### <a name="table-of-functions"></a>Таблица функций

В этом разделе сравниваются функции, доступные в F# типах коллекций. Определенная сложность функции определяется, где N — это размер первой коллекции, а M — размер второй коллекции, если таковой имеется. Тире (-) указывает, что эта функция недоступна в коллекции. Так как последовательности вычисляются отложенно, функция, например seq. DISTINCT, может быть O (1), поскольку она возвращает значение немедленно, хотя она по-прежнему влияет на производительность последовательности при перечислении.

|Функция|Массив|Список|Sequence|Карта|Задать|Описание|
|--------|-----|----|--------|---|---|-----------|
|append|O (M)|O (N)|O (N)|-|-|Возвращает новую коллекцию, содержащую элементы первой коллекции, за которыми следуют элементы второй коллекции.|
|добавление|-|-|-|O (log N)|O (log N)|Возвращает новую коллекцию с добавленным элементом.|
|Среднее значение|O (N)|O (N)|O (N)|-|-|Возвращает среднее значение элементов в коллекции.|
|averageBy|O (N)|O (N)|O (N)|-|-|Возвращает среднее значение для результатов предоставленной функции, примененной к каждому элементу.|
|блит|O (N)|-|-|-|-|Копирует раздел массива.|
|кэш|-|-|O (N)|-|-|Выполняет вычисление и сохраняет элементы последовательности.|
|приведение|-|-|O (N)|-|-|Преобразует элементы в указанный тип.|
|choose|O (N)|O (N)|O (N)|-|-|Применяет заданную функцию `f` к каждому элементу `x` списка. Возвращает список, содержащий результаты для каждого элемента, в котором функция возвращает `Some(f(x))`.|
|сбор|O (N)|O (N)|O (N)|-|-|Применяет заданную функцию к каждому элементу коллекции, сцепляет все результаты и возвращает объединенный список.|
|компаревис|-|-|O (N)|-|-|Сравнивает две последовательности, используя заданную функцию сравнения, элемент по элементу.|
|concat|O (N)|O (N)|O (N)|-|-|Объединяет заданное перечисление перечисления в виде одного объединенного перечисления.|
|содержит|-|-|-|-|O (log N)|Возвращает значение true, если набор содержит указанный элемент.|
|containsKey|-|-|-|O (log N)|-|Проверяет, находится ли элемент в домене схемы.|
|количество|-|-|-|-|O (N)|Возвращает количество элементов в наборе.|
|каунтби|-|-|O (N)|-|-|Применяет функцию создания ключа к каждому элементу последовательности и возвращает последовательность, которая получает уникальные ключи и их количество в исходной последовательности.|
|копирование|O (N)|-|O (N)|-|-|Копирует коллекцию.|
|создание|O (N)|-|-|-|-|Создает массив целых элементов, которые изначально имеют заданное значение.|
|отложить|-|-|O(1)|-|-|Возвращает последовательность, построенную из заданной отложенной спецификации последовательности.|
|различие|-|-|-|-|O (M &#42; log N)|Возвращает новый набор с элементами второго набора, удаленных из первого набора.|
|distinct|||O (1)&#42;|||Возвращает последовательность, которая не содержит повторяющихся записей в соответствии с универсальным хэшем и сравнениями на равенство для записей. Если элемент встречается в последовательности несколько раз, последующие вхождения отбрасываются.|
|дистинктби|||O (1)&#42;|||Возвращает последовательность, которая не содержит повторяющихся записей в соответствии с универсальным хэшем и сравнениями на равенство по ключам, возвращаемым данной функцией формирования ключа. Если элемент встречается в последовательности несколько раз, последующие вхождения отбрасываются.|
|пустых|O(1)|O(1)|O(1)|O(1)|O(1)|Создает пустую коллекцию.|
|exists|O (N)|O (N)|O (N)|O (log N)|O (log N)|Проверяет, удовлетворяет ли какой либо элемент последовательности заданному предикату.|
|exists2-|O (минимум (N, M))|-|O (минимум (N, M))|||Проверяет, удовлетворяет ли ни одной паре соответствующих элементов входной последовательности заданному предикату.|
|fill|O (N)|||||Задает диапазон элементов массива для заданного значения.|
|фильтр|O (N)|O (N)|O (N)|O (N)|O (N)|Возвращает новую коллекцию, содержащую только элементы коллекции, для которой заданный предикат возвращает `true`.|
|find|O (N)|O (N)|O (N)|O (log N)|-|Возвращает первый элемент, для которого заданная функция возвращает `true`. Возвращает `System.Collections.Generic.KeyNotFoundException`, если такого элемента не существует.|
|findIndex|O (N)|O (N)|O (N)|-|-|Возвращает индекс первого элемента в массиве, удовлетворяющего заданному предикату. Вызывает `System.Collections.Generic.KeyNotFoundException`, если ни один элемент не удовлетворяет предикату.|
|финдкэй|-|-|-|O (log N)|-|Вычисляет функцию для каждого сопоставления в коллекции и возвращает ключ для первого сопоставления, в котором функция возвращает `true`. Если такого элемента не существует, эта функция вызывает `System.Collections.Generic.KeyNotFoundException`.|
|папка|O (N)|O (N)|O (N)|O (N)|O (N)|Применяет функцию к каждому элементу коллекции, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Если входная функция — f, а элементы — i0... в эта функция выполняет вычисление f (... (f s I0)...) окне.|
|fold2|O (N)|O (N)|-|-|-|Применяет функцию к соответствующим элементам двух коллекций, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Коллекции должны иметь одинаковые размеры. Если входная функция — f, а элементы — i0... в и j0... ЖН, эта функция вычислит f (... (f s, i0 j0)...) в ЖН.|
|foldBack|O (N)|O (N)|-|O (N)|O (N)|Применяет функцию к каждому элементу коллекции, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Если входная функция — f, а элементы — i0... в эта функция выполняет вычисление f i0 (... (f в s)).|
|foldBack2|O (N)|O (N)|-|-|-|Применяет функцию к соответствующим элементам двух коллекций, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Коллекции должны иметь одинаковые размеры. Если входная функция — f, а элементы — i0... в и j0... ЖН, эта функция вычислит f i0 j0 (... (f в ЖН s)).|
|ForAll|O (N)|O (N)|O (N)|O (N)|O (N)|Проверяет, соответствуют ли все элементы коллекции заданному предикату.|
|forall2|O (N)|O (N)|O (N)|-|-|Проверяет, соответствуют ли все соответствующие элементы коллекции заданному попарному предикату.|
|Get/n|O(1)|O (N)|O (N)|-|-|Возвращает элемент из коллекции по заданному индексу.|
|head|-|O(1)|O(1)|-|-|Возвращает первый элемент коллекции.|
|init|O (N)|O (N)|O(1)|-|-|Создает коллекцию, заданную измерением, и функцию генератора для вычислений элементов.|
|инитинфините|-|-|O(1)|-|-|Формирует последовательность, которая при переборе возвращает последовательные элементы путем вызова заданной функции.|
|секать|-|-|-|-|O (журнал N &#42; м)|Вычисление пересечения двух наборов.|
|интерсектмани|-|-|-|-|O (N1 &#42; N2...)|Вычисление пересечения последовательности наборов. Последовательность не должна быть пустой.|
|isEmpty|O(1)|O(1)|O(1)|O(1)|-|Возвращает `true`, если коллекция пуста.|
|испроперсубсет|-|-|-|-|O (M &#42; log N)|Возвращает `true`, если все элементы первого набора находятся во втором наборе, и хотя бы один элемент второго набора не находится в первом наборе.|
|испроперсуперсет|-|-|-|-|O (M &#42; log N)|Возвращает `true`, если все элементы второго набора находятся в первом наборе, и хотя бы один элемент первого набора не входит во второй набор.|
|подмножество|-|-|-|-|O (M &#42; log N)|Возвращает `true`, если все элементы первого набора находятся во втором наборе.|
|Супермножество|-|-|-|-|O (M &#42; log N)|Возвращает `true`, если все элементы второго набора находятся в первом наборе.|
|iter|O (N)|O (N)|O (N)|O (N)|O (N)|Применяет заданную функцию к каждому элементу коллекции.|
|iteri|O (N)|O (N)|O (N)|-|-|Применяет заданную функцию к каждому элементу коллекции. Целое число, передаваемое в функцию, указывает индекс элемента.|
|iteri2|O (N)|O (N)|-|-|-|Применяет заданную функцию к паре элементов, созданных из совпадающих индексов в двух массивах. Целое число, передаваемое в функцию, указывает индекс элементов. Длина двух массивов должна быть одинаковой.|
|iter2|O (N)|O (N)|O (N)|-|-|Применяет заданную функцию к паре элементов, созданных из совпадающих индексов в двух массивах. Длина двух массивов должна быть одинаковой.|
|последний|O(1)|O (N)|O (N)|-|-|Возвращает последний элемент в применимой коллекции.|
|длина|O(1)|O (N)|O (N)|-|-|Возвращает количество элементов в коллекции.|
|map|O (N)|O (N)|O(1)|-|-|Создает коллекцию, элементы которой являются результатами применения заданной функции к каждому элементу массива.|
|map2|O (N)|O (N)|O(1)|-|-|Создает коллекцию, элементы которой являются результатами применения заданной функции к соответствующим элементам двух коллекций попарно. Длина двух входных массивов должна быть одинаковой.|
|map3|-|O (N)|-|-|-|Создает коллекцию, элементы которой являются результатами применения заданной функции к соответствующим элементам трех коллекций одновременно.|
|действует|O (N)|O (N)|O (N)|-|-|Создает массив, элементы которого являются результатами применения заданной функции к каждому элементу массива. Целочисленный индекс, передаваемый функции, указывает индекс преобразуемого элемента.|
|mapi2|O (N)|O (N)|-|-|-|Выполняет сборку коллекции, элементы которой являются результатами применения заданной функции к соответствующим элементам двух коллекций попарно, также передавая индекс элементов. Длина двух входных массивов должна быть одинаковой.|
|max|O (N)|O (N)|O (N)|-|-|Возвращает наибольший элемент в коллекции по сравнению с использованием оператора [Max](https://msdn.microsoft.com/library/9a988328-00e9-467b-8dfa-e7a6990f6cce) .|
|максби|O (N)|O (N)|O (N)|-|-|Возвращает наибольший элемент в коллекции, по сравнению с использованием параметра [Max](https://msdn.microsoft.com/library/9a988328-00e9-467b-8dfa-e7a6990f6cce) в результатах функции.|
|макселемент|-|-|-|-|O (log N)|Возвращает наибольший элемент в наборе согласно упорядочению, используемому для набора.|
|min|O (N)|O (N)|O (N)|-|-|Возвращает элемент наименьшего уровня в коллекции по сравнению с использованием оператора [min](https://msdn.microsoft.com/library/adea4fd7-bfad-4834-989c-7878aca81fed) .|
|минби|O (N)|O (N)|O (N)|-|-|Возвращает элемент наименьшего уровня в коллекции по сравнению с использованием оператора [min](https://msdn.microsoft.com/library/adea4fd7-bfad-4834-989c-7878aca81fed) в результатах функции.|
|минелемент|-|-|-|-|O (log N)|Возвращает нижний элемент в наборе согласно упорядочению, используемому для набора.|
|офаррай|-|O (N)|O(1)|O (N)|O (N)|Создает коллекцию, содержащую те же элементы, что и заданный массив.|
|офлист|O (N)|-|O(1)|O (N)|O (N)|Создает коллекцию, содержащую те же элементы, что и заданный список.|
|ofSeq|O (N)|O (N)|-|O (N)|O (N)|Создает коллекцию, содержащую те же элементы, что и заданная последовательность.|
|кэширован|-|-|O (N)|-|-|Возвращает последовательность каждого элемента во входной последовательности и его предшественника, за исключением первого элемента, который возвращается только в качестве предшественника второго элемента.|
|partition|O (N)|O (N)|-|O (N)|O (N)|Разделяет коллекцию на две коллекции. Первая коллекция содержит элементы, для которых заданный предикат возвращает `true`, а вторая коллекция содержит элементы, для которых заданный предикат возвращает `false`.|
|permute|O (N)|O (N)|-|-|-|Возвращает массив со всеми элементами переставляются в соответствии с заданной перестановкой.|
|брать|O (N)|O (N)|O (N)|O (log N)|-|Применяет заданную функцию к последовательным элементам, возвращая первый результат, в котором функция возвращает часть. Если функция никогда не возвращает некоторые, возникает `System.Collections.Generic.KeyNotFoundException`.|
|readonly|-|-|O (N)|-|-|Создает объект последовательности, который делегирует заданному объекту последовательности. Эта операция гарантирует, что приведение типа не сможет повторно обнаружить и изменить исходную последовательность. Например, если задан массив, возвращаемая последовательность будет возвращать элементы массива, но возвращаемый объект последовательности нельзя привести к массиву.|
|reduce|O (N)|O (N)|O (N)|-|-|Применяет функцию к каждому элементу коллекции, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Эта функция начинается с применения функции к первым двум элементам, передает этот результат в функцию вместе с третьим элементом и т. д. Функция возвращает окончательный результат.|
|редуцебакк|O (N)|O (N)|-|-|-|Применяет функцию к каждому элементу коллекции, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Если входная функция — f, а элементы — i0... в эта функция выполняет вычисление f i0 (... (f в-1 в)).|
|remove|-|-|-|O (log N)|O (log N)|Удаляет элемент из домена на карте. Если элемент отсутствует, исключение не возникает.|
|водил|-|O (N)|-|-|-|Создает список указанной длины с каждым набором элементов на заданное значение.|
|расширения|O (N)|O (N)|-|-|-|Возвращает новый список с элементами в обратном порядке.|
|наличия|O (N)|O (N)|O (N)|-|-|Применяет функцию к каждому элементу коллекции, перечисляя аргумент накапливаемое в потоке с помощью вычисления. Эта операция применяет функцию ко второму аргументу и первому элементу списка. Затем операция передает этот результат в функцию вместе со вторым элементом и т. д. Наконец, операция возвращает список промежуточных результатов и окончательный результат.|
|scanBack|O (N)|O (N)|-|-|-|Напоминает операцию foldBack, но возвращает и промежуточные, и окончательные результаты.|
|singleton|-|-|O(1)|-|O(1)|Возвращает последовательность, которая получает только один элемент.|
|set|O(1)|-|-|-|-|Задает для элемента массива указанное значение.|
|skip|-|-|O (N)|-|-|Возвращает последовательность, которая пропускает N элементов базовой последовательности, а затем возвращает оставшиеся элементы последовательности.|
|skipWhile|-|-|O (N)|-|-|Возвращает последовательность, которая при переборе пропускает элементы базовой последовательности, пока заданный предикат возвращает `true`, а затем выдает оставшиеся элементы последовательности.|
|sort|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|O (N log N)|O (N log N)|-|-|Сортирует коллекцию по значению элемента. Элементы сравниваются с помощью функции [Compare](https://msdn.microsoft.com/library/295e1320-0955-4c3d-ac31-288fa80a658c).|
|sortBy|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|O (N log N)|O (N log N)|-|-|Сортирует заданный список с помощью ключей, предоставляемых заданной проекцией. Ключи сравниваются с помощью функции [Compare](https://msdn.microsoft.com/library/295e1320-0955-4c3d-ac31-288fa80a658c).|
|сортинплаце|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|-|-|-|-|Сортирует элементы массива, изменяя его на месте и используя заданную функцию сравнения. Элементы сравниваются с помощью функции [Compare](https://msdn.microsoft.com/library/295e1320-0955-4c3d-ac31-288fa80a658c).|
|сортинплацеби|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|-|-|-|-|Сортирует элементы массива, изменяя его на месте и используя заданную проекцию для ключей. Элементы сравниваются с помощью функции [Compare](https://msdn.microsoft.com/library/295e1320-0955-4c3d-ac31-288fa80a658c).|
|сортинплацевис|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|-|-|-|-|Сортирует элементы массива, изменяя его на месте и используя данную функцию сравнения в качестве порядка.|
|сортвис|O (N log N) среднее<br /><br />O (N ^ 2) наихудший случай|O (N log N)|-|-|-|Сортирует элементы коллекции, используя заданную функцию сравнения в качестве порядка и возвращая новую коллекцию.|
|sub|O (N)|-|-|-|-|Создает массив, содержащий заданный поддиапазон, заданный начальным индексом и длиной.|
|сумма|O (N)|O (N)|O (N)|-|-|Возвращает сумму элементов в коллекции.|
|sumBy|O (N)|O (N)|O (N)|-|-|Возвращает сумму результатов, созданных путем применения функции к каждому элементу коллекции.|
|односторонне|-|O(1)|-|-|-|Возвращает список без первого элемента.|
|take|-|-|O (N)|-|-|Возвращает элементы последовательности вплоть до указанного числа.|
|takeWhile|-|-|O(1)|-|-|Возвращает последовательность, которая при переборе возвращает элементы базовой последовательности, пока заданный предикат возвращается `true` а затем возвращает больше элементов.|
|toArray|-|O (N)|O (N)|O (N)|O (N)|Создает массив из заданной коллекции.|
|toList|O (N)|-|O (N)|O (N)|O (N)|Создает список из заданной коллекции.|
|toSeq|O(1)|O(1)|-|O(1)|O(1)|Создает последовательность из заданной коллекции.|
|truncate|-|-|O(1)|-|-|Возвращает последовательность, которая при перечислении возвращает не более N элементов.|
|tryFind|O (N)|O (N)|O (N)|O (log N)|-|Выполняет поиск элемента, удовлетворяющего заданному предикату.|
|tryFindIndex|O (N)|O (N)|O (N)|-|-|Выполняет поиск первого элемента, удовлетворяющего заданному предикату, и возвращает индекс соответствующего элемента или `None`, если такого элемента не существует.|
|трифиндкэй|-|-|-|O (log N)|-|Возвращает ключ первого сопоставления в коллекции, удовлетворяющего заданному предикату, или возвращает `None`, если такого элемента не существует.|
|tryPick|O (N)|O (N)|O (N)|O (log N)|-|Применяет заданную функцию к последовательным элементам, возвращая первый результат, в котором функция возвращает `Some` для некоторого значения. Если такого элемента не существует, операция возвращает `None`.|
|Unfold|-|-|O (N)|-|-|Возвращает последовательность, содержащую элементы, создаваемые данным вычислением.|
|объединение|-|-|-|-|O (M &#42; log N)|Вычисление объединения двух наборов.|
|унионмани|-|-|-|-|O (N1 &#42; N2...)|Выполняет вычисление объединения последовательности наборов.|
|unzip|O (N)|O (N)|O (N)|-|-|Разделяет список пар на два списка.|
|unzip3|O (N)|O (N)|O (N)|-|-|Разделяет список триад на три списка.|
|оконные|-|-|O (N)|-|-|Возвращает последовательность, которая дает скользящие окна элементов, которые были выведены из входной последовательности. Каждое окно возвращается в виде нового массива.|
|zip|O (N)|O (N)|O (N)|-|-|Объединяет две коллекции в список пар. Два списка должны иметь одинаковую длину.|
|zip3|O (N)|O (N)|O (N)|-|-|Объединяет три коллекции в список Тройн. Списки должны иметь одинаковую длину.|

## <a name="see-also"></a>См. также:

- [Типы языка F#](fsharp-types.md)
- [Справочник по языку F#](index.md)
