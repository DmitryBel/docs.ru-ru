---
title: Практическое руководство. Запрет присоединения дочерней задачи к ее родительской задаче
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, preventing attachments
ms.assetid: c0fb85d4-9e80-4905-9f65-29acc54201c4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4ea0254add0592c0c79c03f4e94f02526f9fe689
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33580774"
---
# <a name="how-to-prevent-a-child-task-from-attaching-to-its-parent"></a>Практическое руководство. Запрет присоединения дочерней задачи к ее родительской задаче
В этом документе показано, как предотвратить прикрепление дочерней задачи к родительской. Предотвращение прикрепления дочерней задачи к родительской полезно при вызове компонента, написанного сторонним разработчиком и также использующим задачи. Например, компонент стороннего разработчика, использующий параметр <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> для создания объекта <xref:System.Threading.Tasks.Task> или <xref:System.Threading.Tasks.Task%601>, может вызвать проблемы в коде, если он продолжительный или создает необрабатываемое исключение.  
  
## <a name="example"></a>Пример  
 В следующем примере сравниваются последствия использования параметров по умолчанию с последствиями предотвращения прикрепления дочерней задачи к родительской. В примере создается объект <xref:System.Threading.Tasks.Task>, вызывающий библиотеку стороннего разработчика, которая также использует объект <xref:System.Threading.Tasks.Task>. Библиотека стороннего разработчика использует параметр <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> для создания объекта <xref:System.Threading.Tasks.Task>. Приложение использует параметр <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> для создания родительской задачи. Этот параметр выдает среде выполнения указание удалить спецификацию <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> в дочерних задачах.  
  
 [!code-csharp[TPL_DenyChildAttach#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_denychildattach/cs/denychildattach.cs#1)]
 [!code-vb[TPL_DenyChildAttach#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_denychildattach/vb/denychildattach.vb#1)]  
  
 Поскольку родительская задача не завершается, пока не завершатся все дочерние задачи, длительная дочерняя задача может привести к ухудшению производительности приложения в целом. В этом примере, когда приложение использует параметры по умолчанию для создания родительской задачи, дочерняя задача должна выполниться до завершения родительской задачи. Если приложение использует параметр <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType>, дочерняя задача не будет прикреплена к родительской. Поэтому приложение может выполнять дополнительную работу после завершения родительской задачи и до ожидания завершения дочерней задачи.  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Скопируйте код примера и вставьте его в проект Visual Studio или в файл с именем `DenyChildAttach.cs` (`DenyChildAttach.vb` для Visual Basic), затем выполните в окне командной строки Visual Studio следующую команду.  
  
 Visual C#  
  
 **csc.exe DenyChildAttach.cs**  
  
 Visual Basic  
  
 **vbc.exe DenyChildAttach.vb**  
  
## <a name="robust-programming"></a>Отказоустойчивость  
  
## <a name="see-also"></a>См. также  
 [Асинхронное программирование на основе задач](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)
