---
title: Установка модуля PowerShell | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb82827e-fdb7-4cbf-b3d4-093e72b3ff0e
caps.latest.revision: 28
ms.openlocfilehash: f7899713dd273b793017adfa0a20b3ff3352b62a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56862170"
---
# <a name="installing-a-powershell-module"></a><span data-ttu-id="5026d-102">Установка модуля PowerShell</span><span class="sxs-lookup"><span data-stu-id="5026d-102">Installing a PowerShell Module</span></span>

<span data-ttu-id="5026d-103">После создания модуля PowerShell, скорее всего требуется установить модуль в системе, разработанных вами или другими может использовать его.</span><span class="sxs-lookup"><span data-stu-id="5026d-103">After you have created your PowerShell module, you will likely want to install the module on a system, so that you or others may use it.</span></span> <span data-ttu-id="5026d-104">Вообще говоря это просто состоит из копирования файлы модулей (ie, .psm1, или двоичную сборку, манифеста модуля и другие связанные файлы) на каталог на этом компьютере.</span><span class="sxs-lookup"><span data-stu-id="5026d-104">Generally speaking, this simply consists of copying the module files (ie, the .psm1, or the binary assembly, the module manifest, and any other associated files) onto a directory on that computer.</span></span> <span data-ttu-id="5026d-105">Для очень небольшого проекта это может быть сложнее, чем копирование и вставка файлов с помощью обозревателя Windows на одном удаленном компьютере; Тем не менее для больших решений вы можете использовать более сложный процесс установки.</span><span class="sxs-lookup"><span data-stu-id="5026d-105">For a very small project, this may be as simple as copying and pasting the files with Windows Explorer onto a single remote computer; however, for larger solutions you may wish to use a more sophisticated installation process.</span></span> <span data-ttu-id="5026d-106">Независимо от того, как можно получить модуль в систему PowerShell можно использовать ряд приемов, которые помогут пользователям находить и использовать модули.</span><span class="sxs-lookup"><span data-stu-id="5026d-106">Regardless of how you get your module onto the system, PowerShell can use a number of techniques that will let users find and use your modules.</span></span> <span data-ttu-id="5026d-107">(Дополнительные сведения см. в разделе [импорт модуля PowerShell](./importing-a-powershell-module.md).) Таким образом основная проблема для установки является обеспечение, что PowerShell будут иметь возможность найти ваш модуль.</span><span class="sxs-lookup"><span data-stu-id="5026d-107">(For more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md).) Therefore, the main issue for installation is ensuring that PowerShell will be able to find your module.</span></span>

<span data-ttu-id="5026d-108">Данный раздел включает следующие подразделы:</span><span class="sxs-lookup"><span data-stu-id="5026d-108">This topic contains the following sections:</span></span>

- <span data-ttu-id="5026d-109">Правила для установки модулей</span><span class="sxs-lookup"><span data-stu-id="5026d-109">Rules for Installing Modules</span></span>

- <span data-ttu-id="5026d-110">Место установки модулей</span><span class="sxs-lookup"><span data-stu-id="5026d-110">Where to Install Modules</span></span>

- <span data-ttu-id="5026d-111">Установка нескольких версий модуля</span><span class="sxs-lookup"><span data-stu-id="5026d-111">Installing Multiple Versions of a Module</span></span>

- <span data-ttu-id="5026d-112">Конфликта имен команд обработки</span><span class="sxs-lookup"><span data-stu-id="5026d-112">Handling Command Name Conflicts</span></span>

## <a name="rules-for-installing-modules"></a><span data-ttu-id="5026d-113">Правила для установки модулей</span><span class="sxs-lookup"><span data-stu-id="5026d-113">Rules for Installing Modules</span></span>

<span data-ttu-id="5026d-114">Следующее относится ко всем модулям, включая модули, созданные для собственного использования, модули, которые вы получаете от других производителей и модули, которые распределяют другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="5026d-114">The following information pertains to all modules, including modules that you create for your own use, modules that you get from other parties, and modules that you distribute to others.</span></span>

### <a name="install-modules-in-psmodulepath"></a><span data-ttu-id="5026d-115">Установка модулей в PSModulePath</span><span class="sxs-lookup"><span data-stu-id="5026d-115">Install Modules in PSModulePath</span></span>

