---
title: while (Справочник по C#)
ms.date: 05/28/2018
f1_keywords:
- while_CSharpKeyword
- while
helpviewer_keywords:
- while keyword [C#]
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
ms.openlocfilehash: c082107472ac53d05b3b43dd4d9d8afc508a16cb
ms.sourcegitcommit: bbf70abe6b46073148f78cbf0619de6092b5800c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34565869"
---
# <a name="while-c-reference"></a>while (Справочник по C#)

Оператор `while` выполняет оператор или блок операторов, пока определенное логическое выражение равно `true`. Так как это выражение оценивается перед каждым выполнением цикла, цикл `while` выполняется ноль или несколько раз. Это отличает его от цикла [do](do.md), который выполняется от одного до нескольких раз.

В любой точке блока операторов `while` можно разорвать цикл с помощью оператора [break](break.md).

Можно перейти непосредственно к оценке выражения `while`, воспользовавшись оператором [continue](continue.md). Если значение выражения оценивается как `true`, выполнение продолжается с первого оператора цикла. В противном случае выполнение продолжается с первого оператора после цикла.

Также можно выйти из цикла `while` с помощью операторов [goto](goto.md), [return](return.md) или [throw](throw.md).

## <a name="example"></a>Пример

В следующем примере показано применение оператора `while`. Нажмите **Запустить** для выполнения примера кода. После этого можно изменить код и запустить его еще раз.

[!code-csharp-interactive[while loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#3)]

## <a name="c-language-specification"></a>Спецификация языка C#

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>См. также

 [Справочник по C#](../index.md)  
 [Руководство по программированию на C#](../../programming-guide/index.md)  
 [Ключевые слова в C#](index.md)  
 [Оператор while (C++)](/cpp/cpp/while-statement-cpp)  
 [Операторы итерации](iteration-statements.md)  
 [Оператор do](do.md)  
