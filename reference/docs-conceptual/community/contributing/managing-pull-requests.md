---
title: Рассмотрение запросов на вытягивание
description: В этой статье описывается, как команда PowerShell-Docs управляет запросами на вытягивание.
ms.date: 03/05/2020
ms.topic: conceptual
ms.openlocfilehash: b9b37816dfdf38e4d8b7c2d66799164d0e97d257
ms.sourcegitcommit: 18d832858a7b8ea094763afa753e0f48f01372e7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2020
ms.locfileid: "79060389"
---
# <a name="managing-pull-requests"></a><span data-ttu-id="cb589-103">Управление запросами на вытягивание</span><span class="sxs-lookup"><span data-stu-id="cb589-103">Managing pull requests</span></span>

<span data-ttu-id="cb589-104">В этой статье описывается, как мы управляем запросами на вытягивание в репозитории PowerShell-Docs.</span><span class="sxs-lookup"><span data-stu-id="cb589-104">This article documents how we manage pull requests in the PowerShell-Docs repo.</span></span> <span data-ttu-id="cb589-105">Изначально это памятка для участников команды PowerShell-Docs.</span><span class="sxs-lookup"><span data-stu-id="cb589-105">This article is designed to be a job aid for members of the PowerShell-Docs team.</span></span> <span data-ttu-id="cb589-106">Здесь она публикуется с целью обеспечить прозрачность процесса для широкого круга участников.</span><span class="sxs-lookup"><span data-stu-id="cb589-106">It is published here to provide process transparency for our public contributors.</span></span>

## <a name="best-practices"></a><span data-ttu-id="cb589-107">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb589-107">Best practices</span></span>

- <span data-ttu-id="cb589-108">Пользователь, отправляющий запрос на вытягивание, не должен выполнять его слияние, пока не будет проведена его оценка коллегами.</span><span class="sxs-lookup"><span data-stu-id="cb589-108">The person submitting the PR should not merge the PR without a peer review.</span></span>
- <span data-ttu-id="cb589-109">Назначьте рецензента при отправке запроса на вытягивание.</span><span class="sxs-lookup"><span data-stu-id="cb589-109">Assign the peer reviewer when the PR is submitted.</span></span> <span data-ttu-id="cb589-110">Чем раньше вы его назначите, тем раньше он сможет предоставить свои замечания.</span><span class="sxs-lookup"><span data-stu-id="cb589-110">Early assignment allows the reviewer to respond sooner with editorial remarks.</span></span>
- <span data-ttu-id="cb589-111">Используйте комментарии, чтобы описать характер изменения или тип запрашиваемой проверки.</span><span class="sxs-lookup"><span data-stu-id="cb589-111">Use comments to describe the nature of the change or the type of review being requested.</span></span> <span data-ttu-id="cb589-112">Обязательно упомяните (@mention) рецензента.</span><span class="sxs-lookup"><span data-stu-id="cb589-112">Be sure to @mention the reviewer.</span></span> <span data-ttu-id="cb589-113">Например, если изменение является незначительным и полная техническая проверка не требуется, поясните это в комментарии.</span><span class="sxs-lookup"><span data-stu-id="cb589-113">For example, if the change is minor and you don't need a full technical review, explain this in a comment.</span></span>

## <a name="pr-process-steps"></a><span data-ttu-id="cb589-114">Процедура обработки запроса на вытягивание</span><span class="sxs-lookup"><span data-stu-id="cb589-114">PR Process steps</span></span>

