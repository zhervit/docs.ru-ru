---
ms.openlocfilehash: 8b2a01eb6dfdd5bd2bcbef6014d4edeb3ec82ac1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379550"
---
### <a name="winforms-checkforoverflowunderflow-property-is-now-true-for-systemdrawing"></a>Свойство CheckForOverflowUnderflow WinForm теперь имеет значение true для System.Drawing

|   |   |
|---|---|
|Подробные сведения|Свойство CheckForOverflowUnderflow для сборки System.Drawing.dll имеет значение true.|
|Предложение|Раньше при переполнениях результат усекался без уведомления. Теперь создается исключение <xref:System.OverflowException?displayProperty=name>,|
|Область|Пограничный случай|
|Версия|4.5|
|Тип|Среда выполнения|
