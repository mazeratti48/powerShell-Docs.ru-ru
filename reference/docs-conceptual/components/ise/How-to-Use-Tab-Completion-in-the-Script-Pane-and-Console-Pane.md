---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Использование заполнения нажатием клавиши TAB в областях сценариев и консоли
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: 24a3f00987ff5ca4bf82d1a3206857ec3c4b3f09
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53402216"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Использование заполнения нажатием клавиши TAB в областях сценариев и консоли

Заполнение нажатием клавиши TAB предоставляет автоматическую справку при вводе в области скриптов или команд. Чтобы воспользоваться этой функцией, выполните следующие действия:

## <a name="to-automatically-complete-a-command-entry"></a>Автоматическое завершение ввода команды

В области команд или сценариев введите несколько символов команды и нажмите клавишу TAB, чтобы выбрать нужный текст завершения. Если с изначально введенного текста начинается несколько элементов, нажимайте клавишу TAB, пока не появится нужный. Заполнение нажатием клавиши TAB позволяет ввести имя командлета, параметра, переменной, свойства объекта или путь к файлу.

> [!NOTE]
> В области сценариев нажатие клавиши TAB автоматически завершает команду только при редактировании файлов PS1, PSD1 или PSM1. Заполнение нажатием клавиши TAB работает в любое время при вводе в области команд.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Автоматическое завершение ввода для параметра командлета

В области команд или сценариев введите командлет, поставьте после него дефис и нажмите клавишу TAB.

Например, введите `Get-Process -` и нажмите клавишу TAB несколько раз для отображения параметров командлета по очереди.

## <a name="see-also"></a>См. также

- [Введение в интегрированную среду сценариев Windows PowerShell](Introducing-the-Windows-PowerShell-ISE.md)
- [Создание вкладки PowerShell](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)