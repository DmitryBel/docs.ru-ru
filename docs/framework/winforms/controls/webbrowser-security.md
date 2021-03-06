---
title: Безопасность элемента управления WebBrowser
ms.date: 03/30/2017
helpviewer_keywords:
- WebBrowser control [Windows Forms], security
- security [Windows Forms], WebBrowser control
ms.assetid: 0968846e-48ee-485a-9797-65b5b9a622f8
ms.openlocfilehash: 730d8f692a44a06ea142bb870bbd961d5983c785
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33534616"
---
# <a name="webbrowser-security"></a>Безопасность элемента управления WebBrowser
<xref:System.Windows.Forms.WebBrowser> Управления предназначен для работы в режиме полного доверия. HTML-содержимое, отображаемое на элементе управления могут поступать из внешних веб-серверов и может содержать неуправляемый код в форме скриптов или веб-элементов управления. Если вы используете <xref:System.Windows.Forms.WebBrowser> управления в этом случае элемент управления не менее безопасен, чем бы Internet Explorer, но управляемый <xref:System.Windows.Forms.WebBrowser> управления не препятствует такого неуправляемого кода выполняется.  
  
 Дополнительные сведения о проблемах безопасности, связанные с базовой ActiveX `WebBrowser` управления см. в разделе [элемент управления WebBrowser](http://go.microsoft.com/fwlink/?LinkId=198812).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.WebBrowser>  
 [Общие сведения об элементе управления WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)  
 [Элемент управления WebBrowser](http://go.microsoft.com/fwlink/?LinkId=198812)
