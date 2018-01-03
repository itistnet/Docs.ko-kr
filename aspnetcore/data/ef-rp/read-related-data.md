---
title: "EF 코어-를 사용 하 여 razor 페이지 관련된 데이터 읽기-8 6"
author: rick-anderson
description: "이 자습서에서는 읽기 및 관련된 데이터-Entity Framework 탐색 속성에 로드 하는 데이터를 표시 합니다."
keywords: "ASP.NET Core, Entity Framework Core 관련된 데이터를 조인"
ms.author: riande
manager: wpickett
ms.date: 11/05/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/read-related-data
ms.openlocfilehash: ba9b17ecdcb605d39117d03230b1db37e8e4d0dd
ms.sourcegitcommit: 05e798c9bac7b9e9983599afb227ef393905d023
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="reading-related-data---ef-core-with-razor-pages-6-of-8"></a><span data-ttu-id="fbea8-104">관련 데이터-EF 코어 Razor 페이지 (8 6)에 읽기</span><span class="sxs-lookup"><span data-stu-id="fbea8-104">Reading related data - EF Core with Razor Pages (6 of 8)</span></span>

<span data-ttu-id="fbea8-105">여 [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fbea8-105">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="fbea8-106">이 자습서에서는 관련된 데이터를 읽고 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-106">In this tutorial, related data is read and displayed.</span></span> <span data-ttu-id="fbea8-107">관련된 데이터는 데이터 탐색 속성에 로드 EF 코어입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-107">Related data is data that EF Core loads into navigation properties.</span></span>

<span data-ttu-id="fbea8-108">문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-108">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related).</span></span>

<span data-ttu-id="fbea8-109">다음 그림은이 자습서에 대 한 완료 된 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-109">The following illustrations show the completed pages for this tutorial:</span></span>

![Courses 인덱스 페이지](read-related-data/_static/courses-index.png)

![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a><span data-ttu-id="fbea8-112">관련된 데이터를 신속 하 게, 명시적, 및 지연 로드</span><span class="sxs-lookup"><span data-stu-id="fbea8-112">Eager, explicit, and lazy Loading of related data</span></span>

<span data-ttu-id="fbea8-113">여러 가지 방법으로 EF 코어가 엔터티의 탐색 속성에 관련된 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-113">There are several ways that EF Core can load related data into the navigation properties of an entity:</span></span>

* <span data-ttu-id="fbea8-114">[즉시 로드](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-114">[Eager loading](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading).</span></span> <span data-ttu-id="fbea8-115">즉시 로드 때 한 가지 유형의 엔터티에 대 한 쿼리도 관련된 엔터티를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-115">Eager loading is when a query for one type of entity also loads related entities.</span></span> <span data-ttu-id="fbea8-116">엔터티를 읽을 때 관련된 데이터 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-116">When the entity is read, its related data is retrieved.</span></span> <span data-ttu-id="fbea8-117">일반적으로 필요한 데이터를 모두 검색 하는 단일 조인 쿼리에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-117">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="fbea8-118">EF 코어는 일부 유형의 즉시 로드에 대 한 여러 개의 쿼리를 발행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-118">EF Core will issue multiple queries for some types of eager loading.</span></span> <span data-ttu-id="fbea8-119">여러 쿼리를 실행 EF6에 일부 쿼리의 경우 보다 효율적일 수 있었던 다음 단일 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-119">Issuing multiple queries can be more efficient than was the case for some queries in EF6 where there was a single query.</span></span> <span data-ttu-id="fbea8-120">즉시 로드로 지정 된 `Include` 및 `ThenInclude` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fbea8-120">Eager loading is specified with the `Include` and `ThenInclude` methods.</span></span>

 ![즉시 로드 예제](read-related-data/_static/eager-loading.png)
 
 <span data-ttu-id="fbea8-122">즉시 로드 컬렉션 nvavigation 포함 되는 경우 여러 개의 쿼리를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-122">Eager loading sends multiple queries when a collection nvavigation is included:</span></span>

 * <span data-ttu-id="fbea8-123">주 쿼리에 대 한 쿼리</span><span class="sxs-lookup"><span data-stu-id="fbea8-123">One query for the main query</span></span> 
 * <span data-ttu-id="fbea8-124">"가장자리" 부하 트리의 각 컬렉션에 대해 하나의 쿼리만 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-124">One query for each collection "edge" in the load tree.</span></span>

* <span data-ttu-id="fbea8-125">쿼리 구분 `Load`: 쿼리를 별도 데이터를 검색할 수 있습니다 및 EF 코어 "픽스" 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-125">Separate queries with `Load`: The data can be retrieved in separate queries, and EF Core "fixes up" the navigation properties.</span></span> <span data-ttu-id="fbea8-126">"를 수정" 수단 EF 코어 탐색 속성을 자동으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-126">"fixes up" means that EF Core automatically populates the navigation properties.</span></span> <span data-ttu-id="fbea8-127">쿼리 구분 `Load` 즉시 로드 보다 로드 explict 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-127">Separate queries with `Load` is more like explict loading than eager loading.</span></span>

 ![별도 쿼리 예제](read-related-data/_static/separate-queries.png)

 <span data-ttu-id="fbea8-129">참고: EF 코어 컨텍스트 인스턴스에 이전에 로드 된 다른 엔터티를 탐색 속성을 자동으로 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-129">Note: EF Core automatically fixes up navigation properties to any other entities that were previously loaded into the context instance.</span></span> <span data-ttu-id="fbea8-130">탐색 속성에 대 한 데이터가 있는 경우에 *하지* 경우 일부 속성 채울 수 있습니다 또는 이전에 로드 된 모든 관련된 엔터티가 명시적으로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-130">Even if the data for a navigation property is *not* explicitly included, the property may still be populated if some or all of the related entities were previously loaded.</span></span>

* <span data-ttu-id="fbea8-131">[명시적 로드](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-131">[Explicit loading](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading).</span></span> <span data-ttu-id="fbea8-132">먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-132">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="fbea8-133">코드를 작성 하는 필요할 때 관련된 데이터를 검색 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-133">Code must be written to retrieve the related data when it's needed.</span></span> <span data-ttu-id="fbea8-134">명시적 별도 쿼리 로드 DB에 전송 하는 여러 쿼리에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-134">Explicit loading with separate queries results in multiple queries sent to the DB.</span></span> <span data-ttu-id="fbea8-135">명시적 로드 된 코드를 로드 탐색 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-135">With explicit loading, the code specifies the navigation properties to be loaded.</span></span> <span data-ttu-id="fbea8-136">사용 하 여는 `Load` 명시적 로딩 작업을 수행 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="fbea8-136">Use the `Load` method to do explicit loading.</span></span> <span data-ttu-id="fbea8-137">예:</span><span class="sxs-lookup"><span data-stu-id="fbea8-137">For example:</span></span>

 ![명시적 로드 예제](read-related-data/_static/explicit-loading.png)

* <span data-ttu-id="fbea8-139">[지연 로드](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-139">[Lazy loading](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading).</span></span> <span data-ttu-id="fbea8-140">[EF 코어 현재 지연 로딩을 지원 하지 않는](https://github.com/aspnet/EntityFrameworkCore/issues/3797)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-140">[EF Core does not currently support lazy loading](https://github.com/aspnet/EntityFrameworkCore/issues/3797).</span></span> <span data-ttu-id="fbea8-141">먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-141">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="fbea8-142">탐색 속성에 액세스 하는 처음으로 해당 탐색 속성에 필요한 데이터가 자동으로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-142">The first time a navigation property is accessed, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="fbea8-143">쿼리 될 때마다 처음에 대 한 탐색 속성에 액세스 하 여 DB에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-143">A query is sent to the DB each time a navigation property is accessed for the first time.</span></span>

* <span data-ttu-id="fbea8-144">`Select` 연산자 필요한 관련된 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-144">The `Select` operator loads only the related data needed.</span></span>

## <a name="create-a-courses-page-that-displays-department-name"></a><span data-ttu-id="fbea8-145">부서 이름을 표시 하는 과정 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="fbea8-145">Create a Courses page that displays department name</span></span>

<span data-ttu-id="fbea8-146">포함 된 탐색 속성을 포함 하는 과정 엔터티는 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-146">The Course entity includes a navigation property that contains the `Department` entity.</span></span> <span data-ttu-id="fbea8-147">`Department` 엔터티 과정에 할당 된 부서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-147">The `Department` entity contains the department that the course is assigned to.</span></span>

<span data-ttu-id="fbea8-148">에 표시 하려면 할당 된 부서 이름을 과정의 목록:</span><span class="sxs-lookup"><span data-stu-id="fbea8-148">To display the name of the assigned department in a list of courses:</span></span>

* <span data-ttu-id="fbea8-149">가져오기는 `Name` 에서 속성의 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-149">Get the `Name` property from the `Department` entity.</span></span>
* <span data-ttu-id="fbea8-150">`Department` 에서 제공 되는 엔터티는 `Course.Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-150">The `Department` entity comes from the `Course.Department` navigation property.</span></span>

![ourse 합니다. 부서](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a><span data-ttu-id="fbea8-152">스 캐 폴드 과정 모델</span><span class="sxs-lookup"><span data-stu-id="fbea8-152">Scaffold the Course model</span></span>

* <span data-ttu-id="fbea8-153">Visual Studio를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-153">Exit Visual Studio.</span></span>
* <span data-ttu-id="fbea8-154">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-154">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="fbea8-155">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-155">Run the following command:</span></span>

 ```console
dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
 ```

<span data-ttu-id="fbea8-156">위의 명령은 스 캐 폴드 된 `Course` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-156">The preceding command scaffolds the `Course` model.</span></span> <span data-ttu-id="fbea8-157">Visual Studio에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-157">Open the project in Visual Studio.</span></span>

<span data-ttu-id="fbea8-158">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-158">Build the project.</span></span> <span data-ttu-id="fbea8-159">빌드에서는 다음과 같은 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-159">The build generates errors like the following:</span></span>

`1>Pages/Courses/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Course' and no extension method 'Course' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 <span data-ttu-id="fbea8-160">전역으로 변경 `_context.Course` 를 `_context.Courses` (즉, "s"에 추가 `Course`).</span><span class="sxs-lookup"><span data-stu-id="fbea8-160">Globally change `_context.Course` to `_context.Courses` (that is, add an "s" to `Course`).</span></span> <span data-ttu-id="fbea8-161">7 번 발견 되 고 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-161">7 occurrences are found and updated.</span></span>

<span data-ttu-id="fbea8-162">열기 *Pages/Courses/Index.cshtml.cs* 검사는 `OnGetAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fbea8-162">Open *Pages/Courses/Index.cshtml.cs* and examine the `OnGetAsync` method.</span></span> <span data-ttu-id="fbea8-163">스 캐 폴딩 엔진 지정에 대 한 즉시 로드는 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-163">The scaffolding engine specified eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="fbea8-164">`Include` 메서드 즉시 로드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-164">The `Include` method specifies eager loading.</span></span>

<span data-ttu-id="fbea8-165">응용 프로그램을 실행 하 고 선택 된 **Courses** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-165">Run the app and select the **Courses** link.</span></span> <span data-ttu-id="fbea8-166">Department 열에 표시 됩니다는 `DepartmentID`, 유용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-166">The department column displays the `DepartmentID`, which is not useful.</span></span>

<span data-ttu-id="fbea8-167">`OnGetAsync` 메서드를 다음 코드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-167">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

<span data-ttu-id="fbea8-168">앞의 코드를 추가 `AsNoTracking`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-168">The preceding code adds `AsNoTracking`.</span></span> <span data-ttu-id="fbea8-169">`AsNoTracking`반환 되는 엔터티 추적 되지 않으므로 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-169">`AsNoTracking` improves performance because the entities returned are not tracked.</span></span> <span data-ttu-id="fbea8-170">현재 컨텍스트에서 업데이트 되지 않기 때문에 엔터티를 추적 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-170">The entities are not tracked because they are not updated in the current context.</span></span>

<span data-ttu-id="fbea8-171">업데이트 *Views/Courses/Index.cshtml* 강조 표시 된 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-171">Update *Views/Courses/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

<span data-ttu-id="fbea8-172">스 캐 폴드 코드에 다음과 같은 변경은 적용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-172">The following changes have been made to the scaffolded code:</span></span>

* <span data-ttu-id="fbea8-173">인덱스에서 제목 Courses로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-173">Changed the heading from Index to Courses.</span></span>
* <span data-ttu-id="fbea8-174">추가 **번호** 보여 주는 열은 `CourseID` 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-174">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="fbea8-175">기본적으로 기본 키 이므로 일반적으로 최종 사용자에 게 의미가 스 캐 폴드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-175">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="fbea8-176">그러나이 경우 기본 키가 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-176">However, in this case the primary key is meaningful.</span></span>
* <span data-ttu-id="fbea8-177">변경 된 **부서** 부서 이름을 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-177">Changed the **Department** column to display the department name.</span></span> <span data-ttu-id="fbea8-178">코드 표시는 `Name` 의 속성은 `Department` 에 로드 된 엔터티는 `Department` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="fbea8-178">The code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

<span data-ttu-id="fbea8-179">응용 프로그램을 실행 하 고 선택 된 **Courses** 부서 이름의 목록을 보려면 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-179">Run the app and select the **Courses** tab to see the list with department names.</span></span>

![Courses 인덱스 페이지](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a><span data-ttu-id="fbea8-181">관련 Select와 함께 데이터를 로드</span><span class="sxs-lookup"><span data-stu-id="fbea8-181">Loading related data with Select</span></span>

<span data-ttu-id="fbea8-182">`OnGetAsync` 메서드를 사용 하 여 관련된 데이터 로드는 `Include` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fbea8-182">The `OnGetAsync` method loads related data with the `Include` method:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="fbea8-183">`Select` 연산자 필요한 관련된 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-183">The `Select` operator loads only the related data needed.</span></span> <span data-ttu-id="fbea8-184">단일 항목에 대 한 같은 `Department.Name` 는 SQL INNER JOIN을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-184">For single items, like the `Department.Name` it uses a SQL INNER JOIN.</span></span> <span data-ttu-id="fbea8-185">컬렉션에 대 한 다른 데이터베이스 액세스를 사용 하 여 하지만 사라지면는 합니다.`Include`</span><span class="sxs-lookup"><span data-stu-id="fbea8-185">For collections it uses another database access, but so does the .`Include`</span></span> <span data-ttu-id="fbea8-186">컬렉션에 대 한 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-186">operator on collections.</span></span>

<span data-ttu-id="fbea8-187">다음 코드를 사용 하 여 관련된 데이터 로드는 `Select` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fbea8-187">The following code loads related data with the `Select` method:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

<span data-ttu-id="fbea8-188">`CourseViewModel`:</span><span class="sxs-lookup"><span data-stu-id="fbea8-188">The `CourseViewModel`:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

<span data-ttu-id="fbea8-189">참조 [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) 및 [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) 는 전체 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-189">See [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) and [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) for a complete example.</span></span>

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="fbea8-190">만들기 과정 및 등록을 보여 주는 강사 페이지</span><span class="sxs-lookup"><span data-stu-id="fbea8-190">Create an Instructors page that shows Courses and Enrollments</span></span>

<span data-ttu-id="fbea8-191">이 섹션에서는 강사 페이지가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-191">In this section, the Instructors page is created.</span></span>

<a name="IP"></a>
<span data-ttu-id="fbea8-192">![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)</span><span class="sxs-lookup"><span data-stu-id="fbea8-192">![Instructors Index page](read-related-data/_static/instructors-index.png)</span></span>

<span data-ttu-id="fbea8-193">이 페이지를 읽고 다음과 같이 관련된 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-193">This page reads and displays related data in the following ways:</span></span>

* <span data-ttu-id="fbea8-194">강사 목록은의 관련된 데이터 표시는 `OfficeAssignment` 엔터티 (위 그림에서 사무실).</span><span class="sxs-lookup"><span data-stu-id="fbea8-194">The list of instructors displays related data from the `OfficeAssignment` entity (Office in the preceding image).</span></span> <span data-ttu-id="fbea8-195">`Instructor` 및 `OfficeAssignment` 엔터티는 0 또는 1을 한 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-195">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="fbea8-196">즉시 로드에 사용 되는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-196">Eager loading is used for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="fbea8-197">즉시 로드는 관련된 데이터를 표시 해야 하는 경우 일반적으로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-197">Eager loading is typically more efficient when the related data needs to be displayed.</span></span> <span data-ttu-id="fbea8-198">이 경우 사무실 할당에서 강사에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-198">In this case, office assignments for the instructors are displayed.</span></span>
* <span data-ttu-id="fbea8-199">사용자가 관련 강사 (위 그림에서 Harui)를 선택 하는 경우 `Course` 엔터티 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-199">When the user selects an instructor (Harui in the preceding image), related `Course` entities are displayed.</span></span> <span data-ttu-id="fbea8-200">`Instructor` 및 `Course` 엔터티가 서로 다 대 다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-200">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="fbea8-201">에 대 한 로드 eager는 `Course` 엔터티 및 관련 `Department` 엔터티 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-201">Eager loading for the `Course` entities and their related `Department` entities is used.</span></span> <span data-ttu-id="fbea8-202">이 경우 선택한 강사에 대 한 과정만 더 필요 하므로 별개의 쿼리와 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-202">In this case, separate queries might be more efficient because only courses for the selected instructor are needed.</span></span> <span data-ttu-id="fbea8-203">이 예제에는 탐색 속성에 있는 엔터티에서 탐색 속성에 대 한 즉시 로드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-203">This example shows how to use eager loading for navigation properties in entities that are in navigation properties.</span></span>
* <span data-ttu-id="fbea8-204">데이터와 관련 된 사용자가 과정 (위 그림에서 화학)를 선택 하는 경우는 `Enrollments` 엔터티가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-204">When the user selects a course (Chemistry in the preceding image), related data from the `Enrollments` entity is displayed.</span></span> <span data-ttu-id="fbea8-205">위 그림에서는 학생 이름 및 등급 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-205">In the preceding image, student name and grade are displayed.</span></span> <span data-ttu-id="fbea8-206">`Course` 및 `Enrollment` 엔터티가 서로 일 대 다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-206">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="fbea8-207">강사 인덱스 보기에 대 한 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="fbea8-207">Create a view model for the Instructor Index view</span></span>

<span data-ttu-id="fbea8-208">강사 페이지는 서로 다른 세 테이블에서 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-208">The instructors page shows data from three different tables.</span></span> <span data-ttu-id="fbea8-209">뷰 모델 3 개의 테이블을 나타내는 세 개의 엔터티가 포함 된 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-209">A view model is created that includes the three entities representing the three tables.</span></span>

<span data-ttu-id="fbea8-210">에 *SchoolViewModels* 폴더를 만들 *InstructorIndexData.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-210">In the *SchoolViewModels* folder, create *InstructorIndexData.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a><span data-ttu-id="fbea8-211">스 캐 폴드 강사 모델</span><span class="sxs-lookup"><span data-stu-id="fbea8-211">Scaffold the Instructor model</span></span>

* <span data-ttu-id="fbea8-212">Visual Studio를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-212">Exit Visual Studio.</span></span>
* <span data-ttu-id="fbea8-213">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-213">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="fbea8-214">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-214">Run the following command:</span></span>

 ```console
dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
 ```

<span data-ttu-id="fbea8-215">위의 명령은 스 캐 폴드 된 `Instructor` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-215">The preceding command scaffolds the `Instructor` model.</span></span> <span data-ttu-id="fbea8-216">Visual Studio에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-216">Open the project in Visual Studio.</span></span>

<span data-ttu-id="fbea8-217">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-217">Build the project.</span></span> <span data-ttu-id="fbea8-218">빌드 오류를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-218">The build generates errors.</span></span>

<span data-ttu-id="fbea8-219">전역으로 변경 `_context.Instructor` 를 `_context.Instructors` (즉, "s"에 추가 `Instructor`).</span><span class="sxs-lookup"><span data-stu-id="fbea8-219">Globally change `_context.Instructor` to `_context.Instructors` (that is, add an "s" to `Instructor`).</span></span> <span data-ttu-id="fbea8-220">7 번 발견 되 고 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-220">7 occurrences are found and updated.</span></span>

<span data-ttu-id="fbea8-221">응용 프로그램을 실행 하 고 강사 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-221">Run the app and navigate to the instructors page.</span></span>

<span data-ttu-id="fbea8-222">대체 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-222">Replace *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,20-)]

<span data-ttu-id="fbea8-223">`OnGetAsync` 메서드 선택한 강사의 ID에 대 한 선택적 경로 데이터를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-223">The `OnGetAsync` method accepts optional route data for the ID of the selected instructor.</span></span>

<span data-ttu-id="fbea8-224">쿼리를 검사는 *Pages/Instructors/Index.cshtml* 페이지:</span><span class="sxs-lookup"><span data-stu-id="fbea8-224">Examine the query on the *Pages/Instructors/Index.cshtml* page:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="fbea8-225">에 쿼리는 두 개의 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-225">The query has two includes:</span></span>

* <span data-ttu-id="fbea8-226">`OfficeAssignment`:에 표시 되는 [강사 보기](#IP)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-226">`OfficeAssignment`: Displayed in the [instructors view](#IP).</span></span>
* <span data-ttu-id="fbea8-227">`CourseAssignments`:를 알게 과목에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-227">`CourseAssignments`: Which brings in the courses taught.</span></span>


### <a name="update-the-instructors-index-page"></a><span data-ttu-id="fbea8-228">강사 인덱스 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-228">Update the instructors Index page</span></span>

<span data-ttu-id="fbea8-229">업데이트 *Pages/Instructors/Index.cshtml* 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-229">Update *Pages/Instructors/Index.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

<span data-ttu-id="fbea8-230">위의 태그에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-230">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="fbea8-231">업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int?}"`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-231">Updates the `page` directive from `@page` to `@page "{id:int?}"`.</span></span> <span data-ttu-id="fbea8-232">`"{id:int?}"`경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-232">`"{id:int?}"` is a route template.</span></span> <span data-ttu-id="fbea8-233">경로 템플릿 경로 데이터를 URL에 쿼리 문자열을 정수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-233">The route template changes integer query strings in the URL to route data.</span></span> <span data-ttu-id="fbea8-234">예를 들어,를 클릭 하 고 **선택** 강사 다음과 같은 URL을 생성 하는 page 지시문에 대 한 링크:</span><span class="sxs-lookup"><span data-stu-id="fbea8-234">For example, clicking on the **Select** link for an instructor when the page directive produces a URL like the following:</span></span>

    `http://localhost:1234/Instructors?id=2`

    <span data-ttu-id="fbea8-235">Page 지시문 경우 `@page "{id:int?}"`, 이전 URL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-235">When the page directive is `@page "{id:int?}"`, the previous URL is:</span></span>

    `http://localhost:1234/Instructors/2`

* <span data-ttu-id="fbea8-236">페이지 제목은 **강사**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-236">Page title is **Instructors**.</span></span>
* <span data-ttu-id="fbea8-237">추가 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` null입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-237">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="fbea8-238">0 또는 1을 한 관계 이기 때문에 있을 수 있습니다 하지 관련된 OfficeAssignment 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-238">Because this is a one-to-zero-or-one relationship, there might not be a related OfficeAssignment entity.</span></span>

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* <span data-ttu-id="fbea8-239">추가 **Courses** 과정을 표시 하는 열에서 각 강사 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-239">Added a **Courses** column that displays courses taught by each instructor.</span></span> <span data-ttu-id="fbea8-240">참조 [명시적 줄 전환을 `@:` ](xref:mvc/views/razor#explicit-line-transition-with-) 이 razor 구문에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-240">See [Explicit Line Transition with `@:`](xref:mvc/views/razor#explicit-line-transition-with-) for more about this razor syntax.</span></span>

* <span data-ttu-id="fbea8-241">동적으로 추가 하는 추가 된 코드 `class="success"` 에 `tr` 선택한 강사의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-241">Added code that dynamically adds `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="fbea8-242">부트스트랩 클래스를 사용 하 여 선택된 된 행에 대 한 배경색을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-242">This sets a background color for the selected row using a Bootstrap class.</span></span>

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* <span data-ttu-id="fbea8-243">레이블이 지정 된 새 하이퍼링크 추가 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-243">Added a new hyperlink labeled **Select**.</span></span> <span data-ttu-id="fbea8-244">이 링크를 선택한 강의 ID 보냅니다는 `Index` 메서드 배경색을 가져오거나 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-244">This link sends the selected instructor's ID to the `Index` method and sets a background color.</span></span>

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

<span data-ttu-id="fbea8-245">응용 프로그램을 실행 하 고 선택 된 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` (사무실)에서 관련 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-245">Run the app and select the **Instructors** tab. The page displays the `Location` (office) from the related `OfficeAssignment` entity.</span></span> <span data-ttu-id="fbea8-246">경우 OfficeAssignment'는 null, 빈 테이블 셀 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-246">If OfficeAssignment\` is null, an empty table cell is displayed.</span></span>

![강사 인덱스 페이지에는 아무 선택](read-related-data/_static/instructors-index-no-selection.png)

<span data-ttu-id="fbea8-248">클릭는 **선택** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-248">Click on the **Select** link.</span></span> <span data-ttu-id="fbea8-249">행 스타일 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-249">The row style changes.</span></span>

### <a name="add-courses-taught-by-selected-instructor"></a><span data-ttu-id="fbea8-250">선택한 강사 여 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="fbea8-250">Add courses taught by selected instructor</span></span>

<span data-ttu-id="fbea8-251">업데이트는 `OnGetAsync` 메서드에서 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-251">Update the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-)]

<span data-ttu-id="fbea8-252">업데이트 된 쿼리를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-252">Examine the updated query:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

<span data-ttu-id="fbea8-253">추가 하는 앞의 쿼리는 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-253">The preceding query adds the `Department` entities.</span></span>

<span data-ttu-id="fbea8-254">다음 코드를 실행 하는 강사가 선택 된 경우 (`id != null`).</span><span class="sxs-lookup"><span data-stu-id="fbea8-254">The following code executes when an instructor is selected (`id != null`).</span></span> <span data-ttu-id="fbea8-255">선택한 강사 강사 보기 모델에 있는 목록에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-255">The selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="fbea8-256">뷰 모델 `Courses` 속성으로 로드 되는 `Course` 해당 강사에서 엔터티에 `CourseAssignments` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-256">The view model's `Courses` property is loaded with the `Course` entities from that instructor's `CourseAssignments` navigation property.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

<span data-ttu-id="fbea8-257">`Where` 메서드 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-257">The `Where` method returns a collection.</span></span> <span data-ttu-id="fbea8-258">앞에서 `Where` 메서드를 하나만 `Instructor` 엔터티가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-258">In the preceding `Where` method, only a single `Instructor` entity is returned.</span></span> <span data-ttu-id="fbea8-259">`Single` 메서드를 하나의 컬렉션 변환 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-259">The `Single` method converts the collection into a single `Instructor` entity.</span></span> <span data-ttu-id="fbea8-260">`Instructor` 에 대 한 액세스를 제공 하는 엔터티는 `CourseAssignments` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-260">The `Instructor` entity provides access to the `CourseAssignments` property.</span></span> <span data-ttu-id="fbea8-261">`CourseAssignments`관련 된 항목에 대 한 액세스를 제공 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-261">`CourseAssignments` provides access to the related `Course` entities.</span></span>

![강사-Courses m:M](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="fbea8-263">`Single` 메서드는 컬렉션의 항목을 하나만 때 컬렉션에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-263">The `Single` method is used on a collection when the collection has only one item.</span></span> <span data-ttu-id="fbea8-264">`Single` 컬렉션은 비어 있거나 둘 이상의 항목이 없는 경우 메서드에서 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-264">The `Single` method throws an exception if the collection is empty or if there's more than one item.</span></span> <span data-ttu-id="fbea8-265">대신 `SingleOrDefault`, 값을 반환 하는 기본값 (이 경우 null) 컬렉션이 비어 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="fbea8-265">An alternative is `SingleOrDefault`, which returns a default value (null in this case) if the collection is empty.</span></span> <span data-ttu-id="fbea8-266">사용 하 여 `SingleOrDefault` 빈 컬렉션에:</span><span class="sxs-lookup"><span data-stu-id="fbea8-266">Using `SingleOrDefault` on an empty collection:</span></span>

* <span data-ttu-id="fbea8-267">예외가 발생 (에서 찾으려고 하는 `Courses` 속성에 null 참조).</span><span class="sxs-lookup"><span data-stu-id="fbea8-267">Results in an exception (from trying to find a `Courses` property on a null reference).</span></span>
* <span data-ttu-id="fbea8-268">예외 메시지는 문제의 원인을 477860 덜 명확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-268">The exception message would less clearly indicate the cause of the problem.</span></span>

<span data-ttu-id="fbea8-269">다음 코드의 보기 모델을 채우는 `Enrollments` 속성 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-269">The following code populates the view model's `Enrollments` property when a course is selected:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

<span data-ttu-id="fbea8-270">끝에 다음 태그를 추가 *Pages/Courses/Index.cshtml* Razor 페이지:</span><span class="sxs-lookup"><span data-stu-id="fbea8-270">Add the following markup to the end of the *Pages/Courses/Index.cshtml* Razor Page:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-)]

<span data-ttu-id="fbea8-271">위의 태그 courses 강사 강사 선택 된 경우와 관련 된 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-271">The preceding markup displays a list of courses related to an instructor when an instructor is selected.</span></span>

<span data-ttu-id="fbea8-272">응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-272">Test the app.</span></span> <span data-ttu-id="fbea8-273">클릭는 **선택** 강사 페이지에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-273">Click on a **Select** link on the instructors page.</span></span>

![강사 인덱스 페이지 강사 선택](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a><span data-ttu-id="fbea8-275">학생 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-275">Show student data</span></span>

<span data-ttu-id="fbea8-276">이 섹션에서는 응용 프로그램은 선택한 과정에 학생 데이터를 표시 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-276">In this section, the app is updated to show the student data for a selected course.</span></span>

<span data-ttu-id="fbea8-277">업데이트에 대 한 쿼리는 `OnGetAsync` 메서드에서 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-277">Update the query in the `OnGetAsync` method in *Pages/Instructors/Index.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="fbea8-278">업데이트 *Pages/Instructors/Index.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-278">Update *Pages/Instructors/Index.cshtml*.</span></span> <span data-ttu-id="fbea8-279">파일의 끝에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-279">Add the following markup to the end of the file:</span></span>

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

<span data-ttu-id="fbea8-280">위의 태그 선택한 과정에서 등록 된 학생의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-280">The preceding markup displays a list of the students who are enrolled in the selected course.</span></span>

<span data-ttu-id="fbea8-281">페이지를 새로 고치고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-281">Refresh the page and select an instructor.</span></span> <span data-ttu-id="fbea8-282">등록 된 학생 자신의 등급의 목록을 보려면 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-282">Select a course to see the list of enrolled students and their grades.</span></span>

![강사 인덱스 페이지 강사 및 선택한 과정](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a><span data-ttu-id="fbea8-284">단일를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbea8-284">Using Single</span></span>

<span data-ttu-id="fbea8-285">`Single` 에서 메서드를 전달할 수는 `Where` 조건을 호출 하는 대신는 `Where` 메서드 별도로:</span><span class="sxs-lookup"><span data-stu-id="fbea8-285">The `Single` method can pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21,28-29)]

<span data-ttu-id="fbea8-286">위의 `Single` 접근 방식을 사용 하 여에 비해 없습니다 장점을 제공 `Where`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-286">The preceding `Single` approach provides no benefits over using `Where`.</span></span> <span data-ttu-id="fbea8-287">일부 개발자는 `Single` 스타일에 접근 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-287">Some developers prefer the `Single` approach style.</span></span>

## <a name="explicit-loading"></a><span data-ttu-id="fbea8-288">명시적 로드</span><span class="sxs-lookup"><span data-stu-id="fbea8-288">Explicit loading</span></span>

<span data-ttu-id="fbea8-289">현재 코드에 대 한 즉시 로드 지정 `Enrollments` 및 `Students`:</span><span class="sxs-lookup"><span data-stu-id="fbea8-289">The current code specifies eager loading for `Enrollments` and `Students`:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

<span data-ttu-id="fbea8-290">사용자가 등록 과정에서 참조 하려고 거의 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-290">Suppose users rarely want to see enrollments in a course.</span></span> <span data-ttu-id="fbea8-291">이 경우 최적화 분석이 요청 된 경우에 등록 데이터를 로드 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-291">In that case, an optimization would be to only load the enrollment data if it's requested.</span></span> <span data-ttu-id="fbea8-292">이 섹션에서는 `OnGetAsync` 명시적 로드를 사용 하도록 업데이트 `Enrollments` 및 `Students`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-292">In this section, the `OnGetAsync` is updated to use explicit loading of `Enrollments` and `Students`.</span></span>

<span data-ttu-id="fbea8-293">업데이트는 `OnGetAsync` 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-293">Update the `OnGetAsync` with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

<span data-ttu-id="fbea8-294">위의 코드 삭제는 *ThenInclude* 등록 및 학생 데이터에 대 한 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-294">The preceding code drops the *ThenInclude* method calls for enrollment and student data.</span></span> <span data-ttu-id="fbea8-295">과정을 선택 하면 강조 표시 된 코드를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-295">If a course is selected, the highlighted code retrieves:</span></span>

* <span data-ttu-id="fbea8-296">`Enrollment` 선택한 과정에 대 한 엔터티.</span><span class="sxs-lookup"><span data-stu-id="fbea8-296">The `Enrollment` entities for the selected course.</span></span>
* <span data-ttu-id="fbea8-297">`Student` 각각에 대 한 엔터티 `Enrollment`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-297">The `Student` entities for each `Enrollment`.</span></span>

<span data-ttu-id="fbea8-298">위의 코드를 주석으로 표시 `.AsNoTracking()`합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-298">Notice the preceding code comments out `.AsNoTracking()`.</span></span> <span data-ttu-id="fbea8-299">탐색 속성 추적 된 엔터티에 대 한 명시적으로 로드할만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-299">Navigation properties can only be explicitly loaded for tracked entities.</span></span>

<span data-ttu-id="fbea8-300">응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-300">Test the app.</span></span> <span data-ttu-id="fbea8-301">사용자 관점에서 응용 프로그램에서 이전 버전으로 동일 하 게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-301">From a users perspective, the app behaves identically to the previous version.</span></span>

<span data-ttu-id="fbea8-302">다음 자습서에는 관련된 데이터를 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbea8-302">The next tutorial shows how to update related data.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="fbea8-303">[이전](xref:data/ef-rp/complex-data-model)
>[다음](xref:data/ef-rp/update-related-data)</span><span class="sxs-lookup"><span data-stu-id="fbea8-303">[Previous](xref:data/ef-rp/complex-data-model)
[Next](xref:data/ef-rp/update-related-data)</span></span>