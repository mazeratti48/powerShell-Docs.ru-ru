---
ms.date: 12/12/2018
keywords: dsc,powershell,конфигурация,установка
title: Указание межузловых зависимостей
ms.openlocfilehash: 62e553d894897ae1908745c2788b7b7b9cbe50ff
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "71954111"
---
# <a name="specifying-cross-node-dependencies"></a>Указание межузловых зависимостей

> Область применения: Windows PowerShell 5.0

DSC предоставляет специальные ресурсы, **WaitForAll**, **WaitForAny** и **WaitForSome**, которые можно использовать в конфигурациях для указания зависимостей от конфигураций на других узлах. Поведение этих ресурсов описано ниже.

- **WaitForAll**. Успешное выполнение, если указанный ресурс находится в нужном состоянии на всех целевых узлах, определенных в свойстве **NodeName**.
- **WaitForAny**. Успешное выполнение, если указанный ресурс находится в нужном состоянии как минимум на одном из целевых узлов, определенных в свойстве **NodeName**.
- **WaitForSome**. Указывает свойство **NodeCount** в дополнение к свойству **NodeName**. Ресурс выполняется успешно, если он находится в нужном состоянии на минимальном количестве узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**.

## <a name="syntax"></a>Синтаксис

Ресурсы **WaitForAll** и **WaitForAny** используют одинаковый синтаксис. Замените \<ResourceType\> в примере ниже на **WaitForAny** или **WaitForAll**.
Необходимо отформатировать имя [ResourceType]ResourceName подобно ключевому слову **DependsOn**. Если ресурс принадлежит отдельной [конфигурации](configurations.md), включите **ConfigurationName** в отформатированную строку [ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]. **NodeName** является компьютером или узлом, на котором ожидается текущий ресурс.

```
<ResourceType> [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential]]
    [ RetryCount = [Uint32] ]
    [ RetryIntervalSec = [Uint64] ]
    [ ThrottleLimit = [Uint32]]
}
```

Ресурс **WaitForSome** имеет подобный приведенному выше примеру синтаксис, но содержит ключ **NodeCount**. Ключ **NodeCount** указывает количество узлов, на которых следует ожидать текущий ресурс.

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

Все ресурсы **WaitForXXXX** используют следующие разделы синтаксиса.

|Свойство|  Описание   |
|---------|---------------------|
| RetryIntervalSec| Количество секунд перед повторной попыткой. Минимальное значение — 1.|
| RetryCount| Максимальное число повторных попыток.|
| ThrottleLimit| Количество одновременно подключаемых компьютеров. Значение по умолчанию — `New-CimSession`.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Дополнительные сведения см. в разделе [DependsOn](resource-depends-on.md).|
| PsDscRunAsCredential | См. статью [Запуск DSC с учетными данными пользователя](./runAsUser.md). |

## <a name="using-waitforxxxx-resources"></a>Использование ресурсов WaitForXXXX

Каждый ресурс **WaitForXXXX** ожидает выполнения указанных ресурсов на указанном узле.
После этого другие ресурсы в той же конфигурации могут *зависеть от* ресурса **WaitForXXXX** с помощью ключа **DependsOn**.

Например, в следующей конфигурации целевой узел ожидает завершения выполнения ресурса **xADDomain** на узле **MyDC** не более чем с 30 повторными попытками (с интервалом 15 секунд), прежде чем присоединиться к домену.

По умолчанию ресурсы **WaitForXXX** выполняют одну попытку, а затем выдают ошибку. Хотя это необязательно, обычно требуется указать **RetryCount** и **RetryIntervalSec**.

```powershell
Configuration JoinDomain
{
    Import-DscResource -Module xComputerManagement, xActiveDirectory

    Node myDC
    {
        WindowsFeature InstallAD
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain NewDomain
        {
            DomainName = 'Contoso.com'
            DomainAdministratorCredential = (Get-Credential)
            SafemodeAdministratorPassword = (Get-Credential)
            DatabasePath = "C:\Windows\NTDS"
            LogPath = "C:\Windows\NTDS"
            SysvolPath = "C:\Windows\Sysvol"
        }
    }

    Node myDomainJoinedServer
    {
        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'myPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

При компиляции конфигурации создаются два MOF-файла. Примените их на целевые узлы с помощью командлета [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration)

> [!NOTE]
> Ресурсы **WaitForXXX** используют удаленное управление Windows, чтобы проверить состояние других узлов.
> Дополнительные сведения о требованиях к безопасности и портах для WinRM см. в разделе [Вопросы обеспечения безопасности удаленного взаимодействия PowerShell](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).

## <a name="see-also"></a>См. также

- [Конфигурации DSC](configurations.md)
- [Использование зависимостей ресурсов с DependsOn](resource-depends-on.md)
- [Ресурсы DSC](../resources/resources.md)
- [Настройка локального диспетчера конфигураций](../managing-nodes/metaConfig.md)
