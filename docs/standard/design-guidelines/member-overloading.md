---
title: Перегрузка членов
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- default arguments
- members [.NET Framework], overloaded
- member design guidelines [.NET Framework], overloading
- overloaded members
- signatures, members
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
author: KrzysztofCwalina
ms.openlocfilehash: 4caa0ae78d168b23fd2862153bef0e3960d3ea42
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392943"
---
# <a name="member-overloading"></a>Перегрузка членов
Перегрузка членов означает создание двух или более членов одного типа, которые отличаются только числом или типом параметров, но имеют одинаковые имена. Например, в следующем примере метод `WriteLine` перегружен:  
  
```csharp  
public static class Console {  
    public void WriteLine();  
    public void WriteLine(string value);  
    public void WriteLine(bool value);  
    ...  
}  
```  
  
 Поскольку только методы, конструкторы и индексированные свойства могут иметь параметры, только эти члены могут быть перегружены.  
  
 Перегрузка является одним из наиболее важных методов для повышения удобства использования, производительности и удобочитаемости многократно используемых библиотек. Перегрузка по количеству параметров позволяет предоставить более простые версии конструкторов и методов. Перегрузка типа параметра позволяет использовать одно и то же имя элемента для членов, выполняющих идентичные операции с выбранным набором различных типов.  
  
 **✓ DO** попробуйте использовать описательные имена параметров, чтобы указать значение по умолчанию использовать более короткие перегрузки.  
  
 **X AVOID** произвольного изменения имен параметров в перегрузках. Если параметр в одной перегрузке представляет те же входные данные, что и параметр в другой перегрузке, параметры должны иметь одинаковые имена.  
  
 **X AVOID** Несогласованная в порядок параметров в перегруженных членов. Параметры с одинаковым именем должны отображаться в одной и той же области во всех перегрузках.  
  
 **✓ DO** сделать виртуальной только самую длинную перегрузку (если требуется расширяемость). Более короткие перегрузки должны просто вызывать более длинную перегрузку.  
  
 **X DO NOT** использовать `ref` или `out` модификаторы для перегрузки членов.  
  
 Некоторые языки не могут разрешать вызовы перегрузок следующим образом. Кроме того, такие перегрузки обычно имеют совершенно другую семантику и, вероятно, не должны перегружаться, но вместо этого можно использовать два отдельных метода.  
  
 **X DO NOT** имеют перегрузки с параметрами в одной позиции и похожих, но различную семантику.  
  
 **✓ DO** Разрешить `null` для передачи дополнительных аргументов.  
  
 **✓ DO** использовать член перегрузка предпочтительнее, чем определение членов с аргументами по умолчанию.  
  
 Аргументы по умолчанию несовместимы с CLS.  
  
 *Части © 2005, 2009 Корпорация Майкрософт. Все права защищены.*  
  
 *Перепечатано с разрешения Pearson Education, Inc. из книги [Инфраструктура программных проектов. Соглашения, идиомы и шаблоны для многократно используемых библиотек .NET (2-е издание)](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619), авторы: Кржиштоф Цвалина (Krzysztof Cwalina) и Брэд Абрамс (Brad Abrams). Книга опубликована 22 октября 2008 г. издательством Addison-Wesley Professional в рамках серии, посвященной разработке для Microsoft Windows.*  
  
## <a name="see-also"></a>См. также:

- [Правила разработки членов](../../../docs/standard/design-guidelines/member.md)
- [Рекомендации по проектированию на основе Framework](../../../docs/standard/design-guidelines/index.md)
