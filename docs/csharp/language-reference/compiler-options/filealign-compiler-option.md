---
title: -filealign (параметры компилятора C#)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: d51dd0d63bec251d879ffb5e59ce5f7edaf136b4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33218375"
---
# <a name="-filealign-c-compiler-options"></a>-filealign (параметры компилятора C#)
Параметр **-filealign** позволяет указать размер разделов в выходном файле.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>Аргументы  
 `number`  
 Значение, которое задает размер разделов в выходном файле. Допустимые значения: 512, 1024, 2048, 4096 и 8192. Эти значения указаны в байтах.  
  
## <a name="remarks"></a>Примечания  
 Каждый раздел выравнивается по границе, кратной значению **-filealign**. Фиксированный размер по умолчанию не предусмотрен. Если значение **-filealign** не указано, среда CLR выбирает значение по умолчанию во время компиляции.  
  
 Указанный размер раздела влияет на размер выходного файла. Изменение размера раздела может применяться для программ, выполняющихся на небольших устройствах.  
  
 Используйте [DUMPBIN](/cpp/build/reference/dumpbin-options) для просмотра информации о разделах выходного файла.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio  
  
1.  Откройте страницу **Свойства** проекта.  
  
2.  Щелкните страницу свойств **Сборка**.  
  
3.  Нажмите кнопку **Дополнительно** .  
  
4.  Измените свойство **Выравнивание файла**.  
  
 Сведения об установке этого параметра компилятора программными средствами см. в статье <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>.  
  
## <a name="see-also"></a>См. также  
 [Параметры компилятора C# ](../../../csharp/language-reference/compiler-options/index.md)  
 [Управление свойствами проектов и решений](/visualstudio/ide/managing-project-and-solution-properties)
