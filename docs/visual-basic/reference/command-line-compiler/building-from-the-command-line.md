---
title: Построение из командной строки (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers [Visual Basic], invoking from command line
- command-line builds
- compiling source code
- command-line compilers [Visual Basic], Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
ms.openlocfilehash: 391e16da86aa741a1b78f35d9afd95688f33c4db
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33654140"
---
# <a name="building-from-the-command-line-visual-basic"></a>Построение из командной строки (Visual Basic)
Проект Visual Basic состоит из одного или нескольких отдельным файлам исходного кода. В процессе компиляции эти файлы соединяются в один пакет — исполняемый файл, который запускается как приложение.  
  
 Visual Basic предоставляет компилятора командной строки в качестве альтернативы компилятору в среде разработки Visual Studio (IDE). Компилятор командной строки разработан для случаев, в которых не требуется полный набор возможностей в Интегрированной среде разработки — например, при использовании или создании программы на компьютере с ограниченными системными ресурсами или дисковым пространством.  
  
  Для компиляции исходных файлов из интегрированной среды разработки Visual Studio, выберите **построения** из **построения** меню.  
  
> [!TIP]
>  При создании файлов проекта с помощью интегрированной среды разработки Visual Studio, можно отобразить сведения о связанном **vbc** команду и ее параметры в окне вывода. Чтобы отобразить эти сведения, откройте [диалоговое окно «Параметры», проекты и решения, построения и выполнения](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)и задайте **детализации, выходные данные построения проекта MSBuild** для **обычный** или более высоком уровне детализации. Дополнительные сведения см. в статье [Практическое руководство. Просмотр, сохранение и настройка файлов журнала сборки](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7).  
  
 Файлы проекта (VBPROJ) в командной строке можно скомпилировать с помощью MSBuild. Дополнительные сведения см. в разделе [Справочник по командной строке](/visualstudio/msbuild/msbuild-command-line-reference) и [Пошаговое руководство: использование MSBuild](/visualstudio/msbuild/walkthrough-using-msbuild).  
  
## <a name="in-this-section"></a>В этом разделе  
 [Практическое руководство. Вызов компилятора командной строки](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 Описывает, как вызвать компилятор командной строки, в командной строке MS-DOS или из определенной папки.  
  
 [Примеры командных строк компиляции](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 Список примеров командных строк, которые можно изменять для собственного использования.  
  
## <a name="related-sections"></a>Связанные разделы  
 [Компилятор Visual Basic с интерфейсом командной строки](../../../visual-basic/reference/command-line-compiler/index.md)  
 Предоставляет список параметров компилятора, упорядоченные по алфавиту или по назначению.  
  
 [Условная компиляция](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 Описывает процедуру компиляции определенных частей кода.  
  
 [Построение и очистка проектов и решений в Visual Studio](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 Описывает способ организации будут включены в различные сборки, изменение свойств проекта и убедитесь, что построение проектов в правильном порядке.
