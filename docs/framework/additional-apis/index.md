---
title: Дополнительные библиотеки классов и интерфейсы API
ms.date: 01/29/2018
helpviewer_keywords:
- Additional class libraries
- Additional managed libraries
- .NET Framework out-of-band releases
- out-of-band releases
ms.assetid: cf2d9006-b631-4e5d-81cd-20aab78c60f1
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bdba02feb8cacc6ab1886c12f88716184aa2a81a
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32752433"
---
# <a name="additional-class-libraries-and-apis"></a>Дополнительные библиотеки классов и интерфейсы API

Платформа .NET Framework постоянно развивается. С целью совершенствования кроссплатформенной разработки и оперативного предоставления новых функциональных возможностей нашим клиентам мы выпускаем новые возможности в виде внештатных выпусков. В этом разделе перечислены внештатные проекты, для которых мы предоставляем документацию.  
  
Кроме того, некоторые библиотеки предназначены для конкретных платформ или реализаций .NET Framework. Например <xref:System.Text.CodePagesEncodingProvider> класса делает доступными для приложений UWP, разработанных с помощью .NET Framework кодировок кодовых страниц. В этой статье эти библиотеки перечислены тоже.  
  
## <a name="oob-projects"></a>Встроенные проекты
  
| Проект | Описание |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | Предоставляет потокобезопасные коллекции, содержимое которых никогда не меняется. |
| <xref:System.Net.Http.WinHttpHandler> | Предоставляет обработчик сообщений для <xref:System.Net.Http.HttpClient> на основе интерфейса WinHTTP ОС Windows. |
| [System.Numerics.Vectors](https://msdn.microsoft.com/library/mt452176.aspx) | Представляет собой библиотеку векторных типов, которые могут использовать преимущества аппаратного ускорения SIMD.| 
| <xref:System.Threading.Tasks.Dataflow> | Библиотека потоков данных TPL предоставляет компоненты потока данных, позволяющие повысить надежность приложений с поддержкой параллелизма. |  

## <a name="platform-specific-libraries"></a>Библиотеки для конкретных платформ
  
| Проект | Описание |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | Расширяет <xref:System.Text.EncodingProvider> класса, чтобы сделать доступными для приложений, предназначенных для универсальной платформы Windows кодировок кодовых страниц. |  
  
## <a name="private-apis"></a>Частные интерфейсы API  

Эти API-интерфейсы используются для поддержки инфраструктуры продукта и не предназначены для использования непосредственно в коде.  
  
| Имя API |
| -------- |
| [Класс System.Net.Connection](../../../docs/framework/additional-apis/connection.md) |
| [System.Net.Connection.m\_WriteList поля](../../../docs/framework/additional-apis/m_writelist.md) |
| [Класс System.Net.ConnectionGroup](../../../docs/framework/additional-apis/connectiongroup.md) |
| [System.Net.ConnectionGroup.m\_ConnectionList поля](../../../docs/framework/additional-apis/m_connectionlist.md) |
| [Класс System.Net.CoreResponseData](../../../docs/framework/additional-apis/coreresponsedata.md) |
| [System.Net.CoreResponseData.m\_ResponseHeaders поля](../../../docs/framework/additional-apis/coreresponsedata_m_responseheaders.md) |
| [System.Net.CoreResponseData.m\_StatusCode поля](../../../docs/framework/additional-apis/coreresponsedata_m_statuscode.md) |
| [System.Net.HttpWebRequest. \_AutoRedirects поля](../../../docs/framework/additional-apis/_autoredirects.md) |
| [System.Net.HttpWebRequest. \_CoreResponse поля](../../../docs/framework/additional-apis/httpwebrequest__coreresponse.md) |
| [System.Net.HttpWebRequest. \_HttpResponse поля](../../../docs/framework/additional-apis/_httpresponse.md) |
| [System.Net.ServicePoint.m\_ConnectionGroupList поля](../../../docs/framework/additional-apis/m_connectiongrouplist.md) |
| [System.Net.ServicePointManager.s\_ServicePointTable поля](../../../docs/framework/additional-apis/s_servicepointtable.md) |
| [System.Windows.Diagnostics.VisualDiagnostics.s\_isDebuggerCheckDisabledForTestPurposes поля](../../../docs/framework/additional-apis/s-isdebuggercheckdisabledfortestpurposes-field.md) |
| [Класс System.Windows.Forms.Design.DataMemberFieldEditor](../../../docs/framework/additional-apis/datamemberfieldeditor-class.md) |
| [Класс System.Windows.Forms.Design.DataMemberListEditor](../../../docs/framework/additional-apis/datamemberlisteditor-class.md) |
  
## <a name="see-also"></a>См. также

[.NET Framework и отдельные выпуски](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)