<span data-ttu-id="5026d-116">По возможности установите все модули в пути, указанному в **PSModulePath** переменной среды или добавить путь к модулю для **PSModulePath** значение переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5026d-116">Whenever possible, install all modules in a path that is listed in the **PSModulePath** environment variable or add the module path to the **PSModulePath** environment variable value.</span></span>

<span data-ttu-id="5026d-117">**PSModulePath** переменной среды ($Env: PSModulePath) содержит расположения модулей Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5026d-117">The **PSModulePath** environment variable ($Env:PSModulePath) contains the locations of Windows PowerShell modules.</span></span> <span data-ttu-id="5026d-118">Командлеты используют значение этой переменной среды, чтобы найти модули.</span><span class="sxs-lookup"><span data-stu-id="5026d-118">Cmdlets rely on the value of this environment variable to find modules.</span></span>

<span data-ttu-id="5026d-119">По умолчанию **PSModulePath** значение переменной среды содержит следующие системные и каталоги пользователей модуля, но можно добавить и изменить его.</span><span class="sxs-lookup"><span data-stu-id="5026d-119">By default, the **PSModulePath** environment variable value contains the following system and user module directories, but you can add to and edit the value.</span></span>

- <span data-ttu-id="5026d-120">$PSHome\Modules (%Windir%\System32\WindowsPowerShell\v1.0\Modules)</span><span class="sxs-lookup"><span data-stu-id="5026d-120">$PSHome\Modules (%Windir%\System32\WindowsPowerShell\v1.0\Modules)</span></span>

  > [!WARNING]
  > <span data-ttu-id="5026d-121">Это расположение зарезервирован для модулей, входящие в состав Windows.</span><span class="sxs-lookup"><span data-stu-id="5026d-121">This location is reserved for modules that ship with Windows.</span></span> <span data-ttu-id="5026d-122">Не следует устанавливать модули в этом расположении.</span><span class="sxs-lookup"><span data-stu-id="5026d-122">Do not install modules to this location.</span></span>

- <span data-ttu-id="5026d-123">$Home\Documents\WindowsPowerShell\Modules (%UserProfile%\Documents\WindowsPowerShell\Modules)</span><span class="sxs-lookup"><span data-stu-id="5026d-123">$Home\Documents\WindowsPowerShell\Modules (%UserProfile%\Documents\WindowsPowerShell\Modules)</span></span>

- <span data-ttu-id="5026d-124">$Env:ProgramFiles\WindowsPowerShell\Modules (%ProgramFiles%\WindowsPowerShell\Modules)</span><span class="sxs-lookup"><span data-stu-id="5026d-124">$Env:ProgramFiles\WindowsPowerShell\Modules (%ProgramFiles%\WindowsPowerShell\Modules)</span></span>

  <span data-ttu-id="5026d-125">Чтобы получить значение **PSModulePath** переменной среды, используйте один из следующих команд.</span><span class="sxs-lookup"><span data-stu-id="5026d-125">To get the value of the **PSModulePath** environment variable, use either of the following commands.</span></span>

  ```powershell
  $Env:PSModulePath
  [Environment]::GetEnvironmentVariable("PSModulePath")
  ```

  <span data-ttu-id="5026d-126">Чтобы добавить путь к модулю значение **PSModulePath** переменной среды значение, используйте следующий формат команды.</span><span class="sxs-lookup"><span data-stu-id="5026d-126">To add a module path to value of the **PSModulePath** environment variable value, use the following command format.</span></span> <span data-ttu-id="5026d-127">В этом формате используются **SetEnvironmentVariable** метод **System.Environment** класс для изменения независимый от сеанса к **PSModulePath** среды переменная.</span><span class="sxs-lookup"><span data-stu-id="5026d-127">This format uses the **SetEnvironmentVariable** method of the **System.Environment** class to make a session-independent change to the **PSModulePath** environment variable.</span></span>

  ```powershell

  #Save the current value in the $p variable.
  $p = [Environment]::GetEnvironmentVariable("PSModulePath")

  #Add the new path to the $p variable. Begin with a semi-colon separator.
  $p += ";C:\Program Files (x86)\MyCompany\Modules\"

  #Add the paths in $p to the PSModulePath value.
  [Environment]::SetEnvironmentVariable("PSModulePath",$p)

  ```

  > [!IMPORTANT]
  > <span data-ttu-id="5026d-128">После добавления пути к **PSModulePath**, следует широковещательных сообщение среду об изменении.</span><span class="sxs-lookup"><span data-stu-id="5026d-128">Once you have added the path to **PSModulePath**, you should broadcast an environment message about the change.</span></span> <span data-ttu-id="5026d-129">Широковещательная рассылка изменение позволяет другие приложения, например оболочки получить изменения.</span><span class="sxs-lookup"><span data-stu-id="5026d-129">Broadcasting the change allows other applications, such as the shell, to pick up the change.</span></span> <span data-ttu-id="5026d-130">Для передачи изменений, имеют код установки продукта отправки **WM_SETTINGCHANGE** сообщений с `lParam` равным строке «Среда».</span><span class="sxs-lookup"><span data-stu-id="5026d-130">To broadcast the change, have your product installation code send a **WM_SETTINGCHANGE** message with `lParam` set to the string "Environment".</span></span> <span data-ttu-id="5026d-131">Не забудьте отправить сообщение после установки модуля кода был обновлен **PSModulePath**.</span><span class="sxs-lookup"><span data-stu-id="5026d-131">Be sure to send the message after your module installation code has updated **PSModulePath**.</span></span>

