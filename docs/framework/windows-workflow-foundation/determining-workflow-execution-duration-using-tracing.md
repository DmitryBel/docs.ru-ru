---
title: Определение времени выполнения рабочего процесса с помощью трассировки
ms.date: 03/30/2017
ms.assetid: f04ad0fd-edc7-4cbc-8979-356f2a1131c4
ms.openlocfilehash: 9f9c65f2c873d54da443db14e7f5797ef1e14174
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33515089"
---
# <a name="determining-workflow-execution-duration-using-tracing"></a>Определение времени выполнения рабочего процесса с помощью трассировки
В этом разделе демонстрируется, как определить время, которое требуется для выполнения успешно созданного резидентного рабочего процесса с помощью трассировки рабочего процесса.  
  
### <a name="to-determine-workflow-application-execution-duration-by-using-workflow-tracing"></a>Определение продолжительности выполнения приложения рабочего процесса с помощью трассировки рабочего процесса  
  
1.  Откройте [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  Выберите **файл**, **новый**, **проекта**.  В разделе **C#** выберите **рабочего процесса** узла.  Выберите **консольное приложение рабочего процесса** из списка шаблонов.  Имя для нового проекта `WorkflowDurationTracing` и нажмите кнопку **ОК**.  
  
2.  Откройте файл Workflow1.xaml.  Перетащите действие <xref:System.Activities.Statements.Delay> в область конструктора. Свойству «Duration» действия присвойте значение 00:00:10 (десять секунд).  
  
3.  Откройте средство просмотра событий, щелкнув **запустить**, **запуска**и введя `eventvwr.exe`.  
  
4.  Если вы еще не включена трассировка рабочего процесса, разверните **журналы приложений и служб**, **Microsoft**, **Windows**, **сервер приложений-приложения** . Выберите **представление**, **Отобразить аналитический и отладочный журналы**. Щелкните правой кнопкой мыши **отладки** и выберите **включить журнал**. Оставьте окно просмотра событий открытым, чтобы можно было просмотреть трассировки после запуска рабочего процесса.  
  
5.  Выполните приложение рабочего процесса, нажав CTRL+SHIFT+B.  
  
6.  В окне просмотра событий найдите последнее событие с идентификатором 1009 и сообщение, похожее на следующее. Запишите время регистрации сообщения.  
  
 **Родительское действие '', DisplayName: '', InstanceId: '' запланировало дочернее действие с ' WorkflowDurationTracking.Workflow1', DisplayName: 'Workflow1', InstanceId: "1".**  
  
7.  Найдите еще одно последнее событие с идентификатором 1001 и сообщение, похожее на следующее.  Вычтите время предыдущего сообщения из времени регистрации данного сообщения, чтобы определить продолжительность выполнения рабочего процесса, которая должна составить приблизительно 10 секунд.  
  
 **Элемент WorkflowInstance с идентификатором: '1bbac57b-3322-498e-9e27-8833fda3a5bf' завершил работу в состояние Closed.**  
  
## <a name="see-also"></a>См. также  
 [Трассировка рабочих процессов](../../../docs/framework/windows-workflow-foundation/workflow-tracing.md)  
 [Наблюдение за Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=201273)  
 [Мониторинг приложений с](http://go.microsoft.com/fwlink/?LinkId=201275)
