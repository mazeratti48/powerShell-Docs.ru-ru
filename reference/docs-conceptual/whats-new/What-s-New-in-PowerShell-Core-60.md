---
title: Новые возможности PowerShell Core 6.0
description: Новые возможности и изменения в PowerShell Core 6.0
ms.date: 08/06/2018
ms.openlocfilehash: 39bcb343c44c32d183c8bb90306a8f4a57397eb6
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500486"
---
# <a name="whats-new-in-powershell-core-60"></a>Новые возможности PowerShell Core 6.0

[Core PowerShell 6.0][github] — это новый выпуск PowerShell, который является кроссплатформенным (Windows, macOS и Linux), обладает открытым исходным кодом и предназначен для разнородных сред и гибридного облака.

## <a name="moved-from-net-framework-to-net-core"></a>Переход с .NET Framework на .NET Core

PowerShell Core использует [.NET Core 2.0][] в качестве среды выполнения. .NET Core 2.0 позволяет PowerShell Core работать на различных платформах (Windows, macOS и Linux). PowerShell Core также предлагает набор API, предоставляемый .NET Core 2.0 для использования в командлетах и сценариях PowerShell.

Продукт Windows PowerShell использовал среду выполнения .NET Framework для размещения подсистемы PowerShell. Это означает, что Windows PowerShell предлагает набор API, предоставляемый платформой .NET Framework.

API, используемые .NET Core и .NET Framework совместо, определены как часть [.NET Standard][].

