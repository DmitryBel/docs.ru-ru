---
title: Пошаговое руководство. Упорядочение содержимого WPF для формы Windows Forms во время разработки
ms.date: 03/30/2017
helpviewer_keywords:
- WPF user control [Windows Forms], hosting in a layout panel
- WPF content [Windows Forms], arranging at design time
- Windows Forms, arranging WPF content at design time
- WPF content [Windows Forms], hosting in Windows Forms
- Windows Forms, anchoring and docking WPF content
- interoperability [WPF]
ms.assetid: 5efb1c53-1484-43d6-aa8a-f4861b99bb8a
ms.openlocfilehash: 373a7f977a9dad59cd40fd29fdd39c8fc6996ad0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33529306"
---
# <a name="walkthrough-arranging-wpf-content-on-windows-forms-at-design-time"></a>Пошаговое руководство. Упорядочение содержимого WPF для формы Windows Forms во время разработки
В этом пошаговом руководстве показано, как использовать возможности структуры Windows Forms, такие как закрепление и линии привязки, для размещения элементов управления Windows Presentation Foundation (WPF).  
  
 В этом пошаговом руководстве выполняются следующие задачи:  
  
-   создание проекта;  
  
-   создание элемента управления WPF;  
  
-   размещение элементов управления WPF на панели макета;  
  
-   использование линий привязки для выравнивания элементов управления WPF;  
  
-   привязка и закрепление элементов управления WPF.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в статье [Настройка параметров разработки в Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="prerequisites"></a>Предварительные требования  
 Ниже приведены компоненты, необходимые для выполнения данного пошагового руководства.  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)].  
  
## <a name="creating-the-project"></a>Создание проекта  
 Первым шагом является создание проекта Windows Forms.  
  
> [!NOTE]
>  При размещении содержимого WPF поддерживаются только проекты C# и Visual Basic.  
  
#### <a name="to-create-the-project"></a>Создание проекта  
  
-   Создайте новый проект приложения Windows Forms в Visual Basic или Visual C# с именем `ArrangeElementHost`.  
  
## <a name="creating-the-wpf-control"></a>Создание элемента управления WPF  
 После добавления в проект элемента управления WPF можно разместить его в форме.  
  
#### <a name="to-create-wpf-controls"></a>Создание элементов управления WPF  
  
