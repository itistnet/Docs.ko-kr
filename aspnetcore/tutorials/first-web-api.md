---
title: "ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기"
author: rick-anderson
description: "ASP.NET Core MVC 및 Windows용 Visual Studio를 사용하여 Web API 빌드"
keywords: "ASP.NET Core, WebAPI, Web API, REST, HTTP, 서비스, HTTP 서비스"
ms.author: riande
manager: wpickett
ms.date: 8/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-web-api
ms.openlocfilehash: c57c73c6f9c60874ef88749b838ed1cc1d353ead
ms.sourcegitcommit: 7fef13045e98d716c589a2982613dad261694a65
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2017
---
#<a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a><span data-ttu-id="cf69d-104">ASP.NET Core 및 Windows용 Visual Studio를 사용하여 Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="cf69d-104">Create a web API with ASP.NET Core and Visual Studio for Windows</span></span>

<span data-ttu-id="cf69d-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Mike Wasson](https://github.com/mikewasson)</span><span class="sxs-lookup"><span data-stu-id="cf69d-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Mike Wasson](https://github.com/mikewasson)</span></span>

<span data-ttu-id="cf69d-106">이 자습서에서는 “할 일” 항목 모음을 관리하기 위한 Web API를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-106">In this tutorial, you’ll build a web API for managing a list of "to-do" items.</span></span> <span data-ttu-id="cf69d-107">UI는 빌드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-107">You won’t build a UI.</span></span>

<span data-ttu-id="cf69d-108">이 자습서는 세 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-108">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="cf69d-109">Windows: Windows용 Visual Studio를 사용한 Web API(이 자습서)</span><span class="sxs-lookup"><span data-stu-id="cf69d-109">Windows: Web API with Visual Studio for Windows (This tutorial)</span></span>
* <span data-ttu-id="cf69d-110">macOS: [Mac용 Visual Studio를 사용한 Web API](xref:tutorials/first-web-api-mac)</span><span class="sxs-lookup"><span data-stu-id="cf69d-110">macOS: [Web API with Visual Studio for Mac](xref:tutorials/first-web-api-mac)</span></span>
* <span data-ttu-id="cf69d-111">macOS, Linux, Windows: [Visual Studio Code를 사용한 Web API](xref:tutorials/web-api-vsc)</span><span class="sxs-lookup"><span data-stu-id="cf69d-111">macOS, Linux, Windows: [Web API with Visual Studio Code](xref:tutorials/web-api-vsc)</span></span>

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a><span data-ttu-id="cf69d-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="cf69d-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../includes/install2.0.md)]

<span data-ttu-id="cf69d-113">ASP.NET Core 1.1 버전에 대해서는 [이 PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/_static/_webAPI.pdf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf69d-113">See [this PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/first-web-api/_static/_webAPI.pdf) for the ASP.NET Core 1.1 version.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="cf69d-114">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-114">Create the project</span></span>

<span data-ttu-id="cf69d-115">Visual Studio에서 **파일** 메뉴 > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-115">From Visual Studio, select **File** menu, > **New** > **Project**.</span></span>

<span data-ttu-id="cf69d-116">**ASP.NET Core 웹 응용 프로그램(.NET Core)** 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-116">Select the **ASP.NET Core Web Application (.NET Core)** project template.</span></span> <span data-ttu-id="cf69d-117">프로젝트 이름을 `TodoApi`로 지정하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-117">Name the project `TodoApi` and select **OK**.</span></span>

![새 프로젝트 대화 상자](first-web-api/_static/new-project.png)

<span data-ttu-id="cf69d-119">**새 ASP.NET Core 웹 응용 프로그램 - TodoApi** 대화 상자에서 **Web API** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-119">In the **New ASP.NET Core Web Application - TodoApi** dialog, select the **Web API** template.</span></span> <span data-ttu-id="cf69d-120">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-120">Select **OK**.</span></span> <span data-ttu-id="cf69d-121">**Docker 지원 사용**을 선택하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="cf69d-121">Do **not** select **Enable Docker Support**.</span></span>

![ASP.NET Core 템플릿에서 Web API 프로젝트 템플릿이 선택된 새 ASP.NET 웹 응용 프로그램 대화 상자](first-web-api/_static/web-api-project.png)

### <a name="launch-the-app"></a><span data-ttu-id="cf69d-123">앱 시작</span><span class="sxs-lookup"><span data-stu-id="cf69d-123">Launch the app</span></span>

<span data-ttu-id="cf69d-124">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-124">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="cf69d-125">Visual Studio가 브라우저를 시작하고 `http://localhost:port/api/values`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-125">Visual Studio launches a browser and navigates to `http://localhost:port/api/values`, where *port* is a randomly-chosen port number.</span></span> <span data-ttu-id="cf69d-126">Chrome, Edge 및 Firefox에는 다음 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-126">Chrome, Edge, and Firefox display the following:</span></span>

```
["value1","value2"]
``` 

### <a name="add-a-model-class"></a><span data-ttu-id="cf69d-127">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="cf69d-127">Add a model class</span></span>

<span data-ttu-id="cf69d-128">모델은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-128">A model is an object that represents the data in your application.</span></span> <span data-ttu-id="cf69d-129">이 경우 유일한 모델은 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-129">In this case, the only model is a to-do item.</span></span>

<span data-ttu-id="cf69d-130">“Models” 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-130">Add a folder named "Models".</span></span> <span data-ttu-id="cf69d-131">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-131">In Solution Explorer, right-click the project.</span></span> <span data-ttu-id="cf69d-132">**추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-132">Select **Add** > **New Folder**.</span></span> <span data-ttu-id="cf69d-133">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-133">Name the folder *Models*.</span></span>

<span data-ttu-id="cf69d-134">참고: 모델 클래스는 프로젝트의 아무 곳에나 이동할 수 있지만 일반적으로 *Models* 폴더를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-134">Note: The model classes go anywhere in your project, but the *Models* folder is used by convention.</span></span>

<span data-ttu-id="cf69d-135">`TodoItem` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-135">Add a `TodoItem` class.</span></span> <span data-ttu-id="cf69d-136">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-136">Right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="cf69d-137">클래스 이름을 `TodoItem`으로 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-137">Name the class `TodoItem` and select **Add**.</span></span>

<span data-ttu-id="cf69d-138">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-138">Replace the generated code with the following:</span></span>

<span data-ttu-id="cf69d-139">[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]</span><span class="sxs-lookup"><span data-stu-id="cf69d-139">[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoItem.cs)]</span></span>