Дополнительные сведения о том, как это влияет на совместимость модулей/сценариев между PowerShell Core и Windows PowerShell, см. в разделе [Обратная совместимость с Windows PowerShell](#backwards-compatibility-with-windows-powershell).

## <a name="support-for-macos-and-linux"></a>Поддержка macOS и Linux

Теперь PowerShell официально поддерживает macOS и Linux, включая следующие версии:

- Windows 7, 8.1 и 10
- Windows Server 2008 R2, 2012 R2, 2016
- [Windows Server Semi-Annual Channel][semi-annual]
- Ubuntu 14.04, 16.04 и 17.04
- Debian 8.7+ и 9
- CentOS 7
- Red Hat Enterprise Linux 7
- OpenSUSE 42.2
- Fedora 25, 26
- macOS 10.12+

Наше сообщество также предоставило пакеты для следующих платформ, однако они не поддерживаются официально:

- Arch Linux
- Kali Linux
- AppImage (работает на нескольких платформах Linux)

У нас также есть экспериментальные (неподдерживаемые) выпуски для следующих платформ:

- Windows на базе ARM32/ARM64
- Raspbian (Stretch)

В PowerShell Core 6.0 были внесены некоторые изменения, чтобы улучшить работу в системах, отличных от Windows. Некоторые из них являются критическими изменениями, также затрагивающими и Windows. Другие относятся исключительно к версиям PowerShell Core, предназначенным для других операционных систем.

- Добавлена поддержка стандартных масок для команд на платформах Unix.
- Функциональность `more` учитывает `$PAGER` в Linux и по умолчанию использует `less`. Это означает, что теперь можно использовать подстановочные знаки для собственных двоичных файлов и команды (например, `ls *.txt`). (#3463)
- Обратная косая черта (\) в конце строки автоматически игнорируется интерпретатором командной строки при работе с аргументами собственных команд систем. (#4965)
- Игнорируйте параметр `-ExecutionPolicy` при запуске PowerShell на платформах, отличных от Windows, так как подпись сценариев сейчас не поддерживается. (#3481)
- Исправлен ConsoleHost, чтобы учитывать `NoEcho` на платформах Unix. (#3801)
- Исправлен `Get-Help` для поддержки сопоставления шаблонов без учета регистра для платформ Unix. (#3852)
- В пакет добавлена страница руководства `powershell`.

### <a name="logging"></a>Logging

В системе macOS PowerShell использует собственные API `os_log` для входа в [единую систему ведения журналов][os_log] Apple. В системе Linux PowerShell использует [Syslog][], единое решение для ведения журнала.

### <a name="filesystem"></a>Файловая система

Для macOS и Linux было внесено несколько изменений, позволяющих использовать в именах файлов символы, которые обычно в Windows не поддерживаются:

- Пути, предоставляемые командлетам, теперь не учитывают направление косой черты (в качестве разделителя каталогов можно использовать как /, так и \).
- Теперь спецификация базовых каталогов XDG соблюдается и используется по умолчанию:
  - Путь к профилю Linux/macOS: `~/.config/powershell/profile.ps1`
  - Путь для сохранения журнала: `~/.local/share/powershell/PSReadline/ConsoleHost_history.txt`
  - Путь к модулям пользователя: `~/.local/share/powershell/Modules`
- Поддержка имен файлов и папок, содержащих символ двоеточия в Unix. (#4959)
- Поддержка имен сценариев или полных путей, содержащих запятые. (#4136) (выражаем благодарность [@TimCurwick](https://github.com/TimCurwick))
- Определение, когда `-LiteralPath` используется для подавления расширения подстановочных знаков для командлетов навигации. (#5038)
- Обновление `Get-ChildItem`, чтобы сделать его работу больше похожей на nix-команду `ls -R` и собственные команды Windows `DIR /S`. `Get-ChildItem` теперь возвращает символьные ссылки, обнаруженные при рекурсивном поиске, а не каталоги, на которые они указывают (#3780)

### <a name="case-sensitivity"></a>Чувствительность к регистру

Системы Linux и macOS обычно учитывают регистр, а система Windows — нет, хотя и сохраняет его.
В общем случае PowerShell не учитывает регистр.

Например, переменные среды учитывают регистр в macOS и Linux, поэтому использование регистра для переменной среды `PSModulePath` было стандартизировано. (#3255) `Import-Module` не учитывает регистр, когда использует путь к файлу для определения имени модуля. (#5097)

## <a name="support-for-side-by-side-installations"></a>Поддержка параллельной установки

PowerShell Core устанавливается, настраивается и выполняется отдельно от Windows PowerShell.
PowerShell Core имеет "портативный" ZIP-пакет. С его помощью можно установить любое количество версий в любом месте на диске, в том числе и локально для приложения, зависимого от установки PowerShell.
Параллельная установка упрощает тестирование новых версий PowerShell и перенос существующих сценариев по мере необходимости. Параллельность также обеспечивает обратную совместимость, так как сценарии можно прикрепить к конкретным требуемым им версиям.

> [!NOTE]
> По умолчанию установщик на основе MSI в Windows выполняет установку в режиме обновления.

## <a name="renamed-powershellexe-to-pwshexe"></a>Переименование `powershell(.exe)` в `pwsh(.exe)`

Имя исполняемого файла для PowerShell Core было изменено с `powershell(.exe)` на `pwsh(.exe)`. Это изменение позволяет пользователям детерминированно запускать PowerShell Core на компьютерах для поддержки параллельных установок Windows PowerShell и PowerShell Core.<bpt i="1000001" x="1000001" type="formatting">{b&gt;</bpt><ept i="1000001">&lt;b}</ept> Кроме того, `pwsh` проще вводить из-за меньшей длины.

Дополнительные изменения в `pwsh(.exe)` из `powershell.exe`:

- Первый позиционный параметр изменен с `-Command` на `-File`. Это изменение устраняет использование `#!` в сценариях PowerShell, которые выполняются из оболочек, отличных от PowerShell, на платформах, отличных от Windows. Это также означает, что вы можете выполнять такие команды, как `pwsh foo.ps1` или `pwsh fooScript`, без указания `-File`. Однако это изменение требует явно указать `-c` или `-Command` при попытке запуска таких команд, как `pwsh.exe -Command Get-Command`.
  (#4019)
- PowerShell Core принимает параметр `-i` (или `-Interactive`) для определения интерактивной оболочки.
  (#3558) Это позволяет использовать PowerShell в качестве оболочки по умолчанию для платформ Unix.
- Удалены параметры `-importsystemmodules` и `-psconsoleFile` из `pwsh.exe`. (#4995)
- Изменены `pwsh -version` и встроенная справка для `pwsh.exe` для обеспечения согласованности с другими собственными средствами. (#4958 и #4931) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Сообщения о недопустимом аргументе для `-File` и `-Command`, и коды завершения соответствуют стандартам Unix (#4573)
- Добавлен параметр `-WindowStyle` в Windows. (#4573) Аналогичным образом обновления для установок на основе пакета на платформах, отличных от Windows, являются обновлениями на месте.

## <a name="backwards-compatibility-with-windows-powershell"></a>Обратная совместимость с Windows PowerShell

Задача PowerShell Core заключается в обеспечении максимально возможного уровня совместимости с Windows PowerShell.
PowerShell Core использует [.NET Standard][] 2.0 для обеспечения совместимости двоичных файлов с существующими сборками .NET. Многие модули PowerShell зависят от этих сборок (часто библиотеки DLL), поэтому .NET Standard позволяет продолжить их использование в .NET Core. PowerShell Core также содержит эвристику поиска в стандартных папках, в которых например, размещается глобальный кэш сборок на диске для обнаружения зависимостей DLL платформы .NET Framework.

Дополнительные сведения о .NET Standard см. в [Блог .NET][], в этом видео на [YouTube][] и [Часто задаваемые вопросы][] на GitHub.

Было сделано все возможное, чтобы язык PowerShell и встроенные модули (такие как `Microsoft.PowerShell.Management`, `Microsoft.PowerShell.Utility` и т. д.) работали так же, как и в Windows PowerShell. Во многих случаях при помощи сообщества мы добавили в эти командлеты новые возможности и исправления ошибок. В некоторых случаях из-за отсутствующей зависимости на нижележащих уровнях .NET функция была удалена или стала недоступна.

Большинство модулей, которые входят в состав Windows (например, `DnsClient`, `Hyper-V`, `NetTCPIP`, `Storage` и т. д.), и другие продукты Майкрософт, включая Azure и Office, еще не были *явно* перенесены в .NET Core. Группа разработчиков PowerShell сотрудничает с группами разработчиков этих продуктов, чтобы проверить и перенести имеющиеся у них модули в PowerShell Core. При использовании .NET Standard и [CDXML][] многие из этих традиционных модулей Windows PowerShell работают в PowerShell Core, но они не были проверены формально и официально не поддерживается.

Установив модуль [`WindowsPSModulePath`][windowspsmodulepath], можно использовать модули Windows PowerShell, добавив `PSModulePath` Windows PowerShell в `PSModulePath` PowerShell Core.

Сначала установите модуль `WindowsPSModulePath` из коллекции PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

После установки модуля запустите командлет `Add-WindowsPSModulePath`, чтобы добавить `PSModulePath` Windows PowerShell в PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="docker-support"></a>Поддержка Docker

В PowerShell Core добавлена поддержка контейнеров Docker для всех основных поддерживаемых нами платформ (включая несколько дистрибутивов Linux, Windows Server Core и Nano Server).

Чтобы ознакомиться с полным списком, см. теги на [`microsoft/powershell` в Docker Hub][docker-hub]. Дополнительные сведения о Docker и PowerShell Core см. в разделе [Docker][] на GitHub.

## <a name="ssh-based-powershell-remoting"></a>Удаленное взаимодействие PowerShell на основе SSH

Кроме традиционной службы WinRM, протокол удаленного взаимодействия PowerShell (PSRP) теперь работает с протоколом Secure Shell (SSH).

Это означает, что можно использовать командлеты, такие как `Enter-PSSession` и `New-PSSession`, и проходить проверку подлинности с помощью SSH. Вам нужно лишь зарегистрировать PowerShell в качестве подсистемы на сервере SSH с OpenSSH, чтобы использовать существующие механизмы проверки подлинности на основе SSH (например, пароли или закрытые ключи) с помощью стандартной семантики `PSSession`.

Дополнительные сведения о настройке и использовании удаленного взаимодействия на основе SSH см. в разделе [Удаленное взаимодействие с PowerShell через SSH][ssh-remoting].

## <a name="default-encoding-is-utf-8-without-a-bom-except-for-new-modulemanifest"></a>Кодировка по умолчанию — UTF-8 без метки порядка байтов за исключением New-ModuleManifest.

В прошлом командлеты Windows PowerShell, такие как `Get-Content` и `Set-Content`, использовали различные кодировки, например ASCII и UTF-16. Расхождение в кодировках по умолчанию приводило к проблемам при смешанном использовании командлетов без указания кодировки.

В большинстве случаев платформы, отличные от Windows, используют UTF-8 без метки порядка байтов (BOM) в качестве кодировки по умолчанию для текстовых файлов. Все больше средств и приложений Windows переходят с UTF-16 на UTF-8 без метки порядка байтов. PowerShell Core изменяет кодировку по умолчанию, чтобы привести ее в соответствие с более обширной экосистемой.

Это означает, что все встроенные командлеты, использующие параметр `-Encoding`, используют значение `UTF8NoBOM` по умолчанию. Это изменение затрагивает следующие командлеты:

- Add-Content
- Export-Clixml
- Export-Csv
- Export-PSSession
- Format-Hex
- Get-Content
- Import-Csv
- Out-File
- Select-String
- Send-MailMessage
- Set-Content

Эти командлеты также были обновлены, чтобы параметр `-Encoding` глобально принимал `System.Text.Encoding`.

Значение по умолчанию `$OutputEncoding` также было изменено на UTF-8.

Рекомендуется явно задавать кодировки в сценариях с помощью параметра `-Encoding`, чтобы обеспечить предсказуемость поведения на разных платформах.

Командлет `New-ModuleManifest` не содержит параметра **Encoding**. Кодировка файла манифеста модуля (.psd1), созданного с помощью командлета `New-ModuleManifest`, зависит от среды: при использовании PowerShell Core в Linux используется кодировка UTF-8 (без BOM); в противном случае используется UTF-16 (с BOM). (#3940)

## <a name="support-backgrounding-of-pipelines-with-ampersand--3360"></a>Поддержка фонового выполнения конвейеров с помощью амперсанда (`&`) (#3360)

Использование `&` в конце конвейера приводит к тому, что он выполняется как задание PowerShell. Когда конвейер выполняется в фоновом режиме, возвращается объект задания. После запуска конвейера как задания для управления им можно использовать все стандартные командлеты `*-Job`. Используемые в конвейере переменные (кроме переменных для конкретных процессов) автоматически копируются в это задание, поэтому `Copy-Item $foo $bar &` работает. Кроме того, задание выполняется в текущем каталоге, а не домашнем каталоге пользователя. Дополнительные сведения о заданиях PowerShell см. в разделе [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).

## <a name="semantic-versioning"></a>Семантическое версионирование

- `SemanticVersion` сделан совместимым с `SemVer 2.0`. (#5037) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Изменен `ModuleVersion` по умолчанию в `New-ModuleManifest` на `0.0.1` для согласованности с SemVer. (#4842) (выражаем благодарность [@LDSpits](https://github.com/LDSpits))
- Добавлен `semver` как акселератор типа для `System.Management.Automation.SemanticVersion`. (#4142) (выражаем благодарность [@oising](https://github.com/oising))
- Реализовано сравнение экземпляра `SemanticVersion` и экземпляра `Version`, который создается только при значениях версии `Major` и `Minor`.

## <a name="language-updates"></a>Языковые обновления

- Реализован анализ escape-символов Юникода, чтобы пользователи могли использовать символы Юникода в качестве аргументов, строк или имен переменных. (#3958) (выражаем благодарность [@rkeithhill](https://github.com/rkeithhill))
- Добавлен новый escape-символ ESC: `` `e``.
- Добавлена поддержка преобразования перечислений в строку (#4318) (выражаем благодарность [@KirkMunro](https://github.com/KirkMunro))
- Исправлено приведение одноэлементного массива к типу стандартной коллекции. (#3170)
- Добавлена перегрузка диапазона символов для оператора `..`, чтобы `'a'..'z'` возвращал символы от "a" до "z". (#5026) (выражаем благодарность [@IISResetMe](https://github.com/IISResetMe))
- Исправлено присваивание переменных, чтобы предотвратить перезапись переменных, доступных только для чтения.
- Принудительная отправка локальных значений автоматических переменных в "DottedScopes" при выделении точками командлетов сценариев (#4709)
- Добавлена возможность использования параметров Singleline, Multiline в операторе split (#4721) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))

## <a name="engine-updates"></a>Обновления подсистемы

- `$PSVersionTable` имеет четыре новых свойства:
  - `PSEdition`: имеет значение `Core` в PowerShell Core и `Desktop` в Windows PowerShell.
  - `GitCommitId`: идентификатор фиксации Git ветви Git или тега, где была выполнена сборка PowerShell.
    В сборках выпуска оно, вероятнее всего, будет совпадать с `PSVersion`.
  - `OS`: строка версии ОС, возвращенная `[System.Runtime.InteropServices.RuntimeInformation]::OSDescription`.
  - `Platform`: возвращается `[System.Environment]::OSVersion.Platform`, имеет значение `Win32NT` в Windows, `Unix` в macOS и `Unix` в Linux.
- Удалено свойство `BuildVersion` из `$PSVersionTable`. Это свойство было жестко привязано к версии сборки Windows. Вместо этого мы рекомендуем использовать `GitCommitId` для получения точной версии сборки PowerShell Core. (#3877) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Удалено свойство `ClrVersion` из `$PSVersionTable`. Это свойство не имеет отношения к .NET Core и было оставлено там только для совместимости с устаревшими функциями, которые не применимы к PowerShell.
- Добавлены три новые автоматические переменные, чтобы определить, выполняется ли PowerShell в заданной ОС: `$IsWindows`, `$IsMacOs` и `$IsLinux`.
- Добавлен `GitCommitId` в баннер PowerShell Core. Теперь вам не нужно выполнять `$PSVersionTable` сразу после запуска PowerShell, чтобы получить версию. (#3916) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Добавлен файл конфигурации JSON с именем `powershell.config.json` в `$PSHome` для хранения некоторых параметров, требуемых перед запуском (например, `ExecutionPolicy`).
- Конвейер не блокируется при запуске EXE-файла Windows.
- Реализовано перечисление COM-коллекций. (#4553)

## <a name="cmdlet-updates"></a>Обновления командлетов

### <a name="new-cmdlets"></a>Новые командлеты

- Добавлен `Get-Uptime` в `Microsoft.PowerShell.Utility`.
- Добавлена команда `Remove-Alias`. (#5143) (выражаем благодарность [@PowershellNinja](https://github.com/PowershellNinja))
- Добавлен `Remove-Service` в модуль управления. (#4858) (выражаем благодарность [@joandrsn](https://github.com/joandrsn))

### <a name="web-cmdlets"></a>Веб-командлеты

- Добавлена поддержка проверки подлинности сертификатов для веб-командлетов. (#4646) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Добавлена поддержка для заголовков содержимого в веб-командлетах. (#4494 и #4640) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Добавлена поддержка нескольких заголовков ссылок в веб-командлетах. (#5265) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Поддержка разбивки на страницы для заголовков ссылок в веб-командлетах (#3828)
  - Когда для `Invoke-WebRequest` ответ содержит заголовок ссылки, мы создаем свойство RelationLink в качестве словаря, представляющего URL-адреса и атрибуты `rel`, и делаем эти URL-адреса абсолютными, чтобы упростить задачу разработчику.
  - Когда для `Invoke-RestMethod` ответ содержит заголовок ссылки, мы предоставляем параметр `-FollowRelLink` для автоматического следования по ссылкам `next` `rel`, пока они не перестанут существовать или мы не попадем на необязательное значение параметра `-MaximumFollowRelLink`.
- Добавлен параметр `-CustomMethod` для веб-командлетов, чтобы разрешить нестандартные команды методов. (#3142) (выражаем благодарность @Lee303)
- Добавлена поддержка `SslProtocol` для веб-командлетов. (#5329) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Добавлена поддержка составных данных для веб-командлетов. (#4782) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Добавлен `-NoProxy` для веб-командлетов, чтобы они игнорировали параметры прокси-сервера, действующие на уровне всей системы. (#3447) (выражаем благодарность [@TheFlyingCorpse](https://github.com/TheFlyingCorpse))
- Агент пользователя для веб-командлетов теперь сообщает платформу операционной системы (#4937) (выражаем благодарность [@LDSpits](https://github.com/LDSpits))
- Добавлен параметр `-SkipHeaderValidation` для веб-командлетов, чтобы поддерживать добавление заголовков без проверки их значения. (#4085)
- Разрешение веб-командлетам не проверять сертификат HTTPS сервера, если это необходимо.
- Добавлены параметры проверки подлинности для веб-командлетов. (#5052) (выражаем благодарность [@markekraus](https://github.com/markekraus))
  - Добавлен `-Authentication`, предоставляющий три параметра: Basic, OAuth и Bearer.
  - Добавлен `-Token` для получения токена носителя для параметров OAuth и Bearer.
  - Добавлен `-AllowUnencryptedAuthentication` для обхода проверки подлинности, предоставляемой для любой схемы транспорта, отличной от HTTPS.
- Добавлен`-ResponseHeadersVariable` в `Invoke-RestMethod`, чтобы включить захват заголовков ответа.
  (#4888) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Исправлены веб-командлеты, чтобы включать отклик HTTP в исключение, когда код состояния отклика отличается от успешного. (#3201)
- Изменены веб-командлеты `UserAgent` с `WindowsPowerShell` на `PowerShell`. (#4914) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- Добавлено явное обнаружение `ContentType` в `Invoke-RestMethod` (#4692)
- Исправлены веб-командлеты `-SkipHeaderValidation`, чтобы работать с нестандартными заголовками агента пользователя. (#4479 &
  #<a name="4512-thanks-markekraus"></a>4512) (выражаем благодарность [@markekraus](https://github.com/markekraus))

### <a name="json-cmdlets"></a>Командлеты JSON

- Добавлен `-AsHashtable` в `ConvertFrom-Json`, чтобы возвращать `Hashtable`. (#5043) (выражаем благодарность [@bergmeister](https://github.com/bergmeister))
- Используется более удобный модуль форматирования с выходным параметром `ConvertTo-Json`. (#2787) (выражаем благодарность @kittholland)
- Добавлена поддержка сериализации `Jobject` для `ConvertTo-Json`. (#5141)
- Исправлен `ConvertFrom-Json` для десериализации массива строк из конвейера, которые вместе составляют полную строку JSON. Это устраняет некоторые проблемы, когда символы новой строки нарушали синтаксический анализ JSON.
  (#3823)
- Удалено свойство `AliasProperty "Count"`, определенное для `System.Array`. Это удаляет лишнее свойство `Count` для некоторых выходных данных `ConvertFrom-Json`. (#3231) (выражаем благодарность [@PetSerAl](https://github.com/PetSerAl))

### <a name="csv-cmdlets"></a>Командлеты CSV

- `Import-Csv` теперь поддерживает расширенный формат файла журнала W3C (#2482) (спасибо, [@iSazonov](https://github.com/iSazonov)!)
- Добавлена поддержка `PSTypeName` для `Import-Csv` и `ConvertFrom-Csv`. (#5389) (выражаем благодарность [@markekraus](https://github.com/markekraus))
- В `Import-Csv` реализована поддержка `CR`, `LF` и `CRLF` в качестве разделителей строк. (#5363) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- `-NoTypeInformation` используется по умолчанию в `Export-Csv` и `ConvertTo-Csv`. (#5164) (спасибо, [@markekraus](https://github.com/markekraus))

### <a name="service-cmdlets"></a>Командлеты службы

- Добавлены свойства `UserName`, `Description`, `DelayedAutoStart`, `BinaryPathName` и `StartupType` в объекты `ServiceController`, возвращаемые `Get-Service`. (#4907) (выражаем благодарность [@joandrsn](https://github.com/joandrsn))
- Добавлена возможность задать учетные данные в команде `Set-Service`. (#4844) (выражаем благодарность [@joandrsn](https://github.com/joandrsn))

### <a name="other-cmdlets"></a>Другие командлеты

- В `Get-ChildItem` добавлен параметр `-FollowSymlink`, обходящий символические ссылки по запросу с проверками циклов ссылки. (#4020)
- Обновлен `Add-Type`, чтобы поддерживать `CSharpVersion7`. (#3933) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Удален модуль `Microsoft.PowerShell.LocalAccounts` из-за использования неподдерживаемых API, пока не будет найдено лучшее решение. (#4302)
- Удалены командлеты `*-Counter` в `Microsoft.PowerShell.Diagnostics` из-за использования неподдерживаемых API, пока не будет найдено лучшее решение. (#4303)
- Добавлена поддержка `Invoke-Item -Path <folder>`. (#4262)
- Добавлены параметры `-Extension` и `-LeafBase` в `Split-Path`, чтобы вы могли разделить пути между расширением и остальной частью имени файла. (#2721) (выражаем благодарность [@powercode](https://github.com/powercode))
- Добавлены параметры `-Top` и `-Bottom` в `Sort-Object` для сортировки N вехних/нижних элементов.
- Предоставлен родительский процесс процесса путем добавления `CodeProperty "Parent"` в `System.Diagnostics.Process`. (#2850) (выражаем благодарность [@powercode](https://github.com/powercode))
- Использована единица измерения МБ вместо КБ для столбцов памяти в `Get-Process`.
- Добавлен параметр `-NoNewLine` для `Out-String`. (#5056) (выражаем благодарность [@raghav710](https://github.com/raghav710))
- Командлет `Move-Item` учитывает параметры `-Include`, `-Exclude` и `-Filter`. (#3878)
- Разрешено использовать `*` в пути реестра для `Remove-Item`. (#4866)
- Добавлен `-Title` в `Get-Credential`, и унифицирована работа с запросами для разных платформ.
- Добавлен параметр `-TimeOut` в `Test-Connection`. (#2492)
- Командлеты `Get-AuthenticodeSignature` теперь могут получать метку времени для подписи файла. (#4061)
- Удален неподдерживаемый параметр `-ShowWindow` из `Get-Help`. (#4903)
- Исправлен `Get-Content -Delimiter`, чтобы разделитель не включался в возвращаемые элементы массива (#3706) (выражаем благодарность [@mklement0](https://github.com/mklement0))
- Добавлены параметры `Meta`, `Charset` и `Transitional` в `ConvertTo-HTML` (#4184) (выражаем благодарность [@ergo3114](https://github.com/ergo3114))
- Добавлены свойства `WindowsUBR` и `WindowsVersion` в результат `Get-ComputerInfo`.
- Добавлен параметр `-Group` в `Get-Verb`.
- Добавлена поддержка `ShouldProcess` в `New-FileCatalog` и `Test-FileCatalog` (исправлены `-WhatIf` и `-Confirm`). (#3074) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Добавлен параметр `-WhatIf` в командлет `Start-Process` (#4735) (выражаем благодарность [@sarithsutha](https://github.com/sarithsutha))
- Добавлен `ValidateNotNullOrEmpty` со слишком большим количеством существующих параметров.

## <a name="tab-completion"></a>Заполнение нажатием клавиши TAB

- Улучшено определение типа в функции автодополнения нажатием клавиши TAB на основе значений переменных среды выполнения. (#2744) (выражаем благодарность [@powercode](https://github.com/powercode)) Это позволяет использовать автодополнение нажатием клавиши TAB в следующих ситуациях:

  ```powershell
  $p = Get-Process
  $p | Foreach-Object Prio<tab>
  ```

- Добавлено автодополнение нажатием клавиши TAB в хэш-таблице для `-Property` объекта `Select-Object`. (#3625) (выражаем благодарность [@powercode](https://github.com/powercode))
- Включено автоматическое завершение аргументов для `-ExcludeProperty` и `-ExpandProperty` объекта `Select-Object`.
  (#3443) (выражаем благодарность [@iSazonov](https://github.com/iSazonov))
- Исправлена ошибка с автодополнением нажатием клавиши TAB при вызове `native.exe --<tab>` в собственном завершающем методе. (#3633) (выражаем благодарность [@powercode](https://github.com/powercode))

## <a name="breaking-changes"></a>Критические изменения

Мы представили в PowerShell MSXML 6.0 ряд критически важных изменений.
Подробнее о них см. в разделе [Критические изменения в PowerShell Core 6.0][breaking-changes].

## <a name="debugging"></a>Отладка

- Поддержка удаленной отладки с "шагом с заходом" для `Invoke-Command -ComputerName`. (#3015)
- Возможность ведения журналов отладки для модуля привязки в PowerShell Core.

## <a name="filesystem-updates"></a>Обновления файловой системы

- Разрешено использование поставщика файловой системы из UNC-пути. ($4998)
- `Split-Path` теперь работает с UNC-корнями.
- `cd` без аргументов теперь ведет себя как `cd ~`.
- Исправлен PowerShell Core, чтобы разрешить использование путей длиннее 260 символов. (#3960)

## <a name="bug-fixes-and-performance-improvements"></a>Исправления ошибок и улучшения производительности

Мы внесли *множество* усовершенствований для повышения производительности всего продукта PowerShell, в том числе улучшили время запуска, различные встроенные командлеты и взаимодействие с собственными двоичными файлами.

Мы также исправили несколько ошибок в PowerShell Core. Полный список исправлений и изменений см. в нашем [журнал изменений][] на GitHub.

## <a name="telemetry"></a>Телеметрия

- В PowerShell Core 6.0 добавлена телеметрия на узле консоли для вывода двух значений (#3620):
  - платформа ОС (`$PSVersionTable.OSDescription`);
  - точная версия PowerShell (`$PSVersionTable.GitCommitId`).

Если вы не хотите использовать эту телеметрию, просто создайте переменную среды `POWERSHELL_TELEMETRY_OPTOUT` с одним из следующих значений: `true`, `1` или `yes`. В этом случае обход всей телеметрии выполняется даже до первого запуска PowerShell. Мы также планируем публиковать данные телеметрии и основанные на них аналитические сведения на [панели мониторинга сообщества][community-dashboard]. Дополнительные сведения о том, как мы используем эти данные, см. в этой [записи блога][telemetry-blog].

[github]: https://github.com/PowerShell/PowerShell
[.NET Core 2.0]: https://docs.microsoft.com/dotnet/core/
[.NET Standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[os_log]: https://developer.apple.com/documentation/os/logging
[Syslog]: https://en.wikipedia.org/wiki/Syslog
[ssh-remoting]: ../learn/remoting/SSH-Remoting-in-PowerShell-Core.md
[breaking-changes]: breaking-changes-ps6.md
[журнал изменений]: https://github.com/PowerShell/PowerShell/tree/master/CHANGELOG.md
[community-dashboard]: https://aka.ms/PSGitHubBI
[telemetry-blog]: https://devblogs.microsoft.com/powershell/powershell-open-source-community-dashboard/
[.NET Standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[Блог .NET]: https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard
[YouTube]: https://www.youtube.com/watch?v=YI4MurjfMn8&list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY
[Часто задаваемые вопросы]: https://github.com/dotnet/standard/blob/master/docs/faq.md
[CDXML]: /previous-versions/windows/desktop/wmi_v2/getting-started-with-cdxml
[docker-hub]: https://hub.docker.com/r/microsoft/powershell/
[docker]: https://github.com/PowerShell/PowerShell/tree/master/docker
[windowspsmodulepath]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
