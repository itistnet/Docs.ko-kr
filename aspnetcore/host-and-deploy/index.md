---
title: "ASP.NET Core 호스트 및 배포"
author: tdykstra
description: "호스팅 환경을 설정하고 ASP.NET Core 앱을 배포하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 08/07/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/index
ms.openlocfilehash: 20468e15a00e50b3899931d6dcb28757dbe0b6ad
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="host-and-deploy-aspnet-core"></a><span data-ttu-id="1fa67-103">ASP.NET Core 호스트 및 배포</span><span class="sxs-lookup"><span data-stu-id="1fa67-103">Host and deploy ASP.NET Core</span></span>

<span data-ttu-id="1fa67-104">일반적으로 ASP.NET Core 앱을 호스팅 환경에 배포하기 위해서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-104">In general, to deploy an ASP.NET Core app to a hosting environment:</span></span>

* <span data-ttu-id="1fa67-105">호스팅 서버의 폴더에 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-105">Publish the app to a folder on the hosting server.</span></span>
* <span data-ttu-id="1fa67-106">요청이 도착할 때 앱을 시작하고 작동이 중단되거나 서버가 다시 부팅된 후 앱을 다시 시작하는 프로세스 관리자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-106">Set up a process manager that starts the app when requests arrive and restarts the app after it crashes or the server reboots.</span></span>
* <span data-ttu-id="1fa67-107">요청을 앱에 전달하는 역방향 프록시를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-107">Set up a reverse proxy that forwards requests to the app.</span></span>

## <a name="publish-to-a-folder"></a><span data-ttu-id="1fa67-108">폴더에 게시</span><span class="sxs-lookup"><span data-stu-id="1fa67-108">Publish to a folder</span></span> 

<span data-ttu-id="1fa67-109">[dotnet publish](/dotnet/articles/core/tools/dotnet-publish) CLI 명령은 앱 코드를 컴파일하고 앱을 *publish* 폴더로 실행하는 데 필요한 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-109">The [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) CLI command compiles app code and copies the files needed to run the app into a *publish* folder.</span></span> <span data-ttu-id="1fa67-110">Visual Studio에서 배포할 경우 파일이 배포 대상에 복사되기 전에 `dotnet publish` 단계가 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-110">When deploying from Visual Studio, the `dotnet publish` step happens automatically before the files are copied to the deployment destination.</span></span>

### <a name="folder-contents"></a><span data-ttu-id="1fa67-111">폴더 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="1fa67-111">Folder contents</span></span>

<span data-ttu-id="1fa67-112">*publish* 폴더에는 앱, 해당 종속성 및 필요한 경우 .NET 런타임에 대한 *.exe* 및 *.dll* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-112">The *publish* folder contains *.exe* and *.dll* files for the app, its dependencies, and optionally the .NET runtime.</span></span>

