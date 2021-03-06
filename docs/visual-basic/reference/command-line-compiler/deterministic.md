---
title: -deterministic
ms.date: 04/11/2018
helpviewer_keywords:
- deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
ms.openlocfilehash: 6a83b636dd83534788f3a38971e0fef2919314f5
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005628"
---
# <a name="-deterministic"></a>-deterministic

Указывает компилятору на необходимость создания сборки, чьи побайтовые выходные данные идентичны в разных компиляциях, если входные данные идентичны.

## <a name="syntax"></a>Синтаксис

```console
-deterministic
```

## <a name="remarks"></a>Примечания

По умолчанию выходные данные компилятора из заданного набора входных данных являются уникальными, поскольку компилятор добавляет метку времени и идентификатор GUID, который создается из случайных чисел. Вы можете использовать параметр `-deterministic` для создания *детерминированной сборки*, двоичное содержимое которой идентично в разных компиляциях при условии, что входные данные не изменяются.

Компилятор учитывает идентичность следующих входных данных:

- Последовательность параметров командной строки.
- Содержимое RSP-файла ответов в компиляторе.
- Точная версия компилятора и его связанные сборки.
- Текущий путь к каталогу.
- Двоичное содержимое всех файлов, явным образом переданных компилятору прямо или косвенно, в том числе:
  - Исходные файлы
  - Связанные сборки
  - Связанные модули
  - Ресурсы
  - Файл ключа строгого имени
  - Файлы ответов @
  - Анализаторы
  - Наборы правил
  - Дополнительные файлы, которые могут использоваться анализаторами
- Текущий язык и региональные параметры (для языка сообщений о диагностике и исключениях).
- Кодировка по умолчанию (или текущая кодовая страница), если кодировка не указана.
- Наличие, отсутствие и содержимое файлов на пути поиска компилятора (задается, например, с помощью `/lib` или `/recurse`).
- Платформа среды CLR, в которой выполняется компилятор.
- Значение `%LIBPATH%`, которое может повлиять на загрузку зависимостей анализатора.

Если источники общедоступны, детерминированную компиляцию можно использовать, чтобы установить, компилируются ли двоичные данные из надежного источника. Ее также можно использовать в системе непрерывной сборки, чтобы определить необходимость выполнения шагов сборки, зависящих от изменений в двоичном файле.

## <a name="see-also"></a>См. также

- [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)
- [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
