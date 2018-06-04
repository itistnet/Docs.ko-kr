---
title: ASP.NET Core SignalR.NET 클라이언트
author: rachelappel
description: ASP.NET Core SignalR.NET 클라이언트에 대 한 정보
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/18/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/dotnet-client
ms.openlocfilehash: 412d2362575789f1fb4792940df6d3dd24dbdd5a
ms.sourcegitcommit: 300a1127957dcdbce1b6ad79a7b9dc676f571510
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="ca407-103">ASP.NET Core SignalR.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca407-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="ca407-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="ca407-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="ca407-105">Xamarin, WPF, Windows Forms, 콘솔 및.NET Core 응용 프로그램에서 ASP.NET Core SignalR.NET 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-105">The ASP.NET Core SignalR .NET client can be used by Xamarin, WPF, Windows Forms, Console, and .NET Core apps.</span></span> <span data-ttu-id="ca407-106">마찬가지로 [JavaScript 클라이언트](xref:signalr/javascript-client),.NET 클라이언트를 사용 하면 수신 하 고 보내고 실시간으로 허브에 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-106">Like the [JavaScript client](xref:signalr/javascript-client), the .NET client enables you to receive and send and receive messages to a hub in real time.</span></span>

<span data-ttu-id="ca407-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="ca407-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="ca407-108">이 문서의 코드 예제는 ASP.NET Core SignalR.NET 클라이언트를 사용 하는 WPF 앱.</span><span class="sxs-lookup"><span data-stu-id="ca407-108">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="setup-client"></a><span data-ttu-id="ca407-109">클라이언트를 설치</span><span class="sxs-lookup"><span data-stu-id="ca407-109">Setup client</span></span>

<span data-ttu-id="ca407-110">`Microsoft.AspNetCore.SignalR.Client` SignalR 허브에 연결 하는.NET 클라이언트에 대 한 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-110">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="ca407-111">클라이언트 라이브러리를 설치 하려면에서 다음 명령을 실행의 **패키지 관리자 콘솔** 창:</span><span class="sxs-lookup"><span data-stu-id="ca407-111">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="ca407-112">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="ca407-112">Connect to a hub</span></span>

<span data-ttu-id="ca407-113">연결을 설정 하려면 만듭니다는 `HubConnectionBuilder` 호출 `Build`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-113">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="ca407-114">연결을 구성 하는 동안 허브 URL, 프로토콜, 전송 종류, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-114">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="ca407-115">필수 옵션 중 하나를 삽입 하 여 구성 된 `HubConnectionBuilder` 에 메서드 `Build`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-115">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="ca407-116">사용 하 여 연결 시작 `StartAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-116">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="ca407-117">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-117">Call hub methods from client</span></span>

<span data-ttu-id="ca407-118">`InvokeAsync` 허브에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-118">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="ca407-119">허브 메서드 이름 및 허브 메서드를 정의 하는 인수를 전달 `InvokeAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-119">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="ca407-120">SignalR은 비동기, 따라서 사용 `async` 및 `await` 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="ca407-120">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="ca407-121">허브에서 클라이언트를 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="ca407-121">Call client methods from hub</span></span>

<span data-ttu-id="ca407-122">허브를 사용 하 여 호출 하는 메서드를 정의 `connection.On` 을 빌드한 다음 하지만 연결을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="ca407-122">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

<span data-ttu-id="ca407-123">위의 코드에서 `connection.On` 서버 쪽 코드를 사용 하 여 호출할 때 실행 되는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ca407-123">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="ca407-124">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="ca407-124">Error handling and logging</span></span>

<span data-ttu-id="ca407-125">Try / catch 문 사용 하 여 오류 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-125">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="ca407-126">검사는 `Exception` 오류가 발생 한 후 수행할 적절 한 작업을 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ca407-126">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a><span data-ttu-id="ca407-127">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ca407-127">Additional resources</span></span>

* [<span data-ttu-id="ca407-128">허브</span><span class="sxs-lookup"><span data-stu-id="ca407-128">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="ca407-129">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ca407-129">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="ca407-130">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="ca407-130">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)