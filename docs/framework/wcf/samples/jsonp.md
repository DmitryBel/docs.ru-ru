---
title: JSONP
ms.date: 03/30/2017
ms.assetid: c13b4d7b-dac7-4ffd-9f84-765c903511e1
ms.openlocfilehash: 9002597ef662c78b6519ab0c04700cddf7ee3714
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
---
# <a name="jsonp"></a>JSONP
В этом образце показано, как обеспечить поддержку JSONP(JSON with Padding) в службах WCF REST. JSONP является правилом, используемым для вызова скриптов между доменами путем создания тегов скриптов в текущем документе. Результат возвращается в заданной функции обратного вызова. JSONP основан на идее, что теги, такие как `<script src="http://..." >` могут выполнять скрипты из любого домена, причем скрипт, полученный этими тегами, выполняется в пределах области, в которых могут уже быть определены другие функции.  
  
## <a name="demonstrates"></a>Демонстрации  
 Междоменная работа со скриптами с JSONP.  
  
## <a name="discussion"></a>Обсуждение  
 В образец входит веб-страница, которая динамически добавляет блок скрипта после отображения страницы в веб-браузере. В этом блоке скрипта вызывается служба WCF REST, содержащая одну операцию `GetCustomer`. Служба WCF REST возвращает имя и адрес клиента, заключенные в оболочку функции обратного вызова. Когда служба WCF REST отправляет ответ, вызывается функция обратного вызова на веб-странице с данными о клиенте, и функция обратного вызова выводит эти данные на веб-странице. Вставка тега скрипта и выполнение функции обратного вызова автоматически обрабатываются элементом управления ASP.NET AJAX ScriptManager. Схема использования та же, что и для всех прокси ASP.NET AJAX, плюс добавляется строка для включения JSONP, как показано в следующем коде.  
  
```csharp  
var proxy = new JsonpAjaxService.CustomerService();  
proxy.set_enableJsonp(true);  
proxy.GetCustomer(onSuccess, onFail, null);  
```  
  
 Веб-страница может вызывать службу WCF REST, поскольку эта служба использует объект <xref:System.ServiceModel.Description.WebScriptEndpoint>, где свойство `crossDomainScriptAccessEnabled` установлено в значении `true`. Обе операции настройки выполняются в файле Web.config с \<system.serviceModel > элемент.  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
  <standardEndpoints>  
    <webScriptEndpoint>  
      <standardEndpoint name="" crossDomainScriptAccessEnabled="true"/>  
    </webScriptEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 ScriptManager управляет взаимодействием со службой и устраняет сложности реализации доступа JSONP вручную. Когда `crossDomainScriptAccessEnabled` равно `true` и формат ответа для операции JSON, инфраструктура WCF проверяет URI запроса для параметра строки запроса обратного вызова и заключает ответ JSON с значение строки запроса обратного вызова параметр. В образце веб-страница вызывает службу WCF REST со следующим URI.  
  
```  
http://localhost:33695/CustomerService/GetCustomer?callback=Sys._json0  
```  
  
 Поскольку строковый параметр запроса обратного вызова имеет значение `JsonPCallback`, служба WCF возвращает ответ JSONP, показанный в следующем примере.  
  
```  
Sys._json0({"__type":"Customer:#Microsoft.Samples.Jsonp","Address":"1 Example Way","Name":"Bob"});  
```  
  
 Этот ответ JSONP содержит данные о клиенте в формате JSON, заключенные в имя функции обратного вызова, запрошенной веб-страницей. ScriptManager будет выполнять этот обратный вызов, используя тег скрипта для междоменного запроса, а затем передаст результат в обработчик onSuccess, который передан в операцию GetCustomer прокси ASP.NET AJAX.  
  
 Образец состоит из двух веб-приложений ASP.NET: один содержит службу WCF, а еще один веб-страница ASPX, которая вызывает службу. Во время работы решения [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] размещает два веб-сайта по различным портам, и создается среда, где служба и клиент работают в различных доменах.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] образцов. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\JSONP`  
  
#### <a name="to-run-the-sample"></a>Выполнение образца  
  
1.  Откройте решение для образца JSONP.  
  
2.  Нажмите клавишу F5 для запуска `http://localhost:26648/JSONPClientPage.aspx` в браузере.  
  
3.  Обратите внимание, что после загрузки страницы, поля ввода для «Name» и «Адрес» заполняются значениями.  Эти значения получены из-за обращения к службе WCF после браузер завершил визуализацию страницы.
