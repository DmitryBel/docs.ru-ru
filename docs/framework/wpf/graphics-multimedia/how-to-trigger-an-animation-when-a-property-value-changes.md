---
title: Практическое руководство. Запуск анимации при изменении значения свойства
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], starting when property values change
- triggering animation [WPF]
- Storyboards [WPF], starting when property values change
ms.assetid: 12399c21-0300-4f4f-9e3a-d92d9907e5f5
ms.openlocfilehash: f127f00445a587ee097faa6bed28e124690de10e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33561321"
---
# <a name="how-to-trigger-an-animation-when-a-property-value-changes"></a>Практическое руководство. Запуск анимации при изменении значения свойства
В этом примере показано, как использовать <xref:System.Windows.Trigger> запуск <xref:System.Windows.Media.Animation.Storyboard> при изменении значения свойства. Можно использовать <xref:System.Windows.Trigger> внутри <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, или <xref:System.Windows.DataTemplate>.  
  
## <a name="example"></a>Пример  
 В следующем примере используется <xref:System.Windows.Trigger> для анимации <xref:System.Windows.UIElement.Opacity%2A> из <xref:System.Windows.Controls.Button> при его <xref:System.Windows.UIElement.IsMouseOver%2A> свойство становится `true`.  
  
 [!code-xaml[AnimatePropertyStoryboards#PropertyTriggerExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/PropertyTriggerExample.xaml#propertytriggerexample)]  
  
 Анимации с помощью свойства <xref:System.Windows.Trigger> объекты ведут себя в сложнее, чем <xref:System.Windows.EventTrigger> анимации или анимации работы с использованием <xref:System.Windows.Media.Animation.Storyboard> методов.  Они «передаваться» с анимацией определенные другими <xref:System.Windows.Trigger> объектов, но объединено <xref:System.Windows.EventTrigger> и запустить метод анимации.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Trigger>  
 [Общие сведения о методах анимации свойств](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)  
 [Общие сведения о раскадровке](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)
