---
title: Практическое руководство. Построчное чтение текстового файла (Visual C#)
ms.date: 07/20/2015
helpviewer_keywords:
- ReadLine method [C#]
- reading text files, line by line
- text files [C#]
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
ms.openlocfilehash: 75274d93ee29feb5f79dfc29c24109f25fd98a5c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589963"
---
# <a name="how-to-read-a-text-file-one-line-at-a-time-visual-c"></a>Практическое руководство. Построчное чтение текстового файла (Visual C#)
В этом примере производится построчное чтение содержимого текстового файла в строку с помощью метода `ReadLine` класса `StreamReader`. Каждая строка текста сохраняется в строке `line` и отображается на экране.  
  
## <a name="example"></a>Пример  
  
```csharp
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =   
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine(line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Скопируйте код и вставьте его в метод `Main` консольного приложения.  
  
 Замените `"c:\test.txt"` фактическим именем файла.  
  
## <a name="robust-programming"></a>Отказоустойчивость  
 При следующих условиях возможно возникновение исключения:  
  
- Возможно, файл не существует.  
  
## <a name="net-framework-security"></a>Безопасность платформы .NET Framework  
 По имени файла не всегда можно с уверенностью судить о его содержимом. Например, файл с именем `myFile.cs` может вовсе не быть исходным файлом C#.  
  
## <a name="see-also"></a>См. также

- <xref:System.IO?displayProperty=nameWithType>
- [Руководство по программированию на C#](../index.md)
- [Файловая система и реестр (руководство по программированию на C#)](./index.md)
