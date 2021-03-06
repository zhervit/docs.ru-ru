---
title: Практическое руководство. Блокирование элементов управления в формах Windows Forms.
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms controls, locking
- controls [Windows Forms], locking
ms.assetid: 94efe0d2-c14e-4d14-b903-63ea9b07e290
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d157ddc8be4b5fa0057241b562e76b566e8dad99
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458343"
---
# <a name="how-to-lock-controls-to-windows-forms"></a>Руководство. Блокировка элементов управления в Windows Forms

При проектировании пользовательского интерфейса приложения Windows можно заблокировать элементы управления после их правильного позиционирования, чтобы случайно не перемещать их или изменять их размер при настройке других свойств.

Кроме того, можно одновременно заблокировать и разблокировать все элементы управления в форме, что полезно для форм с множеством элементов управления или разблокирование отдельных элементов управления. После размещения всех элементов управления в форме следует заблокировать их все на месте, чтобы предотвратить ошибочное перемещение.

## <a name="to-lock-a-control"></a>Блокировка элемента управления

В окне **Свойства** в Visual Studio выберите свойство **заблокировано** и выберите **значение true**. (Двойной щелчок по имени переключает параметр свойства.)

Также можно щелкнуть элемент управления правой кнопкой мыши и выбрать пункт **Блокировать элементы управления**.

> [!NOTE]
> Блокировка элементов управления предотвращает их перетаскивание на новый размер или расположение в области конструктора. Однако размер или расположение элементов управления по-прежнему можно изменить с помощью окна « **Свойства** » или в коде.

## <a name="to-lock-all-the-controls-on-a-form"></a>Блокировка всех элементов управления в форме

В меню **Формат** выберите пункт **Блокировать элементы управления**.

> [!NOTE]
> Эта команда также блокирует размер формы, поскольку форма является элементом управления.

## <a name="to-unlock-all-locked-controls-on-a-form"></a>Разблокирование всех заблокированных элементов управления в форме

В меню **Формат** выберите пункт **Блокировать элементы управления**.

Все ранее заблокированные элементы управления в форме теперь разблокированы.

## <a name="to-unlock-locked-controls-individually"></a>Разблокирование заблокированных элементов управления по отдельности

В окне **Свойства** выберите свойство **заблокировано** и нажмите кнопку **false**. (Двойной щелчок по имени переключает параметр свойства.)

## <a name="see-also"></a>См. также

- [Элементы управления Windows Forms](index.md)
- [Создание меток и назначение сочетаний клавиш для элементов управления Windows Forms](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Элементы управления для использования в Windows Forms](controls-to-use-on-windows-forms.md)
- [Функциональная классификация элементов управления Windows Forms](windows-forms-controls-by-function.md)
