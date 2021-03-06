---
title: Поддержка типов в классах System.Xml
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 63570538-06e3-4401-ad4d-ac50be90c7bf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 954ff12ae1ac8b4d601c35fcd76ea35b2bb3acbf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939442"
---
# <a name="type-support-in-the-systemxml-classes"></a>Поддержка типов в классах System.Xml
На платформе .NET Framework версии 2.0 основные классы XML были улучшены, чтобы включить функции поддержки типов. Классы <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> и <xref:System.Xml.XPath.XPathNavigator> включают возможности поддержки типов, включая возможность преобразования между собой типов схемы XML и типов CLR.  
  
 На платформе .NET Framework версии 2.0 классы <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> и <xref:System.Xml.XPath.XPathNavigator> были улучшены, чтобы включить функции поддержки типов.  
  
- Каждый из классов <xref:System.Xml.XmlReader> и <xref:System.Xml.XPath.XPathNavigator> включает свойство **SchemaInfo**, которое возвращает данные о схеме в узле.  
  
- Методы **ReadContentAs** и **ReadElementContentAs** и методы класса <xref:System.Xml.XmlReader> считывают текстовое значение и преобразуют его в значение CLR за один вызов метода.  
  
- Метод <xref:System.Xml.XmlWriter.WriteValue%2A> класса <xref:System.Xml.XmlWriter> преобразует тип CLR в тип схемы XML при записи XML-документа.  
  
- Свойства **ValueAs** и <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> класса <xref:System.Xml.XPath.XPathNavigator> возвращают значение узла и преобразуют его в значение CLR за один вызов метода.  
  
> [!NOTE]
> На платформе .NET Framework версии 1.0 класс <xref:System.Xml.XmlConvert> был нужен для взаимного преобразования типов схемы XML и типов CLR.  
  
## <a name="in-this-section"></a>В этом разделе  
 [Сопоставление типов XML-данных с типами CLR](../../../../docs/standard/data/xml/mapping-xml-data-types-to-clr-types.md)  
 Описывает сопоставления типов данных XML и типов CLR по умолчанию.  
  
 [Примечания по реализации поддержки типов XML](../../../../docs/standard/data/xml/xml-type-support-implementation-notes.md)  
 Обсуждаются некоторые детали реализации поддержки типов.  
  
 [Преобразование типов XML-данных](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)  
 Описывает использование класса <xref:System.Xml.XmlConvert> для взаимного преобразования типов схемы XML и типов CLR.  
  
## <a name="related-sections"></a>Связанные разделы  
 [Доступ к XML-данным со строгой типизацией с помощью XPathNavigator](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
