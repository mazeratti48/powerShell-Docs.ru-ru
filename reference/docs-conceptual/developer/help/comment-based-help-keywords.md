---
title: Ключевые слова справки на основе комментариев | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab90ec96-77f5-42e3-9c7e-2f4156ec207f
caps.latest.revision: 6
ms.openlocfilehash: 534a6c9a43326c8a01b2181c7a799286fa4d3997
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72361363"
---
# <a name="comment-based-help-keywords"></a>Ключевые слова справки на основе комментариев

В этом разделе перечислены и описаны ключевые слова в справке на основе комментариев.

## <a name="keywords-in-comment-based-help"></a>Ключевые слова в справке на основе комментариев

Ниже приведены допустимые ключевые слова справки на основе комментариев. Они перечислены в том порядке, в котором они обычно отображаются в разделе справки, а также их предполагаемое использование. Эти ключевые слова могут отображаться в любом порядке в справке на основе комментариев и не учитывают регистр.

Обратите внимание, что ключевое слово `.ExternalHelp` имеет приоритет над всеми остальными ключевыми словами справки на основе комментариев. При наличии `.ExternalHelp` командлет [Microsoft. PowerShell. Commands. жеселпкомманд](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) не отображает справку на основе комментариев, даже если ей не удается найти файл справки, соответствующий значению ключевого слова.

`.Synopsis` краткое описание функции или скрипта. Это ключевое слово может использоваться только один раз в каждом разделе.

`.Description` подробное описание функции или скрипта. Это ключевое слово может использоваться только один раз в каждом разделе.

`.Parameter` *\<Parameter-Name >* описание параметра. Можно включить ключевое слово `.Parameter` для каждого параметра в функции или скрипте.

Ключевые слова `.Parameter` могут располагаться в любом порядке в блоке комментариев, но порядок, в котором параметры отображаются в инструкции `Param` или в объявлении функции, определяет порядок, в котором параметры отображаются в разделе справки. Чтобы изменить порядок параметров в разделе справки, измените порядок параметров в операторе `Param` или в объявлении функции.

Можно также указать описание параметра, поместив комментарий в операторе `Param` непосредственно перед именем переменной параметра. Если используются как комментарий оператора `Param`, так и ключевое слово `.Parameter`, используется описание, связанное с ключевым словом `.Parameter`, и комментарий оператора `Param` игнорируется.

`.Example` пример команды, использующей функцию или скрипт, при необходимости за которой следует пример выходных данных и описание. Повторите это ключевое слово для каждого примера.

`.Inputs` типы Microsoft .NET платформы объектов, которые можно передать в функцию или скрипт. Можно также включить описание входных объектов.

`.Outputs` тип .NET Framework объектов, возвращаемых командлетом. Можно также включить описание возвращаемых объектов.

`.Notes` дополнительные сведения о функции или скрипте.

`.Link` имя связанного раздела. Повторите это ключевое слово для каждого связанного раздела. Это содержимое отображается в разделе "связанные ссылки" раздела справки.

Содержимое ключевого слова `.Link` может также включать универсальный код ресурса (URI) в Интернет-версию того же раздела справки. При использовании параметра `Online` командлета Get-Help открывается версия в Интернете. URI должен начинаться с "http" или "HTTPS".

`.Component` технологию или функцию, которую использует функция или сценарий, или к которой они относятся. Это содержимое отображается, если команда Get-Help содержит параметр `Component` команды Get-Help.

`.Role` роль пользователя для раздела справки. Это содержимое отображается, если команда Get-Help содержит параметр `Role` команды Get-Help.

`.Functionality` предполагаемое использование функции. Это содержимое отображается, если команда Get-Help содержит параметр `Functionality` команды Get-Help.

`.ForwardHelpTargetName` `<Command-Name>` выполняет перенаправление в раздел справки для указанной команды. Вы можете перенаправить пользователей в любой раздел справки, включая разделы справки для функции, скрипта, командлета или поставщика.

`.ForwardHelpCategory` `<Category>` указывает категорию справки для элемента в Форвардхелптаржетнаме. Допустимые значения: Alias, командлет, HelpFile, функция, поставщик, общие, часто задаваемые вопросы, глоссарий, команду скрипта, Екстерналскрипт, Filter или ALL. Используйте это ключевое слово, чтобы избежать конфликтов при наличии команд с одинаковыми именами.

`.RemoteHelpRunspace` `<PSSession-variable>` указывает сеанс, содержащий раздел справки. Введите переменную, содержащую сеанс PSSession. Это ключевое слово используется командлетом `Export-PSSession` для поиска разделов справки для экспортированных команд.

`.ExternalHelp` `<XML Help File>` указывает путь и (или) имя файла справки на основе XML для скрипта или функции.

Ключевое слово `.ExternalHelp` сообщает командлету [Microsoft. PowerShell. Commands. жеселпкомманд](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) о получении справки для скрипта или функции в XML-файле. Объект **.** Ключевое слово екстерналхелп требуется при использовании файла справки на основе XML для скрипта или функции. Без него `Get-Help` не будет искать файл справки для функции или скрипта.

Ключевое слово `.ExternalHelp` имеет приоритет над всеми остальными ключевыми словами справки на основе комментариев. При наличии `.ExternalHelp` командлет [Microsoft. PowerShell. Commands. жеселпкомманд](/dotnet/api/Microsoft.PowerShell.Commands.gethelpcommand) не отображает справку на основе комментариев, даже если ей не удается найти файл справки, соответствующий значению ключевого слова.

При экспорте функции модулем скрипта значение `.ExternalHelp` должно быть именем файла без пути. `Get-Help` ищет файл в подкаталоге, зависящем от языкового стандарта, в каталоге модуля. Требования к имени файла отсутствуют, но рекомендуется использовать следующий формат имени файла: `<ScriptModule>.psm1-help.xml`.

Если функция не связана с модулем, включите путь и имя файла в значение **.** Ключевое слово екстерналхелп. Если указанный путь к XML-файлу содержит подкаталоги, относящиеся к пользовательскому интерфейсу и языку и региональным параметрам, то `Get-Help` выполняет рекурсивный поиск XML-файла с именем скрипта или функции в соответствии со стандартами переключения языка, установленными для Windows, точно так же, как и для всех разделов справки на основе XML.

Дополнительные сведения о формате файла справки на основе XML для командлета см. в разделе [Создание справки по командлетам Windows PowerShell](./writing-help-for-windows-powershell-cmdlets.md).