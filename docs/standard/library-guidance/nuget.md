---
title: Библиотеки .NET и NuGet
description: Практические рекомендации для упаковки с NuGet для библиотеки .NET.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: d0ea462a7f52dd9a6b2f14be9ed5770160bf66b1
ms.sourcegitcommit: e42d09e5966dd9fd02847d3e7eeb4ec0877069f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2018
ms.locfileid: "49374507"
---
# <a name="nuget"></a>NuGet

NuGet — это диспетчер пакетов для экосистемы .NET и разработчикам основной способ обнаружения и получения библиотек с открытым кодом .NET. [NuGet.org](https://www.nuget.org/), это бесплатная служба, предоставляемые корпорацией Майкрософт, за размещение пакетов NuGet, является основным узлом для открытых пакетов NuGet, но можно опубликовать в пользовательских службах NuGet как [MyGet](https://www.myget.org/) и [артефакты Azure ](https://azure.microsoft.com/services/devops/artifacts/).

![NuGet](./media/nuget/nuget-logo.png "NuGet")

## <a name="create-a-nuget-package"></a>Создание пакета NuGet

Пакет NuGet (`*.nupkg`) представляет собой файл zip, содержащий сборки .NET и связанные метаданные.

Существует два основных способа для создания пакета NuGet. Является новой и рекомендуемый способ для создания пакета из стиле пакетов SDK для проекта (файл проекта, содержимое которых начинается с `<Project Sdk="Microsoft.NET.Sdk">`). Сборки и целевые объекты автоматически добавляются в пакет и оставшихся метаданных добавляется в файл MSBuild, например пакета имя и номер версии. Компиляция с [ `dotnet pack` ](../../core/tools/dotnet-pack.md) выходные данные команды `*.nupkg` файл, а не сборки.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>Contoso.Api</AssemblyName>
    <PackageVersion>1.1.0</PackageVersion>
    <Authors>John Doe</Authors>
  </PropertyGroup>
</Project>
```

Прежний способ создания пакета NuGet — с `*.nuspec` файл и `nuget.exe` средство командной строки. Файл nuspec предоставляет контроле, но должны четко указывать, какие сборки и целевых объектов, включаемых в окончательный пакет NuGet. Это легко допустить ошибку или кому-либо необходимо обновить файл nuspec, при внесении изменений. Преимуществом nuspec, является его можно использовать создание пакетов NuGet для платформы, которые еще не поддерживают файла стиле пакетов SDK для проекта.

**Рассмотрите ВОЗМОЖНОСТЬ ✔️** с файлом проекта стиле пакетов SDK для создание пакета NuGet.

**Рассмотрите ВОЗМОЖНОСТЬ ✔️** Настройка SourceLink Добавление метаданных элемента управления источника сборки и пакет NuGet.

## <a name="package-dependencies"></a>Зависимости пакета

Зависимости пакета NuGet рассматриваются подробно в [зависимости](./dependencies.md) статьи.

## <a name="important-nuget-package-metadata"></a>Важные метаданные пакета NuGet

Пакет NuGet поддерживает многие [свойства метаданных](/nuget/reference/nuspec). В следующей таблице содержатся основные метаданные, которые должен предоставить каждый проект с открытым кодом:

| Имя свойства MSBuild              | Имя Nuspec              | Описание  |
| ---------------------------------- | ------------------------ | ------------ |
| `PackageId`                        | `id`                       | Идентификатор пакета. Можно зарезервировать префикс из идентификатора, если он удовлетворяет [критерии](/nuget/reference/id-prefix-reservation). |
| `PackageVersion`                   | `version`                  | Версия пакета NuGet. Дополнительные сведения см. в разделе [пакет NuGet версии](./versioning.md#nuget-package-version).             |
| `Title`                            | `title`                    | Понятный заголовок пакета. По умолчанию используется `PackageId`.             |
| `Description`                      | `description`              | Подробное описание пакета, который отображается в пользовательском Интерфейсе.             |
| `Authors`                          | `authors`                  | Разделенный запятыми список авторов пакетов, совпадающих с именами профилей на сайте nuget.org.             |
| `PackageTags`                      | `tags`                     | Разделенный пробелами список тегов и ключевых слов, описывающих пакет. Теги используются при поиске пакетов.             |
| `PackageIconUrl`                   | `iconUrl`                  | URL-адрес изображения для использования в качестве значка для пакета. URL-адрес должен использоваться протокол HTTPS, и изображение должно быть 64 x 64 и с прозрачным фоном.             |
| `PackageProjectUrl`                | `projectUrl`               | URL-адрес для домашней страницы или источник репозитория проекта.             |
| `PackageLicenseUrl`                | `licenseUrl`               | URL-адрес лицензии проекта. Может быть URL-адрес `LICENSE` файл в системе управления версиями.             |

**Попробуйте ✔️** Выбор имени пакета NuGet с префиксом, отвечающий резервирование префикса NuGet [критерии](/nuget/reference/id-prefix-reservation).

**Рассмотрите ВОЗМОЖНОСТЬ ✔️** с помощью `LICENSE` файл в системе управления версиями как `LicenseUrl`. Например [LICENSE.md](https://github.com/JamesNK/Newtonsoft.Json/blob/c4af75c8e91ca0d75aa6c335e8c106780c4f7712/LICENSE.md).

> [!IMPORTANT]
> Объект проект без лицензии по умолчанию равно [авторские права монопольного](https://choosealicense.com/no-permission/), что делает невозможным для других пользователей.

**СДЕЛАТЬ ✔️** использовать записи href HTTPS для вашего значок пакета.

> Как NuGet.org сайтах с поддержкой HTTPS и отображении изображения отличных от HTTPS будет создавать предупреждения о смешанном содержимом.

**СДЕЛАТЬ ✔️** используется изображение значка пакета, 64 x 64 с прозрачным фоном для удобства просмотра результатов.

## <a name="pre-release-packages"></a>Пакеты предварительного выпуска

Пакеты NuGet с суффиксом версии считаются [предварительной версии](/nuget/create-packages/prerelease-packages). По умолчанию пользовательский Интерфейс диспетчера пакетов NuGet отображает стабильные выпуски, если пользователь соглашается на участие в предварительной версии пакетов, что идеально подходит для тестирования пользователя с ограниченными правами пакеты предварительного выпуска.

```xml
<PackageVersion>1.0.1-beta1</PackageVersion>
```

> [!NOTE]
> Стабильного пакета не может зависеть от предварительной версии пакета. Необходимо предоставить свои собственные пакету предварительного выпуска или зависят от более ранней версии стабильной.

![Зависимость предварительной версии пакета NuGet](./media/nuget/nuget-prerelease-package.png "зависимость предварительной версии пакета NuGet")

**СДЕЛАТЬ ✔️** публикация предварительной версии пакета при тестировании, предварительном просмотре или экспериментов.

**СДЕЛАТЬ ✔️** публикации стабильного пакета при его готовности чтобы другие стабильные пакеты можно сослаться на него.

## <a name="symbol-packages"></a>Пакеты символов

NuGet поддерживает [формирование пакета отдельный символ](/nuget/create-packages/symbol-packages) содержащий отладочные файлы PDB-ФАЙЛ вместе с основной пакет, содержащий сборки .NET. Пакеты символов суть они размещены на сервере символов и загружаются только с помощью средства, как Visual Studio по требованию.

В настоящее время основной общедоступного узла для символов - [SymbolSource](http://www.symbolsource.org/) -не поддерживает переносимые PDB-файлы создан в стиле пакетов SDK для проектов и пакетов символов не полезны.

**Рассмотрите ВОЗМОЖНОСТЬ ✔️** внедрение PDB-файлы в главный пакет NuGet.

**ИЗБЕГАЙТЕ ❌** Создание пакета символов, содержащий PDB-файлов.

>[!div class="step-by-step"]
[Назад](./strong-naming.md)
[Вперед](./dependencies.md)