1.  Добавьте в проект новый элемент управления WPF <xref:System.Windows.Controls.UserControl>. Используйте имя по умолчанию для этого типа элемента управления (`UserControl1.xaml`). Дополнительные сведения см. в разделе [Пошаговое руководство: Создание нового WPF содержимого в формах Windows Forms во время разработки](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  Убедитесь в том, что элемент `UserControl1` выбран в представлении конструирования. Дополнительные сведения см. в разделе [как: Выбор и перемещение элементов в рабочей области конструирования](http://msdn.microsoft.com/library/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  В **свойства** задайте значение <xref:System.Windows.FrameworkElement.Width%2A> и <xref:System.Windows.FrameworkElement.Height%2A> свойства `200`.  
  
4.  Задайте для свойства <xref:System.Windows.Controls.Control.Background%2A> значение `Blue`.  
  
5.  Выполните построение проекта.  
  
## <a name="hosting-wpf-controls-in-a-layout-panel"></a>Размещение элементов управления WPF на панели макета  
 Элементы управления WPF можно использовать на панели макета так же, как и другие элементы управления Windows Forms.  
  
#### <a name="to-host-wpf-controls-in-a-layout-panel"></a>Размещение элементов управления WPF на панели макета  
  
1.  Откройте `Form1` в конструкторе Windows Forms.  
  
2.  В **элементов**, перетащите <xref:System.Windows.Forms.TableLayoutPanel> в форму элемент управления.  
  
3.  На <xref:System.Windows.Forms.TableLayoutPanel> панель смарт-тегов элемента управления, выберите **удалить последнюю строку**.  
  
4.  Увеличьте высоту и ширину элемента управления <xref:System.Windows.Forms.TableLayoutPanel>.  
  
5.  В **элементов**, дважды щелкните `UserControl1` для создания экземпляра `UserControl1` в первую ячейку <xref:System.Windows.Forms.TableLayoutPanel> элемента управления.  
  
     Экземпляр `UserControl1` размещается в новом элементе управления <xref:System.Windows.Forms.Integration.ElementHost> под именем `elementHost1`.  
  
6.  В **элементов**, дважды щелкните `UserControl1` для создания другого экземпляра в во вторую ячейку <xref:System.Windows.Forms.TableLayoutPanel> элемента управления.  
  
7.  В **Структура документа** выберите `tableLayoutPanel1`. Дополнительные сведения см. в разделе [окно структуры документа](http://msdn.microsoft.com/library/9054f2bc-f6f8-4242-9fe0-be71089b12f8).  
  
8.  В **свойства** задайте значение <xref:System.Windows.Forms.Control.Padding%2A> свойства `10, 10, 10, 10`.  
  
     Размер обоих элементов управления <xref:System.Windows.Forms.Integration.ElementHost> изменится в соответствии с новой структурой.  
  
## <a name="using-snaplines-to-align-wpf-controls"></a>Выравнивание элементов управления WPF с помощью линий привязки  
 Линии привязки позволяют легко выравнивать элементы управления в форме. Линии привязки также можно использовать для выравнивания элементов управления WPF. Дополнительные сведения см. в разделе [Пошаговое руководство: упорядочение элементов управления в формах Windows Forms с помощью линий привязки](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md).  
  
#### <a name="to-use-snaplines-to-align-wpf-controls"></a>Выравнивание элементов управления WPF с помощью линий привязки  
  
1.  Из **элементов**, перетащите экземпляр `UserControl1` в форму и поместите его под <xref:System.Windows.Forms.TableLayoutPanel> элемента управления.  
  
     Экземпляр `UserControl1` размещается в новом элементе управления <xref:System.Windows.Forms.Integration.ElementHost> под именем `elementHost3`.  
  
2.  С помощью линий привязки выровняйте левый край `elementHost3` относительно левого края элемента управления <xref:System.Windows.Forms.TableLayoutPanel>.  
  
3.  С помощью линий привязки установите для `elementHost3` ту же ширину, что и для элемента управления <xref:System.Windows.Forms.TableLayoutPanel>.  
  
4.  Перемещайте `elementHost3` в сторону элемента управления <xref:System.Windows.Forms.TableLayoutPanel> до тех пор, пока между элементами управления не появится центральная линия привязки.  
  
5.  В **свойства** задайте значение свойства поля для `20, 20, 20, 20`.  
  
6.  Перемещайте `elementHost3` от элемента управления <xref:System.Windows.Forms.TableLayoutPanel> до тех пор, пока между элементами управления снова не появится центральная линия привязки. Теперь центральная линия привязки указывает на поле шириной в 20 точек.  
  
7.  Перемещайте элемент управления `elementHost3` вправо до тех пор, пока его левый край не будет выровнен относительно левого края элемента управления `elementHost1`.  
  
8.  Изменяйте ширину элемента `elementHost3` до тех пор, пока его правый край не будет выровнен относительно правого края элемента управления `elementHost2`.  
  
## <a name="anchoring-and-docking-wpf-controls"></a>Привязка и закрепление элементов управления WPF  
 Поведение размещенного в форме элемента управления WPF при привязке и закреплении не отличается от поведения других элементов управления Windows Forms.  
  
#### <a name="to-anchor-and-dock-wpf-controls"></a>Привязка и закрепление элементов управления WPF  
  
1.  Выберите `elementHost1`.  
  
2.  В **свойства** задайте <xref:System.Windows.Forms.Control.Anchor%2A> свойства **верхнего, нижнего, Left, Right**.  
  
3.  Увеличьте размер элемента управления <xref:System.Windows.Forms.TableLayoutPanel>.  
  
     Элемент управления `elementHost1` заполнит всю ячейку.  
  
4.  Выберите `elementHost2`.  
  
5.  В **свойства** задайте значение <xref:System.Windows.Forms.Control.Dock%2A> свойства <xref:System.Windows.Forms.DockStyle.Fill>.  
  
     Элемент управления `elementHost2` заполнит всю ячейку.  
  
6.  Выберите элемент управления <xref:System.Windows.Forms.TableLayoutPanel>.  
  
7.  Задайте для его свойства <xref:System.Windows.Forms.Control.Dock%2A> значение <xref:System.Windows.Forms.DockStyle.Top>.  
  
8.  Выберите `elementHost3`.  
  
9. Задайте для его свойства <xref:System.Windows.Forms.Control.Dock%2A> значение <xref:System.Windows.Forms.DockStyle.Fill>.  
  
     Элемент управления `elementHost3` заполнит все оставшееся пространство в форме.  
  
10. Измените размер формы.  
  
     Размер всех трех элементов управления <xref:System.Windows.Forms.Integration.ElementHost> изменится соответствующим образом.  
  
     Дополнительные сведения см. в разделе [как: привязка и закрепление дочерних элементов управления в элементе управления TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 [Практическое руководство. Привязка и закрепление дочерних элементов управления в элементе управления TableLayoutPanel](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)  
 [Практическое руководство. Выравнивание элементов управления по границам формы во время выполнения](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)  
 [Пример. Упорядочение элементов управления в формах Windows Forms с помощью линий привязки](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)  
 [Миграция и взаимодействие систем](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)  
 [Использование элементов управления WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)  
 [Конструктор WPF](http://msdn.microsoft.com/library/c6c65214-8411-4e16-b254-163ed4099c26)
