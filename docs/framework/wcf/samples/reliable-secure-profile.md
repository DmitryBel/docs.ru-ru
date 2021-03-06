---
title: Надежный защищенный профиль
ms.date: 03/30/2017
ms.assetid: 921edc41-e91b-40f9-bde9-b6148b633e61
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 65523fcc1d08bd48a432e6cf599dfcb73ade8747
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
ms.locfileid: "33805750"
---
# <a name="reliable-secure-profile"></a>Надежный защищенный профиль
В этом примере показано, как составлять WCF и [надежному защищенному профилю](http://go.microsoft.com/fwlink/?LinkId=178140) (RSP). Этот образец демонстрирует реализацию [Создание подключения](http://go.microsoft.com/fwlink/?LinkId=178141) канала, который может формироваться вместе с надежного обмена сообщениями и при необходимости безопасного канала для создания надежных защищенную привязку на основе RSP спецификации.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] образцов. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\ReliableSecureProfile`  
  
## <a name="discussion"></a>Обсуждение  
 В этом образце показан сценарий с надежным двусторонним асинхронным обменом сообщениями. Служба имеет дуплексный контракт, а в клиенте реализован дуплексный контракт обратного вызова. Клиент создает запрос к службе, а ответ ожидается по отдельному соединению. Сообщение запроса отправляется надежным образом. Клиент не открывает со своей стороны конечную точку прослушивания. Поэтому он отправляет службе запросы «Make Connection», чтобы служба отправляла ответ по обратному каналу для таких запросов. В этом образце показано, как организовать защищенную надежную дуплексную связь по HTTP без предоставления конечной точки прослушивания на клиенте (и без создания исключения брандмауэра).  
  
## <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1.  Откройте **ReliableSecureProfile** решения.  
  
2.  Щелкните правой кнопкой мыши **службы** проекта в **обозревателе решений**выберите **отладки**, **запустить новый экземпляр** в контекстном меню. Запустится узел службы.  
  
3.  Щелкните правой кнопкой мыши **клиента** проекта в **обозревателе решений**выберите **отладки**, **запустить новый экземпляр** в контекстном меню. Запустится клиент.  
  
4.  Введите в окне консоли клиента любую строку и нажмите клавишу ВВОД. Введенная строка отправится в службу, которая вычислит для нее хэш.  
  
5.  Просмотрите результат в окне клиента, когда служба выполняет обратный вызов дуплексной операции контракта, чтобы вывести результат в окно консоли клиента. Со стороны службы специально реализована задержка, имитирующая продолжительную операцию по обработке данных.  
  
6.  Наблюдение за HTTP-трафиком (в любом из средств оперативного наблюдения за сетью, например сетевом мониторе, Fiddler и т. п.) показывает, что последовательность связи устанавливается между клиентом и службой согласно надежному защищенному профилю, а клиент отправляет службе запросы «Make Connection». Когда служба готова к отправке обработанного ответа, она использует для отправки результатов обратный канал последнего запроса «Make Connection».  
  
7.  Нажмите в окне консоли службы клавишу ВВОД, чтобы закрыть службу. Нажмите клавишу ВВОД в окне консоли клиента, чтобы закрыть клиент.
