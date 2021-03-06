---
title: Рекомендации по размещению в службах IIS
ms.date: 03/30/2017
ms.assetid: 0834768e-9665-46bf-86eb-d4b09ab91af5
ms.openlocfilehash: 119f14df9d46883a33272903558d83128501b293
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33495766"
---
# <a name="internet-information-services-hosting-best-practices"></a>Рекомендации по размещению в службах IIS
В этом разделе даются некоторые рекомендации для размещения служб Windows Communication Foundation (WCF).  
  
## <a name="implementing-wcf-services-as-dlls"></a>Реализация служб WCF в виде библиотек DLL  
 Реализация WCF службы в виде библиотеки DLL, которая развертывается в каталог \bin веб-приложения позволяет использовать службу вне модели веб-приложения, например, в тестовой среде, не может иметь Internet Information Services (IIS) развернуты.  
  
## <a name="service-hosts-in-iis-hosted-applications"></a>Ведущие приложения служб в приложениях, размещенных в IIS  
 Не используйте императивные резидентные интерфейсы API для создания новых основных приложений служб, которые ожидают передачи данных различного сетевого транспорта, изначально не поддерживаемого средой размещения IIS (например, [!INCLUDE[iis601](../../../../includes/iis601-md.md)] для размещения служб TCP, поскольку связь по протоколу TCP изначально не поддерживается в [!INCLUDE[iis601](../../../../includes/iis601-md.md)]). Такой подход не рекомендуется. Основные приложения служб, созданные принудительно, в среде размещения IIS неизвестны. Ключевым пунктом является то, что обработка, выполненная принудительно созданными службами, не принимается во внимание системой IIS, когда она определяет, простаивает ли пул ведущих приложений. В результате приложения, где есть такие принудительно созданные основные приложения служб, имеют среду размещения IIS, которая агрессивно удаляет ведущие процессы IIS.  
  
## <a name="uris-and-iis-hosted-endpoints"></a>Универсальные коды ресурсов (URI) и размещенные в IIS конечные точки  
 Конечные точки для службы, размещенной в IIS, должны быть настроены с использованием относительных универсальных кодов ресурсов (URI), а не абсолютных адресов. При этом гарантируется попадание адреса конечной точки в ряд адресов URI, принадлежащих ведущему приложению, и обеспечивается надлежащая активация на основе сообщений.  
  
## <a name="state-management-and-process-recycling"></a>Управление состоянием и перезапуск процессов  
 Среда размещения IIS оптимизирована для служб, не поддерживающих локальное состояние в памяти. При появлении множества внешних и внутренних событий система IIS перезапускает ведущий процесс, в результате чего любое непостоянное состояние, сохраненное только в памяти, теряется. Службы, размещенные в IIS, должны сохранять свое состояние во внешней по отношению к процессу среде (например, в базе данных) или в расположенном в памяти кэше, который в случае перезапуска приложения может быть легко восстановлен.  
  
> [!NOTE]
>  Протоколы, которые используют WCF для сообщений уровня надежности и безопасности использование неустойчивого состояния в памяти. Надежные сеансы WCF и сеансы безопасности может привести к непредвиденному завершению из-за перезапусков приложений. Приложения, размещенные в IIS, которые используют эти протоколы, должны либо зависеть нечто, отличное от предоставляемый WCF сеансовый ключ для корреляции состояния прикладного уровня (например, прикладного уровня или пользовательского заголовка корреляции) или отключить Перезапуск процессов IIS для размещенного приложения.  
  
## <a name="optimizing-performance-in-middle-tier-scenarios"></a>Оптимизация производительности в сценариях среднего уровня  
 Для обеспечения оптимальной производительности в *сценариях среднего уровня*— служба, которая вызывает другие службы в ответ на входящие сообщения — один раз экземпляр клиента службы WCF для удаленной службы и используйте его многократно несколько входящих запросы. Создание экземпляров клиентов службы WCF является ресурсоемкой операцией сравнению вызывать в уже существующем экземпляре клиента службы и сценариях среднего уровня представляют повышение производительности благодаря кэшированию удаленных клиентов между запросами. Клиенты службы WCF являются потокобезопасными, поэтому не требуется синхронизировать доступ к клиенту в нескольких потоках.  
  
 Увеличение производительности в сценариях среднего уровня обеспечивается также благодаря использованию асинхронных интерфейсов API, создаваемых параметром `svcutil /a`. `/a` Предписывает [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) для создания `BeginXXX/EndXXX` методы для каждой операции службы, которая позволяет потенциально длительных вызовы к службам удаленных выполнены на фоновые потоки.  
  
