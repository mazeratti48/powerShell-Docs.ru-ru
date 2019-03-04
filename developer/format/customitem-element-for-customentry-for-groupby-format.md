---
title: Элемент CustomItem для CustomEntry для GroupBy (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7c517aa-24f5-41ae-b82d-cb0fac81a245
caps.latest.revision: 7
ms.openlocfilehash: 2d821f5e3bc8d0f81ef8a8a040c6f9bcb1658bee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856930"
---
# <a name="customitem-element-for-customentry-for-groupby-format"></a><span data-ttu-id="439df-102">Элемент CustomItem для элемента CustomEntry для элемента GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-102">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>

<span data-ttu-id="439df-103">Определяет, какие данные отображаются в представлении пользовательского элемента управления и как он отображается.</span><span class="sxs-lookup"><span data-stu-id="439df-103">Defines what data is displayed by the custom control view and how it is displayed.</span></span> <span data-ttu-id="439df-104">Этот элемент используется при определении того, как отображается группу объектов.</span><span class="sxs-lookup"><span data-stu-id="439df-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="439df-105">Элемент (формат) элемент ViewDefinitions (формат) представление элемента (формат) GroupBy элемента конфигурации для элемента представления (формат) пользовательский элемент управления для элемента CustomEntries GroupBy (формат) пользовательский элемент управления для элемента CustomItem GroupBy (формат) CustomEntry для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="439df-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="439df-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <Frame>...</Frame>
  <NewLine/>
  <Text>TextToDisplay</Text>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="439df-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="439df-107">Attributes and Elements</span></span>

<span data-ttu-id="439df-108">Ниже описаны атрибуты, дочерние элементы и родительский элемент `CustomItem` элемент.</span><span class="sxs-lookup"><span data-stu-id="439df-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="439df-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="439df-109">Attributes</span></span>

<span data-ttu-id="439df-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="439df-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="439df-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="439df-111">Child Elements</span></span>

|<span data-ttu-id="439df-112">Элемент</span><span class="sxs-lookup"><span data-stu-id="439df-112">Element</span></span>|<span data-ttu-id="439df-113">Описание</span><span class="sxs-lookup"><span data-stu-id="439df-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="439df-114">Элемент ExpressionBinding для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-114">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="439df-115">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="439df-115">Optional element.</span></span><br /><br /> <span data-ttu-id="439df-116">Определяет данные, отображаемые элементом управления.</span><span class="sxs-lookup"><span data-stu-id="439df-116">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="439df-117">Элемент Frame для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-117">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="439df-118">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="439df-118">Optional element.</span></span><br /><br /> <span data-ttu-id="439df-119">Определяет, какие данные отображаются в представлении пользовательского элемента управления и как он отображается.</span><span class="sxs-lookup"><span data-stu-id="439df-119">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|
|[<span data-ttu-id="439df-120">Элемент новой строки для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-120">NewLine Element for CustomItem for GroupBy (Format)</span></span>](./newline-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="439df-121">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="439df-121">Optional element.</span></span><br /><br /> <span data-ttu-id="439df-122">Добавляет пустой строки для отображения элемента управления.</span><span class="sxs-lookup"><span data-stu-id="439df-122">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="439df-123">Текстовый элемент для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-123">Text Element for CustomItem for GroupBy (Format)</span></span>](./text-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="439df-124">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="439df-124">Optional element.</span></span><br /><br /> <span data-ttu-id="439df-125">Задает дополнительный текст для данных, отображаемых элементом управления.</span><span class="sxs-lookup"><span data-stu-id="439df-125">Specifies additional text to the data displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="439df-126">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="439df-126">Parent Elements</span></span>

|<span data-ttu-id="439df-127">Элемент</span><span class="sxs-lookup"><span data-stu-id="439df-127">Element</span></span>|<span data-ttu-id="439df-128">Описание</span><span class="sxs-lookup"><span data-stu-id="439df-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="439df-129">Элемент CustomEntry для пользовательский элемент управления для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-129">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="439df-130">Предоставляет определение пользовательского элемента управления представления.</span><span class="sxs-lookup"><span data-stu-id="439df-130">Provides a definition of the custom control view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="439df-131">Замечания</span><span class="sxs-lookup"><span data-stu-id="439df-131">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="439df-132">См. также</span><span class="sxs-lookup"><span data-stu-id="439df-132">See Also</span></span>

[<span data-ttu-id="439df-133">Элемент CustomEntry для пользовательский элемент управления для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-133">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)

[<span data-ttu-id="439df-134">Элемент ExpressionBinding для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-134">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="439df-135">Элемент Frame для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-135">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="439df-136">Элемент новой строки для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-136">NewLine Element for CustomItem for GroupBy (Format)</span></span>](./newline-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="439df-137">Текстовый элемент для CustomItem для GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="439df-137">Text Element for CustomItem for GroupBy (Format)</span></span>](./text-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="439df-138">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="439df-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)