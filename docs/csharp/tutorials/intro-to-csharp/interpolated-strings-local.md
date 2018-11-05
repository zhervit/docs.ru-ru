---
title: Интерполяция строк. Руководство по C#
description: В этом руководстве показано, как использовать функцию интерполяции строк в C# для включения форматированных результатов выражений в строку.
author: rpetrusha
ms.author: ronpet
ms.date: 10/23/2018
ms.openlocfilehash: 7308254ec691df6ec2d5b54d3770afb825886e29
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198590"
---
# <a name="use-string-interpolation-to-construct-formatted-strings"></a><span data-ttu-id="87905-103">Создание форматированных строк с помощью интерполяции</span><span class="sxs-lookup"><span data-stu-id="87905-103">Use string interpolation to construct formatted strings</span></span>

<span data-ttu-id="87905-104">В этом руководстве объясняется, как с помощью [интерполяции строк](../../language-reference/tokens/interpolated.md) в C# вставить значения в одну результирующую строку.</span><span class="sxs-lookup"><span data-stu-id="87905-104">This tutorial teaches you how to use C# [string interpolation](../../language-reference/tokens/interpolated.md) to insert values into a single result string.</span></span> <span data-ttu-id="87905-105">Вы напишете код C# и сможете просмотреть результаты его компиляции и выполнения.</span><span class="sxs-lookup"><span data-stu-id="87905-105">You write C# code and see the results of compiling and running it.</span></span> <span data-ttu-id="87905-106">Это руководство содержит ряд уроков по вставке значений в строки и форматированию этих значений различными способами.</span><span class="sxs-lookup"><span data-stu-id="87905-106">The tutorial contains a series of lessons that show you how to insert values into a string and format those values in different ways.</span></span>

