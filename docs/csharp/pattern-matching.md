---
title: Сопоставление шаблонов | Руководство по C#
description: Сведения о выражениях сопоставления шаблонов в C#
ms.date: 01/24/2017
ms.assetid: 1e575c32-2e2b-4425-9dca-7d118f3ed15b
ms.openlocfilehash: 635ab45c89a38f3dedac2d60ea1e31ebf394c9b2
ms.sourcegitcommit: 2ad7d06f4f469b5d8a5280ac0e0289a81867fc8e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2018
ms.locfileid: "35231480"
---
# <a name="pattern-matching"></a>Сопоставление шаблонов #

Шаблоны проверяют, содержит ли значение определенную *фигуру* и может ли оно *извлекать* сведения из значения с соответствующей фигурой. Сопоставление шаблонов позволяет использовать сокращенный синтаксис для тех алгоритмов, которые вы уже применяете. Вы уже создали алгоритмы сопоставления шаблонов с помощью существующего синтаксиса. Для проверки значений можно написать операторы `if` и `switch`. Если операторы совпадают, данные из этого значения извлекаются и используются. Новые элементы синтаксиса — это расширения для операторов, с которыми вы уже знакомы: `is` и `switch`. В этих расширениях объединяются проверка значения и извлечение данных.

В данном разделе мы рассмотрим новый синтаксис и покажем, как с его помощью можно создавать удобочитаемый, краткий код. Сопоставление шаблонов включает идиомы, в которых данные и код отделены, в отличие от объектно-ориентированных структур, в которых данные и методы манипуляции с данными тесно связаны.

