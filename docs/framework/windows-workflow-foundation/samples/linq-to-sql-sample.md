---
title: LINQ to SQL образца
ms.date: 03/30/2017
ms.assetid: 5f39db9e-0e62-42c9-8c98-bb8b54cec98c
ms.openlocfilehash: 3cfcaf3de1a22b8bb5505083f127a9888b99dbd8
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
ms.locfileid: "33806722"
---
# <a name="linq-to-sql-sample"></a>LINQ to SQL образца
В этом образце показано создание действий, использующих запросы к сущностям LINQ to SQL из таблиц в базах данных SQL Server.  
  
> [!IMPORTANT]
>  Образцы WCF уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\Samples\WCFWFCardspace`  
>   
>  Если этот каталог не существует, щелкните ссылку "Загрузить образец" в верхней части страницы. Обратите внимание, что этой ссылке происходит загрузка и установка всех [!INCLUDE[wf1](../../../../includes/wf1-md.md)], WCF, и [!INCLUDE[infocard](../../../../includes/infocard-md.md)] образцов. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\Samples\WCFWFCardSpace\WF\Scenario\ActivityLibrary\Linq\LinqToSql`  
  
## <a name="activity-details-for-findinsqltable"></a>Сведения о действии FindInSqlTable  
 Это действие позволяет пользователям создавать запросы к сущностям из таблиц в базе данных, используя LINQ to SQL. Пользователи действия могут также указать предикат LINQ в форме лямбда-выражения для фильтрации результатов. Если не указан предикат, вся таблица возвращается. В следующих сведениях о таблице подробно описаны свойства и возвращаемые значения для действия.  
  
|Свойство или возвращаемое значение|Описание|  
|------------------------------|-----------------|  
|Свойство `Collection`|Обязательное свойство, в котором указывается исходная коллекция.|  
|Свойство `Predicate`|Обязательное свойство, в котором указывается фильтр для коллекции в виде лямбда-выражения.|  
|Возвращаемое значение|Фильтруемая коллекция.|  
  
## <a name="code-sample-that-uses-the-custom-activity"></a>Образец кода, использующий настраиваемое действие  
 В следующем примере кода пользовательское действие `FindInSqlTable` применяется для нахождения всех строк в таблице SQL Server, имеющей название `Employee`, где значение столбца `Role` равно `SDE`.  
  
```csharp  
new FindInSqlTable<Employee>   
{  
    ConnectionString = @"Data Source=.\SQLExpress;Initial Catalog=LinqToSqlSample;Integrated Security=True",                          
    Predicate = new LambdaValue<Func<Employee, bool>>(c => new Func<Employee, bool>(emp => emp.Role.Equals("SDE"))),  
    Result = new OutArgument<IList<Employee>>(employees)  
},  
```  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1.  Откройте окно командной строки.  
  
2.  Перейдите в папку, содержащую этот образец.  
  
3.  Запустите командный файл Setup.cmd.  
  
    > [!NOTE]
    >  Скрипт Setup.cmd пытается установить образец базы данных в SQL Server Express на локальном компьютере. Для установки данного образца на другом экземпляре SQL Server отредактируйте Setup.cmd.  
  
     Скрипт Setup.cmd выполняет следующие действия:  
  
    -   Создает базу данных c именем LinqToSqlSample.  
  
    -   Создает таблицу Roles.  
  
    -   Создает таблицу Employees.  
  
    -   Вставляет 3 записи в таблицу Roles.  
  
    -   Вставляет 12 записей в таблицу Employees.  
  
4.  Используя [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], откройте файл решения LinqToSQL.sln.  
  
5.  Для построения решения нажмите CTRL+SHIFT+B.  
  
6.  Чтобы запустить решение, нажмите клавишу F5.  
  
#### <a name="to-uninstall-the-linqtosql-sample-database"></a>Удаление образца базы данных LinqToSql  
  
1.  Откройте окно командной строки.  
  
2.  Перейдите в папку, содержащую этот образец.  
  
3.  Запустите командный файл Cleanup.cmd.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите к [Windows Communication Foundation (WCF) и образцы Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) для загрузки всех Windows Communication Foundation (WCF) и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] образцов. Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Liiinq\LinqToSql`  
  
## <a name="see-also"></a>См. также  
 [LINQ to SQL](http://go.microsoft.com/fwlink/?LinkId=150376)  
 [Начало работы (LINQ to SQL)](http://go.microsoft.com/fwlink/?LinkId=150377)