<span data-ttu-id="cf69d-140">`TodoItem`이 만들어질 때 데이터베이스가 `Id`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-140">The database generates the `Id` when a `TodoItem` is created.</span></span>

### <a name="create-the-database-context"></a><span data-ttu-id="cf69d-141">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="cf69d-141">Create the database context</span></span>

<span data-ttu-id="cf69d-142">*데이터베이스 컨텍스트*는 특정 데이터 모델에 맞게 Entity Framework 기능을 조정하는 주 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-142">The *database context* is the main class that coordinates Entity Framework functionality for a given data model.</span></span> <span data-ttu-id="cf69d-143">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-143">This class is created by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span>

<span data-ttu-id="cf69d-144">`TodoContext` 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-144">Add a `TodoContext` class.</span></span> <span data-ttu-id="cf69d-145">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-145">Right-click the *Models* folder and select **Add** > **Class**.</span></span> <span data-ttu-id="cf69d-146">클래스 이름을 `TodoContext`로 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-146">Name the class `TodoContext` and select **Add**.</span></span>

<span data-ttu-id="cf69d-147">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-147">Replace the generated code with the following:</span></span>

<span data-ttu-id="cf69d-148">[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]</span><span class="sxs-lookup"><span data-stu-id="cf69d-148">[!code-csharp[Main](first-web-api/sample/TodoApi/Models/TodoContext.cs)]</span></span>

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a><span data-ttu-id="cf69d-149">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="cf69d-149">Add a controller</span></span>

<span data-ttu-id="cf69d-150">솔루션 탐색기에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-150">In Solution Explorer, right-click the *Controllers* folder.</span></span> <span data-ttu-id="cf69d-151">**추가** > **새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-151">Select **Add** > **New Item**.</span></span> <span data-ttu-id="cf69d-152">**새 항목 추가** 대화 상자에서 **Web API 컨트롤러 클래스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-152">In the **Add New Item** dialog, select the **Web  API Controller Class** template.</span></span> <span data-ttu-id="cf69d-153">클래스 이름을 `TodoController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-153">Name the class `TodoController`.</span></span>

![검색 상자의 컨트롤러 및 Web API 컨트롤러가 선택된 새 항목 추가 대화 상자](first-web-api/_static/new_controller.png)

<span data-ttu-id="cf69d-155">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-155">Replace the generated code with the following:</span></span>

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]
  
### <a name="launch-the-app"></a><span data-ttu-id="cf69d-156">앱 시작</span><span class="sxs-lookup"><span data-stu-id="cf69d-156">Launch the app</span></span>

<span data-ttu-id="cf69d-157">Visual Studio에서 CTRL+F5를 눌러 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-157">In Visual Studio, press CTRL+F5 to launch the app.</span></span> <span data-ttu-id="cf69d-158">Visual Studio가 브라우저를 시작하고 `http://localhost:port/api/values`로 이동합니다. 여기서 *port*는 임의로 선택된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-158">Visual Studio launches a browser and navigates to `http://localhost:port/api/values`, where *port* is a randomly chosen port number.</span></span> <span data-ttu-id="cf69d-159">Chrome, Edge 또는 Firefox를 사용할 경우 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-159">If you're using Chrome, Edge or Firefox, the data will be displayed.</span></span> <span data-ttu-id="cf69d-160">IE를 사용할 경우 IE에서 *values.json* 파일을 열거나 저장할지 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-160">If you're using IE, IE will prompt to you open or save the *values.json* file.</span></span> <span data-ttu-id="cf69d-161">방금 만든 `Todo` 컨트롤러(`http://localhost:port/api/todo`)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cf69d-161">Navigate to the `Todo` controller we just created `http://localhost:port/api/todo`.</span></span>

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