## <a name="wcf-in-multi-homed-or-multi-named-scenarios"></a>WCF в многосетевых сценариях и сценариях со многими именами  
 Можно развернуть служб WCF внутри веб-фермы IIS, где ряд компьютеров совместно используют общее имя внешнего (такие как http://www.contoso.com) , но в разных имен узлов (например, http://www.contoso.com может направлять трафик на два разных с именем http://machine1.internal.contoso.com и http://machine2.internal.contoso.com). Этот сценарий развертывания полностью поддерживается системой WCF, но требуется специальная конфигурация веб-сайта IIS размещение служб WCF для отображения надлежащего (внешнего) имени узла в метаданных службы (языке WSDL).  
  
 Чтобы обеспечить появление правильного имени узла в метаданных службы WCF приводит к возникновению ошибки, настройте идентификацию по умолчанию для веб-узла IIS, на котором размещены службы WCF для использования явно заданного имени узла. Например, компьютеры, расположенные в ферме www.contoso.com следует использовать привязку узла IIS *: 80: www.contoso.com для HTTP и \*: 443:www.contoso.com для HTTPS.  
  
 Привязки веб-узла IIS можно настроить с помощью оснастки консоли управления (MMC) IIS.  
  
## <a name="application-pools-running-in-different-user-contexts-overwrite-assemblies-from-other-accounts-in-the-temporary-folder"></a>Пулы приложений, работающие в разных контекстах пользователей, которые перезаписывают сборки из других учетных записей во временной папке  
 Чтобы пулы приложений, работающие в разных контекстах пользователей, не могли перезаписывать сборки из других учетных записей в папке временных файлов [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], используйте для разных приложений разные идентификаторы и временные папки. Например, если имеется два виртуальных приложения /Application1 и / Application2, можно создать два пула приложений (A и B) с двумя разными идентификаторами. Пул приложений A может работать под одним идентификатором пользователя (user1), а пул приложений B - под другим идентификатором пользователя (user2). Настройте приложение /Application1 на использование пула A, а приложение /Application2 - на использование пула B.  
  
 В файле Web.config можно настроить с помощью временной папки \< system.web/compilation/@tempFolder>. Для приложения/application1 это может быть «c:\tempForUser1» и для приложения application2 может быть «c:\tempForUser2». Предоставьте соответствующее разрешение на запись в эти папки для двух идентификаторов.  
  
 В этом случае пользователь user2 не может изменить папку создания кода для приложения /application2 (в папке c:\tempForUser1).  
  
## <a name="enabling-asynchronous-processing"></a>Включение асинхронной обработки  
 По умолчанию сообщения, отправляемые службой WCF, размещенной в службах IIS 6.0 и более ранних версий, обрабатываются в синхронном режиме. ASP.NET вызывает WCF в своем собственном потоке (рабочий поток ASP.NET) и WCF использует другой поток для обработки запроса. WCF удерживает рабочий поток ASP.NET до завершения обработки. В результате обработка запросов выполняется синхронно. Асинхронная обработка запросов расширяет возможности масштабирования, так как это уменьшает количество потоков, необходимых для обработки запроса, — WCF не удерживает поток ASP.NET при обработке запроса. Асинхронный режим не рекомендуется для компьютеров под управлением IIS 6.0, поскольку отсутствует возможность регулирования входящих запросов, которые открываются серверу *отказ в обслуживании* (DDOS). Начиная с версии IIS 7.0, реализовано регулирование параллельных запросов: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0]"MaxConcurrentRequestsPerCpu`. Новая система регулирования гарантирует безопасность использования асинхронной обработки.  По умолчанию в IIS 7.0 регистрируются асинхронные обработчик и модуль. Если эта функция выключена, то можно вручную включить асинхронную обработку запросов в файле Web.config приложения. Используемые параметры зависят от параметра `aspNetCompatibilityEnabled`. Если параметр `aspNetCompatibilityEnabled` установлен в значение `false`, настройте модуль `System.ServiceModel.Activation.ServiceHttpModule`, как показано в следующем фрагменте конфигурации.  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="false" />      
  </system.serviceModel>  
  <system.webServer>  
    <modules>  
      <remove name="ServiceModel"/>  
      <add name="ServiceModel"   
           preCondition="integratedMode,runtimeVersionv2.0"   
           type="System.ServiceModel.Activation.ServiceHttpModule, System.ServiceModel,Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
    </modules>  
    </system.webServer>  
```  
  
 Если параметр `aspNetCompatibilityEnabled` установлен в значение `true`, настройте модуль `System.ServiceModel.Activation.ServiceHttpHandlerFactory`, как показано в следующем фрагменте конфигурации.  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />      
  </system.serviceModel>  
  <system.webServer>  
    <handlers>  
          <clear/>  
          <add name="TestAsyncHttpHandler"   
               path="*.svc"   
               verb="*"   
               type="System.ServiceModel.Activation.ServiceHttpHandlerFactory, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"           
               />  
    </handlers>      
  </system.webServer>  
```  
  
## <a name="see-also"></a>См. также  
 [Образцы размещения службы](http://msdn.microsoft.com/library/f703a3f6-0fba-418a-a92f-7ce75ccfa47e)  
 [Функции размещения Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=201276)
