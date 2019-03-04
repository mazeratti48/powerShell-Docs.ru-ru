---
title: Способы вызова командлета в командлет из | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: efa4dc9c-ddee-46a3-978a-9dbb61e9bb6f
caps.latest.revision: 12
ms.openlocfilehash: d4564b51b74422cdaec3878b227ffc6be7c97949
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56855890"
---
# <a name="how-to-invoke-a-cmdlet-from-within-a-cmdlet"></a><span data-ttu-id="84e8a-102">Как вызвать командлет из другого командлета</span><span class="sxs-lookup"><span data-stu-id="84e8a-102">How to Invoke a Cmdlet from Within a Cmdlet</span></span>

<span data-ttu-id="84e8a-103">В этом примере показано, как для вызова командлета из в другой командлет, который позволяет добавлять функциональные возможности вызванного командлета в командлет, в которой вы выполняете разработку.</span><span class="sxs-lookup"><span data-stu-id="84e8a-103">This example shows how to invoke a cmdlet from within another cmdlet, which allows you to add the functionality of the invoked cmdlet to the cmdlet you are developing.</span></span> <span data-ttu-id="84e8a-104">В этом примере `Get-Process` командлет вызывается для получения процессов, запущенных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="84e8a-104">In this example, the `Get-Process` cmdlet is invoked to get the processes that are running on the local computer.</span></span> <span data-ttu-id="84e8a-105">Вызов `Get-Process` командлет является эквивалентом следующую команду.</span><span class="sxs-lookup"><span data-stu-id="84e8a-105">The call to the `Get-Process` cmdlet is equivalent to the following command.</span></span> <span data-ttu-id="84e8a-106">Эта команда извлекает все процессы, имена которых начинаются с символов «» до «t».</span><span class="sxs-lookup"><span data-stu-id="84e8a-106">This command retrieves all the processes whose names start with the characters "a" through "t".</span></span>

```powershell
Get-Process -name [a-t]
```

> [!IMPORTANT]
> <span data-ttu-id="84e8a-107">Можно вызвать только нужные командлеты, которые наследуются от [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) класса.</span><span class="sxs-lookup"><span data-stu-id="84e8a-107">You can invoke only those cmdlets that derive directly from the [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) class.</span></span> <span data-ttu-id="84e8a-108">Не удается вызвать командлет, который является производным от [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) класса.</span><span class="sxs-lookup"><span data-stu-id="84e8a-108">You cannot invoke a cmdlet that derives from the [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) class.</span></span>

## <a name="to-invoke-a-cmdlet-from-within-a-cmdlet"></a><span data-ttu-id="84e8a-109">Для вызова из командлета в командлет</span><span class="sxs-lookup"><span data-stu-id="84e8a-109">To invoke a cmdlet from within a cmdlet</span></span>

1. <span data-ttu-id="84e8a-110">Убедитесь, что существует ссылка на сборку, определяющую командлет, чтобы вызвать и что соответствующие `using` добавляется инструкция.</span><span class="sxs-lookup"><span data-stu-id="84e8a-110">Ensure that the assembly that defines the cmdlet to be invoked is referenced and that the appropriate `using` statement is added.</span></span> <span data-ttu-id="84e8a-111">В этом примере добавляются следующие пространства имен.</span><span class="sxs-lookup"><span data-stu-id="84e8a-111">In this example, the following namespaces are added.</span></span>

    ```csharp
    using System.Diagnostics;
    using System.Management.Automation;   // Windows PowerShell assembly.
    using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.
    ```

2. <span data-ttu-id="84e8a-112">В метод командлета обработки входных данных создайте новый экземпляр для вызова командлета.</span><span class="sxs-lookup"><span data-stu-id="84e8a-112">In the input processing method of the cmdlet, create a new instance of the cmdlet to be invoked.</span></span> <span data-ttu-id="84e8a-113">В этом примере объект типа [Microsoft.Powershell.Commands.Getprocesscommand](/dotnet/api/Microsoft.PowerShell.Commands.GetProcessCommand) создается вместе с строка, содержащая аргументы, используемые при вызове командлета.</span><span class="sxs-lookup"><span data-stu-id="84e8a-113">In this example, an object of type [Microsoft.Powershell.Commands.Getprocesscommand](/dotnet/api/Microsoft.PowerShell.Commands.GetProcessCommand) is created along with the string that contains the arguments that are used when the cmdlet is invoked.</span></span>

    ```csharp
    GetProcessCommand gp = new GetProcessCommand();
    gp.Name = new string[] { "[a-t]*" };
    ```

3. <span data-ttu-id="84e8a-114">Вызовите [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) вызываемого метода `Get-Process` командлета.</span><span class="sxs-lookup"><span data-stu-id="84e8a-114">Call the [System.Management.Automation.Cmdlet.Invoke\*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) method to invoke the `Get-Process` cmdlet.</span></span>

    ```csharp
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }
    ```

## <a name="example"></a><span data-ttu-id="84e8a-115">Пример</span><span class="sxs-lookup"><span data-stu-id="84e8a-115">Example</span></span>

<span data-ttu-id="84e8a-116">В этом примере `Get-Process` командлет вызывается изнутри [System.Management.Automation.Cmdlet.Beginprocessing\*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) метод командлета.</span><span class="sxs-lookup"><span data-stu-id="84e8a-116">In this example, the `Get-Process` cmdlet is invoked from within the [System.Management.Automation.Cmdlet.Beginprocessing\*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method of a cmdlet.</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Management.Automation;   // Windows PowerShell assembly.
using Microsoft.PowerShell.Commands;  // Windows PowerShell assembly.

namespace SendGreeting
{
  // Declare the class as a cmdlet and specify an
  // appropriate verb and noun for the cmdlet name.
  [Cmdlet(VerbsCommunications.Send, "GreetingInvoke")]
  public class SendGreetingInvokeCommand : Cmdlet
  {
    // Declare the parameters for the cmdlet.
    [Parameter(Mandatory = true)]
    public string Name
    {
      get { return name; }
      set { name = value; }
    }
    private string name;

    // Override the BeginProcessing method to invoke
    // the Get-Process cmdlet.
    protected override void BeginProcessing()
    {
      GetProcessCommand gp = new GetProcessCommand();
      gp.Name = new string[] { "[a-t]*" };
      foreach (Process p in gp.Invoke<Process>())
      {
        Console.WriteLine(p.ToString());
      }
    }

    // Override the ProcessRecord method to process
    // the supplied user name and write out a
    // greeting to the user by calling the WriteObject
    // method.
    protected override void ProcessRecord()
    {
      WriteObject("Hello " + name + "!");
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="84e8a-117">См. также</span><span class="sxs-lookup"><span data-stu-id="84e8a-117">See Also</span></span>

[<span data-ttu-id="84e8a-118">Запись командлета Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="84e8a-118">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)