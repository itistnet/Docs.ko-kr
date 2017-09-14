---
title: "ASP.NET Core의 스캐폴드된 Razor 페이지"
author: rick-anderson
description: "스캐폴딩을 통해 생성된 Razor 페이지를 설명합니다."
keywords: "ASP.NET Core, Razor 페이지, Razor, MVC"
ms.author: riande
manager: wpickett
ms.date: 7/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/page
ms.openlocfilehash: 02cbc7c7caf5128167dd3ecfdc0e2340f4876df5
ms.sourcegitcommit: d9ec19e5452af83648074db5d96c0a0f4f9e7f9a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scaffolded-razor-pages-in-aspnet-core"></a><span data-ttu-id="da3ee-104">ASP.NET Core의 스캐폴드된 Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="da3ee-104">Scaffolded Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="da3ee-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="da3ee-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="da3ee-106">이 자습서에서는 [이전 자습서](xref:tutorials/razor-pages/page)에서 스캐폴딩을 통해 만든 Razor 페이지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-106">This tutorial examines the Razor Pages created by scaffolding in the [previous tutorial](xref:tutorials/razor-pages/page).</span></span> 

<span data-ttu-id="da3ee-107">샘플을 [보거나 다운로드합니다](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie).</span><span class="sxs-lookup"><span data-stu-id="da3ee-107">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) sample.</span></span>

## <a name="the-create-delete-details-and-edit-pages"></a><span data-ttu-id="da3ee-108">만들기, 삭제, 세부 정보 및 편집 페이지.</span><span class="sxs-lookup"><span data-stu-id="da3ee-108">The Create, Delete, Details, and Edit pages.</span></span>

<span data-ttu-id="da3ee-109">*Pages/Movies/Index.cshtml.cs* 코드 숨김 파일을 살펴봅니다. [!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml.cs)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-109">Examine the *Pages/Movies/Index.cshtml.cs* code-behind file: [!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml.cs)]</span></span>

<span data-ttu-id="da3ee-110">Razor 페이지는 `PageModel`에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-110">Razor Pages are derived from `PageModel`.</span></span> <span data-ttu-id="da3ee-111">일반적으로 `PageModel` 파생 클래스를 `<PageName>Model`이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-111">By convention, the `PageModel`-derived class is called `<PageName>Model`.</span></span> <span data-ttu-id="da3ee-112">생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 `MovieContext`를 페이지에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-112">The constructor uses [dependency injection](xref:fundamentals/dependency-injection) to add the `MovieContext` to the page.</span></span> <span data-ttu-id="da3ee-113">모든 스캐폴드된 페이지가 이 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-113">All the scaffolded pages follow this pattern.</span></span>

<span data-ttu-id="da3ee-114">페이지에 대한 요청을 만들면 `OnGetAsync` 메서드가 Razor 페이지에 동영상 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-114">When a request is made for the page, the `OnGetAsync` method returns a list of movies to the Razor Page.</span></span> <span data-ttu-id="da3ee-115">페이지 상태를 초기화하기 위해 `OnGetAsync` 또는 `OnGet`이 Razor 페이지에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-115">`OnGetAsync` or `OnGet` is called on a Razor Page to initialize the state for the page.</span></span> <span data-ttu-id="da3ee-116">이 경우 `OnGetAsync`는 표시할 동영상 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-116">In this case, `OnGetAsync` gets a list of movies to display.</span></span>

<span data-ttu-id="da3ee-117">*Pages/Movies/Index.cshtml* Razor 페이지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-117">Examine the *Pages/Movies/Index.cshtml* Razor Page:</span></span>

<span data-ttu-id="da3ee-118">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-118">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml)]</span></span>

<span data-ttu-id="da3ee-119">Razor는 HTML에서 C# 또는 Razor 관련 태그로 전환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-119">Razor can transition from HTML into C# or into Razor-specific markup.</span></span> <span data-ttu-id="da3ee-120">`@` 기호 뒤에 [Razor 예약 키워드](xref:mvc/views/razor#razor-reserved-keywords)가 사용되면 이 기호는 Razor 관련 태그로 전환됩니다. 이외의 경우에는 C#으로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-120">When an `@` symbol is followed by a [Razor reserved keyword](xref:mvc/views/razor#razor-reserved-keywords), it transitions into Razor-specific markup, otherwise it transitions into C#.</span></span>

