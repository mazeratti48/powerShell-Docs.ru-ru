---
title: Модули и оснастки | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d342f91-23e0-467f-8de2-f9657d820693
caps.latest.revision: 6
ms.openlocfilehash: 157cd64e286392f3fd770e1e34542682b1e63625
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72365373"
---
# <a name="modules-and-snap-ins"></a>Модули и оснастки

Командлеты можно добавить в сеанс с помощью модулей (представленных в Windows PowerShell 2,0) или оснасток. После добавления командлета в сеанс его можно запустить программно ведущим приложением или интерактивно в командной строке.

В качестве метода доставки для добавления командлетов в сеанс рекомендуется использовать модули по следующим причинам.

- Модули позволяют добавлять командлеты путем загрузки сборки, в которой определен командлет. Реализовывать класс оснастки не требуется.

- Модули позволяют добавлять другие ресурсы, такие как переменные, функции, скрипты, типы и файлы форматирования, и многое другое.

- Оснастки могут использоваться только для добавления командлетов и поставщиков в сеанс.

## <a name="see-also"></a>См. также:

[Написание модуля Windows PowerShell](../module/writing-a-windows-powershell-module.md)

[Запись командлета Windows PowerShell](./writing-a-windows-powershell-cmdlet.md)