### <a name="use-the-correct-module-directory-name"></a><span data-ttu-id="5026d-132">Укажите имя каталога правильный модуль</span><span class="sxs-lookup"><span data-stu-id="5026d-132">Use the Correct Module Directory Name</span></span>

<span data-ttu-id="5026d-133">Модуль «правильного» — это модуль, хранится в каталог, содержащий имя, совпадающее с именем базовое имя хотя бы один файл в каталоге модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-133">A "well-formed" module is a module that is stored in a directory that has the same name as the base name of at least one file in the module directory.</span></span> <span data-ttu-id="5026d-134">Если модуль не имеет правильный формат, Windows PowerShell не распознает его как модуль.</span><span class="sxs-lookup"><span data-stu-id="5026d-134">If a module is not well-formed, Windows PowerShell does not recognize it as a module.</span></span>

<span data-ttu-id="5026d-135">«Базовое имя «файла является имя без расширения имени файла.</span><span class="sxs-lookup"><span data-stu-id="5026d-135">The "base name" of a file is the name without the file name extension.</span></span> <span data-ttu-id="5026d-136">В модуле правильный формат имя каталога, который содержит файлы модуля должно соответствовать имени базового, по крайней мере одного файла в модуле.</span><span class="sxs-lookup"><span data-stu-id="5026d-136">In a well-formed module, the name of the directory that contains the module files must match the base name of at least one file in the module.</span></span>

<span data-ttu-id="5026d-137">Например в модуле Fabrikam образец в каталог, содержащий файлы модулей называется «Fabrikam» и по крайней мере один файл имеет базовое имя, «Fabrikam».</span><span class="sxs-lookup"><span data-stu-id="5026d-137">For example, in the sample Fabrikam module, the directory that contains the module files is named "Fabrikam" and at least one file has the "Fabrikam" base name.</span></span> <span data-ttu-id="5026d-138">В этом случае Fabrikam.psd1 и Fabrikam.dll иметь базовое имя «Fabrikam».</span><span class="sxs-lookup"><span data-stu-id="5026d-138">In this case, both Fabrikam.psd1 and Fabrikam.dll have the "Fabrikam" base name.</span></span>

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

### <a name="effect-of-incorrect-installation"></a><span data-ttu-id="5026d-139">Последствия неправильная установка</span><span class="sxs-lookup"><span data-stu-id="5026d-139">Effect of Incorrect Installation</span></span>

<span data-ttu-id="5026d-140">Если модуль не является правильным и его расположение не включается в значении параметра **PSModulePath** переменной среды, базового обнаружения функции Windows PowerShell, как указано ниже, не работают.</span><span class="sxs-lookup"><span data-stu-id="5026d-140">If the module is not well-formed and its location is not included in the value of the **PSModulePath** environment variable, basic discovery features of Windows PowerShell, such as the following, do not work.</span></span>

- <span data-ttu-id="5026d-141">Компонент модуля автоматическая загрузка не удается импортировать модуль автоматически.</span><span class="sxs-lookup"><span data-stu-id="5026d-141">The Module Auto-Loading feature cannot import the module automatically.</span></span>

- <span data-ttu-id="5026d-142">`ListAvailable` Параметр [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) командлету не удается найти модуль.</span><span class="sxs-lookup"><span data-stu-id="5026d-142">The `ListAvailable` parameter of the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet cannot find the module.</span></span>

