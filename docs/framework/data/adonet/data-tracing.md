---
title: Трассировка данных в ADO.NET
ms.date: 03/30/2017
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.openlocfilehash: 6dd385cd58d1c8400c45139492d84e6ca4fe1bd7
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32758507"
---
# <a name="data-tracing-in-adonet"></a>Трассировка данных в ADO.NET
ADO.NET появились новые встроенные функции трассировки данных, поддерживаемые поставщиками данных .NET для SQL Server, Oracle, OLE DB и ODBC, а также ADO.NET <xref:System.Data.DataSet>и сетевые протоколы SQL Server.  
  
 Трассировка вызовов API-интерфейсов для доступа к данным может помочь в выявлении следующих проблем:  
  
-   несоответствие схемы между клиентской программой и базой данных;  
  
-   недоступность базы данных или проблемы с сетевой библиотекой;  
  
-   неверный SQL-код, фиксированный или сформированный приложением;  
  
-   неверная программная логика;  
  
-   проблемы, возникающие вследствие взаимодействия нескольких компонентов ADO.NET или компонентов ADO.NET и собственных компонентов.  
  
 Трассировка является расширяемой для поддержки разных методов трассировки, поэтому разработчик может отслеживать проблемы на любом уровне стека приложений. Хотя трассировка не является возможностью только ADO.NET, поставщики Майкрософт пользуются преимуществами обобщенных API трассировки и инструментария.  
  
 Дополнительные сведения об установке и настройке управляемой трассировки в ADO.NET см. в разделе [трассировка доступа к данным](http://msdn.microsoft.com/library/hh880086.aspx).  
  
## <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Доступ к диагностической информации в расширенном журнале событий  
 В [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] поставщика данных для SQL Server, доступ к данным трассировки ([трассировка доступа к данным](http://msdn.microsoft.com/library/hh880086.aspx)) был обновлен, чтобы упростить его сопоставление событий клиентов с диагностической информацией — ошибками соединения, из Подключение сервера кольца буфера и приложения данные производительности в журнале расширенных событий. Сведения о чтении журнала расширенных событий см. в разделе [Просмотр данных сеанса события](http://msdn.microsoft.com/library/hh710068\(SQL.110\).aspx).  
  
 Для операций соединения ADO.NET передает идентификатор соединения клиента. При сбое соединения, можно получить доступ к кольцевой буфер связи ([Устранение неполадок подключения в SQL Server 2008 с помощью кольцевого буфера подключения](http://go.microsoft.com/fwlink/?LinkId=207752)) и найти `ClientConnectionID` и получить диагностические сведения Ошибка подключения. Идентификаторы соединения клиента регистрируются в кольцевом буфере только при возникновении ошибки. (Если установление соединения завершилось неудачно перед отправкой пакета предварительного согласования, то идентификатор соединения клиента не будет сформирован.) Идентификатор соединения клиента - это 16-байтное значение идентификатора GUID. Можно также найти идентификатор соединения клиента в расширенном выводе целевых событий, если целевое действие `client_connection_id` добавляется в события в расширенном сеансе событий. Если необходима дополнительная помощь по устранению неполадок драйвера клиента, можно включить трассировку для доступа к данным, повторно запустить команду соединения и проверить поле `ClientConnectionID` в трассировке доступа к данным.  
  
 Можно получить идентификатор соединения клиента программно через свойство `SqlConnection.ClientConnectionID`.  
  
 Идентификатор `ClientConnectionID` доступен для объекта <xref:System.Data.SqlClient.SqlConnection>, который успешно устанавливает соединение. Если попытка соединения завершилась ошибкой, то `ClientConnectionID` можно попробовать получить через `SqlException.ToString`.  
  
 ADO.NET также отправляет идентификатор действия, определенный для потока. Идентификатор действия захватывается в сеансах расширенных событий, если сеансы запускаются с включенным параметром TRACK_CAUSAILITY. Для устранения проблем производительности с активным соединением можно получить идентификатор действия из трассировки клиента для доступа к данным (поле `ActivityID`), а затем найти идентификатор действия в выходных данных расширенных событий. Идентификатор действия в расширенных событиях представляет собой 16-байтовый GUID (не совпадает с идентификатором GUID для идентификатора соединения клиента) с добавленным к нему четырехбайтовым порядковым номером. Порядковый номер представляет собой порядковый номер запроса в потоке и указывает относительное упорядочение инструкций пакета RPC для потока. Идентификатор `ActivityID` в настоящее время (необязательно) отправляется для инструкций пакета SQL и запросов RPC, если включена трассировка доступа к данным и включен 18-й бит в слове настройки трассировки доступа к данным.  
  
 Далее приведен образец, в котором используется [!INCLUDE[tsql](../../../../includes/tsql-md.md)] для запуска расширенного сеанса событий, который будет сохранен в кольцевом буфере и будет регистрировать идентификатор действия, отправленный с клиента в операциях RPC и пакета.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>См. также  
 [Трассировка сети в .NET Framework](../../../../docs/framework/network-programming/network-tracing.md)  
 [Трассировка и инструментирование приложений](../../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