1. <span data-ttu-id="cb589-115">Автор. Создает запрос на вытягивание.</span><span class="sxs-lookup"><span data-stu-id="cb589-115">Writer: Create PR</span></span>
   - <span data-ttu-id="cb589-116">Приводит ссылки на проблемы, устраняемые запросом на вытягивание.</span><span class="sxs-lookup"><span data-stu-id="cb589-116">Link any issues resolved by the PR</span></span>
   - <span data-ttu-id="cb589-117">Использует функцию [автоматического закрытия](https://help.github.com/en/articles/closing-issues-using-keywords) GitHub для закрытия проблемы.</span><span class="sxs-lookup"><span data-stu-id="cb589-117">Use GitHub's [autoclose](https://help.github.com/en/articles/closing-issues-using-keywords) feature to close the issue</span></span>
1. <span data-ttu-id="cb589-118">Автор. Назначает рецензента из числа коллег.</span><span class="sxs-lookup"><span data-stu-id="cb589-118">Writer: Assign peer reviewer</span></span>
1. <span data-ttu-id="cb589-119">Рецензент. Вычитывает текст и предоставляет комментарии (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="cb589-119">Reviewer: proofreads and comments (as necessary)</span></span>
1. <span data-ttu-id="cb589-120">Автор. Вносит предложенные правки.</span><span class="sxs-lookup"><span data-stu-id="cb589-120">Writer: Incorporate review feedback</span></span>
1. <span data-ttu-id="cb589-121">Оба. Проверяют предварительную версию.</span><span class="sxs-lookup"><span data-stu-id="cb589-121">Both: Review preview rendering</span></span>
1. <span data-ttu-id="cb589-122">Оба. Проверяют отчет о проверке и исправляют предупреждения и ошибки.</span><span class="sxs-lookup"><span data-stu-id="cb589-122">Both: Review validation report - fix warnings and errors</span></span>
1. <span data-ttu-id="cb589-123">Автор. Добавляет комментарий об утверждении (включая сведения Acrolinx).</span><span class="sxs-lookup"><span data-stu-id="cb589-123">Writer: Add sign-off comment (include Acrolinx info)</span></span>
1. <span data-ttu-id="cb589-124">Рецензент. Помечает запрос как утвержденный.</span><span class="sxs-lookup"><span data-stu-id="cb589-124">Reviewer: Mark review "Approved"</span></span>
1. <span data-ttu-id="cb589-125">Администратор репозитория. Выполняет слияние запроса на вытягивание (критерии см. ниже).</span><span class="sxs-lookup"><span data-stu-id="cb589-125">Repo Admin: Merge PR (see below for criteria)</span></span>

## <a name="content-reviewer-checklist"></a><span data-ttu-id="cb589-126">Контрольный список для рецензента содержимого</span><span class="sxs-lookup"><span data-stu-id="cb589-126">Content Reviewer Checklist</span></span>

<span data-ttu-id="cb589-127">Более полный список см.в статье [Контрольный список для редактора](editorial-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="cb589-127">See the [editorial checklist](editorial-checklist.md) for a more comprehensive list.</span></span>

- <span data-ttu-id="cb589-128">Проверка на наличие грамматических и стилистических ошибок, лаконичность, техническую точность</span><span class="sxs-lookup"><span data-stu-id="cb589-128">Proofread for grammar, style, concision, technical accuracy</span></span>
- <span data-ttu-id="cb589-129">Проверка актуальности примеров для целевой версии</span><span class="sxs-lookup"><span data-stu-id="cb589-129">Ensure examples still apply for the target version</span></span>
- <span data-ttu-id="cb589-130">Проверка предварительной версии</span><span class="sxs-lookup"><span data-stu-id="cb589-130">Check Preview rendering</span></span>
- <span data-ttu-id="cb589-131">Проверка метаданных: правильно указано значение ms.date, удалено значение ms.assetid, имеются все требуемые поля</span><span class="sxs-lookup"><span data-stu-id="cb589-131">Check metadata - ms.date, remove ms.assetid, ensure required fields</span></span>
- <span data-ttu-id="cb589-132">Проверка правильности разметки Markdown</span><span class="sxs-lookup"><span data-stu-id="cb589-132">Validate markdown correctness</span></span>
  - <span data-ttu-id="cb589-133">Сведения о форматировании см. в руководстве по стилю.</span><span class="sxs-lookup"><span data-stu-id="cb589-133">See style guide for formatting specific content</span></span>
- <span data-ttu-id="cb589-134">Проверка правильности структуры примеров:</span><span class="sxs-lookup"><span data-stu-id="cb589-134">Reorganize examples as follows:</span></span>
  - <span data-ttu-id="cb589-135">вводные предложения;</span><span class="sxs-lookup"><span data-stu-id="cb589-135">Intro sentence(s)</span></span>
  - <span data-ttu-id="cb589-136">код и выходные данные;</span><span class="sxs-lookup"><span data-stu-id="cb589-136">Code and output</span></span>
  - <span data-ttu-id="cb589-137">подробное описание кода (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="cb589-137">Detailed explanation of code (as necessary)</span></span>
- <span data-ttu-id="cb589-138">Проверка точности гиперссылок</span><span class="sxs-lookup"><span data-stu-id="cb589-138">Check hyperlinks for accuracy</span></span>
  - <span data-ttu-id="cb589-139">Замена или удаление ссылок на TechNet и MSDN</span><span class="sxs-lookup"><span data-stu-id="cb589-139">Replace or remove TechNet/MSDN links</span></span>
  - <span data-ttu-id="cb589-140">Обеспечение минимального количества перенаправлений к целевому адресу</span><span class="sxs-lookup"><span data-stu-id="cb589-140">Ensure minimum number of redirects to target</span></span>
  - <span data-ttu-id="cb589-141">Проверка использования HTTPS</span><span class="sxs-lookup"><span data-stu-id="cb589-141">Ensure HTTPS</span></span>
  - <span data-ttu-id="cb589-142">Правильный тип ссылки</span><span class="sxs-lookup"><span data-stu-id="cb589-142">Correct link type</span></span>
    - <span data-ttu-id="cb589-143">Ссылки на файлы для локальных файлов</span><span class="sxs-lookup"><span data-stu-id="cb589-143">File links for local files</span></span>
    - <span data-ttu-id="cb589-144">URL-ссылки для файлов за пределами набора документов</span><span class="sxs-lookup"><span data-stu-id="cb589-144">URL links for files outside of the docset</span></span>
  - <span data-ttu-id="cb589-145">Удаление языкового стандарта из URL-адресов</span><span class="sxs-lookup"><span data-stu-id="cb589-145">Remove locales from URLs</span></span>
  - <span data-ttu-id="cb589-146">Упрощение URL-адресов, указывающих на `docs.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="cb589-146">Simplify URLs pointing to `docs.microsoft.com`</span></span>

## <a name="branch-merge-process"></a><span data-ttu-id="cb589-147">Процедура слияния ветвей</span><span class="sxs-lookup"><span data-stu-id="cb589-147">Branch Merge Process</span></span>

<span data-ttu-id="cb589-148">Ветвь staging — это единственная ветвь, подлежащая слиянию с ветвью live.</span><span class="sxs-lookup"><span data-stu-id="cb589-148">The staging branch is the only branch that should ever be merged into live.</span></span> <span data-ttu-id="cb589-149">Слияние временных (рабочих) ветвей должно выполняться со сжатием.</span><span class="sxs-lookup"><span data-stu-id="cb589-149">Merges from short-lived (working) branches should be squashed.</span></span>

| <span data-ttu-id="cb589-150">*Ветвь для слияния*</span><span class="sxs-lookup"><span data-stu-id="cb589-150">*Merge from/to*</span></span>  | <span data-ttu-id="cb589-151">*release-branch*</span><span class="sxs-lookup"><span data-stu-id="cb589-151">*release-branch*</span></span> | <span data-ttu-id="cb589-152">*staging*</span><span class="sxs-lookup"><span data-stu-id="cb589-152">*staging*</span></span>        | <span data-ttu-id="cb589-153">*live*</span><span class="sxs-lookup"><span data-stu-id="cb589-153">*live*</span></span>      |
| ---------------- |:----------------:|:----------------:|:-----------:|
| <span data-ttu-id="cb589-154">*working-branch*</span><span class="sxs-lookup"><span data-stu-id="cb589-154">*working-branch*</span></span> | <span data-ttu-id="cb589-155">слияние со сжатием</span><span class="sxs-lookup"><span data-stu-id="cb589-155">squash and merge</span></span> | <span data-ttu-id="cb589-156">слияние со сжатием</span><span class="sxs-lookup"><span data-stu-id="cb589-156">squash and merge</span></span> | <span data-ttu-id="cb589-157">Не разрешено</span><span class="sxs-lookup"><span data-stu-id="cb589-157">Not allowed</span></span> |
| <span data-ttu-id="cb589-158">*release-branch*</span><span class="sxs-lookup"><span data-stu-id="cb589-158">*release-branch*</span></span> | &mdash;          | <span data-ttu-id="cb589-159">merge</span><span class="sxs-lookup"><span data-stu-id="cb589-159">merge</span></span>            | <span data-ttu-id="cb589-160">Не разрешено</span><span class="sxs-lookup"><span data-stu-id="cb589-160">Not allowed</span></span> |
| <span data-ttu-id="cb589-161">*staging*</span><span class="sxs-lookup"><span data-stu-id="cb589-161">*staging*</span></span>        | <span data-ttu-id="cb589-162">перемещение</span><span class="sxs-lookup"><span data-stu-id="cb589-162">rebase</span></span>           | &mdash;          | <span data-ttu-id="cb589-163">merge</span><span class="sxs-lookup"><span data-stu-id="cb589-163">merge</span></span>       |

### <a name="pr-merger-checklist"></a><span data-ttu-id="cb589-164">Контрольный список для выполняющего слияние запроса на вытягивание</span><span class="sxs-lookup"><span data-stu-id="cb589-164">PR Merger checklist</span></span>

- <span data-ttu-id="cb589-165">Проверка содержимого завершена</span><span class="sxs-lookup"><span data-stu-id="cb589-165">Content review complete</span></span>
- <span data-ttu-id="cb589-166">Правильная целевая ветвь для изменения</span><span class="sxs-lookup"><span data-stu-id="cb589-166">Correct target branch for the change</span></span>
- <span data-ttu-id="cb589-167">Конфликты при слиянии отсутствуют</span><span class="sxs-lookup"><span data-stu-id="cb589-167">No merge conflicts</span></span>
- <span data-ttu-id="cb589-168">Все шаги проверки и сборки пройдены</span><span class="sxs-lookup"><span data-stu-id="cb589-168">All validation and build step pass</span></span>
  - <span data-ttu-id="cb589-169">Предупреждения и предложения учтены (исключения см. в разделе [Примечания](#notes))</span><span class="sxs-lookup"><span data-stu-id="cb589-169">Warnings and suggestions should be fixed (see [Notes](#notes) for exceptions)</span></span>
  - <span data-ttu-id="cb589-170">Нет неработающих ссылок</span><span class="sxs-lookup"><span data-stu-id="cb589-170">No broken links</span></span>
- <span data-ttu-id="cb589-171">Слияние в соответствии с таблицей</span><span class="sxs-lookup"><span data-stu-id="cb589-171">Merge according to table</span></span>

### <a name="notes"></a><span data-ttu-id="cb589-172">Примечания</span><span class="sxs-lookup"><span data-stu-id="cb589-172">Notes</span></span>

<span data-ttu-id="cb589-173">Представленные ниже предупреждения можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="cb589-173">The following warnings can be ignored:</span></span>

```
Can't find service name for `<version>/<modulepath>/About/About.md`
```

```
Metadata with following name(s) are not allowed to be set in Yaml header, or as file level
metadata in docfx.json, or as global metadata in docfx.json: `locale`. They are generated by
Docs platform, so the values set in these 3 places will be ignored. Please remove them from all
3 places to resolve the warning.
```

<span data-ttu-id="cb589-174">При слиянии запроса на вытягивание указатель HEAD целевой ветви меняется.</span><span class="sxs-lookup"><span data-stu-id="cb589-174">When a PR is merged, the HEAD of the target branch is changed.</span></span> <span data-ttu-id="cb589-175">Все открытые запросы на вытягивание, основанные на предыдущем указателе HEAD, устаревают.</span><span class="sxs-lookup"><span data-stu-id="cb589-175">Any open PRs that were based on the previous HEAD are now outdated.</span></span> <span data-ttu-id="cb589-176">Для слияния устаревшего запроса на вытягивание требуются права администратора, которые позволяют игнорировать предупреждения о слиянии в GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb589-176">The outdated PR can be merged using Admin rights to override the merge warnings in GitHub.</span></span> <span data-ttu-id="cb589-177">Это можно делать без риска, если запросы на вытягивание, слияние которых было выполнено ранее, не затрагивали те же файлы.</span><span class="sxs-lookup"><span data-stu-id="cb589-177">This is safe to do if the previously merged PR(s) have not touched the same files.</span></span> <span data-ttu-id="cb589-178">Однако безопаснее будет нажать кнопку **Update Branch** (Обновить ветвь).</span><span class="sxs-lookup"><span data-stu-id="cb589-178">However, clicking the **Update Branch** button is the safest option.</span></span> <span data-ttu-id="cb589-179">Может потребоваться устранить неразрешенные конфликты.</span><span class="sxs-lookup"><span data-stu-id="cb589-179">You may have unresolved conflicts that need to be fixed.</span></span>

## <a name="publishing-to-live"></a><span data-ttu-id="cb589-180">Публикация в ветви Live</span><span class="sxs-lookup"><span data-stu-id="cb589-180">Publishing to Live</span></span>

<span data-ttu-id="cb589-181">Изменения, накопленные в ветви `staging`, необходимо периодически публиковать на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="cb589-181">Periodically, the changes accumulated in the `staging` branch need to be published to the live website.</span></span> <span data-ttu-id="cb589-182">Для этого нужно выполнить слияние ветви `staging` с ветвью `live`.</span><span class="sxs-lookup"><span data-stu-id="cb589-182">This require merging the `staging` branch into the `live` branch.</span></span>

- <span data-ttu-id="cb589-183">Слияние ветви `staging` с ветвью `live` следует выполнять не реже одного раза в неделю.</span><span class="sxs-lookup"><span data-stu-id="cb589-183">The `staging` branch should be merged to `live` at least once per week.</span></span>
- <span data-ttu-id="cb589-184">Слияние ветви `staging` с ветвью `live` следует выполнять после любого значительного изменения:</span><span class="sxs-lookup"><span data-stu-id="cb589-184">The `staging` branch should be merged to `live` after any significant change.</span></span>
  - <span data-ttu-id="cb589-185">внесения изменений в 50 или более файлов;</span><span class="sxs-lookup"><span data-stu-id="cb589-185">Changes to 50 or more files</span></span>
  - <span data-ttu-id="cb589-186">слияния ветви выпуска;</span><span class="sxs-lookup"><span data-stu-id="cb589-186">After merging a release branch</span></span>
  - <span data-ttu-id="cb589-187">внесения изменений в конфигурацию репозитория или набора документов (docfx.json, конфигурации OPS, скрипты сборки и т. д.);</span><span class="sxs-lookup"><span data-stu-id="cb589-187">Changes to repo or docset configurations (docfx.json, OPS configs, build scripts, etc.)</span></span>
  - <span data-ttu-id="cb589-188">внесения изменений в файл перенаправления;</span><span class="sxs-lookup"><span data-stu-id="cb589-188">Changes to the redirection file</span></span>
  - <span data-ttu-id="cb589-189">внесения изменений в оглавление;</span><span class="sxs-lookup"><span data-stu-id="cb589-189">Changes to the TOC</span></span>
  - <span data-ttu-id="cb589-190">слияния ветви проекта (для реорганизации содержимого, массового обновления и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cb589-190">After merging a "project" branch (content reorg, bulk update, etc.)</span></span>