<span data-ttu-id="da3ee-121">`@page` Razor 지시문은 파일을 MVC 작업으로 만들고, 이것은 요청을 처리할 수 있음을 의미합니다.&mdash;</span><span class="sxs-lookup"><span data-stu-id="da3ee-121">The `@page` Razor directive makes the file into an MVC action &mdash; which means that it can handle requests.</span></span> <span data-ttu-id="da3ee-122">`@page`는 페이지의 첫 번째 Razor 지시문이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-122">`@page` must be the first Razor directive on a page.</span></span> <span data-ttu-id="da3ee-123">`@page`는 Razor 관련 태그로 전환되는 하나의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-123">`@page` is an example of transitioning into Razor-specific markup.</span></span> <span data-ttu-id="da3ee-124">자세한 내용은 [Razor 구문](xref:mvc/views/razor#razor-syntax)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da3ee-124">See [Razor syntax](xref:mvc/views/razor#razor-syntax) for more information.</span></span>

<span data-ttu-id="da3ee-125">다음 HTML 도우미에서 사용되는 람다 식을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-125">Examine the lambda expression used in the following HTML Helper:</span></span>

`@Html.DisplayNameFor(model => model.Movie[0].Title))`

<span data-ttu-id="da3ee-126">`DisplayNameFor` HTML 도우미는 람다 식에서 참조되는 `Title` 속성을 검사하여 표시 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-126">The `DisplayNameFor` HTML Helper inspects the `Title` property referenced in the lambda expression to determine the display name.</span></span> <span data-ttu-id="da3ee-127">람다 식은 계산되는 것이 아니라 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-127">The lambda expression is inspected rather than evaluated.</span></span> <span data-ttu-id="da3ee-128">즉, `model`, `model.Movies` 또는 `model.Movies[0]`가 `null`이거나 비어 있을 경우 액세스 위반이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-128">That means there is no access violation when `model`, `model.Movies`, or `model.Movies[0]` are `null` or empty.</span></span> <span data-ttu-id="da3ee-129">람다 식이 계산될 경우(예: `@Html.DisplayFor(modelItem => item.Title)` 사용) 모델의 속성 값이 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-129">When the lambda expression is evaluated (for example, with `@Html.DisplayFor(modelItem => item.Title)`), the model's property values are evaluated.</span></span>

<a name="md"></a>
### <a name="the-model-directive"></a><span data-ttu-id="da3ee-130">@model 지시문</span><span class="sxs-lookup"><span data-stu-id="da3ee-130">The @model directive</span></span>

<span data-ttu-id="da3ee-131">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml?range=1-2&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-131">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml?range=1-2&highlight=2)]</span></span>

<span data-ttu-id="da3ee-132">`@model` 지시문은 Razor 페이지에 전달되는 모델 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-132">The `@model` directive specifies the type of the model passed to the Razor Page.</span></span> <span data-ttu-id="da3ee-133">이전 예제에서 `@model` 줄은 Razor 페이지에서 `PageModel` 파생 클래스를 사용할 수 있게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-133">In the preceding example, the `@model` line makes the `PageModel`-derived class available to the Razor Page.</span></span> <span data-ttu-id="da3ee-134">모델은 페이지에서 `@Html.DisplayNameFor` 및 `@Html.DisplayName` [HTML 도우미](https://docs.microsoft.com/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-134">The model is used in the `@Html.DisplayNameFor` and `@Html.DisplayName` [HTML Helpers](https://docs.microsoft.com/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers) on the page.</span></span>

<span data-ttu-id="da3ee-135"><!-- why don't xref links work?
[HTML Helpers 2](xref:aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs)
-->

<a name="vd">
</a>
### ViewData 및 레이아웃</span><span class="sxs-lookup"><span data-stu-id="da3ee-135"><!-- why don't xref links work?
[HTML Helpers 2](xref:aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs)
-->

<a name="vd"></a>
### ViewData and layout</span></span>

<span data-ttu-id="da3ee-136">다음 코드를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="da3ee-136">Consider the following code:</span></span>

<span data-ttu-id="da3ee-137">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml?range=1-6&highlight=4-)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-137">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Index.cshtml?range=1-6&highlight=4-)]</span></span>

<span data-ttu-id="da3ee-138">이전 강조 표시된 코드는 C#으로 전환되는 Razor의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-138">The preceding highligted code is an example of Razor transitioning into C#.</span></span> <span data-ttu-id="da3ee-139">`{` 및 `}` 문자로 C# 코드 블록을 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-139">The `{` and `}` characters enclose a block of C# code.</span></span>

<span data-ttu-id="da3ee-140">`Controller` 기본 클래스에는 뷰에 전달할 데이터를 추가하는 데 사용될 수 있는 `ViewData` 사전 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-140">The `Controller` base class has a `ViewData` dictionary property that can be used to add data that you want to pass to a View.</span></span> <span data-ttu-id="da3ee-141">키/쌍 패턴을 사용하여 개체를 `ViewData` 사전에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-141">You add objects into the `ViewData` dictionary using a key/value pattern.</span></span> <span data-ttu-id="da3ee-142">이전 샘플에서는 “Title” 속성이 `ViewData` 사전에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-142">In the preceding sample, the "Title" property is added to the `ViewData` dictionary.</span></span> <span data-ttu-id="da3ee-143">“Title” 속성은 *Pages/_Layout.cshtml* 파일에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-143">The "Title" property is used in the *Pages/_Layout.cshtml* file.</span></span> <span data-ttu-id="da3ee-144">다음 태그는 *Pages/_Layout.cshtml* 파일의 처음 몇 줄을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-144">The following markup shows the first few lines of the *Pages/_Layout.cshtml* file.</span></span>

<span data-ttu-id="da3ee-145">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/NU/_Layout1.cshtml?highlight=6-)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-145">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/NU/_Layout1.cshtml?highlight=6-)]</span></span>

