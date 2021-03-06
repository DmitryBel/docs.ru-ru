---
title: Выбор и проверка сертификата
ms.date: 03/30/2017
ms.assetid: c933aca2-4cd0-4ff1-9df9-267143f25a6f
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: f163de89a3edbf3a4ca8509fdecd10f1aa1adf1b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33396796"
---
# <a name="certificate-selection-and-validation"></a>Выбор и проверка сертификата
Классы <xref:System.Net> поддерживают несколько способов выбора и проверки <xref:System.Security.Cryptography.X509Certificates> для подключений SSL. Клиент может выбрать один или несколько сертификатов для прохождения проверки подлинности на сервере. Сервер может потребовать наличия в сертификате клиента одного или нескольких атрибутов для проверки подлинности.  
  
## <a name="definition"></a>Определение  
 Сертификат — это поток байтов в кодировке ASCII, который содержит открытый ключ, атрибуты (такие как номер версии, серийный номер и дата истечения срока действия) и цифровую подпись из центра сертификации. Сертификаты служат для установления зашифрованных соединений или для проверки подлинности клиента на сервере.  
  
## <a name="client-certificate-selection-and-validation"></a>Выбор и проверка сертификата клиента  
 Клиент может выбрать для SSL-соединения один или несколько сертификатов. Сертификаты клиента могут быть связаны с SSL-соединением с веб-сервером или почтовым SMTP-сервером. Клиент добавляет сертификаты в коллекцию объектов класса <xref:System.Security.Cryptography.X509Certificates.X509Certificate> или <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>. Если взять для примера электронную почту, коллекция сертификатов — это экземпляр <xref:System.Security.Cryptography.X509Certificates.X509CertificateCollection>, связанный со свойством <xref:System.Net.Mail.SmtpClient.ClientCertificates%2A> класса <xref:System.Net.Mail.SmtpClient>. Класс <xref:System.Net.HttpWebRequest> имеет аналогичное свойство <xref:System.Net.HttpWebRequest.ClientCertificates%2A>.  
  
 Основное различие между классами <xref:System.Security.Cryptography.X509Certificates.X509Certificate> и <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> заключается в том, что для класса <xref:System.Security.Cryptography.X509Certificates.X509Certificate> закрытый ключ должен находиться в хранилище сертификатов.  
  
 Даже если сертификаты добавлены в коллекцию и связаны с определенным SSL-соединением, они не будут отправлены на сервер, пока он их не запросит. Если для соединения задано несколько сертификатов клиента, будет выбран наиболее подходящий их них. Для этого используется алгоритм, который сопоставляет имя издателя сертификата клиента со списком издателей сертификатов, предоставляемым сервером.  
  
 Класс <xref:System.Net.Security.SslStream> позволяет еще лучше контролировать подтверждение SSL. Клиент может указать делегат для выбора используемого сертификата клиента.  
  
 Удаленный сервер может проверить, является ли сертификат клиента действительным, актуальным и подписан ли он соответствующим центром сертификации. Делегат можно добавить в <xref:System.Net.ServicePointManager.ServerCertificateValidationCallback%2A> для принудительной проверки сертификата.  
  
## <a name="client-certificate-selection"></a>Выбор сертификата клиента  
 Платформа .NET Framework выбирает сертификат клиента для предъявления серверу указанным ниже образом.  
  
1.  Если сертификат клиента предъявлялся серверу ранее, он был кэширован при первом предъявлении и используется повторно при последующих запросах сертификата клиента.  
  
2.  При наличии делегата всегда используйте возвращаемый им результат в качестве требуемого сертификата клиента. Старайтесь по возможности использовать кэшированный сертификат, но не применяйте кэшированные анонимные учетные данные, если делегат вернул значение null и коллекция сертификатов не пуста.  
  
3.  Если это первый запрос сертификата клиента, платформа перечисляет сертификаты в объектах класса <xref:System.Security.Cryptography.X509Certificates.X509Certificate> или <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>, связанных с соединением, и ищет совпадение с именем издателя сертификата клиента в списке издателей сертификатов, предоставляемом сервером. Первый совпадающий сертификат отправляется на сервер. Если совпадений нет или коллекция сертификатов пуста, на сервер отправляются анонимные учетные данные.  
  
## <a name="tools-for-certificate-configuration"></a>Средства для настройки сертификатов  
 Для настройки сертификатов клиента и сервера имеется ряд средств.  
  
 С помощью средства *Winhttpcertcfg.exe* можно настраивать сертификаты клиента. Средство *Winhttpcertcfg.exe* входит в состав набора ресурсов Windows Server 2003. Его также можно скачать в составе средств набора ресурсов Windows Server 2003 на сайте www.microsoft.com.  
  
 С помощью средства *The HttpCfg.exe* можно настраивать сертификаты сервера для класса <xref:System.Net.HttpListener>. Средство *HttpCfg.exe* входит в состав вспомогательных средств для Windows Server 2003 и Windows XP с пакетом обновления 2 (SP2). *HttpCfg.exe* и другие вспомогательные средства не устанавливаются в Windows Server 2003 и Windows XP по умолчанию. В Windows Server 2003 вспомогательные средства устанавливаются отдельно из следующего файла на компакт-диске с Windows Server 2003:  
  
 \Support\Tools\Suptools.msi  
  
 Для Windows XP с пакетом обновления 2 (SP2) вспомогательные средства можно скачать с сайта www.microsoft.com.  
  
 Исходный код версии средства *HttpCfg.exe* также предоставляется в качестве образца в пакете SDK для Windows Server. Исходный код образца *HttpCfg.exe* устанавливается по умолчанию вместе с другими образцами сетевого взаимодействия из пакета Windows SDK в следующей папке:  
  
 *C:\Program Files\Microsoft SDKs\Windows\v1.0\Samples\NetDS\http\serviceconfig*  
  
 Помимо этих средств, классы <xref:System.Security.Cryptography.X509Certificates.X509Certificate> и <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> предоставляют методы для загрузки сертификата из файловой системы.  
  
## <a name="see-also"></a>См. также  
 [Безопасность в сетевом программировании](../../../docs/framework/network-programming/security-in-network-programming.md)  
 [Сетевое программирование в .NET Framework](../../../docs/framework/network-programming/index.md)