Чтобы проиллюстрировать новые идиомы, поработаем со структурами, представляющими геометрические фигуры, применив операторы сопоставления шаблонов. Вы должны уже знать, как строить иерархии классов и создавать [виртуальные и переопределенные методы](methods.md#inherited) и настраивать поведение объектов исходя из их типа среды выполнения.

Эти методы недоступны для данных, не структурированных в иерархии классов. Если данные отделены от методов, вам потребуются другие инструменты. Новые конструкции *сопоставления шаблонов* включают более четкий синтаксис для проверки данных и манипуляций с потоком управления с учетом условий этих данных. Вы уже писали операторы `if` и `switch`, тестирующие значение переменной, и операторы `is`, проверяющие тип переменной. *Сопоставление шаблонов* расширяет возможности этих операторов.

В этом разделе мы создадим метод, вычисляющий площадь различных геометрических фигур. Однако при этом мы не будем применять повторную сортировку в объектно-ориентированные методы и собирать иерархию классов для разных форм.
Вместо этого прибегнем к *сопоставлению шаблонов*. Чтобы дополнительно подчеркнуть тот факт, что наследование не используется, каждая форма у нас будет не классом, а `struct`. Обратите внимание на то, что разные типы `struct` не могут определять общий пользовательский базовый тип, поскольку наследование использовать нельзя.
Изучите этот пример и сравните код с его возможной структурой в виде иерархии объектов. Данные, которые вам необходимо запрашивать и использовать при выполнении операций, не являются иерархией классов; сопоставление шаблонов позволяет создавать удобные структуры.

Вместо того, чтобы начать с абстрактного определения фигуры и добавления различных конкретных классов фигур, составим для каждой геометрической фигуры определения, содержащие только простые данные:

[!code-csharp[ShapeDefinitions](../../samples/csharp/PatternMatching/Shapes.cs#01_ShapeDefinitions "Shape definitions")]

Опираясь на эти структуры, напишем метод, вычисляющий площадь определенной фигуры.

## <a name="the-is-type-pattern-expression"></a>Выражение шаблона для типа `is`

До выхода C# 7.0 каждый тип необходимо было тестировать в ряде операторов `if` и `is`:

[!code-csharp[ClassicIsExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#02_ClassicIsExpression "Classic type pattern using is")]

Приведенный выше код представляет собой классическое выражение *шаблона типа*: он тестирует переменную, чтобы определить ее тип, и выполняет различные действия с учетом этого типа.

Код упрощается за счет расширений, которые добавляются в выражение `is` для назначения переменной в случае успешного завершения теста:

[!code-csharp[IsPatternExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#03_IsPatternExpression "is pattern expression")]

В этой обновленной версии выражение `is` и проверяет переменную, и присваивает ее новой переменной соответствующего типа. Обратите внимание также на то, что эта версия включает тип `Rectangle`, который представляет собой `struct`. Новое выражение `is` работает и с типами значений, и со ссылочными типами.

Правила языка для выражений сопоставления шаблонов защищают от неправильного использования результатов примененного выражения match. В приведенном выше примере переменные `s`, `c` и `r` находятся в области действия и назначаются явно, только если соответствующие выражения сопоставления шаблонов содержат результат `true`. При попытке использовать одну из этих переменных в другом месте кода возникнут ошибки компилятора.

Рассмотрим оба эти правила подробно, начиная с области действия. Переменная `c` находится в области действия только в ветви `else` первого оператора `if`. Переменная `s` находится в области действия в методе `ComputeAreaModernIs`. Это связано с тем, что каждая ветвь оператора `if` задает отдельную область действия для переменных. Сам оператор `if` это не делает. Это значит, что переменные, объявленные в операторе `if`, находятся в той же области действия, что и оператор `if` (в данном случае это метод). Такое поведение не связано с сопоставлением шаблонов, но представляет собой поведение, определенное для области действия переменных и операторов `if` и `else`.

Переменные `c` и `s` назначаются, если соответствующие операторы `if` имеют значение true, поскольку явно назначаются при использовании механизма true.

> [!TIP]
> Примеры в этом разделе включают рекомендуемую конструкцию, в которой выражение сопоставления шаблонов `is` явно назначает переменную сопоставления в ветви `true` оператора `if`.
> Эту логику можно изменить, указав `if (!(shape is Square s))`, после чего переменная `s` будет явно назначаться только в ветви `false`. В C# это допустимо, но не рекомендуется, поскольку в этом случае логику проследить сложно.

Эти правила защищают от случайного доступа к результату выражения сопоставления шаблонов в отсутствие соответствия.

## <a name="using-pattern-matching-switch-statements"></a>Использование операторов сопоставления шаблонов `switch`

Со временем вам может потребоваться поддержка других типов фигур. Чем больше условий нужно проверять, тем более громоздкими становятся выражения сопоставления шаблонов `is`. Кроме того, что для каждого проверяемого типа требуются операторы `if`, выражения `is` позволяют осуществлять тестирование, только если входные данные соответствуют одному типу. В этом случае лучше отдать предпочтение выражениям сопоставления шаблонов `switch`. 

Традиционный оператор `switch` был выражением шаблона: он поддерживал шаблон константы.
Переменную можно сравнивать с любой константой в операторе `case`:

[!code-csharp[ClassicSwitch](../../samples/csharp/PatternMatching/GeometricUtilities.cs#04_ClassicSwitch "Classic switch statement")]

Единственным шаблоном, который поддерживался оператором `switch`, был шаблон константы. Кроме того, он ограничивался числовыми типами и типом `string`.
Эти ограничения были устранены, и теперь оператор `switch` можно записывать, используя шаблон типа:

[!code-csharp[Switch Type Pattern](../../samples/csharp/PatternMatching/GeometricUtilities.cs#05_SwitchTypePattern "Compute with `switch` expression")]

В операторе сопоставления шаблона `switch` используется синтаксис, знакомый тем разработчикам, которые имели дело с традиционным для C оператором `switch`. Вычисляется каждый оператор `case`, и выполняется код, лежащий в основе условия, которое соответствует входной переменной. Выполнение кода не может передаваться из одного выражения в следующее; синтаксис оператора `case` требует, чтобы каждый оператор `case` всегда заканчивался на `break`, `return` или `goto`.

> [!NOTE]
> Операторы `goto` для перехода к другой метке доступны только для шаблона с константами (классический оператор switch).

Теперь оператор `switch` регулируют два новых правила. Ограничения на тип переменной в выражении `switch` удалены.
Можно использовать любой тип, как, например, `object` в этом примере. Выражения case больше не ограничиваются постоянными значениями. Устранение этого ограничения означает, что изменение в порядке следования разделов `switch` может изменить поведение программы.

При ограничении постоянными значениями значению выражения `switch` может соответствовать только одна метка `case`. В сочетании с правилом, запрещающим передавать все разделы `switch` в следующий раздел, это означало, что разделы `switch` можно было располагать в любом порядке, не влияя на поведение программы.
Теперь, когда выражения `switch` стали более обобщенными, порядок разделов имеет значение. Выражения `switch` вычисляются в алфавитном порядке. Выполнение переходит к первой метке `switch`, соответствующей выражению `switch`.  
Обратите внимание на то, что вариант `default` будет выполнен только в отсутствие совпадений с метками других вариантов. Вариант `default` вычисляется последним, независимо от его текстуального порядка. Если варианта `default` нет и ни с одним другим оператором `case` совпадение не обнаружено, выполнение продолжается с оператора, следующего за оператором `switch`. Ни один код с меткой `case` не выполняется.

## <a name="when-clauses-in-case-expressions"></a>Предложения `when` в выражениях `case`

Для фигур с нулевой площадью можно создать специальные варианты, вставив предложение `when` в метку `case`. Квадрат с длиной стороны 0 или круг с радиусом 0 имеют нулевую площадь. Это условие задается с помощью предложения `when` в метке `case`:  

[!code-csharp[ComputeDegenerateShapes](../../samples/csharp/PatternMatching/GeometricUtilities.cs#07_ComputeDegenerateShapes "Compute shapes with 0 area")]

Это изменение демонстрирует несколько важных моментов, связанных с новым синтаксисом. Во-первых, к одному разделу `switch` можно применить сразу несколько меток `case`. Этот блок оператора выполняется, если одна из этих меток — `true`. В данном случае если выражение `switch` представляет круг или квадрат с нулевой площадью, метод возвращает константу 0.

В этом примере представлены две различные переменные в двух метках `case` для первого блока `switch`. Обратите внимание на то, что операторы в этом блоке `switch` не включают переменные `c` (для круга) или `s` (для квадрата).
Ни одна из этих переменных не назначается в этом блоке `switch` явно.
Разумеется, в случае совпадения с одним из вариантов одна из переменных назначается.
При этом сказать, *какая* из них была назначена во время компиляции, нельзя, поскольку во время выполнения возможно совпадение с любым из этих вариантов. В связи с этим в большинстве случаев, когда для одного и того же блока задается сразу несколько меток `case`, новую переменную вводить в оператор `case` не следует, иначе будет использоваться только переменная в предложении `when`.

Теперь, когда мы добавили формы с нулевой площадью, добавим еще пару типов фигур — прямоугольник и треугольник:

[!code-csharp[AddRectangleAndTriangle](../../samples/csharp/PatternMatching/GeometricUtilities.cs#09_AddRectangleAndTriangle "Add rectangle and triangle")]

 Этот набор изменений добавляет метки `case` для вырожденного варианта, а также метки и блоки для каждой из новых фигур. 

Наконец, можно добавить вариант `null`, чтобы в качестве аргумента не использовался `null`:

[!code-csharp[NullCase](../../samples/csharp/PatternMatching/GeometricUtilities.cs#10_NullCase "Add null case")]

Особый случай с шаблоном `null` интересен тем, что константа `null` в этом шаблоне не имеет типа, но может быть преобразована в любой ссылочный тип или тип, допускающий значение NULL. Вместо того, чтобы преобразовывать значение `null` в любой тип, в языке определяется, что значение `null` не будет соответствовать какому-либо шаблону типа, независимо от типа переменной во время компиляции. Такой подход позволяет обеспечить согласованность нового шаблона типа на основе `switch` с оператором `is`: операторы `is` всегда возвращают значение `false`, если проверяемое значение равно `null`. Более того, это проще, поскольку после проверки типа не требуется дополнительно выполнять проверку на значения NULL. Это видно из того факта, что в приведенном выше примере ни в одном блоке case не выполняется проверка на значения NULL. Это излишне, поскольку сопоставление с шаблоном типа уже гарантирует отсутствие значения NULL.

## <a name="var-declarations-in-case-expressions"></a>Объявления `var` в выражениях `case`

Вследствие введения `var` в качестве одного из выражений сопоставления начинают действовать новые правила в отношении сопоставления шаблонов.

Первое правило заключается в том, что объявление `var` подчиняется обычным правилам определения типа: тип определяется как статический тип выражения выбора вариантов. Согласно этому правилу, тип всегда является соответствующим.

Второе правило заключается в том, что в объявлении `var` нет проверки значения NULL, которая предусмотрена в других выражениях шаблона для типа. Это означает, что переменная может иметь значение NULL и в этом случае требуется проверка значения NULL.

Из этих двух правил следует, что во многих случаях объявление `var` в выражении `case` соответствует тем же условиям, что и выражение `default`.
Так как любой вариант, отличный от варианта по умолчанию, предпочтительнее варианта `default`, вариант `default` никогда не выполняется.

> [!NOTE]
> Компилятор не выдает предупреждения в случаях, когда вариант `default` записан, но не выполняется. Это согласуется с текущим поведением оператора `switch`, когда перечислены все возможные варианты.

Третье правило относится к случаям, когда может быть полезен вариант `var`. Предположим, производится сопоставление шаблона, причем входные данные представляют собой строку и нужно найти известные значения команд. Код может выглядеть так:

[!code-csharp[VarCaseExpression](../../samples/csharp/PatternMatching/Program.cs#VarCaseExpression "use a var case expression to filter white space")]

Вариант `var` соответствует `null`, пустой строке или любой строке, которая содержит только пробелы. Обратите внимание на то, что в приведенном выше коде используется оператор `?.`, чтобы случайно не произошло исключение <xref:System.NullReferenceException>. Вариант `default` обрабатывает все остальные строковые значения, которые не распознает этот анализатор команд.

Это один из примеров ситуации, в которой может требоваться выражение для варианта выбора `var`, отличное от выражения `default`.

## <a name="conclusions"></a>Выводы

*Конструкции сопоставления шаблонов* позволяют легко управлять потоком управления между различными переменными и типами, не связанными иерархией наследования. Логику управления можно настроить на использование любого условия, которое вы тестируете в переменной. Она включает шаблоны и идиомы, которые вам потребуются при создании более распределенных приложений, в которых данные и методы манипуляции этими данными разделены. Как видите, структуры фигур в этом примере не включают никакие методы, только свойства, доступные исключительно для чтения.
Сопоставление шаблонов работает с любым типом данных. Выражения записываются для изучения объекта и управления потоком управления решениями, которые принимаются на основе этих условий.

Сравните код из этого примера со структурой, которая начинается с создания иерархии классов для абстрактной фигуры `Shape` и ряда производных фигур, каждая из которых включает собственную реализацию виртуального метода для вычисления площади. Выражения сопоставления шаблонов часто полезны при работе с данными, если аспекты хранилища данных необходимо отделить от аспектов поведения.