<span data-ttu-id="da3ee-146">`@*Markup removed for brevity.*@` 줄은 Razor 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-146">The line `@*Markup removed for brevity.*@` is a Razor comment.</span></span> <span data-ttu-id="da3ee-147">HTML 주석(`<!-- -->`)과 달리 Razor 주석은 클라이언트에 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-147">Unlike HTML comments (`<!-- -->`), Razor comments are not sent to the client.</span></span>

<span data-ttu-id="da3ee-148">앱을 실행하고 프로젝트의 링크를 테스트합니다(**홈**, **정보**, **연락처**, **만들기**, **편집** 및 **삭제**).</span><span class="sxs-lookup"><span data-stu-id="da3ee-148">Run the app and test the links in the project (**Home**, **About**, **Contact**, **Create**, **Edit**, and **Delete**).</span></span> <span data-ttu-id="da3ee-149">각 페이지에서 설정되는 제목은 브라우저 탭에서 확인할 수 있습니다. 페이지의 책갈피를 지정하면 제목이 책갈피에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-149">Each page sets the title, which you can see in the browser tab. When you bookmark a page, the title is used for the bookmark.</span></span> <span data-ttu-id="da3ee-150">*Pages/Index.cshtml* 및 *Pages/Movies/Index.cshtml*의 제목은 현재 동일하지만 다른 값으로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-150">*Pages/Index.cshtml* and *Pages/Movies/Index.cshtml* currently have the same title, but you can modify them to have different values.</span></span>

<span data-ttu-id="da3ee-151">`Layout` 속성은 *Pages/_ViewStart.cshtml* 파일에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-151">The `Layout` property is set in the *Pages/_ViewStart.cshtml* file:</span></span>

<span data-ttu-id="da3ee-152">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-152">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]</span></span>

<span data-ttu-id="da3ee-153">이전 태그는 *Pages* 폴더 아래에 있는 모든 Razor 파일에 대한 레이아웃 파일을 *Pages/_Layout.cshtml*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-153">The preceding markup sets the layout file to *Pages/_Layout.cshtml* for all Razor files under the *Pages* folder.</span></span> <span data-ttu-id="da3ee-154">자세한 내용은 [레이아웃](xref:mvc/razor-pages/index#layout)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da3ee-154">See [Layout](xref:mvc/razor-pages/index#layout) for more information.</span></span>

### <a name="update-the-layout"></a><span data-ttu-id="da3ee-155">레이아웃 업데이트</span><span class="sxs-lookup"><span data-stu-id="da3ee-155">Update the layout</span></span>

<span data-ttu-id="da3ee-156">*Pages/_Layout.cshtml* 파일에서 `<title>` 요소를 변경하여 더 짧은 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-156">Change the `<title>` element in the *Pages/_Layout.cshtml* file to use a shorter string.</span></span>

<span data-ttu-id="da3ee-157">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml?range=1-6&highlight=6-)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-157">[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml?range=1-6&highlight=6-)]</span></span>

