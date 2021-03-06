---
title: Automatic Memory Management
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, automatic memory management
- memory, allocating
- memory, automatic memory management
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- managed heap
- runtime, automatic memory management
ms.assetid: d4850de5-fa63-4936-a250-5678d118acba
ms.openlocfilehash: d112bf6d145893bd7b0f99e2b233fc83e72fe227
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73140569"
---
# <a name="automatic-memory-management"></a>Automatic Memory Management
Для автоматического управления памятью используется одна из служб, которые среда CLR предоставляет при [управляемом выполнении](../../docs/standard/managed-execution-process.md). Сборщик мусора среды CLR управляет освобождением и выделением памяти для приложения. Для разработчиков это означает, что при разработке управляемого приложения не нужно писать код для управления памятью. Автоматическое управление памятью позволяет устранить распространенные проблемы, такие как не освобожденный по забывчивости объект, вызывающий утечку памяти, или попытки доступа к памяти для уже удаленного объекта. В этом разделе описано, каким образом сборщик мусора выделяет и освобождает память.  
  
## <a name="allocating-memory"></a>Выделение памяти  
 При инициализации нового процесса среда выполнения резервирует для него непрерывную область адресного пространства. Это зарезервированное адресное пространство называется управляемой кучей. Эта управляемая куча содержит указатель адреса, с которого будет выделена память для следующего объекта в куче. Изначально этот указатель устанавливается в базовый адрес управляемой кучи. Все [ссылочные типы](../../docs/standard/base-types/common-type-system.md) размещаются в управляемой куче. Когда приложение создает первый ссылочный тип, память для него выделяется, начиная с базового адреса управляемой кучи. При создании приложением следующего объекта сборщик мусора выделяет для него память в адресном пространстве, непосредственно следующем за первым объектом. Пока имеется доступное адресное пространство, сборщик мусора продолжает выделять пространство для новых объектов по этой схеме.  
  
 Выделение памяти из управляемой кучи происходит быстрее, чем неуправляемое выделение памяти. Поскольку среда выполнения выделяет память для объекта путем добавления значения к указателю, это осуществляется почти так же быстро, как выделение памяти из стека. Кроме того, поскольку выделяемые последовательно новые объекты и располагаются последовательно в управляемой куче, приложение может получать доступ к объектам очень быстро.  
  
<a name="cpconautomaticmemorymanagementreleasingmemoryanchor1"></a>   
## <a name="releasing-memory"></a>Освобождение памяти  
 Механизм оптимизации сборщика мусора определяет наилучшее время для выполнения сбора, основываясь на произведенных выделениях памяти. Когда сборщик мусора выполняет очистку, он освобождает память, выделенную для объектов, которые больше не используются приложением. Он определяет, какие объекты больше не используются, основываясь на корнях приложения. Каждое приложение имеет набор корней. Каждый корень либо ссылается на объект, находящийся в управляемой куче, либо имеет значение NULL. Корни приложения содержат статические поля, локальные переменные и параметры стека потока, а также регистры процессора. Сборщик мусора имеет доступ к списку активных корней, которые поддерживаются [JIT-компилятором](../../docs/standard/managed-execution-process.md) и средой выполнения. С помощью этого списка он проверяет корни приложения и в процессе проверки создает граф, содержащий все объекты, к которым можно получить доступ из этих корней.  
  
 Объекты, не входящие в этот граф, являются недостижимыми из данных корней приложения. Сборщик мусора считает недостижимые объекты мусором и будет освобождать выделенную для них память. В процессе очистки сборщик мусора проверяет управляемую кучу, отыскивая блоки адресного пространства, занятые недостижимыми объектами. При обнаружении недостижимого объекта он использует функцию копирования памяти для уплотнения достижимых объектов в памяти, освобождая блоки адресного пространства, выделенные под недостижимые объекты. После уплотнения памяти, занимаемой достижимыми объектами, сборщик мусора вносит необходимые поправки в указатель, чтобы корни приложения указывали на новые расположения объектов. Он также устанавливает указатель управляемой кучи в положение после последнего достижимого объекта. Обратите внимание, что память уплотняется, только если при очистке обнаруживается значительное число недостижимых объектов. Если после сборки мусора все объекты в управляемой куче остаются на месте, то уплотнение памяти не требуется.  
  
 Для повышения производительности среда выполнения выделяет память для больших объектов в отдельной куче. Сборщик мусора автоматически освобождает память, выделенную для больших объектов. Однако для устранения перемещений в памяти больших объектов эта память не сжимается.  
  
