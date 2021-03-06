---
title: Практическое руководство. Выравнивание элементов управления по границам формы во время выполнения
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], docking using designer
- Dock property [Windows Forms], aligning controls (using designer)
ms.assetid: 51f08998-5e3b-4330-be58-a4edd0eb60f4
ms.openlocfilehash: 5b36879413442ff99da034fcbee6bf6388affa6d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33528724"
---
# <a name="how-to-align-a-control-to-the-edges-of-forms-at-design-time"></a>Практическое руководство. Выравнивание элементов управления по границам формы во время выполнения
Можно сделать элемент управления Выровнять по границе формы, задав <xref:System.Windows.Forms.Control.Dock%2A>. Это свойство определяет, в каком месте формы будет размещаться элемент управления. Свойство <xref:System.Windows.Forms.Control.Dock%2A> может принимать указанные ниже значения.  
  
|Параметр|Влияние на элемент управления|  
|-------------|----------------------------|  
|<xref:System.Windows.Forms.DockStyle.Bottom>|Фиксирует элемент управления у нижнего края формы.|  
|<xref:System.Windows.Forms.DockStyle.Fill>|Заполняет все свободное пространство формы.|  
|<xref:System.Windows.Forms.DockStyle.Left>|Фиксирует элемент управления у левого края формы.|  
|<xref:System.Windows.Forms.DockStyle.None>|Не фиксирует элемент нигде, он отображается в месте, указанном в его <xref:System.Windows.Forms.Control.Location%2A>.|  
|<xref:System.Windows.Forms.DockStyle.Right>|Фиксирует элемент управления у правого края формы.|  
|<xref:System.Windows.Forms.DockStyle.Top>|Фиксирует элемент управления у верхнего края формы.|  
  
 Эти значения можно также задать в коде. Дополнительные сведения см. в разделе [как: выравнивание элементов управления на границы формы](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md).  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в статье [Настройка параметров разработки в Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-set-the-dock-property-for-your-control-at-design-time"></a>Чтобы задать свойства Dock для элемента управления во время разработки  
  
1.  В конструкторе Windows Forms выберите элемент управления.  
  
2.  В **свойства** окно, щелкните раскрывающийся список полю <xref:System.Windows.Forms.Control.Dock%2A> свойство.  
  
     Графический интерфейс с шестью возможными <xref:System.Windows.Forms.Control.Dock%2A> параметров отображается.  
  
3.  Выберите соответствующий параметр.  
  
4.  Элемент управления будет зафиксировано в соответствии с параметр.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=nameWithType>  
 [Практическое руководство. Выравнивание элементов управления по границам формы](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md)  
 [Пример. Упорядочение элементов управления в формах Windows Forms с помощью линий привязки](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)  
 [Практическое руководство. Привязка элементов управления в формах Windows Forms](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)  
 [Практическое руководство. Привязка и закрепление дочерних элементов управления в элементе управления TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)  
 [Практическое руководство. Закрепление дочерних элементов управления в элементе управления FlowLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)  
 [Пошаговое руководство. Упорядочение элементов управления в формах Windows Forms с помощью элемента TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)  
 [Пошаговое руководство. Упорядочение элементов управления в формах Windows Forms с помощью элемента FlowLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)  
 [Создание элементов управления Windows Forms во время разработки](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)
