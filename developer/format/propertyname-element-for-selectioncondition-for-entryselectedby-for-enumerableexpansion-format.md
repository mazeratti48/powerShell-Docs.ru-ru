---
title: Элемент PropertyName для SelectionCondition для EntrySelectedBy для EnumerableExpansion (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ae11924-0072-451e-bf70-c5ffb25dccc0
caps.latest.revision: 13
ms.openlocfilehash: 0c20512e660c8d2b61d063dbd7078b55b23efeb8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56859630"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="77f27-102">Элемент PropertyName для элемента SelectionCondition для элемента EntrySelectedBy для элемента EnumerableExpansion (формат)</span><span class="sxs-lookup"><span data-stu-id="77f27-102">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="77f27-103">Задает свойство .NET, которое активирует условие.</span><span class="sxs-lookup"><span data-stu-id="77f27-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="77f27-104">Если этому свойству присвоено присутствует или когда оно оценивается как `true`условие выполняется, и используется определение.</span><span class="sxs-lookup"><span data-stu-id="77f27-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="77f27-105">Элемент (формат) элемент DefaultSettings (формат) элемент EnumerableExpansions (формат) элемент EnumerableExpansion (формат) EntrySelectedBy элемента конфигурации для элемента SelectionCondition EnumerableExpansion (формат) EntrySelectedBy для Элемент PropertyName EnumerableExpansion (формат) для SelectionCondition для EntrySelectedBy для EnumerableExpansion (формат)</span><span class="sxs-lookup"><span data-stu-id="77f27-105">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="77f27-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="77f27-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="77f27-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="77f27-107">Attributes and Elements</span></span>

<span data-ttu-id="77f27-108">Ниже описаны атрибуты, дочерние элементы и родительский элемент `PropertyName` элемент.</span><span class="sxs-lookup"><span data-stu-id="77f27-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="77f27-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="77f27-109">Attributes</span></span>

<span data-ttu-id="77f27-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="77f27-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="77f27-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="77f27-111">Child Elements</span></span>

<span data-ttu-id="77f27-112">Нет.</span><span class="sxs-lookup"><span data-stu-id="77f27-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="77f27-113">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="77f27-113">Parent Elements</span></span>

|<span data-ttu-id="77f27-114">Элемент</span><span class="sxs-lookup"><span data-stu-id="77f27-114">Element</span></span>|<span data-ttu-id="77f27-115">Описание</span><span class="sxs-lookup"><span data-stu-id="77f27-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="77f27-116">Элемент SelectionCondition для EntrySelectedBy для EnumerableExpansion (формат)</span><span class="sxs-lookup"><span data-stu-id="77f27-116">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="77f27-117">Определяет условие, которое должно существовать разверните коллекцию объектов данного определения.</span><span class="sxs-lookup"><span data-stu-id="77f27-117">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="77f27-118">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="77f27-118">Text Value</span></span>

<span data-ttu-id="77f27-119">Укажите имя свойства .NET.</span><span class="sxs-lookup"><span data-stu-id="77f27-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="77f27-120">Замечания</span><span class="sxs-lookup"><span data-stu-id="77f27-120">Remarks</span></span>

<span data-ttu-id="77f27-121">Условию выбора необходимо указать по крайней мере для одного имени свойства или сценарий для оценки, но нельзя указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="77f27-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="77f27-122">Дополнительные сведения об использовании условий выборки см. в разделе [определение условий при отображении данных](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="77f27-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="77f27-123">См. также</span><span class="sxs-lookup"><span data-stu-id="77f27-123">See Also</span></span>

[<span data-ttu-id="77f27-124">Определение условия для данных, когда отображается</span><span class="sxs-lookup"><span data-stu-id="77f27-124">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="77f27-125">Элемент ScriptBlock для SelectionCondition для EntrySelectedBy для EnumerableExpansion (формат)</span><span class="sxs-lookup"><span data-stu-id="77f27-125">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="77f27-126">Элемент SelectionCondition для EntrySelectedBy для EnumerableExpansion (формат)</span><span class="sxs-lookup"><span data-stu-id="77f27-126">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="77f27-127">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="77f27-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)