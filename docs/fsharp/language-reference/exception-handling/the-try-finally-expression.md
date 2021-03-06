---
title: 'Выражения: выражение try...finally (F#)'
description: 'Узнайте, как F # "try... finally" выражение дает возможность выполнить код очистки, даже если блок кода выдал исключение.'
ms.date: 05/16/2016
ms.openlocfilehash: a5fdec7b3986fc9a85c34b08d20dc31947c92b2e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33563497"
---
# <a name="exceptions-the-tryfinally-expression"></a>Выражения: выражение try...finally

`try...finally` Выражение дает возможность выполнить код очистки, даже если блок кода выдал исключение.


## <a name="syntax"></a>Синтаксис

```fsharp
try
    expression1
finally
    expression2
```

## <a name="remarks"></a>Примечания
`try...finally` Выражение можно использовать для выполнения кода в *expression2* приведенный выше синтаксис, независимо от того, создается ли исключение во время выполнения *expression1*.

Тип *expression2* не влияет на значение всего выражения; Если исключения не возникло, возвращаемым типом является последнее значение в *expression1*. При возникновении исключения, не имеет значения, и поток управления передает Далее соответствующего обработчика исключений в стек вызовов. Если не обнаруживается, выполнение программы прекращается. Перед выполнением кода в соответствующий обработчик или завершении работы программы, код в `finally` выполняет ветвь.

В следующем коде показано использование `try...finally` выражение.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5701.fs)]

Ниже приведен вывод на консоль.

```
Closing stream
Exception handled.
```

Как видно из выходных данных, поток был закрыт, прежде чем исключение было обработано и файл `test.txt` с текстом `test1`, указывающая, что буферы были записаны на диск и записываются на диск, несмотря на то, что исключение передаются Управление внешнему обработчику исключений.

Обратите внимание, что `try...with` конструкция — это отдельные конструкции `try...finally` построения. Таким образом Если код требует выполнения обоих `with` блока и `finally` блока, нужно вложить две конструкции, как показано в следующем примере кода.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5702.fs)]

В контексте вычисления выражений, включая выражения последовательностей и асинхронные рабочие потоки **try... finally** выражения могут иметь собственную реализацию. Дополнительные сведения см. в разделе [вычислительных выражениях](../computation-expressions.md).


## <a name="see-also"></a>См. также
[Обработка исключений](index.md)

[Исключения: выражение `try...with`](the-try-with-expression.md)
