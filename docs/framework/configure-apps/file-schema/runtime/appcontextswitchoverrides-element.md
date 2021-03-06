---
title: '&lt;AppContextSwitchOverrides&gt; элемент'
ms.custom: updateeachrelease
ms.date: 04/19/2018
helpviewer_keywords:
- AppContextSwitchOverrides
- compatibility switches
- configuration switches
- configuration
ms.assetid: 4ce07f47-7ddb-4d91-b067-501bd8b88752
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d16ce7f2744869c812b9988e91edd153d9cb4fd2
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32747529"
---
# <a name="ltappcontextswitchoverridesgt-element"></a>&lt;AppContextSwitchOverrides&gt; элемент
Определяет один или несколько коммутаторов, используемых классом <xref:System.AppContext> для предоставления механизма отказа от новых функциональных возможностей.  
  
 \<configuration>  
 \<Среда выполнения >  
\<AppContextSwitchOverrides >  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<AppContextSwitchOverrides value="name1=value1[[;name2=value2];...]" />  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`value`|Обязательный атрибут.<br /><br /> Определяет одно или несколько имен коммутатора и связанные с ними значения типа Boolean.|  
  
### <a name="value-attribute"></a>значение атрибута  
  
|Значение|Описание|  
|-----------|-----------------|  
|«имя = значение»|Имя коммутатора предопределенных вместе со значением (`true` или `false`). Несколько пар имя значение коммутатора разделяются точками с запятой («;»). Список стандартных коммутатора имен, поддерживаемых платформой .NET Framework см. в разделе "Примечания".|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|  
|`runtime`|Содержит сведения о параметрах инициализации среды выполнения.|  
  
## <a name="remarks"></a>Примечания  
 Начиная с .NET Framework 4.6 `<AppContextSwitchOverrides>` элемент в файле конфигурации, разрешающий вызовы API-интерфейса для определения их приложения можно воспользоваться преимуществами новых функций или сохранить совместимость с предыдущими версиями библиотеки. Например, если между двумя версиями библиотеки, изменилось поведение API-интерфейса `<AppContextSwitchOverrides>` элемент позволяет вызывающим объектам, API, чтобы отказаться от нового поведения в версиях библиотеки, которые поддерживают новые функциональные возможности. Для приложения, которые вызывают API-интерфейсов в платформе .NET Framework `<AppContextSwitchOverrides>` элемент также позволяет вызывающим объектам которого приложений более ранней версии платформы .NET Framework согласиться на новые функциональные возможности, если их приложение выполняется на версии .NET Framework, которая включает функциональные возможности.  
  
 `value` Атрибут `<AppContextSwitchOverrides>` элемент состоит из одну строку, которая состоит из одного или нескольких пар имен и значений, разделенных точкой с запятой.  Каждое имя определяет переключатель совместимости, и его соответствующее значение является логическое значение (`true` или `false`), указывающее, установлен ли переключатель. По умолчанию, что коммутатор является `false`, и библиотеки предоставляют новые функциональные возможности. Они только предоставляют прежние функции, если установлен переключатель (то есть его значение равно `true`). Это позволяет библиотекам для предоставления новое поведение для существующих API, позволяет вызывающим объектам, которые зависят от предыдущего поведения отказаться от новых функциональных возможностей.  
  
 Платформа .NET Framework поддерживает следующие параметры:  
  
