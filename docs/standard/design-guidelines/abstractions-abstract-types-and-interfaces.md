---
title: Абстракции (абстрактные типы и интерфейсы)
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- interfaces [.NET Framework], abstract
- abstract interfaces [.NET Framework]
- abstract types [.NET Framework]
- types [.NET Framework], abstract
ms.assetid: 0a632bc7-9b03-44ee-8842-c82f88672a45
author: KrzysztofCwalina
ms.openlocfilehash: fcf566c24677630fdbb1fcd0eb7628f830b3be2b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61789224"
---
# <a name="abstractions-abstract-types-and-interfaces"></a>Абстракции (абстрактные типы и интерфейсы)
Абстракция — это тип, который описывает контракт, но не содержит полной реализации контракта. Абстракции обычно реализуются как абстрактных классов или интерфейсов, и они поставляются с четко определенный набор справочная документация, описывающие необходимую семантику типов, реализующих контракт. Ниже перечислены некоторые из важнейших абстракций в .NET Framework <xref:System.IO.Stream>, <xref:System.Collections.Generic.IEnumerable%601>, и <xref:System.Object>.  
  
 Платформы можно расширить путем реализации конкретный тип, поддерживает контракт абстракции и использовать этот конкретный тип framework API-интерфейсы много (работе) абстракции.  
  
 Значимые и полезные абстракции, который способен выдержать испытание времени для разработки очень сложно. Основные сложности является получение правильного набора элементов, не больше и не меньше. Если это абстракция имеет слишком много элементов, становится трудно или даже невозможно реализовать. Если он имеет слишком мало элементов для обещанный функциональных возможностей, он не стал бесполезен в много интересных ситуаций.  
  
 Слишком много абстракции в платформе также отрицательно повлиять на удобство использования платформы. Часто бывает довольно сложно понять абстракцию, не понимая, как ИТ вписывается в общую картину конкретные реализации и API-интерфейсы, работающие с абстракцией. Кроме того имена абстракций и члены являются обязательно абстрактными, часто делает их интерпретировать и unapproachable без первого основные сведения о более широком контексте их использования.  
  
 Тем не менее абстракции предоставляют очень эффективно расширяемости, часто не может совпадать с другие механизмы расширяемости. Они являются основой множество архитектурных шаблонов, таких как подключаемые модули, инверсии управления (IoC), конвейеры и т. д. Они также крайне важно для тестирования платформ. Хороший абстракции позволяют заглушки для интенсивной зависимости для целей модульного тестирования. Таким образом абстракции отвечают за популярных разнообразие современных платформ объектно ориентированного.  
  
 **X DO NOT** предоставляют абстракции, пока не проверите их путем разработки нескольких конкретных реализаций и использует эти абстракции API-интерфейсы.  
  
 **✓ DO** тщательно выбирайте между абстрактным классом и интерфейсом при проектировании абстракции.  
  
 **✓ CONSIDER** предоставление тесты конкретных реализаций абстракций. Такие тесты позволят пользователям проверить их реализации правильной реализации контракта.  
  
 *Фрагменты: © Корпорация Майкрософт (Microsoft Corporation), 2005, 2009. Все права защищены.*  
  
 *Перепечатано разрешением Пирсона для образовательных учреждений, Inc. из [рекомендации по разработке Framework: Условные обозначения, стили и шаблоны для библиотеки .NET для повторного использования, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Кшиштов Квалина и Брэд Абрамс, опубликованных 22 октября 2008 г., издательство Addison-Wesley Professional как части цикла разработки Microsoft Windows.*  
  
## <a name="see-also"></a>См. также

- [Рекомендации по проектированию на основе Framework](../../../docs/standard/design-guidelines/index.md)
- [Разработка с обеспечением расширяемости](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
