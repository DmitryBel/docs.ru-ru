---
title: 'Взаимодействие с политикой кэша: максимальный возраст и устаревание'
ms.date: 03/30/2017
helpviewer_keywords:
- maximum staleness
- freshness of cached resources
- time, cached resources
- maximum age policy
- staleness of cached resources
- age of cached resources
ms.assetid: 7f775925-89a1-4956-ba90-c869c1749a94
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: 4ee2b3a0a97a0526802d6cb4c8f546a5ec4e7b85
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33392610"
---
# <a name="cache-policy-interactionmaximum-age-and-maximum-staleness"></a>Взаимодействие с политикой кэша: максимальный возраст и устаревание
Чтобы обеспечить возврат клиентскому приложению самого актуального содержимого, в результате взаимодействия политики кэша клиента и требований к повторной проверке сервера всегда применяется наиболее консервативная политика кэша. Все примеры в этом разделе иллюстрируют политику кэша для ресурса, который кэшируется 1 января и срок действия которого истекает 4 января.  
  
 В следующих примерах значение максимального возраста (`maxStale`) используется в сочетании со значением максимального срока действия (`maxAge`):  
  
-   Если в политике кэша значение `maxAge` задано равным 5 дням, а значение `maxStale` не задано, то в соответствии со значением `maxAge` содержимое можно использовать до 6 января. Однако согласно требованиям сервера к повторной проверке срок действия содержимого истекает 4 января. Так как дата истечения срока действия содержимого более консервативна (наступает раньше), она имеет приоритет над политикой `maxAge`. Поэтому срок действия содержимого истекает 4 января и его необходимо проверить повторно, несмотря на то, что максимальный срок действия не достигнут.  
  
-   Если политика кэша задает значение `maxAge` равным 5 дням, а значение `maxStale` равным 3 дням, то в соответствии со значением `maxAge` содержимое можно использовать до 6 января. Согласно значению `maxStale` содержимое можно использовать до 7 января. Поэтому оно будет проверено повторно 6 января.  
  
-   Если политика кэша задает значение `maxAge` равным 5 дням, а значение `maxStale` равным 1 дню, то в соответствии со значением `maxAge` содержимое можно использовать до 6 января. Согласно значению `maxStale` содержимое можно использовать до 5 января. Поэтому оно будет проверено повторно 5 января.  
  
 Если максимальный срок действия заканчивается раньше фактической даты истечения срока действия, приоритет имеет более консервативный критерий кэширования и значение максимального возраста не действует. В следующих примерах показан результат задания максимального возраста (`maxStale`) в случае, если максимальный срок действия (`maxAge`) истекает до того, как содержимое станет недействительным:  
  
-   Если политика кэша задает значение `maxAge` равным 1 дню, а значение `maxStale` не задано, содержимое проверяется повторно 2 января, даже если срок его действия не истек.  
  
-   Если политика кэша задает значение `maxAge` равным 1 дню, а значение `maxStale` равным 3 дням, содержимое проверяется повторно 2 января в соответствии с более консервативным параметром политики.  
  
-   Если политика кэша задает значения `maxAge` и `maxStale` равными 1 дню, содержимое повторно проверяется 2 января.  
  
## <a name="see-also"></a>См. также  
 [Управление кэшем для сетевых приложений](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [Политика кэша](../../../docs/framework/network-programming/cache-policy.md)  
 [Политики кэша на основе расположения](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 [Политики кэша на основе времени](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [Настройка кэширования в сетевых приложениях](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 [Взаимодействие с политикой кэша: максимальный возраст и минимальная актуальность](../../../docs/framework/network-programming/cache-policy-interaction-maximum-age-and-minimum-freshness.md)