## <a name="generations-and-performance"></a>Поколения и производительность  
 Для оптимизации производительности сборщика мусора управляемая куча делится на три поколения: 0, 1 и 2. Алгоритм сборки мусора в среде выполнения основан на ряде обобщений, к которым пришла программная индустрия в процессе экспериментов со схемами сборки мусора. Во-первых, уплотнять память для части управляемой кучи быстрее, чем для всей кучи. Во-вторых, более новые объекты имеют меньшее время жизни, а более старые объекты имеют большее время жизни. Наконец, более новые объекты теснее связаны друг с другом, и приложение обращается к ним приблизительно в одно и то же время.  
  
 Сборщик мусора среды выполнения хранит новые объекты в поколении 0. Уровень объектов, созданных на раннем этапе работы приложения и оставшихся после сборок мусора, повышается, и они сохраняются в поколении 1 и 2. Процесс продвижения объекта по уровням описан далее в этом разделе. Поскольку быстрее сжать часть управляемой кучи, чем всю кучу, эта схема позволяет сборщику мусора освобождать память в определенном поколении, а не освобождать память для всей кучи каждый раз при сборке мусора.  
  
 В действительности сборщик мусора выполняет очистку при заполнении поколения 0. Если приложение пытается создать новый объект, когда поколение 0 заполнено, сборщик мусора обнаруживает, что в поколении 0 не осталось свободного адресного пространства для объекта. Сборщик мусора выполняет сборку, пытаясь освободить для этого объекта адресное пространство в поколении 0. Сборщик мусора начинает проверять объекты в поколении 0, а не все объекты в управляемой куче. Это наиболее эффективный подход, поскольку, как правило, новые объекты имеют меньшее время жизни, и можно ожидать, что многие из объектов в поколении 0 к моменту проведения сборки мусора уже не используются приложением. Кроме того, сборка мусора только в поколении 0 зачастую освобождает достаточно памяти для того, чтобы приложение могло продолжить создавать новые объекты.  
  
 После того как сборщик мусора выполнит освобождение для поколения 0, он уплотняет память для достижимых объектов, как описано ранее в разделе [Освобождение памяти](#cpconautomaticmemorymanagementreleasingmemoryanchor1). Затем сборщик мусора продвигает эти объекты и считает эту часть управляемой кучи поколением 1. Так как объекты, оставшиеся после сборки, обычно склонны к долгой жизни, имеет смысл продвинуть их в поколение более высокого уровня. В результате сборщику мусора не обязательно выполнять повторную проверку объектов поколений 1 и 2 при каждой сборке мусора в поколении 0.  
  
 После того как сборщик мусора выполнит первую сборку поколения 0 и продвинет доступные объекты в поколение 1, он считает оставшуюся часть управляемой кучи поколением 0. Он продолжает размещать память для новых объектов в поколении 0, до тех пор пока поколение 0 не заполнится и необходимо будет провести следующую сборку. В этот момент оптимизатор сборщика мусора определяет, есть ли необходимость проверки объектов в более старых поколениях. Например, если сборка поколения 0 не освобождает достаточно памяти, чтобы приложение могло успешно завершить создание объекта, сборщик мусора может выполнить сборку мусора поколения 1, а затем поколения 2. Если и это не действие не освободит достаточно памяти, сборщик мусора может выполнить сборку мусора поколений 2, 1, и 0. После каждой сборки сборщик мусора собирает доступные объекты в поколении 0 и продвигает их в поколение 1. Объекты в поколении 1, оставшиеся после сборок, продвигаются в поколение 2. Поскольку сборщик мусора поддерживает только три поколения, объекты в поколении 2, оставшиеся после сборки, остаются в поколении 2 до тех пор, пока они не перестанут быть доступными в результате сборки мусора.  
  
## <a name="releasing-memory-for-unmanaged-resources"></a>Освобождение памяти для неуправляемых ресурсов  
 Для большинства объектов, созданных приложением, сборщик мусора автоматически выполнит необходимые задачи по управлению памятью. Однако для неуправляемых ресурсов требуется явная очистка. Основным типом неуправляемых ресурсов являются объекты, образующие упаковку для ресурсов операционной системы, такие как дескриптор файлов, дескриптор окна или сетевое подключение. Хотя сборщик мусора может отслеживать время жизни управляемого объекта, инкапсулирующего неуправляемые ресурсы, он не имеет определенных сведений о том, как освобождать эти ресурсы. При создании объекта, который инкапсулирует неуправляемый ресурс, рекомендуется включить код для очистки неуправляемого ресурса в общий метод **Dispose**. Метод **Dispose** позволяет явно освобождать память при завершении работы с объектом. При использовании объекта, который инкапсулирует неуправляемый ресурс, следует помнить о методе **Dispose** и при необходимости вызывать его. Дополнительные сведения об освобождении неуправляемых ресурсов и пример шаблона для реализации метода **Dispose** см. в разделе [Сборка мусора](../../docs/standard/garbage-collection/index.md).  
  
## <a name="see-also"></a>См. также

- <xref:System.GC>
- [Сборка мусора](../../docs/standard/garbage-collection/index.md)
- [Процесс управляемого выполнения](../../docs/standard/managed-execution-process.md)
