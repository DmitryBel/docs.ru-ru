---
title: Комментарии в коде (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Uncomment button
- REM statement [Visual Basic]
- comments [Visual Basic], in code
- comments [Visual Basic], Visual Basic code
- Comment button
- buttons [Visual Basic], Uncomment
- buttons [Visual Basic], Comment
- code comments [Visual Basic], Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
ms.openlocfilehash: 4486b5be42f4a356b2017fe8629bc96f6ad47eda
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33650973"
---
# <a name="comments-in-code-visual-basic"></a>Комментарии в коде (Visual Basic)
В примерах кодов часто встречается символ начала комментария (`'`). Этот символ дает компилятору Visual Basic проигнорировать последующий текст, или *комментарий*. Комментарии — это краткие заметки, внесенные в код, чтобы сделать чтение кода более легким.  
  
 Хорошим стилем программирования считается начинать все процедуры с краткого комментария, описывающего функциональные характеристики процедуры (то, что она делает). Это необходимо для вашего собственного удобства и удобства того, кто читает этот код. Следует отличать детали реализации (как процедура работает) от комментариев, описывающих функциональные характеристики. Если в комментарий включены детали реализации, их следует обновлять при редактировании кода.  
  
 Комментарии могут располагаться в конце той же строки, где содержится оператор, или занимать отдельную строку. Оба способа представлены в следующем коде:  
  
 [!code-vb[VbVbcnConventions#16](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_1.vb)]  
  
 Если комментарий занимает более одной строки, каждая строка должна начинаться с символа начала комментария, как показано в следующем примере.  
  
 [!code-vb[VbVbcnConventions#17](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_2.vb)]  
  
## <a name="commenting-guidelines"></a>Правила комментирования  
 В следующей таблице приведены общие рекомендации по тому, какие типы комментариев могут предшествовать разделу кода. Это всего лишь рекомендации; Visual Basic нет жестких норм, касающихся добавления комментариев. В комментарий по желанию автора кода может быть включена любая информация.  
  
|||  
|---|---|  
|Тип комментария|Описание комментария|  
|Цель|Описание действий, совершаемых процедурой (но не того, каким образом совершаются эти действия)|  
|Допущения|Список всех внешних переменных, элементов управления, открытых файлов, к которым осуществляется доступ из процедуры |  
|Произведенный эффект|Список внешних переменных, элементов управления или файлов, на которые влияет данная процедура (если это влияние не очевидно)|  
|Inputs|Описание назначения аргументов|  
|Returns|Описание значений, возвращаемых процедурой|  
  
 Также рекомендуется принять во внимание следующие моменты.  
  
-   Объявление каждой важной переменной должно предшествовать комментарию, описывающему ее назначение.  
  
-   Имена переменных, элементов управления и процедур должны быть функционально понятными, чтобы комментарии требовались только в случае особо сложных деталей реализации.  
  
-   Комментарии не могут располагаться за последовательностью продолжения строки в той же строке.  
  
 Можно добавить или удалить символы начала комментария для блоков кода, выберите одну или несколько строк кода, выберите **комментарий** (![VisualBasicWinAppCodeEditorCommentButton](../../../visual-basic/programming-guide/program-structure/media/vacommentbutton.gif "vaCommentButton ")) и **Uncomment** (![VisualStudioWinAppProjectUncommentButton](../../../visual-basic/programming-guide/program-structure/media/vauncommentbutton.gif "vaUncommentButton")) кнопок, расположенных на **изменение**  инструментов.  
  
> [!NOTE]
>  Кроме того, можно добавить в код комментарии, поставив в начале текста ключевое слово `REM`. Тем не менее `'` символов и **комментарий**/**Uncomment** кнопок, проще использовать и требует меньше места и памяти.  
  
## <a name="see-also"></a>См. также  
 [Документирование кода с комментариями XML](http://msdn.microsoft.com/magazine/dd722812.aspx)  
 [Практическое руководство. Создание XML-документации](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
 [XML-теги для комментариев](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
 [Соглашения о структуре программы и коде](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)  
 [Оператор REM](../../../visual-basic/language-reference/statements/rem-statement.md)
