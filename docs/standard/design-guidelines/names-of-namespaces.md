---
title: Имена пространств имен.
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], conflicts
- names [.NET Framework], namespaces
- type names, conflicts
- namespaces [.NET Framework], names
- names [.NET Framework], type names
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
author: KrzysztofCwalina
ms.openlocfilehash: b8b6ec195fd3f95a4255ea820f2bffcb3e27ba19
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615222"
---
# <a name="names-of-namespaces"></a>Имена пространств имен.
Как с помощью других рекомендациях по именованию, целью при именовании пространств имен является создание достаточно ясности для программиста, с помощью платформы для сразу знать содержимое пространства имен, вероятно, будет. Следующий шаблон определяет правило именования пространства имен:  
  
 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`  
  
 Ниже приведены примеры:  
  
 `Fabrikam.Math`  
 `Litware.Security`  
  
 **✓ DO** префикса пространства имен названия название компании, чтобы предотвратить пространства имен из разных компаний с одинаковым именем.  
  
 **✓ DO** название стабильной, независимые от версии продукта, используемое на втором уровне пространства имен.  
  
 **X DO NOT** использовать организационные иерархии как основу для имен в иерархии пространств имен, так как имена групп в организации, как правило краткосрочны. Организуйте иерархию пространств имен вокруг группы связанных технологий.  
  
 **✓ DO** использовать PascalCasing и компонентов в отдельном пространстве имен с точками (например, `Microsoft.Office.PowerPoint`). Если марки используется нетрадиционных регистр, соблюдайте торговой марки, даже если оно отклоняется от обычных имен регистр.  
  
 **✓ CONSIDER** с помощью имена во множественном числе пространств имен, где это применимо.  
  
 Например, используйте `System.Collections` вместо `System.Collection`. Марки и акронимы, тем не менее исключения из этого правила. Например, используйте `System.IO` вместо `System.IOs`.  
  
 **X DO NOT** использовать то же имя для пространства имен и типа в этом пространстве имен.  
  
 Например, не используйте `Debug` как пространство имен имя и нужно будет указать класс с именем `Debug` в одном пространстве имен. Некоторые компиляторы требуют таких типов должен быть полностью специфицированным.  
  
### <a name="namespaces-and-type-name-conflicts"></a>Пространства имен и конфликтов имен типов  
 **X DO NOT** ввести имена универсальных типов, таких как `Element`, `Node`, `Log`, и `Message`.  
  
 Есть очень велика вероятность того, что это приведет к введите имя конфликтует в распространенных сценариях. Вы должны квалифицироваться имена универсальных типов (`FormElement`, `XmlNode`, `EventLog`, `SoapMessage`).  
  
 Существуют определенные правила для предотвращения конфликтов имен типов для различных категорий пространств имен.  
  
- **Пространства имен модели приложения**  
  
     Пространства имен, принадлежащих одной модели приложения очень часто используются совместно, но они почти никогда не используются с пространствами имен других моделей приложений. Например <xref:System.Windows.Forms?displayProperty=nameWithType> вместе с очень редко используется пространство имен <xref:System.Web.UI?displayProperty=nameWithType> пространства имен. Ниже приведен список известных приложений модели пространство имен групп:  
  
     `System.Windows*`   
     `System.Web.UI*`  
  
     **X DO NOT** дать одинаковые имена, чтобы типы в пространствах имен в пределах одной модели приложения.  
  
     Например, не добавляйте тип с именем `Page` для <xref:System.Web.UI.Adapters?displayProperty=nameWithType> пространства имен, так как <xref:System.Web.UI?displayProperty=nameWithType> пространство имен уже содержит тип с именем `Page`.  
  
- **Пространства имен инфраструктуры**  
  
     Эта группа содержит пространства имен, которые редко импортируются во время разработки распространенных приложений. Например `.Design` пространства имен используются главным образом, при разработке программирования средств. Предотвращение конфликтов с типами из этих пространств имен не является критически важным.  
  
- **Основные пространства имен**  
  
     Основные пространства имен включают все `System` пространства имен, за исключением пространства имен модели приложений и инфраструктуры пространств имен. Основные пространства имен включают, помимо прочего, `System`, `System.IO`, `System.Xml`, и `System.Net`.  
  
     **X DO NOT** предоставляют типы имен, которые могли бы конфликтовать с любым типом из основных пространств имен.  
  
     Например, никогда не используйте `Stream` как имя типа. Это вызовет конфликт с <xref:System.IO.Stream?displayProperty=nameWithType>, очень часто используемый тип.  
  
- **Группы пространств имен технологий**  
  
     В эту категорию входят все пространства имен с тем же два первых узла пространства имен `(<Company>.<Technology>*`), такие как `Microsoft.Build.Utilities` и `Microsoft.Build.Tasks`. Очень важно, что типы, принадлежащие к одной технологии не конфликтуют друг с другом.  
  
     **X DO NOT** назначить имена типов, которые могли бы конфликтовать с другими типами внутри одной технологии.  
  
     **X DO NOT** вводит конфликтов имен типов между типами из пространств имен технологии и пространстве имен модели приложения (если компонент не предназначен для использования с моделью приложения).  
  
 *Фрагменты: © Корпорация Майкрософт (Microsoft Corporation), 2005, 2009. Все права защищены.*  
  
 *Перепечатано разрешением Пирсона для образовательных учреждений, Inc. из [рекомендации по разработке Framework: Условные обозначения, стили и шаблоны для библиотеки .NET для повторного использования, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Кшиштов Квалина и Брэд Абрамс, опубликованных 22 октября 2008 г., издательство Addison-Wesley Professional как части цикла разработки Microsoft Windows.*  
  
## <a name="see-also"></a>См. также

- [Рекомендации по проектированию на основе Framework](../../../docs/standard/design-guidelines/index.md)
- [Правила именования](../../../docs/standard/design-guidelines/naming-guidelines.md)
