---
title: Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control contract [WPF]
- controls [WPF], visual structure changes
- ControlTemplate [WPF], customizing for existing controls
- skinning controls [WPF]
- controls [WPF], appearance specified by state
- templates [WPF], custom for existing controls
ms.assetid: 678dd116-43a2-4b8c-82b5-6b826f126e31
ms.openlocfilehash: bbdc79fabf8dbe344baae66d718d79ac6375db7e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33558061"
---
# <a name="customizing-the-appearance-of-an-existing-control-by-creating-a-controltemplate"></a>Настройка внешнего вида существующего элемента управления путем создания объекта ControlTemplate
<a name="introduction"></a> Объект <xref:System.Windows.Controls.ControlTemplate> указывает визуальную структуру и визуальное поведение элемента управления. Можно настроить внешний вид элемента управления, предоставляя ему новый <xref:System.Windows.Controls.ControlTemplate>. При создании <xref:System.Windows.Controls.ControlTemplate>, замените внешний вид существующего элемента управления без изменения его функциональность. Например, можно сделать кнопки в приложении round, а не по умолчанию квадратных, но будет по-прежнему вызывать кнопки <xref:System.Windows.Controls.Primitives.ButtonBase.Click> событий.  
  
 В этом разделе объясняется различные части <xref:System.Windows.Controls.ControlTemplate>, показано, как создать простой <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.Button>и объясняется, как понимать контракт элемента управления, чтобы можно было настроить его внешний вид. Поскольку вы создаете <xref:System.Windows.Controls.ControlTemplate> в [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], можно изменить внешний вид элемента управления без написания кода. Можно также использовать конструктор, например Microsoft Expression Blend, чтобы создать шаблоны пользовательского элемента управления. В этом разделе приведены примеры [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] , настроить внешний вид <xref:System.Windows.Controls.Button> и перечислены в полном примере в конце этого раздела. Дополнительные сведения об использовании Expression Blend см. в статье [Настройка стиля элемента управления, поддерживающего шаблон](http://go.microsoft.com/fwlink/?LinkId=161153).  
  
 На следующих рисунках <xref:System.Windows.Controls.Button> , использующий <xref:System.Windows.Controls.ControlTemplate> , созданного в этом разделе.  
  
 ![Кнопка с пользовательским шаблоном элемента управления. ] (../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP_ButtonNormal")  
Кнопка, использующая пользовательский шаблон элемента управления  
  
 ![Кнопка с красной границей. ] (../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP_ButtonMouseOver")  
Кнопка, использующая пользовательский шаблон элемента управления, когда на ней находится указатель мыши  
  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Предварительные требования  
 В этом разделе предполагается, что пользователь понимает процесс создания и использования элементов управления и стилей, который рассматривался в разделе [Элементы управления](../../../../docs/framework/wpf/controls/index.md). Концепции, описанные в этом разделе применяются к элементам, которые наследуют от <xref:System.Windows.Controls.Control> класса, за исключением <xref:System.Windows.Controls.UserControl>. Не удается применить <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.UserControl>.  
  
<a name="when_you_should_create_a_controltemplate"></a>   
## <a name="when-you-should-create-a-controltemplate"></a>Когда следует создавать объект ControlTemplate  
 Элементы управления обладают множеством свойств, таких как <xref:System.Windows.Controls.Border.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>, и <xref:System.Windows.Controls.Control.FontFamily%2A>, можно задать для указания различных аспектов внешнего вида элемента управления, но изменения, сделанные при установке этих свойств ограничены. Например, можно задать <xref:System.Windows.Controls.Control.Foreground%2A> свойство на синий и <xref:System.Windows.Controls.Control.FontStyle%2A> к тексту курсивного на <xref:System.Windows.Controls.CheckBox>.  
  
 Без возможности для создания нового <xref:System.Windows.Controls.ControlTemplate> для элементов управления, все элементы управления в каждом [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-приложения будет иметь общие одинаково, что ограничивает возможность создания приложения с помощью пользовательского интерфейса. По умолчанию каждый <xref:System.Windows.Controls.CheckBox> имеет одинаковые характеристики. Например, содержимое <xref:System.Windows.Controls.CheckBox> всегда находится справа от индикатора выделения, а флажок всегда используется для указания того, что <xref:System.Windows.Controls.CheckBox> выбран.  
  
 Вы создаете <xref:System.Windows.Controls.ControlTemplate> используется для настройки внешнего вида элемента управления за пределами какие задавать другие свойства элемента управления будет выполнять. В качестве примера <xref:System.Windows.Controls.CheckBox>, предположим, что вы хотите содержимое флажок, чтобы быть над индикатором выделения и знак x, чтобы указать, что <xref:System.Windows.Controls.CheckBox> выбран. Укажите эти изменения в <xref:System.Windows.Controls.ControlTemplate> из <xref:System.Windows.Controls.CheckBox>.  
  
 На следующем рисунке показана <xref:System.Windows.Controls.CheckBox> , используется значение по умолчанию <xref:System.Windows.Controls.ControlTemplate>.  
  
 ![Флажок с шаблоном элемента управления по умолчанию. ] (../../../../docs/framework/wpf/controls/media/ndp-checkboxdefault.png "NDP_CheckBoxDefault")  
Элемент управления CheckBox, использующий шаблон элемента управления по умолчанию  
  
 На следующем рисунке показана <xref:System.Windows.Controls.CheckBox> , использующий пользовательский <xref:System.Windows.Controls.ControlTemplate> для размещения содержимого <xref:System.Windows.Controls.CheckBox> над индикатором выделения и отображения знака X при <xref:System.Windows.Controls.CheckBox> выбран.  
  
 ![Флажок с пользовательским шаблоном элемента управления. ] (../../../../docs/framework/wpf/controls/media/ndp-checkboxcustom.png "NDP_CheckBoxCustom")  
Элемент управления CheckBox, использующий пользовательский шаблон элемента управления  
  
 <xref:System.Windows.Controls.ControlTemplate> Для <xref:System.Windows.Controls.CheckBox> в этом примере — сравнительно сложная, поэтому в этом разделе используется простой пример создания <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.Button>.  
  
<a name="changing_the_visual_structure_of_a_control"></a>   
## <a name="changing-the-visual-structure-of-a-control"></a>Изменение визуальной структуры элемента управления  
 В [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], чаще всего элемента управления составного <xref:System.Windows.FrameworkElement> объектов. При создании <xref:System.Windows.Controls.ControlTemplate>, можно объединить <xref:System.Windows.FrameworkElement> объектов для построения одного элемента управления. Объект <xref:System.Windows.Controls.ControlTemplate> должен иметь только один <xref:System.Windows.FrameworkElement> качестве корневого элемента. Корневой элемент обычно содержит другие <xref:System.Windows.FrameworkElement> объекты. Комбинация объектов составляет визуальную структуру элемента управления.  
  
 В следующем примере создается настраиваемый <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.Button>. <xref:System.Windows.Controls.ControlTemplate> Создается структура visual <xref:System.Windows.Controls.Button>. В этом примере не меняется внешний вид кнопки при перемещении на нее указателя мыши или при ее нажатии. Изменение внешнего вида кнопки при ее переходе в другое состояние рассматривается далее в этом разделе.  
  
 В данном примере визуальная структура состоит из следующих частей:  
  
-   Объект <xref:System.Windows.Controls.Border> с именем `RootElement` , служит в качестве корневого шаблона <xref:System.Windows.FrameworkElement>.  
  
-   Объект <xref:System.Windows.Controls.Grid> , являющийся потомком `RootElement`.  
  
-   Объект <xref:System.Windows.Controls.ContentPresenter> , отображающий содержимое кнопки. <xref:System.Windows.Controls.ContentPresenter> Позволяет любой тип объекта для отображения.  
  
 [!code-xaml[VSMButtonTemplate#BasicTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#basictemplate)]  
  
### <a name="preserving-the-functionality-of-a-controls-properties-by-using-templatebinding"></a>Сохранение функциональности свойств элемента управления с помощью TemplateBinding  
 При создании нового <xref:System.Windows.Controls.ControlTemplate>, по-прежнему может потребоваться использовать общие свойства для изменения внешнего вида элемента управления. [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) расширение разметки привязывает свойство элемента, который находится в <xref:System.Windows.Controls.ControlTemplate> к открытым свойством, которое определяется элементом управления. Использование расширения [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) позволяет свойствам элемента управления действовать в качестве параметров шаблона. Это означает, что при задании свойства элемента управления соответствующее значение передается в элемент, который содержит [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md).  
  
 В следующем примере повторяется часть предыдущего примера, который использует [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) расширение разметки, чтобы привязать свойства элементов, которые находятся в <xref:System.Windows.Controls.ControlTemplate> к общим свойствам, которые определены на кнопке.  
  
 [!code-xaml[VSMButtonTemplate#TemplateBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#templatebinding)]  
  
 В этом примере <xref:System.Windows.Controls.Grid> имеет его <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> шаблон свойство привязан к <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType>. Поскольку <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> будет привязано к шаблону, можно создать несколько кнопок, использующих один <xref:System.Windows.Controls.ControlTemplate> и задайте <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> в разные значения для каждой кнопки. Если <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> шаблон не был привязан к свойству элемента в <xref:System.Windows.Controls.ControlTemplate>, параметр <xref:System.Windows.Controls.Control.Background%2A?displayProperty=nameWithType> кнопки окажет никакого воздействия на внешний вид кнопки.  
  
 Следует отметить, что не требуется, чтобы имена этих двух свойств совпадали. В приведенном выше примере <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=nameWithType> свойство <xref:System.Windows.Controls.Button> привязано к шаблону <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=nameWithType> свойство <xref:System.Windows.Controls.ContentPresenter>. Это позволяет располагать содержимое кнопки горизонтально. <xref:System.Windows.Controls.ContentPresenter> имеет свойство с именем `HorizontalContentAlignment`, но <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=nameWithType> могут быть привязаны к <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=nameWithType>. Перед привязкой свойства к шаблону следует убедиться, что целевое и исходное свойства имеют один и тот же тип.  
  
 <xref:System.Windows.Controls.Control> Класс определяет несколько свойств, которые необходимо использовать шаблон элемента управления для оказывать влияние на элемент управления, если они заданы. Как <xref:System.Windows.Controls.ControlTemplate> использует свойство зависит от свойства. <xref:System.Windows.Controls.ControlTemplate> Необходимо использовать свойство одним из следующих способов:  
  
-   На элемент <xref:System.Windows.Controls.ControlTemplate> шаблона привязывается к свойству.  
  
-   Элемент в <xref:System.Windows.Controls.ControlTemplate> наследует свойство от родительского объекта <xref:System.Windows.FrameworkElement>.  
  
 В следующей таблице перечислены визуальные свойства, наследуемые элементом управления от <xref:System.Windows.Controls.Control> класса. В таблице также указывается, использует ли шаблон элемента управления по умолчанию значение наследуемого свойства или оно должно быть привязано к шаблону.  
  
|Свойство.|Способ использования|  
|--------------|------------------|  
|<xref:System.Windows.Controls.Control.Background%2A>|Привязка к шаблону|  
|<xref:System.Windows.Controls.Control.BorderThickness%2A>|Привязка к шаблону|  
|<xref:System.Windows.Controls.Control.BorderBrush%2A>|Привязка к шаблону|  
|<xref:System.Windows.Controls.Control.FontFamily%2A>|Наследование свойства или привязка к шаблону|  
|<xref:System.Windows.Controls.Control.FontSize%2A>|Наследование свойства или привязка к шаблону|  
|<xref:System.Windows.Controls.Control.FontStretch%2A>|Наследование свойства или привязка к шаблону|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|Наследование свойства или привязка к шаблону|  
|<xref:System.Windows.Controls.Control.Foreground%2A>|Наследование свойства или привязка к шаблону|  
|<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>|Привязка к шаблону|  
|<xref:System.Windows.Controls.Control.Padding%2A>|Привязка к шаблону|  
|<xref:System.Windows.Controls.Control.VerticalContentAlignment%2A>|Привязка к шаблону|  
  
 В таблице перечислены только визуальные свойства, наследуемые от <xref:System.Windows.Controls.Control> класса. Помимо свойств, перечисленных в таблице, также может наследовать элемент управления <xref:System.Windows.FrameworkElement.DataContext%2A>, <xref:System.Windows.FrameworkElement.Language%2A>, и <xref:System.Windows.Controls.TextBlock.TextDecorations%2A> свойства из родительского элемента структуры.  
  
 Кроме того Если <xref:System.Windows.Controls.ContentPresenter> в <xref:System.Windows.Controls.ControlTemplate> из <xref:System.Windows.Controls.ContentControl>, <xref:System.Windows.Controls.ContentPresenter> будет автоматически привязан к <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> и <xref:System.Windows.Controls.ContentControl.Content%2A> свойства. Аналогичным образом <xref:System.Windows.Controls.ItemsPresenter> , находящийся в <xref:System.Windows.Controls.ControlTemplate> из <xref:System.Windows.Controls.ItemsControl> будет автоматически привязан к <xref:System.Windows.Controls.ItemsControl.Items%2A> и <xref:System.Windows.Controls.ItemsPresenter> свойства.  
  
 В следующем примере создается две кнопки, которые используют <xref:System.Windows.Controls.ControlTemplate> определенный в предыдущем примере. В примере устанавливается <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>, и <xref:System.Windows.Controls.Control.FontSize%2A> свойства на каждой кнопке. Установка <xref:System.Windows.Controls.Control.Background%2A> свойство имеет значение, поскольку это шаблон, привязанных к <xref:System.Windows.Controls.ControlTemplate>. Несмотря на то что <xref:System.Windows.Controls.Control.Foreground%2A> и <xref:System.Windows.Controls.Control.FontSize%2A> свойства не привязаны к шаблону, настраивать их действует так, как их значения будут наследоваться.  
  
 [!code-xaml[VSMButtonTemplate#ButtonDeclaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#buttondeclaration)]  
  
 В предыдущем примере получался результат, аналогичный показанному на следующем рисунке.  
  
 ![Две кнопки, одна синяя и другая — фиолетовая. ] (../../../../docs/framework/wpf/controls/media/ndp-buttontwo.png "NDP_ButtonTwo")  
Две кнопки с различными цветами фона  
  
<a name="changing_the_appearance_of_a_control_depending_on_its_state"></a>   
## <a name="changing-the-appearance-of-a-control-depending-on-its-state"></a>Изменение внешнего вида элемента управления в зависимости от его состояния  
 Разница между кнопкой с внешним видом по умолчанию и кнопкой из предыдущего примера состоит в том, что кнопка по умолчанию слегка изменяется при переходе в другое состояние. Например, внешний вид кнопки по умолчанию изменяется при нажатии этой кнопки или при наведении на нее указателя мыши. Несмотря на то что <xref:System.Windows.Controls.ControlTemplate> не изменяет функциональные возможности элемента управления, это приводит к изменению поведения визуального элемента управления. Визуальное поведение описывает внешний вид элемента управления в определенных состояниях. Чтобы лучше понять разницу между функциональностью и визуальным поведением элемента управления, рассмотрим пример с кнопкой. Представляет собой вызов функции кнопок <xref:System.Windows.Controls.Primitives.ButtonBase.Click> событие при щелчке, однако поведение visual кнопки при нажатии и указывает, изменить его внешний вид.  
  
 Вы используете <xref:System.Windows.VisualState> объекты для указания вида элемента управления, когда он находится в определенном состоянии. Объект <xref:System.Windows.VisualState> содержит <xref:System.Windows.Media.Animation.Storyboard> , изменяется внешний вид элементов, которые находятся в <xref:System.Windows.Controls.ControlTemplate>. Не нужно писать код, чтобы это происходило, поскольку логика элемента управления изменяет состояние с помощью <xref:System.Windows.VisualStateManager>. Когда элемент управления переходит в состояние, который задается параметром <xref:System.Windows.VisualState.Name%2A?displayProperty=nameWithType> свойства <xref:System.Windows.Media.Animation.Storyboard> начинается. Если элемент управления выходит из состояния <xref:System.Windows.Media.Animation.Storyboard> останавливается.  
  
 В следующем примере показан <xref:System.Windows.VisualState> , изменяется внешний вид <xref:System.Windows.Controls.Button> когда указатель мыши находится над ним. <xref:System.Windows.Media.Animation.Storyboard> Изменяет цвет границы кнопки путем изменения цвета `BorderBrush`. Если вы ссылаетесь на <xref:System.Windows.Controls.ControlTemplate> примере в начале этого раздела, можно увидеть, что `BorderBrush` имя <xref:System.Windows.Media.SolidColorBrush> , которые назначены <xref:System.Windows.Controls.Border.Background%2A> из <xref:System.Windows.Controls.Border>.  
  
 [!code-xaml[VSMButtonTemplate#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#4)]  
  
 Элемент управления отвечает за определение состояний как часть своего контракта, что подробно рассматривается в подразделе [Настройка других элементов управления через понимание контракта элемента управления](#customizing_other_controls_by_understanding_the_control_contract) далее в этом разделе. В следующей таблице перечислены состояния, которые указаны для <xref:System.Windows.Controls.Button>.  
  
|Имя VisualState|Имя VisualStateGroup|Описание|  
|----------------------|---------------------------|-----------------|  
|Норм.|CommonStates|Состояние по умолчанию.|  
|MouseOver|CommonStates|Указатель мыши расположен в элементе управления.|  
|Нажато|CommonStates|Элемент управления нажат.|  
|Отключено|CommonStates|Элемент управления отключен.|  
|Focused|FocusStates|Элемент управления имеет фокус.|  
|Без фокуса ввода|FocusStates|Элемент управления не имеет фокуса.|  
  
 <xref:System.Windows.Controls.Button> Определяет две группы: `CommonStates` группа содержит `Normal`, `MouseOver`, `Pressed`, и `Disabled` состояния. Группа `FocusStates` содержит состояния `Focused` и `Unfocused`. Состояния, входящие в одну группу, являются взаимоисключающими. Элемент управления всегда находится строго в одном состоянии из каждой группы. Например <xref:System.Windows.Controls.Button> может иметь фокус, даже в том случае, если указатель мыши наведен не, поэтому <xref:System.Windows.Controls.Button> в `Focused` состояние может быть в `MouseOver`, `Pressed`, или `Normal` состояния.  
  
 Добавить <xref:System.Windows.VisualState> объектов <xref:System.Windows.VisualStateGroup> объектов. Добавить <xref:System.Windows.VisualStateGroup> объектов <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> вложенное свойство. В следующем примере определяется <xref:System.Windows.VisualState> объектов для `Normal`, `MouseOver`, и `Pressed` состояний, которые находятся в `CommonStates` группы. <xref:System.Windows.VisualState.Name%2A> Каждого <xref:System.Windows.VisualState> совпадает с именем в предыдущей таблице. Состояние `Disabled` и состояния из группы `FocusStates` опущены для сохранения краткости примера, но они включены в полный пример, приведенный в конце этого раздела.  
  
> [!NOTE]
>  Не забудьте задать <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> вложенное свойство в корне <xref:System.Windows.FrameworkElement> из <xref:System.Windows.Controls.ControlTemplate>.  
  
 [!code-xaml[VSMButtonTemplate#VisualStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualstates)]  
  
 В предыдущем примере получался результат, аналогичный показанному на следующих рисунках.  
  
 ![Кнопка с пользовательским шаблоном элемента управления. ] (../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP_ButtonNormal")  
Кнопка, использующая пользовательский шаблон элемента управления в нормальном состоянии  
  
 ![Кнопка с красной границей. ] (../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP_ButtonMouseOver")  
Кнопка, использующая пользовательский шаблон элемента управления в состоянии, когда указатель мыши находится над кнопкой  
  
 ![Граница прозрачна на нажатой кнопке. ] (../../../../docs/framework/wpf/controls/media/ndp-buttonpressed.png "NDP_ButtonPressed")  
Кнопка, использующая пользовательский шаблон элемента управления в состоянии, когда она нажата  
  
 Визуальные состояния элементов управления, включенных в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], см. в разделе [Стили и шаблоны элемента Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md).  
  
<a name="specifying_the_behavior_of_a_control_when_it_transitions_between_states"></a>   
## <a name="specifying-the-behavior-of-a-control-when-it-transitions-between-states"></a>Задание поведения элемента управления, когда он переходит между состояниями  
 В предыдущем примере внешний вид кнопки изменяется, когда пользователь нажимает ее, но если кнопка остается нажатой менее полной секунды, то пользователь не видит эффекта нажатия. По умолчанию для запуска анимации требуется одна секунда. Поскольку пользователи, скорее всего, нажмите и отпустите кнопку гораздо меньше времени, визуальную обратную связь не будет действовать в том случае, если оставить <xref:System.Windows.Controls.ControlTemplate> в состоянии по умолчанию.  
  
 Можно указать время, затрачиваемое анимации плавно переходил элемент управления из одного состояния в другое, добавив <xref:System.Windows.VisualTransition> объектов <xref:System.Windows.Controls.ControlTemplate>. При создании <xref:System.Windows.VisualTransition>, вы указываете одну или несколько из следующих:  
  
-   время, которое занимает переход между состояниями;  
  
-   дополнительные изменения внешнего вида элемента управления, возникающие во время перехода;  
  
-   Какие состояния <xref:System.Windows.VisualTransition> применяется.  
  
### <a name="specifying-the-duration-of-a-transition"></a>Задание продолжительности перехода  
 Можно указать, как долго выполняет переход, задав <xref:System.Windows.VisualTransition.GeneratedDuration%2A> свойство. В предыдущем примере имеется <xref:System.Windows.VisualState> , указывающий, что граница кнопки становится прозрачной при нажатии кнопки, но анимация продолжается слишком долго будет заметно, если быстро нажата и отпущена кнопка. Можно использовать <xref:System.Windows.VisualTransition> чтобы указать количество времени, необходимое элемента управления для перехода в нажатом состоянии. В следующем примере задается, что переход элемента управления в нажатое состояние занимает одну сотую секунды.  
  
 [!code-xaml[VSMButtonTemplate#PressedTransition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#pressedtransition)]  
  
### <a name="specifying-changes-to-the-controls-appearance-during-a-transition"></a>Задание изменений внешнего вида элемента управления во время перехода  
 <xref:System.Windows.VisualTransition> Содержит <xref:System.Windows.Media.Animation.Storyboard> , начинается при переходе элемента управления между состояниями. Например, можно указать, что определенная анимация происходит при переходе элемента управления из состояния `MouseOver` в состояние `Normal`. В следующем примере создается <xref:System.Windows.VisualTransition> , определяет, что когда пользователь перемещает указатель мыши за пределы кнопки, граница кнопки изменяет цвет на синий, затем становится желтым, а затем в черный цвет в 1,5 секунд.  
  
 [!code-xaml[VSMButtonTemplate#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#8)]  
  
### <a name="specifying-when-a-visualtransition-is-applied"></a>Указание места применения VisualTransition  
 Объект <xref:System.Windows.VisualTransition> можно ограничить только определенными состояниями, или оно может применяться каждый раз управления переходы между состояниями. В приведенном выше примере <xref:System.Windows.VisualTransition> применяется, когда элемент управления переходит от `MouseOver` состояние `Normal` состояние; в примере перед <xref:System.Windows.VisualTransition> применяется, когда элемент управления переходит в `Pressed` состояние. Ограничивается <xref:System.Windows.VisualTransition> применяется, задав <xref:System.Windows.VisualTransition.To%2A> и <xref:System.Windows.VisualTransition.From%2A> свойства. В таблице ниже приведено описание уровней ограничений от наибольшего до наименьшего.  
  
|Тип ограничения|Состояние, из которого выполняется переход|Состояние, в которое выполняется переход|  
|-------------------------|-------------------|-----------------|  
|Из указанного состояния в другое указанное состояние|Имя <xref:System.Windows.VisualState>|Имя <xref:System.Windows.VisualState>|  
|Из любого состояния в указанное состояние|Не задано|Имя <xref:System.Windows.VisualState>|  
|Из указанного состояния в любое состояние|Имя <xref:System.Windows.VisualState>|Не задано|  
|Из любого состояния в любое другое состояние|Не задано|Не задано|  
  
 Может иметь несколько <xref:System.Windows.VisualTransition> объекты в <xref:System.Windows.VisualStateGroup> , которые ссылаются на том же состоянии, но они будут использоваться в том порядке, в предыдущей таблице. В следующем примере есть два <xref:System.Windows.VisualTransition> объектов. Когда элемент управления переходит из `Pressed` состояние `MouseOver` состояние, <xref:System.Windows.VisualTransition> , имеет оба <xref:System.Windows.VisualTransition.From%2A> и <xref:System.Windows.VisualTransition.To%2A> набор используется. Когда элемент управления переходит из состояния, отличного от `Pressed`, в состояние `MouseOver`, используется другой объект.  
  
 [!code-xaml[VSMButtonTemplate#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#7)]  
  
 <xref:System.Windows.VisualStateGroup> Имеет <xref:System.Windows.VisualStateGroup.Transitions%2A> свойство, содержащее <xref:System.Windows.VisualTransition> объектов, которые применяются к <xref:System.Windows.VisualState> объекты в <xref:System.Windows.VisualStateGroup>. Как <xref:System.Windows.Controls.ControlTemplate> автор, вы может включать любые <xref:System.Windows.VisualTransition> требуется. Однако если <xref:System.Windows.VisualTransition.To%2A> и <xref:System.Windows.VisualTransition.From%2A> свойствам присваиваются названия штатов, которые не находятся в <xref:System.Windows.VisualStateGroup>, <xref:System.Windows.VisualTransition> учитывается.  
  
 В следующем примере показан <xref:System.Windows.VisualStateGroup> для `CommonStates`. В примере определяется <xref:System.Windows.VisualTransition> для каждого из следующих кнопки перехода.  
  
-   в состояние `Pressed`;  
  
-   в состояние `MouseOver`;  
  
-   из состояния `Pressed` в состояние `MouseOver`;  
  
-   из состояния `MouseOver` в состояние `Normal`.  
  
 [!code-xaml[VSMButtonTemplate#VisualTransitions](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualtransitions)]  
  
<a name="customizing_other_controls_by_understanding_the_control_contract"></a>   
## <a name="customizing-other-controls-by-understanding-the-control-contract"></a>Настройка других элементов управления через понимание контракта элемента управления  
 Элемент управления, использующий <xref:System.Windows.Controls.ControlTemplate> для задания визуальной структуры (с помощью <xref:System.Windows.FrameworkElement> объектов) и поведение (с помощью <xref:System.Windows.VisualState> объекты) использует модель частей элемента управления. Множество элементов управления, имеющихся в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 4, используют эту модель. Компоненты, <xref:System.Windows.Controls.ControlTemplate> автор необходимо иметь в виду, взаимодействуют с помощью контракта элемента управления. Поняв части контракта элемента управления, можно настроить внешний вид любого элемента управления, использующего модель частей элемента управления.  
  
 Контракт элемента управления имеет три элемента:  
  
-   визуальный элемент, используемый логикой элемента управления;  
  
-   состояния элемента управления и группа, к которой принадлежит каждое состояние;  
  
-   общие свойства, визуально воздействующие на элемент управления.  
  
### <a name="visual-elements-in-the-control-contract"></a>Визуальные элементы в контракте элемента управления  
 Иногда логика элемента управления взаимодействует с <xref:System.Windows.FrameworkElement> , находящийся в <xref:System.Windows.Controls.ControlTemplate>. Например, элемент управления может обрабатывать событие одного из своих элементов. Если элемент управления ожидает найти определенный <xref:System.Windows.FrameworkElement> в <xref:System.Windows.Controls.ControlTemplate>, он должен предоставить эти данные для <xref:System.Windows.Controls.ControlTemplate> автора. Элемент управления использует <xref:System.Windows.TemplatePartAttribute> для передачи типа элемента, которая ожидается и имя элемента, которое должно быть. <xref:System.Windows.Controls.Button> Не имеет <xref:System.Windows.FrameworkElement> частей в контракте элемента управления, но другие элементы управления, такие как <xref:System.Windows.Controls.ComboBox>, сделать.  
  
 В следующем примере показан <xref:System.Windows.TemplatePartAttribute> объекты, указанные на <xref:System.Windows.Controls.ComboBox> класса. Логика <xref:System.Windows.Controls.ComboBox> ожидает найти <xref:System.Windows.Controls.TextBox> с именем `PART_EditableTextBox` и <xref:System.Windows.Controls.Primitives.Popup> с именем `PART_Popup` в его <xref:System.Windows.Controls.ControlTemplate>.  
  
 [!code-csharp[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#comboboxcontract)]
 [!code-vb[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#comboboxcontract)]  
  
 В следующем примере показан упрощенный <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.ComboBox> , включающий элементы, которые определяются <xref:System.Windows.TemplatePartAttribute> объектов на <xref:System.Windows.Controls.ComboBox> класса.  
  
 [!code-xaml[VSMButtonTemplate#ComboBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/window1.xaml#comboboxtemplate)]  
  
### <a name="states-in-the-control-contract"></a>Состояния в контракте элемента управления  
 Состояния элемента управления также являются частью контракта элемента управления. Пример создания <xref:System.Windows.Controls.ControlTemplate> для <xref:System.Windows.Controls.Button> показано, как задавать внешний вид <xref:System.Windows.Controls.Button> в зависимости от его состояния. Вы создаете <xref:System.Windows.VisualState> для каждого указанного состояния и переведите все <xref:System.Windows.VisualState> объекты, совместно использующие <xref:System.Windows.TemplateVisualStateAttribute.GroupName%2A> в <xref:System.Windows.VisualStateGroup>, как описано в [изменение внешнего вида элемента управления в зависимости от его состояния](#changing_the_appearance_of_a_control_depending_on_its_state) ранее в этом раздел. Элементы управления сторонних поставщиков должны указывать состояния с помощью <xref:System.Windows.TemplateVisualStateAttribute>, который позволяет средствам разработки, таких как Expression Blend, для предоставления состояния элемента управления для создания шаблонов элементов управления.  
  
 Контракты элементов управления, включенных в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], в разделе [Стили и шаблоны элемента Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md).  
  
### <a name="properties-in-the-control-contract"></a>Свойства в контракте элемента управления  
 Общие свойства, визуально влияющие на элемент управления, также включаются в контракт элемента управления. Можно задать эти свойства для изменения внешнего вида элемента управления без создания нового <xref:System.Windows.Controls.ControlTemplate>. Можно также использовать [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) расширение разметки, чтобы привязать свойства элементов, которые находятся в <xref:System.Windows.Controls.ControlTemplate> к общим свойствам, которые определены в <xref:System.Windows.Controls.Button>.  
  
 В следующем примере показан контракт элемента управления "Кнопка".  
  
 [!code-csharp[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#buttoncontract)]
 [!code-vb[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#buttoncontract)]  
  
 При создании <xref:System.Windows.Controls.ControlTemplate>, часто бывает проще всего начать с существующего <xref:System.Windows.Controls.ControlTemplate> и вносить в него изменения. Можно выполнить одно из следующих действий, чтобы изменить существующий <xref:System.Windows.Controls.ControlTemplate>:  
  
-   Воспользоваться конструктором, таким как Expression Blend, который предоставляет графический пользовательский интерфейс для создания шаблонов элементов управления. Дополнительные сведения см. в статье [Настройка стиля элемента управления, поддерживающего шаблон](http://go.microsoft.com/fwlink/?LinkId=161153).  
  
-   Получить значение по умолчанию <xref:System.Windows.Controls.ControlTemplate> и изменить его. Шаблоны элементов управления по умолчанию, включенных в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], см. в документе [Default WPF Themes](http://go.microsoft.com/fwlink/?LinkID=158252).  
  
<a name="complete_example"></a>   
## <a name="complete-example"></a>Полный пример  
 В следующем примере показано полное <xref:System.Windows.Controls.Button> <xref:System.Windows.Controls.ControlTemplate> , обсуждаются в этом разделе.  
  
 [!code-xaml[VSMButtonTemplate#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#3)]  
  
## <a name="see-also"></a>См. также  
 [Стилизация и использование шаблонов](../../../../docs/framework/wpf/controls/styling-and-templating.md)
