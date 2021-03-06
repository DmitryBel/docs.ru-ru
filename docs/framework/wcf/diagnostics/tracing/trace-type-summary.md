---
title: Сводка типов трассировок
ms.date: 03/30/2017
ms.assetid: e639410b-d1d1-479c-b78e-a4701d4e4085
ms.openlocfilehash: e3bc66753dd44e1dc4c7417caf593820300f69a5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33486046"
---
# <a name="trace-type-summary"></a>Сводка типов трассировок
[Уровни источника](http://go.microsoft.com/fwlink/?LinkID=94943) определяются различные уровни трассировки: критическое, ошибка, предупреждение, сведения и подробные сведения, а также приводится описание `ActivityTracing` границ и действие передачи событий трассировки флага, которые выводом.  
  
 Можно также просмотреть [TraceEventType](http://go.microsoft.com/fwlink/?LinkId=95169) для типов трассировок, которые могут выдаваться в <xref:System.Diagnostics>.  
  
 В следующей таблице перечислены наиболее важные из них.  
  
|Тип трассировки|Описание|  
|----------------|-----------------|  
|Critical|Неустранимая ошибка или сбой в работе приложения.|  
|Ошибка|Устранимая ошибка.|  
|Предупреждение|Информационное сообщение.|  
|Сведения|Некритическая ошибка.|  
|Verbose|Трассировка отладки.|  
|Запуск|Начало логического блока обработки.|  
|Suspend|Приостановка обработки логическую единицу.|  
|возобновление|Возобновление логический блок обработки.|  
|Остановить|Остановка логический блок обработки.|  
|Transfer|Изменение идентификации взаимосвязей.|  
  
 Действие определяется как сочетание перечисленных выше типов трассировок.  
  
 Ниже приведено регулярное выражение, определяющее идеальное действие в локальной области (области источника трассировки):  
  
 `R = Start (Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop`  
  
 Это означает, что действие должно удовлетворять следующим условиям.  
  
-   Должно запускаться и останавливаться трассировками Start и Stop соответственно.  
  
-   Трассировка Transfer должна непосредственно предшествовать трассировке Suspend или Resume.  
  
-   Не должно содержать никаких трассировок между трассировками Suspend и Resume, если такие трассировки имеются.  
  
-   Может содержать любые и в любом количестве трассировки уровня Critical/Error/Warning/Information/Verbose/Transfer при условии соблюдения предыдущих условий.  
  
 Ниже приведено регулярное выражение, определяющее идеальное действие в глобальной области,  
  
```  
R+   
```  
  
 где R - регулярное выражение для действия в локальной области. Таким образом, получаем:  
  
```  
[R+ = Start ( Critical | Error | Warning | Information | Verbose | Transfer | (Transfer Suspend Transfer Resume) )* Stop]+  
```
