---
title: Общие сведения о процессе определения схемы набора данных
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 35e9b67d2d0a47aa69eabdb4b7e94f95b0b9589f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833983"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>Общие сведения о процессе определения схемы набора данных
Процесс вывода схемы из XML-документа вначале определяет, какие элементы будут выведены как таблицы. Из оставшегося XML процесс вывода схемы определяет столбцы этих таблиц. Для вложенных таблиц процесс вывода формирует вложенные объекты <xref:System.Data.DataRelation> и <xref:System.Data.ForeignKeyConstraint>.  
  
 Ниже приведен краткий обзор правил вывода.  
  
- Элементы с атрибутами выводятся как таблицы.  
  
- Элементы, имеющие дочерние элементы, выводятся как таблицы.  
  
- Повторяющиеся элементы выводятся как одна таблица.  
  
- Если элемент документа (корневой элемент) не имеет ни атрибутов, ни дочерних элементов, которые выводились бы как столбцы, он выводится как <xref:System.Data.DataSet>. В противном случае элемент документа выводится как таблица.  
  
- Атрибуты выводятся как столбцы.  
  
- Элементы, которые не повторяются и не имеют ни атрибутов, ни дочерних элементов, выводятся как столбцы.  
  
- Для элементов, которые выводятся в виде вложенных таблиц в других элементах, которые также выводятся в виде таблиц, между двумя таблицами создается вложенная **связь DataRelation** . Новый первичный ключевой столбец с именем **TableName_Id** добавляется в обе таблицы и используется **DataRelation**. Объект **ForeignKeyConstraint** создается между двумя таблицами с помощью столбца **TableName_Id** .  
  
- Для элементов, которые выводятся в виде таблиц и содержат текст, но не имеют дочерних элементов, для текста каждого элемента создается новый столбец с именем **TableName_Text** . Если элемент выводится как таблица и имеет текст, но при этом имеет дочерние элементы, текст пропускается.  
  
## <a name="see-also"></a>См. также

- [Определение реляционной структуры DataSet из XML](inferring-dataset-relational-structure-from-xml.md)
- [Загрузка DataSet из XML](loading-a-dataset-from-xml.md)
- [Загрузка сведений о схеме DataSet из XML](loading-dataset-schema-information-from-xml.md)
- [Использование XML в наборах данных](using-xml-in-a-dataset.md)
- [Наборы данных, таблицы данных и объекты DataView](index.md)
- [Общие сведения об ADO.NET](../ado-net-overview.md)