<span data-ttu-id="87905-107">Для работы с этим руководством вам потребуется компьютер, который можно использовать для разработки.</span><span class="sxs-lookup"><span data-stu-id="87905-107">This tutorial expects that you have a machine you can use for development.</span></span> <span data-ttu-id="87905-108">В руководстве по [началу работы с .NET за 10 минут](https://www.microsoft.com/net/core) содержатся инструкции по настройке локальной среды разработки на компьютерах Mac, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="87905-108">The .NET topic [Get Started in 10 minutes](https://www.microsoft.com/net/core) has instructions for setting up your local development environment on Mac, PC or Linux.</span></span> <span data-ttu-id="87905-109">Краткий обзор команд, которые будут здесь использоваться, и ссылки на дополнительные сведения представлены во [вводной статье к руководствам по локальной разработке](local-environment.md).</span><span class="sxs-lookup"><span data-stu-id="87905-109">A quick overview of the commands you'll use is in [introduction to the local tutorials](local-environment.md), with links to more details.</span></span> <span data-ttu-id="87905-110">Вы также можете воспользоваться [интерактивной версией](interpolated-strings.yml) этого руководства в браузере.</span><span class="sxs-lookup"><span data-stu-id="87905-110">You also can complete the [interactive version](interpolated-strings.yml) of this tutorial in your browser.</span></span>

## <a name="create-an-interpolated-string"></a><span data-ttu-id="87905-111">Создание интерполированной строки</span><span class="sxs-lookup"><span data-stu-id="87905-111">Create an interpolated string</span></span>

<span data-ttu-id="87905-112">Создайте каталог с именем **interpolated**.</span><span class="sxs-lookup"><span data-stu-id="87905-112">Create a directory named **interpolated**.</span></span> <span data-ttu-id="87905-113">Сделайте его текущим, выполнив следующую команду в окне консоли:</span><span class="sxs-lookup"><span data-stu-id="87905-113">Make it the current directory and run the following command from a console window:</span></span>

```console
dotnet new console
```

<span data-ttu-id="87905-114">Эта команда создает консольное приложение .NET Core в текущем каталоге.</span><span class="sxs-lookup"><span data-stu-id="87905-114">This command creates a new .NET Core console application in the current directory.</span></span>

<span data-ttu-id="87905-115">Откройте файл **Program.cs** в любом редакторе и замените строку `Console.WriteLine("Hello World!");` следующим кодом, указав вместо `<name>` свое имя:</span><span class="sxs-lookup"><span data-stu-id="87905-115">Open **Program.cs** in your favorite editor, and replace the line `Console.WriteLine("Hello World!");` with the following code, where you replace `<name>` with your name:</span></span>

```csharp
var name = "<name>";
Console.WriteLine($"Hello, {name}. It's a pleasure to meet you!");
```

<span data-ttu-id="87905-116">Чтобы выполнить этот код, введите `dotnet run` в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="87905-116">Try this code by typing `dotnet run` in your console window.</span></span> <span data-ttu-id="87905-117">При запуске программы отображается одна строка, которая содержит ваше имя в приветствии.</span><span class="sxs-lookup"><span data-stu-id="87905-117">When you run the program, it displays a single string that includes your name in the greeting.</span></span> <span data-ttu-id="87905-118">Строка, включенная в вызов метода <xref:System.Console.WriteLine%2A>, является *интерполированной*.</span><span class="sxs-lookup"><span data-stu-id="87905-118">The string included in the <xref:System.Console.WriteLine%2A> method call is an *interpolated string*.</span></span> <span data-ttu-id="87905-119">Это похоже на шаблон, позволяющий создать одну строку (называемую *результирующей строкой*) из строки, содержащей внедренный код.</span><span class="sxs-lookup"><span data-stu-id="87905-119">It's a kind of template that lets you construct a single string (called the *result string*) from a string that includes embedded code.</span></span> <span data-ttu-id="87905-120">Интерполированные строки особенно удобны при вставке значений в строку или сцеплении (объединении) строк.</span><span class="sxs-lookup"><span data-stu-id="87905-120">Interpolated strings are particularly useful for inserting values into a string or concatenating (joining together) strings.</span></span>

<span data-ttu-id="87905-121">Этот простой пример содержит два элемента, обязательные для каждой интерполированной строки:</span><span class="sxs-lookup"><span data-stu-id="87905-121">This simple example contains the two elements that every interpolated string must have:</span></span>

- <span data-ttu-id="87905-122">Строковый литерал, который начинается с символа `$`, стоящего до открывающей кавычки.</span><span class="sxs-lookup"><span data-stu-id="87905-122">A string literal that begins with the `$` character before its opening quotation mark character.</span></span> <span data-ttu-id="87905-123">Между символом `$` и знаком кавычки не должно быть пробелов.</span><span class="sxs-lookup"><span data-stu-id="87905-123">There can't be any spaces between the `$` symbol and the quotation mark character.</span></span> <span data-ttu-id="87905-124">(Если вы хотите узнать, что при этом случится, вставьте пробел после символа `$`, сохраните файл и снова запустите программу, введя `dotnet run` в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="87905-124">(If you'd like to see what happens if you include one, insert a space after the `$` character, save the file, and run the program again by typing `dotnet run` in the console window.</span></span> <span data-ttu-id="87905-125">Компилятор C# отображает сообщение "Ошибка CS1056. Непредвиденный знак "$"".)</span><span class="sxs-lookup"><span data-stu-id="87905-125">The C# compiler displays an error message, "error CS1056: Unexpected character '$'".)</span></span>

- <span data-ttu-id="87905-126">Одно или несколько *интерполированных выражений*.</span><span class="sxs-lookup"><span data-stu-id="87905-126">One or more *interpolated expressions*.</span></span> <span data-ttu-id="87905-127">Интерполированное выражение обозначено открывающей и закрывающей фигурной скобкой (`{` и `}`).</span><span class="sxs-lookup"><span data-stu-id="87905-127">An interpolated expression is indicated by an opening and closing brace (`{` and `}`).</span></span> <span data-ttu-id="87905-128">Вы можете указать внутри фигурных скобок любое выражение C#, возвращающее значение (включая `null`).</span><span class="sxs-lookup"><span data-stu-id="87905-128">You can put any C# expression that returns a value (including `null`) inside the braces.</span></span>

<span data-ttu-id="87905-129">Давайте рассмотрим еще несколько примеров интерполяции строк с другими типами данных.</span><span class="sxs-lookup"><span data-stu-id="87905-129">Let's try a few more string interpolation examples with some other data types.</span></span>

## <a name="include-different-data-types"></a><span data-ttu-id="87905-130">Включение разных типов данных</span><span class="sxs-lookup"><span data-stu-id="87905-130">Include different data types</span></span>

<span data-ttu-id="87905-131">В предыдущем разделе вы использовали интерполяцию строк для вставки одной строки внутрь другой.</span><span class="sxs-lookup"><span data-stu-id="87905-131">In the previous section, you used string interpolation to insert one string inside of another.</span></span> <span data-ttu-id="87905-132">Однако интерполированное выражение может относиться к любому типу данных.</span><span class="sxs-lookup"><span data-stu-id="87905-132">The result of an interpolated expression can be of any data type, though.</span></span> <span data-ttu-id="87905-133">Давайте включим в интерполированную строку значения разных типов данных.</span><span class="sxs-lookup"><span data-stu-id="87905-133">Let's include values of various data types in an interpolated string.</span></span>

<span data-ttu-id="87905-134">В приведенном ниже примере сначала мы определим тип данных для [класса](../../programming-guide/classes-and-structs/classes.md) `Vegetable`, обладающего [свойством](../../properties.md) `Name` и [методом](../../methods.md) `ToString`. Этот метод [переопределяет](../../language-reference/keywords/override.md) поведение метода <xref:System.Object.ToString?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="87905-134">In the following example, we first define a [class](../../programming-guide/classes-and-structs/classes.md) data type `Vegetable` that has a `Name` [property](../../properties.md) and a `ToString` [method](../../methods.md), which [overrides](../../language-reference/keywords/override.md) the behavior of the <xref:System.Object.ToString?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="87905-135">[Модификатор доступа ](../../language-reference/keywords/public.md)`public` делает этот метод доступным любому клиентскому коду и позволяет получить строковое представление экземпляра `Vegetable`.</span><span class="sxs-lookup"><span data-stu-id="87905-135">The [`public` access modifier](../../language-reference/keywords/public.md) makes that method available to any client code to get the string representation of a `Vegetable` instance.</span></span> <span data-ttu-id="87905-136">В нашем примере метод `Vegetable.ToString` возвращает значение свойства `Name`, которое инициализируется в [конструкторе](../../programming-guide/classes-and-structs/constructors.md) `Vegetable`.</span><span class="sxs-lookup"><span data-stu-id="87905-136">In the example the `Vegetable.ToString` method returns the value of the `Name` property that is initialized at the `Vegetable` [constructor](../../programming-guide/classes-and-structs/constructors.md):</span></span>

```csharp
public Vegetable(string name) => Name = name;
```

<span data-ttu-id="87905-137">Затем создайте экземпляр класса `Vegetable` с именем `item`. Для этого воспользуйтесь [ключевым словом`new`](../../language-reference/keywords/new-operator.md) и укажите параметр имени для конструктора `Vegetable`.</span><span class="sxs-lookup"><span data-stu-id="87905-137">Then we create an instance of the `Vegetable` class named `item` by using the [`new` keyword](../../language-reference/keywords/new-operator.md) and providing a name for the constructor `Vegetable`:</span></span>

```csharp
var item = new Vegetable("eggplant");
```

<span data-ttu-id="87905-138">Наконец, переменная `item` включается в интерполированную строку, которая также содержит значение <xref:System.DateTime>, значение <xref:System.Decimal> и значение [перечисления](../../programming-guide/enumeration-types.md) `Unit`.</span><span class="sxs-lookup"><span data-stu-id="87905-138">Finally, we include the `item` variable into an interpolated string that also contains a <xref:System.DateTime> value, a <xref:System.Decimal> value, and a `Unit` [enumeration](../../programming-guide/enumeration-types.md) value.</span></span> <span data-ttu-id="87905-139">Замените весь код C# в редакторе следующим кодом, а затем используйте команду `dotnet run`, чтобы запустить его:</span><span class="sxs-lookup"><span data-stu-id="87905-139">Replace all of the C# code in your editor with the following code, and then use the `dotnet run` command to run it:</span></span>

```csharp
using System;

public class Vegetable
{
   public Vegetable(string name) => Name = name;
   
   public string Name { get; }
   
   public override string ToString() => Name;
}

public class Program
{
   public enum Unit { item, kilogram, gram, dozen };

   public static void Main()
   {
      var item = new Vegetable("eggplant");
      var date = DateTime.Now;
      var price = 1.99m;
      var unit = Unit.item;
      Console.WriteLine($"On {date}, the price of {item} was {price} per {unit}.");
   }
}
```

<span data-ttu-id="87905-140">Обратите внимание на то, что интерполированное выражение `item` в интерполированной строке разрешается в текст "eggplant" в результирующей строке.</span><span class="sxs-lookup"><span data-stu-id="87905-140">Note that the interpolated expression `item` in the interpolated string resolves to the text "eggplant" in the result string.</span></span> <span data-ttu-id="87905-141">Связано это с тем, что если результат выражения не имеет строковый тип, он разрешается в строку описанным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="87905-141">That's because, when the type of the expression result is not a string, the result is resolved to a string in the following way:</span></span>

- <span data-ttu-id="87905-142">Если результатом вычисления интерполированного выражения является `null`, используется пустая строка ("" или <xref:System.String.Empty?displayProperty=nameWithType>).</span><span class="sxs-lookup"><span data-stu-id="87905-142">If the interpolated expression evaluates to `null`, an empty string ("", or <xref:System.String.Empty?displayProperty=nameWithType>) is used.</span></span>

- <span data-ttu-id="87905-143">Если результатом вычисления интерполированного выражения не является `null`, обычно вызывается метод `ToString` результирующего типа.</span><span class="sxs-lookup"><span data-stu-id="87905-143">If the interpolated expression doesn't evaluate to `null`, typically the `ToString` method of the result type is called.</span></span> <span data-ttu-id="87905-144">Чтобы проверить это, можно изменить реализацию метода `Vegetable.ToString`.</span><span class="sxs-lookup"><span data-stu-id="87905-144">You can test this by updating the implementation of the `Vegetable.ToString` method.</span></span> <span data-ttu-id="87905-145">Возможно, вам вообще не потребуется реализовывать метод `ToString`, так как его реализация в той или иной форме присутствует в каждом типе.</span><span class="sxs-lookup"><span data-stu-id="87905-145">You might not even need to implement the `ToString` method since every type has some implementation of this method.</span></span> <span data-ttu-id="87905-146">Это можно проверить, закомментировав определение метода `Vegetable.ToString` в примере, для чего перед ним нужно поставить символ комментария (`//`).</span><span class="sxs-lookup"><span data-stu-id="87905-146">To test this, comment out the definition of the `Vegetable.ToString` method in the example (to do that, put a comment symbol, `//`, in front of it).</span></span> <span data-ttu-id="87905-147">В выходных данных строка "eggplant" заменяется полным именем типа ("Vegetable" в этом примере), что является стандартным поведением метода <xref:System.Object.ToString?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="87905-147">In the output, the string "eggplant" is replaced by the fully qualified type name ("Vegetable" in this example), which is the default behavior of the <xref:System.Object.ToString?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="87905-148">По умолчанию метод `ToString` возвращает для значения перечисления строковое представление значения.</span><span class="sxs-lookup"><span data-stu-id="87905-148">The default behavior of the `ToString` method for an enumeration value is to return the string representation of the value.</span></span>

<span data-ttu-id="87905-149">В выходных данных этого примера дата является слишком точной (цена на баклажаны не меняется каждую секунду), а в значении цены не указана единица валюты.</span><span class="sxs-lookup"><span data-stu-id="87905-149">In the output from this example, the date is too precise (the price of eggplant doesn't change every second), and the price value doesn't indicate a unit of currency.</span></span> <span data-ttu-id="87905-150">В следующем разделе вы узнаете, как устранить эти проблемы, управляя форматом строковых представлений результатов выражений.</span><span class="sxs-lookup"><span data-stu-id="87905-150">In the next section, you'll learn how to fix those issues by controlling the format of string representations of the expression results.</span></span>

## <a name="control-the-formatting-of-interpolated-expressions"></a><span data-ttu-id="87905-151">Управление форматированием интерполированных выражений</span><span class="sxs-lookup"><span data-stu-id="87905-151">Control the formatting of interpolated expressions</span></span>

<span data-ttu-id="87905-152">В предыдущем разделе мы вставили две неправильно отформатированные строки в результирующую строку.</span><span class="sxs-lookup"><span data-stu-id="87905-152">In the previous section, two poorly formatted strings were inserted into the result string.</span></span> <span data-ttu-id="87905-153">Первая была значением даты и времени, при этом допустимой была только дата.</span><span class="sxs-lookup"><span data-stu-id="87905-153">One was a date and time value for which only the date was appropriate.</span></span> <span data-ttu-id="87905-154">Вторая была ценой, в которой отсутствовала единица валюты.</span><span class="sxs-lookup"><span data-stu-id="87905-154">The second was a price that didn't indicate its unit of currency.</span></span> <span data-ttu-id="87905-155">Обе эти проблемы легко решить.</span><span class="sxs-lookup"><span data-stu-id="87905-155">Both issues are easy to address.</span></span> <span data-ttu-id="87905-156">Интерполяция строк позволяет указывать *строки формата*, управляющие форматированием определенных типов.</span><span class="sxs-lookup"><span data-stu-id="87905-156">String interpolation lets you specify *format strings* that control the formatting of particular types.</span></span> <span data-ttu-id="87905-157">Измените вызов `Console.WriteLine` из предыдущего примера, включив в него строки формата для выражений даты и цены, как показано в следующей строке:</span><span class="sxs-lookup"><span data-stu-id="87905-157">Modify the call to `Console.WriteLine` from the previous example to include the format strings for the date and price expressions as shown in the following line:</span></span>

```csharp
Console.WriteLine($"On {date:d}, the price of {item} was {price:C2} per {unit}.");
```

<span data-ttu-id="87905-158">Задайте строку формата, указав ее после интерполированного выражения через точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="87905-158">You specify a format string by following the interpolated expression with a colon (":") and the format string.</span></span> <span data-ttu-id="87905-159">"d" — это [стандартная строка формата для даты и времени](../../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier), представляющая краткий формат.</span><span class="sxs-lookup"><span data-stu-id="87905-159">"d" is a [standard date and time format string](../../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier) that represents the short date format.</span></span> <span data-ttu-id="87905-160">"C2" — это [стандартная строка числового формата](../../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier), представляющая число в виде денежной единицы с точностью два знака после запятой.</span><span class="sxs-lookup"><span data-stu-id="87905-160">"C2" is a  [standard numeric format string](../../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier) that represents a number as a currency value with two digits after the decimal point.</span></span>

<span data-ttu-id="87905-161">Некоторые типы в библиотеках .NET поддерживают предопределенный набор строк формата.</span><span class="sxs-lookup"><span data-stu-id="87905-161">A number of types in the .NET libraries support a predefined set of format strings.</span></span> <span data-ttu-id="87905-162">К ним относятся все числовые типы, а также типы даты и времени.</span><span class="sxs-lookup"><span data-stu-id="87905-162">These include all the numeric types and the date and time types.</span></span> <span data-ttu-id="87905-163">Полный список типов, поддерживающих строки формата, см. в разделе [Строки формата и типы библиотек классов .NET](../../../standard/base-types/formatting-types.md#stringRef) статьи [Типы форматирования в .NET](../../../standard/base-types/formatting-types.md).</span><span class="sxs-lookup"><span data-stu-id="87905-163">For a complete list of types that support format strings, see [Format Strings and .NET Class Library Types](../../../standard/base-types/formatting-types.md#stringRef) in the [Formatting Types in .NET](../../../standard/base-types/formatting-types.md) article.</span></span>

<span data-ttu-id="87905-164">Попробуйте изменить строки формата в текстовом редакторе, возвращаясь в программу после каждого изменения, чтобы узнать, как они влияют на форматирование даты и времени, а также числового значения.</span><span class="sxs-lookup"><span data-stu-id="87905-164">Try modifying the format strings in your text editor and, each time you make a change, rerun the program to see how the changes affect the formatting of the date and time and the numeric value.</span></span> <span data-ttu-id="87905-165">Измените "d" в `{date:d}` на "t" (чтобы отобразить краткий формат времени), "y" (чтобы отобразить год и месяц) и "yyyy" (чтобы отобразить год в виде четырехзначного числа).</span><span class="sxs-lookup"><span data-stu-id="87905-165">Change the "d" in `{date:d}` to "t" (to display the short time format), "y" (to display the year and month), and "yyyy" (to display the year as a four-digit number).</span></span> <span data-ttu-id="87905-166">Измените "C2" в `{price:C2}` на "e" (для экспоненциального представления) и "F3" (чтобы получить числовое значение с тремя знаками после запятой).</span><span class="sxs-lookup"><span data-stu-id="87905-166">Change the "C2" in `{price:C2}` to "e" (for exponential notation) and "F3" (for a numeric value with three digits after the decimal point).</span></span>

<span data-ttu-id="87905-167">Кроме форматирования, вы можете управлять шириной поля и выравниванием для форматированных строк, включаемых в результирующую строку.</span><span class="sxs-lookup"><span data-stu-id="87905-167">In addition to controlling formatting, you can also control the field width and alignment of the formatted strings that are included in the result string.</span></span> <span data-ttu-id="87905-168">В следующем разделе вы научитесь это делать.</span><span class="sxs-lookup"><span data-stu-id="87905-168">In the next section, you'll learn how to do this.</span></span>

## <a name="control-the-field-width-and-alignment-of-interpolated-expressions"></a><span data-ttu-id="87905-169">Управление шириной поля и выравниванием для интерполированных выражений</span><span class="sxs-lookup"><span data-stu-id="87905-169">Control the field width and alignment of interpolated expressions</span></span>

<span data-ttu-id="87905-170">Как правило, когда результат интерполированного выражения форматируется как строка, эта строка включается в результирующую без начальных или конечных пробелов.</span><span class="sxs-lookup"><span data-stu-id="87905-170">Ordinarily, when the result of an interpolated expression is formatted to string, that string is included in a result string without leading or trailing spaces.</span></span> <span data-ttu-id="87905-171">Особенно когда вы работаете с набором данных, возможность управления шириной поля и выравниванием помогает получить более понятные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="87905-171">Particularly when you work with a set of data, being able to control a field width and text alignment helps to produce a more readable output.</span></span> <span data-ttu-id="87905-172">Чтобы увидеть это, замените весь код в текстовом редакторе следующим кодом, а затем введите `dotnet run` для выполнения программы:</span><span class="sxs-lookup"><span data-stu-id="87905-172">To see this, replace all the code in your text editor with the following code, then type `dotnet run` to execute the program:</span></span>

```csharp
using System;
using System.Collections.Generic;

public class Example
{
   public static void Main()
   {
      var titles = new Dictionary<string, string>()
      {
          ["Doyle, Arthur Conan"] = "Hound of the Baskervilles, The",
          ["London, Jack"] = "Call of the Wild, The",
          ["Shakespeare, William"] = "Tempest, The"
      };

      Console.WriteLine("Author and Title List");
      Console.WriteLine();
      Console.WriteLine($"|{"Author",-25}|{"Title",30}|");
      foreach (var title in titles)
         Console.WriteLine($"|{title.Key,-25}|{title.Value,30}|");
   }
}
```

<span data-ttu-id="87905-173">Имена авторов выровнены по левому краю, а названия их произведений — по правому.</span><span class="sxs-lookup"><span data-stu-id="87905-173">The names of authors are left-aligned, and the titles they wrote are right-aligned.</span></span> <span data-ttu-id="87905-174">Вы можете указать выравнивание, добавив запятую (",") после интерполированного выражения и назначив *минимальную* ширину поля.</span><span class="sxs-lookup"><span data-stu-id="87905-174">You specify the alignment by adding a comma (",") after an interpolated expression and designating the *minimum* field width.</span></span> <span data-ttu-id="87905-175">Если указанное значение является положительным числом, то поле выравнивается по правому краю.</span><span class="sxs-lookup"><span data-stu-id="87905-175">If the specified value is a positive number, the field is right-aligned.</span></span> <span data-ttu-id="87905-176">Если оно является отрицательным числом, то поле выравнивается по левому краю.</span><span class="sxs-lookup"><span data-stu-id="87905-176">If it is a negative number, the field is left-aligned.</span></span>

<span data-ttu-id="87905-177">Попробуйте удалить знаки "минус" из кода `{"Author",-25}` и `{title.Key,-25}`, а затем снова выполните пример, как показано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="87905-177">Try removing the negative signs from the `{"Author",-25}` and `{title.Key,-25}` code and run the example again, as the following code does:</span></span>

```csharp
Console.WriteLine($"|{"Author",25}|{"Title",30}|");
foreach (var title in titles)
   Console.WriteLine($"|{title.Key,25}|{title.Value,30}|");
```

<span data-ttu-id="87905-178">На этот раз сведения об авторе выровнены по правому краю.</span><span class="sxs-lookup"><span data-stu-id="87905-178">This time, the author information is right-aligned.</span></span>

<span data-ttu-id="87905-179">Вы можете совмещать описатель выравнивания и строку формата в одном интерполированном выражении.</span><span class="sxs-lookup"><span data-stu-id="87905-179">You can combine an alignment specifier and a format string for a single interpolated expression.</span></span> <span data-ttu-id="87905-180">Для этого сначала укажите выравнивание, а затем через двоеточие строку формата.</span><span class="sxs-lookup"><span data-stu-id="87905-180">To do that, specify the alignment first, followed by a colon and the format string.</span></span> <span data-ttu-id="87905-181">Замените весь код внутри метода `Main` приведенным ниже кодом, который отображает три отформатированные строки с заданной шириной поля.</span><span class="sxs-lookup"><span data-stu-id="87905-181">Replace all of the code inside the `Main` method with the following code, which displays three formatted strings with defined field widths.</span></span> <span data-ttu-id="87905-182">Запустите программу, введя команду `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="87905-182">Then run the program by entering the `dotnet run` command.</span></span>

```csharp
Console.WriteLine($"[{DateTime.Now,-20:d}] Hour [{DateTime.Now,-10:HH}] [{1063.342,15:N2}] feet");
```

<span data-ttu-id="87905-183">Выходные данные выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="87905-183">The output looks something like the following:</span></span>

```console
[04/14/2018          ] Hour [16        ] [       1,063.34] feet
```

<span data-ttu-id="87905-184">Вы завершили работу с руководством по интерполяции строк.</span><span class="sxs-lookup"><span data-stu-id="87905-184">You've completed the string interpolation tutorial.</span></span>

<span data-ttu-id="87905-185">Теперь вы можете выполнить задачи руководства по [коллекциям в виде списков](arrays-and-collections.md) в своей среде разработки.</span><span class="sxs-lookup"><span data-stu-id="87905-185">You can continue with the [List collection](arrays-and-collections.md) tutorial in your own development environment.</span></span>

<span data-ttu-id="87905-186">Дополнительные сведения об интерполяции строк см. в разделе [Интерполяция строк](../../language-reference/tokens/interpolated.md) и в руководстве [Интерполяция строк в C#](../../tutorials/string-interpolation.md).</span><span class="sxs-lookup"><span data-stu-id="87905-186">For more information, see the [String interpolation](../../language-reference/tokens/interpolated.md) topic and the [String interpolation in C#](../../tutorials/string-interpolation.md) tutorial.</span></span>