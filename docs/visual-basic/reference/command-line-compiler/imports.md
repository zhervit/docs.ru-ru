---
title: -imports
ms.date: 03/10/2018
helpviewer_keywords:
- /imports compiler option [Visual Basic]
- imports compiler option [Visual Basic]
- -imports compiler option [Visual Basic]
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
ms.openlocfilehash: 380e71e462f736d4564a37b83567007fa9461b05
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/22/2019
ms.locfileid: "74332957"
---
# <a name="-imports-visual-basic"></a>-Imports (Visual Basic)
Импортирует пространства имен из указанной сборки.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-imports:namespaceList  
```  
  
## <a name="arguments"></a>Аргументы  
  
|Термин|Определение|  
|---|---|  
|`namespaceList`|Обязательно. Разделенный запятыми список пространств имен для импорта.|  
  
## <a name="remarks"></a>Примечания  
 Параметр `-imports` импортирует любое пространство имен, определенное в текущем наборе исходных файлов или в любой связанной сборке.  
  
 Элементы в пространстве имен, заданном с помощью `-imports`, доступны для всех файлов исходного кода в компиляции. Используйте [оператор Imports (пространство имен .NET и тип)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) , чтобы использовать пространство имен в одном файле исходного кода.  
  
|Установка/Imports в интегрированной среде разработки Visual Studio|  
|---|  
|1. Выберите проект в **Обозреватель решений**. В меню **Проект** выберите пункт **Свойства**. <br />2. Перейдите на вкладку **ссылки** .<br />3. Введите имя пространства имен в поле рядом с кнопкой **Добавить пользовательский импорт** .<br />4. Нажмите кнопку **Добавить пользовательский импорт** .|  
  
## <a name="example"></a>Пример  
 Следующий код компилируется при указании `/imports:system.globalization`. В противном случае для успешной компиляции требуется, чтобы инструкция `Imports System.Globalization` была включена в начало файла исходного кода или что свойство полностью определено как `System.Globalization.CultureInfo.CurrentCulture.Name`.

```vb
Module Example
   Public Sub Main()
      Console.WriteLine($"The current culture is {CultureInfo.CurrentCulture.Name}")
   End Sub
End Module
```

## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [Ссылки и оператор Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