<span data-ttu-id="1fa67-113">.NET Core 앱은 *자체 포함* 또는 *프레임워크 종속* 앱으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-113">A .NET Core app can be published as *self-contained* or *framework-dependent* app.</span></span> <span data-ttu-id="1fa67-114">앱이 자체 포함인 경우 .NET 런타임이 포함된 *.dll* 파일은 *publish* 폴더에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-114">If the app is self-contained, the *.dll* files that contain the .NET runtime are included in the *publish* folder.</span></span> <span data-ttu-id="1fa67-115">앱이 프레임워크 종속인 경우 서버에 설치된 .NET 버전에 대한 참조가 앱에 포함되므로 .NET 런타임 파일이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-115">If the app is framework-dependent, the .NET runtime files aren't included because the app has a reference to a version of .NET that is installed on the server.</span></span> <span data-ttu-id="1fa67-116">기본 배포 모델은 프레임워크 종속입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-116">The default deployment model is framework-dependent.</span></span> <span data-ttu-id="1fa67-117">자세한 내용은 [.NET Core 응용 프로그램 배포](/dotnet/articles/core/deploying/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-117">For more information, see [.NET Core application deployment](/dotnet/articles/core/deploying/index).</span></span>

<span data-ttu-id="1fa67-118">*.exe* 및 *.dll* 파일 이외에 ASP.NET Core 앱에 대한 *publish* 폴더에는 일반적으로 구성 파일, 정적 자산 및 MVC 뷰가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-118">In addition to *.exe* and *.dll* files, the *publish* folder for an ASP.NET Core app typically contains configuration files, static assets, and MVC views.</span></span> <span data-ttu-id="1fa67-119">자세한 내용은 [디렉터리 구조](xref:host-and-deploy/directory-structure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-119">For more information, see [Directory structure](xref:host-and-deploy/directory-structure).</span></span>

## <a name="set-up-a-process-manager"></a><span data-ttu-id="1fa67-120">프로세스 관리자 설정</span><span class="sxs-lookup"><span data-stu-id="1fa67-120">Set up a process manager</span></span>

<span data-ttu-id="1fa67-121">ASP.NET Core 앱은 서버가 부팅되고 작동 중단 후 다시 시작될 때 시작되어야 하는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-121">An ASP.NET Core app is a console app that must be started when a server boots and restarted if it crashes.</span></span> <span data-ttu-id="1fa67-122">시작 및 다시 시작을 자동화하려면 프로세스 관리자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-122">To automate starts and restarts, a process manager is required.</span></span> <span data-ttu-id="1fa67-123">ASP.NET Core에 대한 가장 일반적인 프로세스 관리자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-123">The most common process managers for ASP.NET Core are:</span></span>

* <span data-ttu-id="1fa67-124">Linux</span><span class="sxs-lookup"><span data-stu-id="1fa67-124">Linux</span></span>
  * [<span data-ttu-id="1fa67-125">nginx</span><span class="sxs-lookup"><span data-stu-id="1fa67-125">nginx</span></span>](xref:host-and-deploy/linux-nginx)
  * [<span data-ttu-id="1fa67-126">Apache</span><span class="sxs-lookup"><span data-stu-id="1fa67-126">Apache</span></span>](xref:host-and-deploy/linux-apache)
* <span data-ttu-id="1fa67-127">Windows</span><span class="sxs-lookup"><span data-stu-id="1fa67-127">Windows</span></span>
  * [<span data-ttu-id="1fa67-128">IIS</span><span class="sxs-lookup"><span data-stu-id="1fa67-128">IIS</span></span>](xref:host-and-deploy/iis/index)
  * [<span data-ttu-id="1fa67-129">Windows 서비스</span><span class="sxs-lookup"><span data-stu-id="1fa67-129">Windows Service</span></span>](xref:host-and-deploy/windows-service)

## <a name="set-up-a-reverse-proxy"></a><span data-ttu-id="1fa67-130">역방향 프록시 설정</span><span class="sxs-lookup"><span data-stu-id="1fa67-130">Set up a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1fa67-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1fa67-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1fa67-132">앱에서 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용할 경우 [nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) 또는 [IIS](xref:host-and-deploy/iis/index)를 역방향 프록시 서버로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-132">If the app uses the [Kestrel](xref:fundamentals/servers/kestrel) web server, [nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache), or [IIS](xref:host-and-deploy/iis/index) can be used as a reverse proxy server.</span></span> <span data-ttu-id="1fa67-133">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-133">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span> <span data-ttu-id="1fa67-134">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-134">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1fa67-135">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1fa67-135">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1fa67-136">앱에서 [Kestrel](xref:fundamentals/servers/kestrel) 웹 서버를 사용하고 앱이 인터넷에 노출될 경우 [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache) 또는 [IIS](xref:host-and-deploy/iis/index)를 역방향 프록시 서버로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-136">If the app uses the [Kestrel](xref:fundamentals/servers/kestrel) web server and will be exposed to the Internet, use [nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache), or [IIS](xref:host-and-deploy/iis/index) as a reverse proxy server.</span></span> <span data-ttu-id="1fa67-137">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-137">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span> <span data-ttu-id="1fa67-138">역방향 프록시를 사용하는 주요 이유는 보안 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-138">The main reason for using a reverse proxy is security.</span></span> <span data-ttu-id="1fa67-139">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel?tabs=aspnetcore1x#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-139">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel?tabs=aspnetcore1x#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

---

## <a name="using-visual-studio-and-msbuild-to-automate-deployment"></a><span data-ttu-id="1fa67-140">Visual Studio 및 MSBuild를 사용하여 배포 자동화</span><span class="sxs-lookup"><span data-stu-id="1fa67-140">Using Visual Studio and MSBuild to automate deployment</span></span>

<span data-ttu-id="1fa67-141">일반적으로 배포에는 `dotnet publish`에서 서버로 출력을 복사하는 것 외에 추가 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-141">Deployment often requires additional tasks besides copying the output from `dotnet publish` to a server.</span></span> <span data-ttu-id="1fa67-142">예를 들어 추가 파일이 필요하거나 *publish* 폴더에서 제외될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-142">For example, extra files might be required or excluded from the *publish* folder.</span></span> <span data-ttu-id="1fa67-143">Visual Studio에서는 웹 배포에 MSBuild를 사용하고 MSBuild를 사용자 지정하여 배포 중에 많은 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-143">Visual Studio uses MSBuild for web deployment, and MSBuild can be customized to do many other tasks during deployment.</span></span> <span data-ttu-id="1fa67-144">자세한 내용은 [Visual Studio에서 프로필 게시](xref:host-and-deploy/visual-studio-publish-profiles) 및 [MSBuild 및 Team Foundation Build 사용](http://msbuildbook.com/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-144">For more information, see [Publish profiles in Visual Studio](xref:host-and-deploy/visual-studio-publish-profiles) and the [Using MSBuild and Team Foundation Build](http://msbuildbook.com/) book.</span></span>

<span data-ttu-id="1fa67-145">[웹 게시 기능](xref:tutorials/publish-to-azure-webapp-using-vs)을 사용하거나 [기본 제공 Git 지원](xref:host-and-deploy/azure-apps/azure-continuous-deployment)을 사용하여 Visual Studio에서 Azure App Service로 앱을 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-145">By using [the Publish Web feature](xref:tutorials/publish-to-azure-webapp-using-vs) or [built-in Git support](xref:host-and-deploy/azure-apps/azure-continuous-deployment), apps can be deployed directly from Visual Studio to the Azure App Service.</span></span> <span data-ttu-id="1fa67-146">Visual Studio Team Services에서는 [Azure App Service에 연속 배포](/vsts/build-release/apps/cd/azure/aspnet-core-to-azure-webapp?tabs=vsts)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-146">Visual Studio Team Services supports [continuous deployment to Azure App Service](/vsts/build-release/apps/cd/azure/aspnet-core-to-azure-webapp?tabs=vsts).</span></span>

## <a name="publishing-to-azure"></a><span data-ttu-id="1fa67-147">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="1fa67-147">Publishing to Azure</span></span>

<span data-ttu-id="1fa67-148">Visual Studio를 사용하여 Azure에 앱을 게시하는 방법에 관한 지침은 [Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시](xref:tutorials/publish-to-azure-webapp-using-vs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-148">See [Publish an ASP.NET Core web app to Azure App Service using Visual Studio](xref:tutorials/publish-to-azure-webapp-using-vs) for instructions on how to publish an app to Azure using Visual Studio.</span></span> <span data-ttu-id="1fa67-149">[명령줄](xref:tutorials/publish-to-azure-webapp-using-cli)에서도 앱을 Azure에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fa67-149">The app can also be published to Azure from the [command line](xref:tutorials/publish-to-azure-webapp-using-cli).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fa67-150">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1fa67-150">Additional resources</span></span>

<span data-ttu-id="1fa67-151">Docker를 호스팅 환경으로 사용하는 방법에 대한 자세한 내용은 [Docker에서 ASP.NET Core 앱 호스트](xref:host-and-deploy/docker/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fa67-151">For information on using Docker as a hosting environment, see [Host ASP.NET Core apps in Docker](xref:host-and-deploy/docker/index).</span></span>