---
title: Практическое руководство. Циклическое воспроизведение звука в Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sound loops
- SoundPlayer class [Windows Forms], play looping
- sounds [Windows Forms], looping
- playing sounds [Windows Forms], looping
ms.assetid: ea95dd46-10a3-46c0-8263-4b205f00df7f
ms.openlocfilehash: 67e1f8abe6872358a29ab8f6734b58c1c1bc809c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33533761"
---
# <a name="how-to-loop-a-sound-playing-on-a-windows-form"></a>Практическое руководство. Циклическое воспроизведение звука в Windows Forms
В следующем примере кода выполняется повторяющееся воспроизведение звука. Когда этот код запускается в обработчике события `stopPlayingButton_Click`, воспроизведение звука останавливается. Если звук не воспроизводится, то ничего не происходит.  
  
## <a name="example"></a>Пример  
 [!code-csharp[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.PlayLooping#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.PlayLooping/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Для этого примера требуются:  
  
-   ссылки на сборки System и System.Windows.Forms;  
  
-   замена имени файла `"c:\Windows\Media\chimes.wav"` на допустимое имя файла.  
  
 Сведения о построении этого примера из командной строки для visual Basic или Visual C# см. в разделе [построение из командной строки](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) или [построение с командной строки csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Можно также построить этот пример, в Visual Studio, вставив код в новый проект.  См. также [Практическое руководство. Компиляция и выполнение откомпилированного примера кода формы Windows Forms с помощью Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="robust-programming"></a>Отказоустойчивость  
 Операции с файлами должны быть включены в соответствующие блоки обработки исключений.  
  
 При следующих условиях возможно возникновение исключения:  
  
-   Недопустимое имя пути (например, путь содержит недопустимые символы или состоит только из символ-разделитель (класс <xref:System.ArgumentException>)).  
  
-   Путь доступен только для чтения (класс <xref:System.IO.IOException>).  
  
-   Имя пути — `Nothing` (класс <xref:System.ArgumentNullException>).  
  
-   Указано слишком длинное имя пути (класс <xref:System.IO.PathTooLongException>).  
  
-   Недопустимый путь (класс <xref:System.IO.DirectoryNotFoundException>).  
  
-   Путь содержит только двоеточие (":") (класс <xref:System.NotSupportedException>).  
  
## <a name="net-framework-security"></a>Безопасность платформы .NET Framework  
 По имени файла не всегда можно с уверенностью судить о его содержимом. Например, файл с именем Form1.vb может вовсе не быть исходным файлом Visual Basic. Следует проверять все входные данные перед использованием их в приложении.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Media.SoundPlayer.PlayLooping%2A>  
 [Практическое руководство. Воспроизведение звука в Windows Forms](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)  
 [Общие сведения о классе SoundPlayer](../../../../docs/framework/winforms/controls/soundplayer-class-overview.md)