|Имя коммутатора|Описание|Представленные|  
|-----------------|-----------------|----------------|  
|`Switch.MS.Internal.`<br/>`DoNotApplyLayoutRoundingToMarginsAndBorderThickness`|Определяет, использует ли Windows Presentation Foundation устаревший алгоритм для макета элемента управления. Дополнительные сведения см. в разделе [Устранение рисков. Макет WPF](~/docs/framework/migration-guide/mitigation-wpf-layout.md).|.NET Framework 4.6|  
|`Switch.MS.Internal.`<br/>`UseSha1AsDefaultHashAlgorithmForDigitalSignatures`|Определяет, является ли используемый по умолчанию алгоритм, используемый для подписи частей пакета с PackageDigitalSignatureManager SHA1 или SHA256.|.NET Framework 4.7.1|
|`Switch.System.Activities.`<br/>`UseMD5CryptoServiceProviderForWFDebugger`|Если задано значение `false`, позволяет выполнить отладку рабочего процесса на основе XAML проектов с помощью Visual Studio, при включении FIPS. Без него <xref:System.NullReferenceException> вызывается в вызовы методов в сборке System.Activities.|.NET Framework 4.7|
|`Switch.System.Activities.`<br/>`UseMD5ForWFDebugger`|Определяет, использует ли контрольная сумма для экземпляра рабочего процесса в отладчике MD5 или SHA1. | .NET Framework 4.7|
|`Switch.System.Diagnostics.`<br/>`IgnorePortablePDBsInStackTraces`|Элементы управления ли получать трассировки стека при использовании переносимой PDB-файлы могут включать сведения о файле и строке источника. `false` для включения сведений о файле и строке источника; в противном случае `true`.|.NET framework 4.7.2|
|`Switch.System.Drawing.`<br/>`DontSupportPngFramesInIcons`|Элементы управления ли <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> метод создает исключение при <xref:System.Drawing.Icon> наличии кадров PNG в объекте. Дополнительные сведения см. в разделе [Устранение рисков: кадры PNG кадров в объектах Icon](~/docs/framework/migration-guide/mitigation-png-frames-in-icon-objects.md).|.NET Framework 4.6|  
|`Switch.System.Drawing.Text.`<br/>`DoNotRemoveGdiFontsResourcesFromFontCollection`|Определяет, является ли <xref:System.Drawing.Text.PrivateFontCollection?displayProperty=nameWithType> должным образом при удалении объектов при добавлении в коллекцию по <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile(System.String)?displayProperty=nameWithType> метод. `true` для поддержки поведения предыдущих версий; `false` для удаления всех объектов закрытого шрифта. |.NET framework 4.7.2|
|`Switch.System.Drawing.Printing.`</br>`OptimizePrintPreview`|Элементы управления ли производительность <xref:System.Windows.Forms.PrintPreviewDialog> оптимизирован для сетевых принтеров. Дополнительные сведения см. в разделе [Обзор элемента управления PrintPreviewDialog](../../../winforms/controls/printpreviewdialog-control-overview-windows-forms.md).|.NET Framework 4.6|
|`Switch.System.Globalization.NoAsyncCurrentCulture`|Управляет ли асинхронные операции не проходят из контекста вызывающего потока. Дополнительные сведения см. в разделе [CurrentCulture и CurrentUICulture проходят через задачи](~/docs/framework/migration-guide/retargeting/4.5.2-4.6.md#currentculture-and-currentuiculture-flow-across-tasks).|.NET Framework 4.6|  
|`Switch.System.IdentityModel.`<br/>`DisableMultipleDNSEntriesInSANCertificate`|Элементы управления ли <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType> метод пытается сопоставить тип утверждения только с последней записью DNS. Дополнительные сведения см. в разделе [Устранение рисков: метод X509CertificateClaimSet.FindClaims](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md).|.NET Framework 4.6.1|  
|`Switch.System.IdentityModel.`<br/>`EnableCachedEmptyDefaultAuthorizationContext`|Определяет, следует ли разрешить AuthorizationContext.Empty для возврата изменяемого объекта.|.NET Framework 4.6|  
|`Switch.System.IO.BlockLongPaths`|Элементы управления ли пути длиной более `MAX_PATH` throw (260 символов) <xref:System.IO.PathTooLongException>. Дополнительные сведения см. в разделе [длинные пути поддержки](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#long-path-support).|.NET Framework 4.6.2|  
|`Switch.System.IO.Compression.`<br/>`DoNotUseNativeZipLibraryForDecompression`|Указывает, используются ли собственные процедуры ОС для распаковки с <xref:System.IO.Compression.DeflateStream> класса. `false` Чтобы использовать собственные интерфейсы API; `true` использовать <xref:System.IO.Compression.DeflateStream> реализации.|.NET framework 4.7.2|
|`Switch.System.IO.Compression.ZipFile.`<br/>`UseBackslash`|Использует обратной косой черты («\\«) вместо косой черты («/») как разделитель пути в <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A?displayProperty=nameWithType> свойство. Дополнительные сведения см. в разделе [устранение рисков: разделитель пути ZipArchiveEntry.FullName](~/docs/framework/migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md).|.NET Framework 4.6.1|  
|`Switch.System.IO.Ports.`<br/>`DoNotCatchSerialStreamThreadExceptions`|Контролирует операционной системы исключений, возникших в фоновых потоках, созданных с помощью <xref:System.IO.Ports.SerialPort> потоки завершить процесс.|.NET Framework 4.7.1| 
|`Switch.System.IO.`<br/>`UseLegacyPathHandling`|Управляет ли используется устаревший путь нормализации и поддерживаемых пути URI <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> и <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> методы. Дополнительные сведения см. в разделе [устранение рисков: путь нормализации](~/docs/framework/migration-guide/mitigation-path-normalization.md) и [устранение рисков: путь двоеточие проверяет](~/docs/framework/migration-guide/mitigation-path-colon-checks.md).|.NET Framework 4.6.2|  
|`Switch.System.`<br/>`MemberDescriptorEqualsReturnsFalseIfEquivalent`|Управляет ли тест для проверки равенства сравнивает <xref:System.ComponentModel.MemberDescriptor.Category%2A?displayProperty=nameWithType> свойства одного объекта с <xref:System.ComponentModel.MemberDescriptor.Description%2A?displayProperty=nameWithType> свойство второго объекта. Дополнительные сведения см. в разделе [неправильная реализация MemberDescriptor.Equals](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#incorrect-implementation-of-memberdescriptorequals).|.NET Framework 4.6.2|  
 `Switch.System.Net.`<br/>`DontCheckCertificateEKUs`|Отключает сертификата проверки идентификатор (OID) расширенного использования ключа (EKU) объектов. Расширение расширенного использования ключа (EKU) — это коллекция идентификаторов объекта (OID), которые указывают приложения, использующие ключ.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchSendAuxRecord`|Отключает уменьшение TLS1.0 браузера воспользоваться для SSL/TLS (BEAST), отключив использование SCH_SEND_AUX_RECORD.|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSchUseStrongCrypto`|Элементы управления ли <xref:System.Net.ServicePointManager?displayProperty=nameWithType> и <xref:System.Net.Security.SslStream?displayProperty=nameWithType> классы могут использовать протокол SSL 3.0. Дополнительные сведения см. в разделе [Устранение рисков. Протоколы TLS](~/docs/framework/migration-guide/mitigation-tls-protocols.md).|.NET Framework 4.6|
|`Switch.System.Net.`<br/>`DontEnableSystemDefaultTlsVersions`|Отключает SystemDefault TLS версии, вернитесь к Tls12, Tls11, Tls значение по умолчанию.|.NET Framework 4.7|
|`Switch.System.Net.`<br/>`DontEnableTlsAlerts`|Отключает предупреждения серверные SslStream TLS.|.NET Framework 4.7|
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseECMAScriptV6EscapeControlCharacter` |Элементы управления ли [DataContractJsonSerializer](xref:System.Runtime.Serialization.Json.DataContractJsonSerializer) сериализует некоторые управляющие символы, основанные на стандартах версии ECMAScript 6 и V8. Дополнительные сведения см. в статье [Устранение рисков. Сериализация управляющих символов с помощью DataContractJsonSerializer](Mitigation:%20Serialization%20of%20Control%20Characters%20with%20the%20DataContractJsonSerializer.md)| .NET Framework 4.7 |
|`Switch.System.Runtime.Serialization.`<br/>`DoNotUseTimeZoneInfo`|Элементы управления ли <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> поддерживает несколько корректировки или только одного набора для часового пояса. Если `true`, он использует <xref:System.TimeZoneInfo> тип для сериализации и десериализации данных даты и времени; в противном случае он использует <xref:System.TimeZone> тип, который не поддерживает несколько правил коррекции.|.NET Framework 4.6.2|
|`Switch.System.Security.ClaimsIdentity.`<br/>`SetActorAsReferenceWhenCopyingClaimsIdentity`|Элементы управления ли <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=nameWithType> конструктор задает новый объект <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=nameWithType> свойство с существующие ссылки на объект. Дополнительные сведения см. в разделе [Устранение рисков. Конструктор ClaimsIdentity](~/docs/framework/migration-guide/mitigation-claimsidentity-constructor.md).|.NET Framework 4.6.2|  
|`Switch.System.Security.Cryptography.`<br/>`AesCryptoServiceProvider.DontCorrectlyResetDecryptor`|Элементы управления ли при попытке повторного использования <xref:System.Security.Cryptography.AesCryptoServiceProvider> вызывает дешифратор <xref:System.Security.Cryptography.CryptographicException>. Дополнительные сведения см. в разделе [AesCryptoServiceProvider дешифратор предоставляет преобразование для повторного использования](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#aescryptoserviceprovider-decryptor-provides-a-reusable-transform).|.NET Framework 4.6.2|
|`Switch.System.Security.Cryptography.`<br/>`DoNotAddrOfCspParentWindowHandle`|Элементы управления ли значение [CspParameters.ParentWindowHandle](xref:System.Security.Cryptography.CspParameters.ParentWindowHandle) свойство [IntPtr](xref:System.IntPtr) , область памяти окна обработку или это дескриптор окна (HWND). Дополнительные сведения см. в статье [Mitigation: CspParameters.ParentWindowHandle Expects an HWND](Mitigation:%20CspParameters.ParentWindowHandle%20Expects%20an%20HWND.md) (Устранение рисков. CspParameters.ParentWindowHandle ожидает HWND). |.NET Framework 4.7|   
|`Switch.System.Security.Cryptography.Pkcs.`<br/>`UseInsecureHashAlgorithms`|Определяет, является ли значение по умолчанию для некоторых операций SignedCMS SHA1 или SHA256. |.NET Framework 4.7.1|
|`Switch.System.Security.Cryptography.Xml.`<br/>`UseInsecureHashAlgorithms`|Определяет, является ли значение по умолчанию для некоторых операций SignedXML SHA1 или SHA256. |.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`AllowUnsignedToHeader`|Определяет, является ли `TransportWithMessageCredential` режим безопасности позволяет сообщения с неподписанным заголовок «to». Это коммутатору включаемая пользователем. Дополнительные сведения см. в разделе [изменения среды выполнения в .NET Framework 4.6.1](https://msdn.microsoft.com/library/mt592686.aspx#WCF).|.NET Framework 4.6.1| 
|`Switch.System.ServiceModel.`<br/>`DisableAddressHeaderCollectionValidation`>|Элементы управления ли <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> вызывает конструктор <xref:System.ArgumentException> Если один из элементов `null`.|.NET Framework 4.7.1| 
|`Switch.System.ServiceModel.`<br />`DisableCngCertificates`|Определяет ли попытка использовать X509 сертификаты с помощью поставщика хранилища ключей CSG возникло исключение. Дополнительные сведения см. в разделе [безопасности транспорта WCF поддерживает сертификаты, сохраненных с помощью CNG](~/docs/framework/migration-guide/retargeting/4.6.1-4.6.2.md#wcf-transport-security-supports-certificates-stored-using-cng).|.NET Framework 4.6.1|
|`Switch.System.ServiceModel.`<br/>`DisableExplicitConnectionCloseHeader`|При использовании транспорта HTTP с резидентной службы, установка этого значения в `true` заставляет игнорировать Добавление приложения WCF `Connection: close` заголовок, чтобы заголовки ответа для запроса. Установка этого значения в `false` включает добавление `Connection: close` заголовок, чтобы заголовки ответа, что приводит к закрытие сокета запроса после отправки ответа.|.NET Framework 4.6|
|`Switch.System.ServiceModel.`<br/>`DisableOperationContextAsyncFlow`|Обрабатывает взаимоблокировок, возникающие в результате ограничение экземпляров реентерабельным службы к одному потоку за раз.|.NET Framework 4.6.2|
|`Switch.System.ServiceModel.`<br/>`DisableUsingServicePointManagerSecurityProtocols`|Вместе с `Switch.System.Net.DontEnableSchUseStrongCrypto`, определяет, используется ли безопасность сообщений WCF TLS 1.1 и TLS 1.2.|.NET Framework 4.7 |    
|`Switch.System.ServiceModel.`<br/>`DontEnableSystemDefaultTlsVersions`|Значение `false` задает конфигурацию по умолчанию, чтобы разрешить операционной системе для выбора протокола. Значение `true` задаются наибольший протокола, доступного по умолчанию. (Также доступно для обслуживания ветвь из предыдущей версии framework)|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InMsmqEncryptionAlgorithm`|Определяет, является ли сообщение по умолчанию алгоритм для сообщения MSMQ в WCF подписи SHA1 или SHA256.|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.`<br/>`UseSha1InPipeConnectionGetHashAlgorithm`|Определяет, использует ли WCF, SHA1 или хэш SHA256 для формирования случайных имен для именованных каналов.|.NET Framework 4.7.1|
|`Switch.System.ServiceModel.Internals`<br/>`IncludeNullExceptionMessageInETWTrace`|Определяет, будет ли выбрасываться [NullReferenceException](xref:System.NullReferenceException) при сообщении об исключении имеет значение null.|.NET Framework 4.7|  
|`Switch.System.ServiceProcess.`<br/>`DontThrowExceptionsOnStart`|Определяет, распространяются ли исключения, возникшие при запуске службы вызывающему объекту <xref:System.ServiceProcess.ServiceBase.Run%2A?displayProperty=nameWithType> метод.|.NET Framework 4.7.1|
|`Switch.System.Uri.`<br/>`DontEnableStrictRFC3986ReservedCharacterSets`|Определяет ли определенные закодированные иногда декодирования теперь постоянно слева кодируются символы. Если `true`, декодированный; в противном случае — `false`.|.NET framework 4.7.2|
|`Switch.System.Uri.`<br/>`DontKeepUnicodeBidiFormattingCharacters`|Определяет обработку двунаправленный символов Юникода в URI. `true` Чтобы убрать их из URI; `false` для сохранения и процент закодировать их.|.NET framework 4.7.2|
|`Switch.System.Windows.Controls.Grid.`<br/>`StarDefinitionsCanExceedAvailableSpace` |Определяет, применяется ли Windows Presentation Foundation старый алгоритм (`true`) или новый алгоритм (`false`) в выделение пространства для \*-столбцов. Дополнительные сведения см. в статье [Mitigation: Grid Control's Space Allocation to Star-columns](Mitigation:%20Grid%20Control's%20Space%20Allocation%20to%20Star-columns.md) (Устранение рисков. Выделение пространства элемента управления "сетка" для столбцов со звездочкой). |.NET Framework 4.7 |
|`Switch.System.Windows.Controls.TabControl.`<br/>`SelectionPropertiesCanLagBehindSelectionChangedEvent`|Событие изменения ли селектора или вкладку управления всегда обновляет значение свойства выбранное значение перед созданием Выбор элементов управления.|.NET Framework 4.7.1|
|`Switch.System.Windows.Controls.Text.`<br/>`UseAdornerForTextboxSelectionRendering`|Определяет, является ли отрисовки не графический элемент на основе выбора для <xref:System.Windows.Controls.TextBox> и <xref:System.Windows.Controls.PasswordBox> для предотвращения перекрыто текст (`false`), текст выводится только в слое графических элементов или (`true`).|.NET framework 4.7.2|
|`Switch.System.Windows.DoNotScaleForDpiChanges`|Определяет, происходят ли изменения DPI в системе (значение `false`) или для каждого монитора (значение `true`).|.NET Framework 4.6.2|
|`Switch.System.Windows.Forms.`<br/>`DomainUpDown.UseLegacyScrolling`|Определяет, должен ли разработчик специально обрабатывать <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> действие, если присутствует текст элемента управления. `true` для обработки <xref:System.Windows.Forms.DomainUpDown.UpButton> действия; `false` для <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> и <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> действия должны быть правильно синхронизированы.|.NET framework 4.7.2|
|`Switch.System.Windows.Forms.`<br />`DontSupportReentrantFilterMessage`|Код, который позволяет использовать настраиваемый отказ <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=nameWithType> реализацию безопасно фильтровать сообщения без создания исключения при <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=nameWithType> вызывается метод. Дополнительные сведения см. в разделе [Устранение рисков: пользовательские реализации IMessageFilter.PreFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).|.NET Framework 4.6.1|  
|`Switch.System.Windows.Forms.`<br/>`UseLegacyContextMenuStripSourceControlValue`|Определяет, является ли <xref:System.Windows.Forms.ContextMenuStrip.SourceControl?displayProperty=nameWithType> свойство возвращает системы управления версиями, когда пользователь открывает меню из вложенного <xref:System.Windows.Forms.ToolStripMenuItem> элемента управления. `true` для возврата `null`, устаревшее поведение; `false` для возврата системы управления версиями.|.NET framework 4.7.2|
|`Switch.System.Windows.Input.Stylus.`<br/>`EnablePointerSupport`|Определяет необязательный `WM_POINTER`-стека на основе сенсорный ввод и пера реализуется в приложениях WPF. Дополнительные сведения см. в разделе [устранение рисков: на основе указателя касания и поддержку пера](../../../migration-guide/mitigation-pointer-based-touch-and-stylus-support.md)|.NET Framework 4.7|
|`Switch.System.Windows.Markup.`<br/>`DoNotUseSha256ForMarkupCompilerChecksumAlgorithm`|Определяет, является ли по умолчанию алгоритм хэширования, используемый для контрольные суммы SHA256 (`false`) или SHA1 (`true`).|.NET framework 4.7.2|
|`Switch.System.Windows.Media.ImageSourceConverter.`<br/>`OverrideExceptionWithNullReferenceException`|Контролирует прежних версий [NullReferenceException](xref:System.NullReferenceException) исключение вместо исключение, указывающее причину исключения, в частности (такие как [DirectoryNotFoundException](xref:System.IO.DirectoryNotFoundException) или [ FileNotFoundException](xref:System.IO.FileNotFoundException). Он предназначен для использования из кода, зависящего от обработки [NullReferenceException](xref:System.NullReferenceException). | .NET Framework 4.7 |
|`Switch.UseLegacyAccessibilityFeatures`|Элементы управления ли специальные функции, которое доступно начиная с .NET Framework 4.7.1 включены или отключены. | .NET Framework 4.7.1 |
|`Switch.UseLegacyAccessibilityFeatures.2`|Элементы управления, включены ли специальные функции, доступные в .NET Framework 4.7.2 (`false`) или отключена (`true`). Если `true`, `Switch.UseLegacyAccessibilityFeatures` также должен быть `true` для включения .NET Framework 4.7.1 специальных возможностей.|.NET framework 4.7.2|
|`System.Xml.`<br /><br /> `IgnoreEmptyKeySequences`|Определяет, игнорируются ли пустые последовательности ключей в составные ключи, проверка схемы XSD. Дополнительные сведения см. в разделе [устранение рисков: проверка схемы XML](~/docs/framework/migration-guide/mitigation-xml-schema-validation.md).|.NET Framework 4.6|  
  
> [!NOTE]
>  Вместо добавления `AppContextSwitchOverrides` элемент в файле конфигурации приложения можно также задать параметры программно, вызвав `static` (в C#) или `Shared` (в Visual Basic) <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> метод.  
  
 Разработчики библиотек можно также определить пользовательские переключатели, чтобы вызывающие методы могли отказаться от измененные функции, представленные в более поздних версиях их библиотеки. Дополнительные сведения см. в описании класса <xref:System.AppContext>.  
  
## <a name="example"></a>Пример  
 В следующем примере используется `AppContextSwitchOverrides` для определения переключателя совместимости одного приложения, `Switch.System.Globalization.NoAsyncCurrentCulture`, который препятствует проходящих через потоков в асинхронных вызовах методов языка и региональных параметров.  
  
```xml  
<configuration>  
   <runtime>  
      <AppContextSwitchOverrides value="Switch.System.Globalization.NoAsyncCurrentCulture=true" />  
   </runtime>  
</configuration>  
```  
  
 В следующем примере используется `AppContextSwitchOverrides` для определения двух параметры совместимости приложения, `Switch.System.Globalization.NoAsyncCurrentCulture` и `Switch.System.IO.BlockLongPaths`. Обратите внимание, что точка с запятой разделяет две пары имя значение.  
  
```xml  
<configuration>  
    <runtime>  
       <AppContextSwitchOverrides   
          value="Switch.System.Globalization.NoAsyncCurrentCulture=true;Switch.System.IO.BlockLongPaths=true" />  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.AppContext?displayProperty=nameWithType>  
 [\<Среда выполнения > элемент](runtime-element.md)  
 [Элемент \<configuration>](../configuration-element.md)
