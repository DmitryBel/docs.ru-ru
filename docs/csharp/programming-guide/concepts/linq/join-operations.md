---
title: Операции соединения (C#)
ms.date: 07/20/2015
ms.assetid: 5105e0da-1267-4c00-837a-f0e9602279b8
ms.openlocfilehash: caf93848450bcef35fef492985ef9703321b1dcb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33325348"
---
# <a name="join-operations-c"></a>Операции соединения (C#)
*Соединение* двух источников данных — это связь объектов в одном источнике данных с объектами, которые имеют общий атрибут в другом источнике данных.  
  
 Соединение является важной операцией в запросах, направленных на источники данных, отношения которых друг к другу нельзя отследить напрямую. В объектно-ориентированном программировании оно может означать корреляцию между немоделируемыми объектами, например такими, как обратное направление одностороннего отношения. Примером одностороннего отношения является класс Customer, имеющий свойство типа City (город), в то время как класс City не имеет свойства, которое является коллекцией объектов Customer (клиент). В случае наличия списка объектов City для поиска всех клиентов в каждом городе можно использовать операцию соединения.  
  
 На платформе LINQ представлены методы объединения <xref:System.Linq.Enumerable.Join%2A> и <xref:System.Linq.Enumerable.GroupJoin%2A>. Они выполняют эквисоединения, или соединения, которые сопоставляют два источника данных на основе равенства их ключей. (Для сравнения, Transact-SQL поддерживает операции соединения, отличные от оператора "равно", например оператор "меньше, чем".) В терминах реляционных баз данных <xref:System.Linq.Enumerable.Join%2A> реализует внутреннее соединение — тип соединения, в котором возвращаются только те объекты, у которых есть совпадения в другом наборе данных. Метод <xref:System.Linq.Enumerable.GroupJoin%2A> не имеет прямого эквивалента в терминах реляционных баз данных, но реализует надмножество внутренних соединений и левых внешних соединений. Левое внешнее соединение — это соединение, которое возвращает каждый элемент первого (левого) источника данных, даже если в другом источнике данных не имеется соответствующих элементов.  
  
 На следующем рисунке показано концептуальное представление из двух наборов и элементов, входящих в эти наборы, которые включены либо во внутреннее соединение, либо в левое внешнее соединение.  
  
 ![Два перекрывающихся кольца, отображающие внешнее и внутреннее соединение.](../../../../csharp/programming-guide/concepts/linq/media/joincircles.png "JoinCircles")  
  
## <a name="methods"></a>Методы  
  
|Имя метода|Описание:|Синтаксис выражения запроса C#|Дополнительные сведения|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Join|Соединяет две последовательности на основании функций селектора ключа и извлекает пары значений.|`join … in … on … equals …`|<xref:System.Linq.Enumerable.Join%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Join%2A?displayProperty=nameWithType>|  
|GroupJoin|Соединяет две последовательности на основании функций селектора ключа и группирует полученные при сопоставлении данные для каждого элемента.|`join … in … on … equals … into …`|<xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>См. также  
 <xref:System.Linq>  
 [Общие сведения о стандартных операторах запроса (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
 [Анонимные типы](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)  
 [Формулировка запросов-объединений и запросов векторного произведения](http://msdn.microsoft.com/library/d8072ede-0521-4670-9bec-1778ceeb875b)  
 [предложение join](../../../../csharp/language-reference/keywords/join-clause.md)  
 [Практическое руководство. Соединение с помощью составных ключей](../../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)  
 [Практическое руководство. Объединение содержимого из файлов разных форматов (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-join-content-from-dissimilar-files-linq.md)  
 [Практическое руководство. Упорядочение результатов предложения соединения](../../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)  
 [Практическое руководство. Выполнение пользовательских операций соединения](../../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)  
 [Практическое руководство. Выполнение групповых соединений](../../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)  
 [Практическое руководство. Выполнение внутренних соединений](../../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)  
 [Практическое руководство. Выполнение левых внешних соединений](../../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)  
 [Практическое руководство. Заполнение коллекций объектов из нескольких источников (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)
