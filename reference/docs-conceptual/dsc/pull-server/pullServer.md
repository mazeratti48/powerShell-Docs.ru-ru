---
ms.date: 01/08/2020
keywords: dsc,powershell,конфигурация,установка
title: Опрашивающая служба DSC
ms.openlocfilehash: 821f183c91e805154323f9f6a42f7f5006499182
ms.sourcegitcommit: 30ccbbb32915b551c4cd4c91ef1df96b5b7514c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/01/2020
ms.locfileid: "80500724"
---
# <a name="desired-state-configuration-pull-service"></a>Опрашивающая служба Desired State Configuration

> [!IMPORTANT]
> Опрашивающий сервер (компонент Windows *служба DSC*) — поддерживаемый компонент Windows Server, но реализация новых функций и возможностей для него не планируется. Рекомендуется начать перенос управляемых клиентов на [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (включает возможности опрашивающего сервера в Windows Server) или на одно из решений сообщества, указанных [в следующем списке](pullserver.md#community-solutions-for-pull-service).

Управление локальным диспетчером (LCM) конфигураций можно централизировать с помощью опрашиваемой службы. При использовании такого подхода управляемый узел регистрируется в службе, и ему в параметрах локального диспетчера конфигураций назначается конфигурация. Конфигурация и все ресурсы DSC, которые необходимы в качестве зависимостей конфигурации, загружаются на компьютер и используются локальным диспетчером конфигураций для управления конфигурацией. Сведения о состоянии управляемого компьютера отправляются в службу для отчетности. Эта концепция называется "опрашивающей службой".

Текущие варианты опрашиваемой службы:

- служба Desired State Configuration в службе автоматизации Azure;
- Опрашиваемая служба в Windows Server
- Решения с открытым исходным кодом, поддерживаемые сообществом
- Общий ресурс SMB

Для каждого решения рекомендуется использовать следующий масштаб:

|                   Решение                   |              Клиентские узлы              |
| -------------------------------------------- | -------------------------------------- |
| Опрашивающий сервер Windows, использующий базу данных MDB или ESENT | До 500 узлов                        |
| Опрашивающий сервер Windows, использующий базу данных SQL       | До 3500 узлов                       |
| DSC службы автоматизации Azure                         | Малые и большие среды      |

**Рекомендуемое решение** и вариант с наибольшим числом доступных функций — [DSC в службе автоматизации Azure](/azure/automation/automation-dsc-getting-started). Не определен верхний предел количества узлов на учетную запись службы автоматизации.

Служба Azure может управлять узлами в локальных частных центрах обработки данных или в общедоступных облаках, таких как Azure и AWS. Для частных сред, где серверы не могут напрямую подключаться к Интернету, рекомендуем ограничить исходящий трафик только опубликованным диапазоном IP-адресов Azure (см. сведения о [диапазонах IP-адресов для центров обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653)).

Функции веб-службы, которые сейчас недоступны в опрашиваемой службе в Windows Server:

- Шифрование всех данных при передаче и хранении.
- Автоматическое создание и обслуживание клиентских сертификатов.
- Хранение секретов с централизованным управлением [паролями и учетными данными](/azure/automation/automation-credentials) или [переменными](/azure/automation/automation-variables), такими как имена серверов или строки подключения.
- Централизованное управление [конфигурацией LCM](../managing-nodes/metaConfig.md#basic-settings) в узле.
- Централизованное назначение конфигураций клиентским узлам.
- Выпуск изменений конфигурации для небольших групп пользователей, позволяющий протестировать решение перед реализацией в рабочей среде.
- Графические отчеты:
  - сведения о состоянии на уровне ресурсов DSC;
  - подробные сообщения об ошибках с клиентских компьютеров для устранения неполадок.
- [Интеграция с Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) для отправки предупреждений, автоматизации задач, а также выполнения приложений Android или iOS для создания отчетов и оповещений.

## <a name="dsc-pull-service-in-windows-server"></a>Опрашиваемая служба DSC в Windows Server

Опрашиваемую службу можно настроить для работы в Windows Server. Учтите, что решение опрашиваемой службы в составе Windows Server включает только возможности хранения конфигураций и модулей для скачивания и записи данных отчетов в базу данных. Она не включает многих функций, предоставляемых службой в Azure, и поэтому не совсем подходит для оценки потенциального использования службы.

Опрашиваемая служба в Windows Server — это веб-служба в составе IIS, которая использует интерфейс OData для создания файлов конфигурации DSC, доступных целевым узлам по запросу.

Требования к использованию опрашиваемого сервера:

- Сервер под управлением:
  - WMF/PowerShell 4.0 или более поздней версии
  - Роль сервера служб IIS
  - Служба DSC
- Рекомендуется использовать средства создания сертификата для защиты учетных данных, передаваемых в локальный диспетчер конфигураций (LCM) на целевых узлах

Для настройки размещения опрашиваемой службы в Windows Server лучше всего воспользоваться конфигурацией DSC. Пример сценария приведен ниже.

### <a name="supported-database-systems"></a>Поддерживаемые системы баз данных

| WMF 4.0 |       WMF 5.0        |       WMF 5.1        | WMF 5.1 (Windows Server Insider Preview версии 17090) |
| ------- | -------------------- | -------------------- | ---------------------------------------------- |
| MDB     | ESENT (по умолчанию), MDB | ESENT (по умолчанию), MDB | ESENT (по умолчанию), SQL Server, MDB               |

Начиная с выпуска Windows Server 17090 в опрашивающей службе (компонент Windows *служба DSC*) поддерживается SQL Server. Это новый вариант масштабирования крупных сред DSC, которые не были перенесены в [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> [!NOTE]
> Поддержка SQL Server не будет добавлена в предыдущие версии WMF 5.1 (или более ранние версии) и будет доступна только в Windows Server версии 17090 и более поздних версиях.

Чтобы настроить на опрашивающем сервере использование SQL Server, установите значение `$true` для параметра **SqlProvider** и допустимую строку подключения SQL Server для параметра **SqlConnectionString**. Дополнительные сведения см. в разделе [Строки подключения SqlClient](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Чтобы ознакомиться с настройкой SQL Server с помощью **xDscWebService**, прочтите статью [Использование ресурса xDscWebService](#using-the-xdscwebservice-resource) и просмотрите файл [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 в GitHub](https://github.com/dsccommunity/xPSDesiredStateConfiguration/blob/master/source/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>Использование ресурса xDSCWebService

Самый простой способ настроить опрашиваемый веб-сервер — использовать ресурс **xDscWebService**, включенный в модуль **xPSDesiredStateConfiguration**. В следующих действиях показано, как использовать ресурс в скрипте `Configuration`, используемом для настройки веб-службы.

1. Вызовите командлет [Install-Module](/powershell/module/PowerShellGet/Install-Module), чтобы установить модуль **xPSDesiredStateConfiguration**.

   > [!NOTE]
   > `Install-Module` включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0 и более поздних версий.

1. Получите SSL-сертификат для опрашивающего сервера DSC из доверенного центра сертификации (общедоступного или входящего в состав вашей организации). Полученный из центра сертификат обычно имеет формат PFX.
1. Установите сертификат на узле, который должен стать опрашиваемым сервером DSC, в расположении по умолчанию (`CERT:\LocalMachine\My`).
   - Запишите отпечаток сертификата.
1. Выберите идентификатор GUID для использования в качестве ключа регистрации. Чтобы создать его с помощью PowerShell, в командной строке PS введите следующее и нажмите клавишу ВВОД: `[guid]::newGuid()` или `New-Guid`. Этот ключ будет использоваться клиентскими узлами в качестве общего ключа для проверки подлинности во время регистрации. Дополнительные сведения см. в разделе "Ключ регистрации" ниже.
1. В ISE PowerShell запустите (нажав клавишу <kbd>F5</kbd>) следующий скрипт конфигурации (включенный в пример папки модуля **xPSDesiredStateConfiguration** в качестве `Sample_xDscWebServiceRegistration.ps1`). Этот сценарий настраивает опрашиваемый сервер.

    ```powershell
    configuration Sample_xDscWebServiceRegistration
    {
        param
        (
            [string[]]$NodeName = 'localhost',

            [ValidateNotNullOrEmpty()]
            [string] $certificateThumbPrint,

            [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
            [ValidateNotNullOrEmpty()]
            [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
        )

        Import-DSCResource -ModuleName PSDesiredStateConfiguration
        Import-DSCResource -ModuleName xPSDesiredStateConfiguration

        Node $NodeName
        {
            WindowsFeature DSCServiceFeature
            {
                Ensure = "Present"
                Name   = "DSC-Service"
            }

            xDscWebService PSDSCPullServer
            {
                Ensure                  = "Present"
                EndpointName            = "PSDSCPullServer"
                Port                    = 8080
                PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
                CertificateThumbPrint   = $certificateThumbPrint
                ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
                ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
                State                   = "Started"
                DependsOn               = "[WindowsFeature]DSCServiceFeature"
                RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
                AcceptSelfSignedCertificates = $true
                UseSecurityBestPractices     = $true
                Enable32BitAppOnWin64   = $false
            }

            File RegistrationKeyFile
            {
                Ensure          = 'Present'
                Type            = 'File'
                DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
                Contents        = $RegistrationKey
            }
        }
    }
    ```

1. Запустите конфигурацию, передав отпечаток SSL-сертификата в виде параметра **certificateThumbPrint** и ключ регистрации GUID в виде параметра **RegistrationKey**:

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a>Ключ регистрации

Чтобы разрешить клиентским узлам регистрироваться на сервере для использования имен конфигурации вместо идентификаторов конфигурации, созданный конфигурацией ключ сохраняется в файле `RegistrationKeys.txt` в `C:\Program Files\WindowsPowerShell\DscService`. Ключ регистрации работает как общий секрет, используемый во время первоначальной регистрации клиента с опрашиваемым сервером. Клиент создает самозаверяющий сертификат, который используется для уникальной проверки подлинности на опрашиваемом сервере после успешного завершения регистрации. Отпечаток этого сертификата сохраняется локально и связывается с URL-адресом опрашиваемого сервера.

> [!NOTE]
> Ключи регистрации не поддерживаются в PowerShell 4.0.

Для настройки проверки подлинности узла опрашиваемом сервере необходимо поместить ключ регистрации в метаконфигурацию всех целевых узлов, которые будут регистрироваться на этом опрашиваемом сервере. Обратите внимание, что **RegistrationKey** в метаконфигурации ниже удаляется после успешной регистрации целевого компьютера, и значение должно соответствовать значению в файле `RegistrationKeys.txt` на опрашиваемом сервере (в этом примере — "140a952b-b9d6-406b-b416-e0f759c9c0e4"). Значение ключа регистрации должно оставаться конфиденциальным, так как с ним любой целевой компьютер сможет зарегистрироваться на опрашиваемом сервере.

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to set up pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> [!NOTE]
> Раздел **ReportServerWeb** позволяет отправлять данные отчетов на опрашиваемый сервер.

Отсутствие свойства **ConfigurationID** в файле метаконфигурации неявно означает, что опрашиваемый сервер поддерживает версию 2 протокола опрашиваемого сервера и требуется начальная регистрация. Наоборот, наличие свойства **ConfigurationID** означает, что используется версия 1 протокола опрашиваемого сервера и регистрация не выполняется.

> [!NOTE]
> В сценарии PUSH в текущем выпуске есть ошибка, из-за которой необходимо определять свойство ConfigurationID в файле метаконфигурации для узлов, которые никогда не регистрировались на опрашиваемом сервере. Это приведет к принудительному использованию версии 1 протокола опрашиваемого сервера и позволит избежать сообщений об ошибках регистрации.

## <a name="placing-configurations-and-resources"></a>Размещение конфигураций и ресурсов

После завершения установки опрашиваемого сервера папки для размещения модулей и конфигурации, которые будут доступны целевым узлам, задаются свойствами  **ConfigurationPath** и **ModulePath** в конфигурации опрашиваемого сервера.сервера. Для правильной обработки опрашиваемым сервером эти файлы должны иметь специальный формат.

### <a name="dsc-resource-module-package-format"></a>Формат пакета модуля для ресурсов DSC

Каждый модуль ресурса необходимо упаковать в ZIP-архив и переименовать согласно следующему шаблону: `{Module Name}_{Module Version}.zip`.

Например, модуль с именем **xWebAdminstration** с версией модуля 3.1.2.0 будет иметь имя `xWebAdministration_3.1.2.0.zip`. Каждая версия модуля должна находиться в собственном ZIP-файле.
Так как в каждом ZIP-файле существует только одна версия ресурса, формат модулей с поддержкой нескольких версий модуля в одном каталоге, который появился в WMF 5.0, не поддерживается. Это означает, что перед упаковкой модулей ресурсов DSC для опрашиваемого сервера необходимо внести небольшое изменение в структуру каталогов. Формат модулей, содержащих ресурсы DSC, в WMF 5.0 по умолчанию таков: `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`. Перед упаковкой для опрашиваемого сервера удалите папку **{Module version}** , чтобы путь стал таким: `{Module Folder}\DscResources\{DSC Resource Folder}\`. Выполнив это изменение, упакуйте папку в ZIP-архив, как описано выше, и поместите ZIP-архивы в папку **ModulePath**.

Используйте `New-DscChecksum {module zip file}`, чтобы создать файл контрольной суммы для только что добавленного модуля.

### <a name="configuration-mof-format"></a>Формат файлов конфигурации MOF

MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. Чтобы создать контрольную сумму, вызовите командлет [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum). Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке. Поместите файлы MOF и их файлы контрольных сумм в папку **ConfigurationPath**.

> [!NOTE]
> Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

### <a name="tooling"></a>Инструменты

Для упрощения настройки, проверки опрашиваемого сервера и управления им в последнюю версию модуля xPSDesiredStateConfiguration в качестве примеров включены следующие инструменты:

1. Модуль, который помогает упаковывать модули ресурсов и конфигурационные файлы DSC для использования на опрашиваемом сервере.
   [PublishModulesAndMofsToPullServer.psm1](https://github.com/dsccommunity/xPSDesiredStateConfiguration/blob/master/source/Modules/DscPullServerSetup/DscPullServerSetup.psm1).
   Примеры ниже:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Сценарий, который проверяет, что опрашиваемый сервер настроен правильно. [PullServerSetupTests.ps1](https://github.com/dsccommunity/xPSDesiredStateConfiguration/blob/master/source/Modules/DscPullServerSetup/DscPullServerSetupTest/DscPullServerSetupTest.ps1).

## <a name="community-solutions-for-pull-service"></a>Решения сообщества для опрашиваемой службы

Сообщество DSC разработало несколько решений для реализации протокола опрашиваемой службы. В случае локальных сред эти решения предоставляют функции опрашиваемой службы и дают возможность поделиться с сообществом своими улучшениями.

- [Tug](https://github.com/powershellorg/tug)
- [DSC-TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Настройка опрашивающего клиента

В следующих разделах настройка опрашивающих клиентов описывается более подробно:

- [Настройка опрашивающего клиента DSC с помощью идентификатора конфигурации](pullClientConfigID.md)
- [Настройка опрашивающего клиента DSC с помощью имен конфигурации](pullClientConfigNames.md)
- [Частичные конфигурации](partialConfigs.md)

## <a name="see-also"></a>См. также раздел

- [Обзор Windows PowerShell Desired State Configuration](../overview/overview.md)
- [Активированные конфигурации](enactingConfigurations.md)
- [Использование сервера отчетов DSC](reportServer.md)
- [[MS-DSCPM]: Требуемое состояние конфигурации протокола с активным опросом сообщений](https://docs.microsoft.com/openspecs/windows_protocols/ms-dscpm/ea744c01-51a2-4000-9ef2-312711dcc8c9)
- [[MS-DSCPM]: Требуемое состояние конфигурации протокола с активным опросом сообщений (поправки)](https://docs.microsoft.com/openspecs/windows_protocols/ms-winerrata/f5fc7ae3-9172-41e8-ac6a-2a5a5b7bfaf5)