- <span data-ttu-id="5026d-143">[Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) командлету не удается найти модуль.</span><span class="sxs-lookup"><span data-stu-id="5026d-143">The [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet cannot find the module.</span></span> <span data-ttu-id="5026d-144">Чтобы импортировать модуль, необходимо указать полный путь к корневой файл модуля или файлу манифеста модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-144">To import the module, you must provide the full path to the root module file or module manifest file.</span></span>

  <span data-ttu-id="5026d-145">Дополнительные возможности, как указано ниже, не работают, если модуль импортируется в сеанс.</span><span class="sxs-lookup"><span data-stu-id="5026d-145">Additional features, such as the following, do not work unless the module is imported into the session.</span></span> <span data-ttu-id="5026d-146">В модули правильного формата в **PSModulePath** переменной среды, эти функции работают даже в том случае, если модуль не импортируется в сеанс.</span><span class="sxs-lookup"><span data-stu-id="5026d-146">In well-formed modules in the **PSModulePath** environment variable, these features work even when the module is not imported into the session.</span></span>

- <span data-ttu-id="5026d-147">[Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) командлету не удается найти команды в модуле.</span><span class="sxs-lookup"><span data-stu-id="5026d-147">The [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) cmdlet cannot find commands in the module.</span></span>

- <span data-ttu-id="5026d-148">[Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) и [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) командлеты не удается обновить или сохранить файлы справки для модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-148">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) cmdlets cannot update or save help for the module.</span></span>

- <span data-ttu-id="5026d-149">[Show-Command](/powershell/module/Microsoft.PowerShell.Utility/Show-Command) командлет не удается найти и отобразить команды в модуле.</span><span class="sxs-lookup"><span data-stu-id="5026d-149">The [Show-Command](/powershell/module/Microsoft.PowerShell.Utility/Show-Command) cmdlet cannot find and display the commands in the module.</span></span>

  <span data-ttu-id="5026d-150">Команды в модуле отсутствуют `Show-Command` окна в Windows PowerShell среды (Интегрированная скриптов).</span><span class="sxs-lookup"><span data-stu-id="5026d-150">The commands in the module are missing from the `Show-Command` window in Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="where-to-install-modules"></a><span data-ttu-id="5026d-151">Место установки модулей</span><span class="sxs-lookup"><span data-stu-id="5026d-151">Where to Install Modules</span></span>

<span data-ttu-id="5026d-152">В этом разделе объясняется в файловой системе для установки модулей Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5026d-152">This section explains where in the file system to install Windows PowerShell modules.</span></span> <span data-ttu-id="5026d-153">Расположение зависит от того, как используется модуль.</span><span class="sxs-lookup"><span data-stu-id="5026d-153">The location depends on how the module is used.</span></span>

### <a name="installing-modules-for-a-specific-user"></a><span data-ttu-id="5026d-154">Установка модулей для конкретного пользователя</span><span class="sxs-lookup"><span data-stu-id="5026d-154">Installing Modules for a Specific User</span></span>

<span data-ttu-id="5026d-155">Если создать собственный модуль или получить модуль от другой стороны, таких как веб-сайт сообщества Windows PowerShell, и требуется, чтобы модуль был доступен для учетной записи пользователя только, установите модуль в каталоге модулей конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="5026d-155">If you create your own module or get a module from another party, such as a Windows PowerShell community website, and you want the module to be available for your user account only, install the module in your user-specific Modules directory.</span></span>

```
$home\Documents\WindowsPowerShell\Modules\<Module Folder>\<Module Files>
```

<span data-ttu-id="5026d-156">Каталог Modules конкретного пользователя добавляется к значению **PSModulePath** переменной среды по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5026d-156">The user-specific Modules directory is added to the value of the **PSModulePath** environment variable by default.</span></span>

### <a name="installing-modules-for-all-users-in-program-files"></a><span data-ttu-id="5026d-157">Установка модулей для всех пользователей в каталоге Program Files</span><span class="sxs-lookup"><span data-stu-id="5026d-157">Installing Modules for all Users in Program Files</span></span>

<span data-ttu-id="5026d-158">Если требуется, чтобы модуль был доступен всем учетным записям пользователей на компьютере, установите модуль в папке Program Files.</span><span class="sxs-lookup"><span data-stu-id="5026d-158">If you want a module to be available to all user accounts on the computer, install the module in the Program Files location.</span></span>

```
$Env:ProgramFiles\WindowsPowerShell\Modules\<Module Folder>\<Module Files>
```

> [!NOTE]
> <span data-ttu-id="5026d-159">Расположение программных файлов добавляется к значению переменной среды PSModulePath по умолчанию в Windows PowerShell 4.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5026d-159">The Program Files location is added to the value of the PSModulePath environment variable by default in Windows PowerShell 4.0 and later.</span></span> <span data-ttu-id="5026d-160">Для более ранних версиях Windows PowerShell, можно вручную создать ((%ProgramFiles%\WindowsPowerShell\Modules) расположение Program Files и добавить этот путь в переменную среды PSModulePath, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="5026d-160">For earlier versions of Windows PowerShell, you can manually create the Program Files location ((%ProgramFiles%\WindowsPowerShell\Modules) and add this path to your PSModulePath environment variable as described above.</span></span>

### <a name="installing-modules-in-a-product-directory"></a><span data-ttu-id="5026d-161">Установка модулей в каталоге продуктов</span><span class="sxs-lookup"><span data-stu-id="5026d-161">Installing Modules in a Product Directory</span></span>

<span data-ttu-id="5026d-162">Если планируется распространять модуль другим сторонам, используйте расположение по умолчанию Program Files, описанных выше, или создайте собственные конкретной компании или конкретного продукта подкаталог в каталоге % ProgramFiles %.</span><span class="sxs-lookup"><span data-stu-id="5026d-162">If you are distributing the module to other parties, use the default Program Files location described above, or create your own company-specific or product-specific subdirectory of the %ProgramFiles% directory.</span></span>

<span data-ttu-id="5026d-163">Например Fabrikam технологий, вымышленной компании продается модуль Windows PowerShell для своего продукта Fabrikam Manager.</span><span class="sxs-lookup"><span data-stu-id="5026d-163">For example, Fabrikam Technologies, a fictitious company, is shipping a Windows PowerShell module for their Fabrikam Manager product.</span></span> <span data-ttu-id="5026d-164">Их установщика модулей создает подкаталог модули в подкаталоге продукта Fabrikam Manager.</span><span class="sxs-lookup"><span data-stu-id="5026d-164">Their module installer creates a Modules subdirectory in the Fabrikam Manager product subdirectory.</span></span>

```
C:\Program Files
  Fabrikam Technologies
    Fabrikam Manager
      Modules
        Fabrikam
          Fabrikam.psd1 (module manifest)
          Fabrikam.dll (module assembly)

```

<span data-ttu-id="5026d-165">Чтобы включить функции обнаружения, работающего в модуле Windows PowerShell найти модуль Fabrikam, установщика модулей Fabrikam добавляет расположение модуля значение **PSModulePath** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5026d-165">To enable the Windows PowerShell module discovery features to find the Fabrikam module, the Fabrikam module installer adds the module location to the value of the **PSModulePath** environment variable.</span></span>

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += "C:\Program Files\Fabrikam Technolgies\Fabrikam Manager\Modules\"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

### <a name="installing-modules-in-the-common-files-directory"></a><span data-ttu-id="5026d-166">Установка модулей в каталоге общих файлов</span><span class="sxs-lookup"><span data-stu-id="5026d-166">Installing Modules in the Common Files Directory</span></span>

<span data-ttu-id="5026d-167">Если модуль используется в нескольких компонентах продукта или несколько версий продукта, установите модуль в подкаталоге каталога конкретного модуля в подкаталог в каталоге %ProgramFiles%\Common Files\Modules.</span><span class="sxs-lookup"><span data-stu-id="5026d-167">If a module is used by multiple components of a product or by multiple versions of a product, install the module in a module-specific subdirectory of the %ProgramFiles%\Common Files\Modules subdirectory.</span></span>

<span data-ttu-id="5026d-168">В следующем примере в подкаталоге каталога Fabrikam в подкаталог в каталоге %ProgramFiles%\Common Files\Modules установлен модуль Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="5026d-168">In the following example, the Fabrikam module is installed in a Fabrikam subdirectory of the %ProgramFiles%\Common Files\Modules subdirectory.</span></span> <span data-ttu-id="5026d-169">Обратите внимание на то, что каждый модуль находится в свой собственный подкаталог в подкаталоге модулей.</span><span class="sxs-lookup"><span data-stu-id="5026d-169">Note that each module resides in its own subdirectory in the Modules subdirectory.</span></span>

```
C:\Program Files
  Common Files
    Modules
      Fabrikam
        Fabrikam.psd1 (module manifest)
        Fabrikam.dll (module assembly)

```

<span data-ttu-id="5026d-170">Затем установщик гарантирует значение **PSModulePath** переменной среды включает в себя путь подкаталога, общие файлы модулей.</span><span class="sxs-lookup"><span data-stu-id="5026d-170">Then, the installer assures the value of the **PSModulePath** environment variable includes the path of the common files modules subdirectory.</span></span>

```powershell
$m = $env:ProgramFiles + '\Common Files\Modules'
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$q = $p -split ';'
if ($q -notContains $m) {
    $q += ";$m"
}
$p = $q -join ';'
[Environment]::SetEnvironmentVariable("PSModulePath", $p)
```

## <a name="installing-multiple-versions-of-a-module"></a><span data-ttu-id="5026d-171">Установка нескольких версий модуля</span><span class="sxs-lookup"><span data-stu-id="5026d-171">Installing Multiple Versions of a Module</span></span>

<span data-ttu-id="5026d-172">Чтобы установить несколько версий одного модуля, используйте следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="5026d-172">To install multiple versions of the same module, use the following procedure.</span></span>

1. <span data-ttu-id="5026d-173">Создайте каталог для каждой версии модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-173">Create a directory for each version of the module.</span></span> <span data-ttu-id="5026d-174">Включите номер версии в имени каталога.</span><span class="sxs-lookup"><span data-stu-id="5026d-174">Include the version number in the directory name.</span></span>

2. <span data-ttu-id="5026d-175">Создание манифеста модуля для каждой версии модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-175">Create a module manifest for each version of the module.</span></span> <span data-ttu-id="5026d-176">В значении параметра **ModuleVersion** ключа в манифесте, введите номер версии модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-176">In the value of the **ModuleVersion** key in the manifest, enter the module version number.</span></span> <span data-ttu-id="5026d-177">Сохраните файл манифеста (psd1) в каталоге конкретной версии модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-177">Save the manifest file (.psd1) in the version-specific directory for the module.</span></span>

3. <span data-ttu-id="5026d-178">Добавьте путь к корневой папке модуля значению **PSModulePath** переменной среды, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="5026d-178">Add the module root folder path to the value of the **PSModulePath** environment variable, as shown in the following examples.</span></span>

<span data-ttu-id="5026d-179">Чтобы импортировать определенную версию модуля, пользователь может использовать `MinimumVersion` или `RequiredVersion` параметры [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) командлета.</span><span class="sxs-lookup"><span data-stu-id="5026d-179">To import a particular version of the module, the end-user can use the `MinimumVersion` or `RequiredVersion` parameters of the [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet.</span></span>

<span data-ttu-id="5026d-180">К примеру Если модуль Fabrikam доступна в версии 8.0 и 9.0, структура каталога Fabrikam модуля может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5026d-180">For example, if the Fabrikam module is available in versions 8.0 and 9.0, the Fabrikam module directory structure might resemble the following.</span></span>

 ```
C:\Program Files
Fabrikam Manager
  Fabrikam8
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "8.0")
      Fabrikam.dll (module assembly)
  Fabrikam9
    Fabrikam
      Fabrikam.psd1 (module manifest: ModuleVersion = "9.0")
      Fabrikam.dll (module assembly)
```

<span data-ttu-id="5026d-181">Установщик добавляет Оба модуля путей к **PSModulePath** значение переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5026d-181">The installer adds both of the module paths to the **PSModulePath** environment variable value.</span></span>

```powershell
$p = [Environment]::GetEnvironmentVariable("PSModulePath")
$p += ";C:\Program Files\Fabrikam\Fabrikam8;C:\Program Files\Fabrikam\Fabrikam9"
[Environment]::SetEnvironmentVariable("PSModulePath",$p)
```

<span data-ttu-id="5026d-182">После выполнения этих действий, **ListAvailable** параметр [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) командлет получает обоих модулей Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="5026d-182">When these steps are complete, the **ListAvailable** parameter of the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet gets both of the Fabrikam modules.</span></span> <span data-ttu-id="5026d-183">Чтобы импортировать определенного модуля, используйте `MiminumVersion` или `RequiredVersion` параметры [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) командлета.</span><span class="sxs-lookup"><span data-stu-id="5026d-183">To import a particular module, use the `MiminumVersion` or `RequiredVersion` parameters of the [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet.</span></span>

<span data-ttu-id="5026d-184">Если оба модуля, импортируются в том же сеансе, а модули содержат командлеты с одинаковыми именами, командлеты, которые импортируются последнего вступают в силу в сеансе.</span><span class="sxs-lookup"><span data-stu-id="5026d-184">If both modules are imported into the same session, and the modules contain cmdlets with the same names, the cmdlets that are imported last are effective in the session.</span></span>

## <a name="handling-command-name-conflicts"></a><span data-ttu-id="5026d-185">Конфликта имен команд обработки</span><span class="sxs-lookup"><span data-stu-id="5026d-185">Handling Command Name Conflicts</span></span>

<span data-ttu-id="5026d-186">Команда конфликты имен могут возникать, когда команды, которые экспортирует модуль имеют имя, совпадающее с именем команды в сеансе пользователя.</span><span class="sxs-lookup"><span data-stu-id="5026d-186">Command name conflicts can occur when the commands that a module exports have the same name as commands in the user's session.</span></span>

<span data-ttu-id="5026d-187">Если сеанс содержит две команды, которые имеют одинаковые имена, Windows PowerShell выполняет тип команды, который имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="5026d-187">When a session contains two commands that have the same name, Windows PowerShell runs the command type that takes precedence.</span></span> <span data-ttu-id="5026d-188">Если сеанс содержит две команды, которые имеют то же имя и тот же тип, Windows PowerShell выполняет команду, который был добавлен к сеансу наиболее недавно.</span><span class="sxs-lookup"><span data-stu-id="5026d-188">When a session contains two commands that have the same name and the same type, Windows PowerShell runs the command that was added to the session most recently.</span></span> <span data-ttu-id="5026d-189">Чтобы выполнить команду, которая выполняется не по умолчанию, пользователям можно уточнить имя команды с именем модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-189">To run a command that is not run by default, users can qualify the command name with the module name.</span></span>

<span data-ttu-id="5026d-190">Например, если сеанс содержит `Get-Date` функции и `Get-Date` командлета Windows PowerShell выполняет функцию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5026d-190">For example, if the session contains a `Get-Date` function and the `Get-Date` cmdlet, Windows PowerShell runs the function by default.</span></span> <span data-ttu-id="5026d-191">Для выполнения командлета, введите перед командой имя модуля, такие как:</span><span class="sxs-lookup"><span data-stu-id="5026d-191">To run the cmdlet, preface the command with the module name, such as:</span></span>

```powershell
Microsoft.PowerShell.Utility\Get-Date
```

<span data-ttu-id="5026d-192">Чтобы предотвратить конфликты имен, авторы модулей могут использовать **DefaultCommandPrefix** экспорта ключа в манифесте модуля, чтобы указать предлог для всех команд из модуля.</span><span class="sxs-lookup"><span data-stu-id="5026d-192">To prevent name conflicts, module authors can use the **DefaultCommandPrefix** key in the module manifest to specify a noun prefix for all commands exported from the module.</span></span>

<span data-ttu-id="5026d-193">Пользователи могут использовать **префикс** параметр `Import-Module` командлет, чтобы использовать альтернативный префикс.</span><span class="sxs-lookup"><span data-stu-id="5026d-193">Users can use the **Prefix** parameter of the `Import-Module` cmdlet to use an alternate prefix.</span></span> <span data-ttu-id="5026d-194">Значение **префикса** имеет приоритет над значением **DefaultCommandPrefix** ключ.</span><span class="sxs-lookup"><span data-stu-id="5026d-194">The value of the **Prefix** parameter takes precedence over the value of the **DefaultCommandPrefix** key.</span></span>

## <a name="see-also"></a><span data-ttu-id="5026d-195">См. также</span><span class="sxs-lookup"><span data-stu-id="5026d-195">See Also</span></span>

[<span data-ttu-id="5026d-196">about_Command_Precedence</span><span class="sxs-lookup"><span data-stu-id="5026d-196">about_Command_Precedence</span></span>](/powershell/module/microsoft.powershell.core/about/about_command_precedence)

[<span data-ttu-id="5026d-197">Написание модуля Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="5026d-197">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)