<span data-ttu-id="da3ee-158">*Pages/_Layout.cshtml* 파일에서 다음 앵커 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-158">Find the following anchor element in the *Pages/_Layout.cshtml* file.</span></span>

```cshtml
<a asp-page="/Index" class="navbar-brand">RazorPagesMovie</a>
```
<span data-ttu-id="da3ee-159">이전 요소를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-159">Replace the preceding element with the following markup.</span></span>

```cshtml
<a asp-page="/Movies/Index" class="navbar-brand">RpMovie</a>
```

<span data-ttu-id="da3ee-160">이전 앵커 요소는 [태그 도우미](xref:mvc/views/tag-helpers/intro)입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-160">The preceding anchor element is a [Tag Helper](xref:mvc/views/tag-helpers/intro).</span></span> <span data-ttu-id="da3ee-161">이 경우에는 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/AnchorTagHelper)입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-161">In this case, it's the [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/AnchorTagHelper).</span></span> <span data-ttu-id="da3ee-162">`asp-page="/Movies/Index"` 태그 도우미 특성 및 값으로 `/Movies/Index` Razor 페이지의 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-162">The `asp-page="/Movies/Index"` Tag Helper attribute and value creates a link to the `/Movies/Index` Razor Page.</span></span>

<span data-ttu-id="da3ee-163">변경 내용을 저장하고 **RpMovie** 링크를 클릭하여 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-163">Save your changes, and test the app by clicking on the **RpMovie** link.</span></span> <span data-ttu-id="da3ee-164">GitHub에서 [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da3ee-164">See the [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_Layout.cshtml) file in GitHub.</span></span>

### <a name="the-create-code-behind-page"></a><span data-ttu-id="da3ee-165">만들기 코드 숨김 페이지</span><span class="sxs-lookup"><span data-stu-id="da3ee-165">The Create code-behind page</span></span>

<span data-ttu-id="da3ee-166">*Pages/Movies/Create.cshtml.cs* 코드 숨김 파일을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-166">Examine the *Pages/Movies/Create.cshtml.cs* code-behind file:</span></span>

<span data-ttu-id="da3ee-167">[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml.cs?name=snippetALL)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-167">[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml.cs?name=snippetALL)]</span></span>

<span data-ttu-id="da3ee-168">`OnGet` 메서드는 페이지에 필요한 상태를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-168">The `OnGet` method initializes any state needed for the page.</span></span> <span data-ttu-id="da3ee-169">만들기 페이지에는 초기화할 상태가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-169">The Create page doesn't have any state to initialize.</span></span> <span data-ttu-id="da3ee-170">`Page` 메서드는 *Create.cshtml* 페이지를 렌더링하는 `PageResult` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-170">The `Page` method creates a `PageResult` object that renders the *Create.cshtml* page.</span></span>

<span data-ttu-id="da3ee-171">`Movie` 속성은 `[BindProperty]` 특성을 사용하여 [모델 바인딩](xref:mvc/models/model-binding)을 옵트인(opt in)합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-171">The `Movie` property uses the `[BindProperty]` attribute to opt-in to [model binding](xref:mvc/models/model-binding).</span></span> <span data-ttu-id="da3ee-172">만들기 폼이 폼 값을 게시하면 ASP.NET Core 런타임이 게시된 값을 `Movie` 모델에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-172">When the Create form posts the form values, the ASP.NET Core runtime binds the posted values to the `Movie` model.</span></span>

<span data-ttu-id="da3ee-173">페이지에 폼 데이터가 게시되면 `OnPostAsync` 메서드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-173">The `OnPostAsync` method is run when the page posts form data:</span></span>

<span data-ttu-id="da3ee-174">[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml.cs?name=snippetPost)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-174">[!code-csharp[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml.cs?name=snippetPost)]</span></span>

<span data-ttu-id="da3ee-175">모델 오류가 있는 경우 폼과 게시된 모든 폼 데이터가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-175">If there are any model errors, the form is redisplayed, along with any form data posted.</span></span> <span data-ttu-id="da3ee-176">대부분의 모델 오류는 폼이 게시되기 전에 클라이언트 쪽에서 catch할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-176">Most model errors can be caught on the client-side before the form is posted.</span></span> <span data-ttu-id="da3ee-177">예를 들어 데이터로 변환될 수 없는 날짜 필드에 대한 값을 게시하는 모델 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-177">An example of a model error is posting a value for the date field that cannot be converted to a date.</span></span> <span data-ttu-id="da3ee-178">자습서의 뒷부분에서 클라이언트 쪽 유효성 검사 및 모델 유효성 검사를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-178">We'll talk more about client-side validation and model validation later in the tutorial.</span></span>

