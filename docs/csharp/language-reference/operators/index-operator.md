---
title: Оператор [] (Справочник по C#)
ms.date: 07/20/2015
f1_keywords:
- '[]_CSharpKeyword'
helpviewer_keywords:
- subscript operator [C#]
- square brackets [ ] operator [C#]
- '[] operator [C#]'
- indexing operator [C#]
ms.assetid: 5c16bb45-88f7-45ff-b42c-1af1972b042c
ms.openlocfilehash: 65908bb3bcd8912ef81fc094e5958ae8dc4ae1f1
ms.sourcegitcommit: 60645077dc4b62178403145f8ef691b13ffec28e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/10/2018
ms.locfileid: "37961449"
---
# <a name="-operator-c-reference"></a>Оператор [] (Справочник по C#)
Квадратные скобки (`[]`) используются для массивов, индексаторов и атрибутов. Кроме того, их можно использовать с указателями.  
  
## <a name="remarks"></a>Примечания  
 Тип массива указывается перед оператором `[]`:  
  
 [!code-csharp[csRefOperators#43](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_1.cs)]  
  
 Для доступа к элементу массива его индекс необходимо заключить в скобки:  
  
 [!code-csharp[csRefOperators#44](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_2.cs)]  
  
 Если индекс массива выходит за границы диапазона, создается исключение.  
  
 Перегрузка оператора индексирования массива невозможна. Однако типы могут определять индексаторы и свойства, принимающие один или несколько параметров. Параметры индексатора заключаются в квадратные скобки, как и индексы массива, но, в отличие от индексов массива, которые должны быть целочисленными, эти параметры могут быть любого типа.  
  
 Например, в платформе .NET Framework определен тип `Hashtable`, связывающий ключи и значения произвольного типа.  
  
 [!code-csharp[csRefOperators#45](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_3.cs)]  
  
 Кроме того, квадратные скобки используются для определения [атрибутов](../../../csharp/programming-guide/concepts/attributes/index.md):  
  
 [!code-csharp[csRefOperators#46](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_4.cs)]  
  
 Квадратные скобки можно использовать для создания индекса на основе указателя:  
  
 [!code-csharp[csRefOperators#47](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_5.cs)]  
  
 Проверка границ не выполняется.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Справочник по C#](../../../csharp/language-reference/index.md)  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
 [Операторы в C#](../../../csharp/language-reference/operators/index.md)  
 [Массивы](../../../csharp/programming-guide/arrays/index.md)  
 [Индексаторы](../../../csharp/programming-guide/indexers/index.md)  
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
 [Оператор fixed](../../../csharp/language-reference/keywords/fixed-statement.md)
