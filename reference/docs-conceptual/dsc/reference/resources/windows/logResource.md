---
ms.date: 09/20/2019
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Log в DSC
ms.openlocfilehash: a1b7bf44fbaf36a3adaf0666e9f0a754fa3f6ee1
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954671"
---
# <a name="dsc-log-resource"></a><span data-ttu-id="0fff9-103">Ресурс Log в DSC</span><span class="sxs-lookup"><span data-stu-id="0fff9-103">DSC Log Resource</span></span>

> <span data-ttu-id="0fff9-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.x</span><span class="sxs-lookup"><span data-stu-id="0fff9-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.x</span></span>

<span data-ttu-id="0fff9-105">Ресурс **Log** в DSC Windows PowerShell предоставляет механизм записи сообщений в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="0fff9-105">The **Log** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

## <a name="syntax"></a><span data-ttu-id="0fff9-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0fff9-106">Syntax</span></span>

```Syntax
Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

> [!NOTE]
> <span data-ttu-id="0fff9-107">По умолчанию включены только операционные журналы DSC.</span><span class="sxs-lookup"><span data-stu-id="0fff9-107">By default only the Operational logs for DSC are enabled.</span></span> <span data-ttu-id="0fff9-108">Чтобы журнал аналитики стал доступным или видимым, его необходимо включить.</span><span class="sxs-lookup"><span data-stu-id="0fff9-108">Before the Analytic log will be available or visible, it must be enabled.</span></span> <span data-ttu-id="0fff9-109">См. дополнительные сведения о [расположении журналов событий DSC](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span><span class="sxs-lookup"><span data-stu-id="0fff9-109">For more information, see [Where are DSC Event Logs?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span></span>

## <a name="properties"></a><span data-ttu-id="0fff9-110">Свойства</span><span class="sxs-lookup"><span data-stu-id="0fff9-110">Properties</span></span>

|<span data-ttu-id="0fff9-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="0fff9-111">Property</span></span> |<span data-ttu-id="0fff9-112">Описание</span><span class="sxs-lookup"><span data-stu-id="0fff9-112">Description</span></span> |
|---|---|
|<span data-ttu-id="0fff9-113">Сообщение</span><span class="sxs-lookup"><span data-stu-id="0fff9-113">Message</span></span> |<span data-ttu-id="0fff9-114">Указывает сообщение для записи в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="0fff9-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="0fff9-115">Общие свойства</span><span class="sxs-lookup"><span data-stu-id="0fff9-115">Common properties</span></span>

|<span data-ttu-id="0fff9-116">Свойство</span><span class="sxs-lookup"><span data-stu-id="0fff9-116">Property</span></span> |<span data-ttu-id="0fff9-117">Описание</span><span class="sxs-lookup"><span data-stu-id="0fff9-117">Description</span></span> |
|---|---|
|<span data-ttu-id="0fff9-118">DependsOn</span><span class="sxs-lookup"><span data-stu-id="0fff9-118">DependsOn</span></span> |<span data-ttu-id="0fff9-119">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="0fff9-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0fff9-120">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="0fff9-120">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="0fff9-121">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="0fff9-121">PsDscRunAsCredential</span></span> |<span data-ttu-id="0fff9-122">Задает учетные данные для выполнения всего ресурса от другого имени.</span><span class="sxs-lookup"><span data-stu-id="0fff9-122">Sets the credential for running the entire resource as.</span></span> |

> [!NOTE]
> <span data-ttu-id="0fff9-123">В WMF 5.0 было добавлено общее свойство **PsDscRunAsCredential**, разрешающее запуск любого ресурса DSC в контексте других учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0fff9-123">The **PsDscRunAsCredential** common property was added in WMF 5.0 to allow running any DSC resource in the context of other credentials.</span></span> <span data-ttu-id="0fff9-124">Дополнительные сведения см. в разделе [Использование учетных данных с ресурсами DSC](../../../configurations/runasuser.md).</span><span class="sxs-lookup"><span data-stu-id="0fff9-124">For more information, see [Use Credentials with DSC Resources](../../../configurations/runasuser.md).</span></span>

## <a name="example"></a><span data-ttu-id="0fff9-125">Пример</span><span class="sxs-lookup"><span data-stu-id="0fff9-125">Example</span></span>

<span data-ttu-id="0fff9-126">В следующем примере показано, как добавить сообщение в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="0fff9-126">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> [!NOTE]
> <span data-ttu-id="0fff9-127">Если этот ресурс настроен, при выполнении командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) всегда возвращается значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="0fff9-127">If you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```