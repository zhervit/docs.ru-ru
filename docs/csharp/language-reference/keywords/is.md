---
title: is. Справочник по C#
ms.custom: seodec18
ms.date: 06/21/2019
f1_keywords:
- is_CSharpKeyword
- is
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
ms.openlocfilehash: a04105137fad7cd3a25b869c3aa7fcbe91ed20ab
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566305"
---
# <a name="is-c-reference"></a>is (Справочник по C#)

Оператор `is` проверяет совместимость результата выражения с заданным типом или (начиная с C# 7.0) проверяет выражение на соответствие шаблону. Сведения об операторе тестирования типов `is` см. в соответствующем [разделе](../operators/type-testing-and-cast.md#is-operator) статьи об [операторах приведения и тестирования типов](../operators/type-testing-and-cast.md).

## <a name="pattern-matching-with-is"></a>Сопоставление шаблонов с `is`

Начиная с C# 7.0 операторы `is` и [switch](switch.md) поддерживают сопоставление шаблонов. Ключевое слово `is` поддерживает следующие шаблоны:

- [Шаблон типа](#type-pattern), который проверяет, можно ли преобразовать выражение в указанный тип и, если можно, приводит его к переменной этого типа.

- [Шаблон константы](#constant-pattern), который проверяет, получает ли выражение указанное постоянное значение.

- [Шаблон переменной](#var-pattern) — совпадение всегда является успешным и привязывает значение выражения к новой локальной переменной.

### <a name="type-pattern"></a>Шаблон типа

При использовании шаблона типа для сопоставления шаблонов `is` проверяет, можно ли преобразовать выражение в указанный тип и, если это возможно, приводит его к переменной этого типа. Это простое расширение оператора `is` для краткого определения и преобразования типов. Шаблон типа `is` имеет следующий общий вид:

```csharp
   expr is type varname
```

где *expr* — это выражение, значением которого является экземпляр какого-либо типа, *type* — это имя типа, в который должен быть преобразован результат *expr*, *varname* — это объект, в который преобразуется результат *expr*, если проверка `is` возвращает значение `true`. 

Выражение `is` имеет значение `true`, если *expr* не имеет значение `null` и выполняется одно из следующих условий:

- *expr* представляет собой экземпляр того же типа, что и *type*;

- *expr* является экземпляром типа, производного от *type*. Другими словами, результат *expr* может быть приведен с повышением к экземпляру *type*.

- *expr* имеет тип времени компиляции, который является базовым классом для *type*, и *expr* имеет тип среды выполнения, который является *type* или производным от *type*. *Тип времени компиляции* переменной представляет собой тип переменной, как определено в объявлении. *Тип среды выполнения* переменной представляет собой тип экземпляра, назначенный этой переменной.

- *expr* является экземпляром типа, который реализует интерфейс *type*.

Начиная с версии C# 7.1, *expr* может иметь тип времени компиляции, определяемый параметром универсального типа и его ограничениями.

Если *expr* — `true` и `is` используется с инструкцией `if`, *varname* назначается только в пределах инструкции `if`. Область видимости *varname* — от выражения `is` до конца блока, включающего инструкцию `if`. Использование *varname* в любом другом месте вызовет ошибку во время компиляции из-за использования переменной, которая не была назначена.

В следующем примере используется шаблон типа `is`, который обеспечивает реализацию метода <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> типа.

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

Без сопоставления шаблонов этот код может быть написан следующим образом. При использовании шаблона типа создается более лаконичный и удобочитаемый код, причем проверять результат преобразования (`null`) не требуется.  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

Шаблон типа `is` также позволяет создавать более компактный код при определении типа для типа значения. В следующем примере используется шаблон типа `is`, чтобы определить, является ли объект экземпляром `Person` или `Dog` перед отображением значения соответствующего свойства.

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

Для эквивалентного кода без сопоставления шаблонов требуется отдельное назначение, которое включает явное приведение.

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="constant-pattern"></a>Шаблон константы

При выполнении сопоставления с шаблоном константы `is` проверяет, равно ли выражение указанной константе. В C# 6 и более ранних версиях шаблон константы поддерживается оператором [switch](switch.md). Начиная с версии C# 7.0, также включена поддержка оператором `is`. Он имеет следующий синтаксис:

```csharp
   expr is constant
```

где *expr* — это выражение для вычисления, а *constant* — это значение, которое нужно проверить. *constant* может быть любой из следующих константных выражений:

- литеральное значение;

- имя объявленной переменной `const`;

- константа перечисления.

Константное выражение вычисляется следующим образом.

- Если *expr* и *constant* являются целочисленными типами, оператор равенства C# определяет, возвращает ли выражение `true` (то есть выполняется ли условие `expr == constant`).

- В противном случае значение выражения определяется с помощью вызова статического метода [Object.Equals (expr, constant)](xref:System.Object.Equals(System.Object,System.Object)).  

В следующем примере шаблон типа и шаблон константы объединяются для проверки того, является ли объект экземпляром `Dice` и, если это так, определяют, равно ли 6 значение броска кости.

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]

Проверку значения `null` можно выполнять с использованием константного шаблона. Ключевое слово `null` поддерживается оператором `is`. Он имеет следующий синтаксис:

```csharp
   expr is null
```

Следующий пример демонстрирует сравнение проверок `null`:

[!code-csharp[is#11](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern11.cs#11)]

### <a name="var-pattern"></a>Шаблон var

Шаблон `var` является универсальным и подходит для любых типов и значений. Значение *expr* всегда назначается локальной переменной того же типа, что и тип времени компиляции *expr*. Результат выражения `is` всегда равен `true`. Он имеет следующий синтаксис:

```csharp
   expr is var varname
```

В следующем примере шаблон переменной используется для назначения выражения переменной с именем `obj`. Затем отображается значение и тип `obj`.

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

## <a name="c-language-specification"></a>Спецификация языка C#
  
Подробные сведения см. в разделе [The is operator](~/_csharplang/spec/expressions.md#the-is-operator) (Оператор is) [спецификации языка C#](~/_csharplang/spec/introduction.md) и в следующих предложениях для языка C#:

- [Сопоставление шаблонов](~/_csharplang/proposals/csharp-7.0/pattern-matching.md)
- [Сопоставление шаблонов с универсальными шаблонами](~/_csharplang/proposals/csharp-7.1/generics-pattern-match.md)
  
## <a name="see-also"></a>См. также

- [справочник по C#](../index.md)
- [Ключевые слова C#](index.md)
- [Операторы приведения и тестирования типов](../operators/type-testing-and-cast.md)