<span data-ttu-id="da3ee-179">모델 오류가 없는 경우 데이터가 저장되고 브라우저가 인덱스 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-179">If there are no model errors, the data is saved, and the browser is redirected to the Index page.</span></span>

### <a name="the-create-razor-page"></a><span data-ttu-id="da3ee-180">만들기 Razor 페이지</span><span class="sxs-lookup"><span data-stu-id="da3ee-180">The Create Razor Page</span></span>

<span data-ttu-id="da3ee-181">*Pages/Movies/Create.cshtml* Razor 페이지 파일을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-181">Examine the *Pages/Movies/Create.cshtml* Razor Page file:</span></span>

<span data-ttu-id="da3ee-182">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-182">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml)]</span></span>

<span data-ttu-id="da3ee-183">Visual Studio에서는 `<form method="post">` 태그를 태그 도우미에 사용되는 독특한 글꼴로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-183">Visual Studio displays the `<form method="post">` tag in a distinctive font used for Tag Helpers.</span></span> <span data-ttu-id="da3ee-184">`<form method="post">` 요소는 [폼 태그 도우미](xref:mvc/views/working-with-forms#the-form-tag-helper)입니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-184">The `<form method="post">` element is a [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="da3ee-185">폼 태그 도우미에는 [위조 방지 토큰](xref:security/anti-request-forgery)이 자동으로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-185">The Form Tag Helper automatically includes an [antiforgery token](xref:security/anti-request-forgery).</span></span>

![Create.cshtml 페이지의 VS17 뷰](page/_static/th.png)

<span data-ttu-id="da3ee-187">스캐폴딩 엔진은 다음과 비슷한 모델에서 각 필드(ID 제외)에 대한 Razor 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-187">The scaffolding engine creates Razor markup for each field in the model (except the ID) similar to the following:</span></span>

<span data-ttu-id="da3ee-188">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml?range=15-20)]</span><span class="sxs-lookup"><span data-stu-id="da3ee-188">[!code-cshtml[Main](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movie/Create.cshtml?range=15-20)]</span></span>

<span data-ttu-id="da3ee-189">[유효성 검사 태그 도우미](xref:mvc/views/working-with-forms#the-validation-tag-helpers)(`<div asp-validation-summary` 및 ` <span asp-validation-for`)는 유효성 검사 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-189">The [Validation Tag Helpers](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` and ` <span asp-validation-for`) display validation errors.</span></span> <span data-ttu-id="da3ee-190">유효성 검사는 이 시리즈의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-190">Validation is covered in more detail later in this series.</span></span>

<span data-ttu-id="da3ee-191">[레이블 태그 도우미](xref:mvc/views/working-with-forms#the-label-tag-helper)(`<label asp-for="Movie.Title" class="control-label"></label>`)는 `Title` 속성에 대한 레이블 캡션 및 `for` 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-191">The [Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) generates the label caption and `for` attribute for the `Title` property.</span></span>

<span data-ttu-id="da3ee-192">[입력 태그 도우미](xref:mvc/views/working-with-forms)(`<input asp-for="Movie.Title" class="form-control" />`)는 [DataAnnotations](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 특성을 사용하고 클라이언트 쪽의 jQuery 유효성 검사에 필요한 HTML 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-192">The [Input Tag Helper](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) uses the [DataAnnotations](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span>

<span data-ttu-id="da3ee-193">다음 자습서에서는 SQL Server LocalDB 및 데이터베이스 시딩에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da3ee-193">The next tutorial explains SQL Server LocalDB and seeding the database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="da3ee-194">[이전: 모델 추가](xref:tutorials/razor-pages/modelz)
[다음: SQL Server LocalDB](xref:tutorials/razor-pages/sql)</span><span class="sxs-lookup"><span data-stu-id="da3ee-194">[Previous: Adding a model](xref:tutorials/razor-pages/modelz)
[Next: SQL Server LocalDB](xref:tutorials/razor-pages/sql)</span></span>