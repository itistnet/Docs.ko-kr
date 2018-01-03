---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: "SignalR 추적 사용 | Microsoft Docs"
author: tfitzmac
description: "이 문서에서는 SignalR 서버와 클라이언트에 대 한 추적을 구성 하는 방법에 설명 합니다. 추적을 사용 하면 이벤트에 대 한 진단 정보를 볼 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/08/2014
ms.topic: article
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 2f01ab5d66e44cd82634f1b3df1ca6c78b7fd9d5
ms.sourcegitcommit: c07fb5cb5df0a12f9fe6735fcbc90964608fa687
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2017
---
<a name="enabling-signalr-tracing"></a><span data-ttu-id="cf960-104">SignalR 추적 사용</span><span class="sxs-lookup"><span data-stu-id="cf960-104">Enabling SignalR Tracing</span></span>
====================
<span data-ttu-id="cf960-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cf960-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="cf960-106">이 문서에서는 SignalR 서버와 클라이언트에 대 한 추적을 구성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="cf960-107">추적을 사용 하 여 SignalR 응용 프로그램에서 이벤트에 대 한 진단 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
> 
> <span data-ttu-id="cf960-108">이 항목 원래 Patrick Fletcher 썼습니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-108">This topic was originally written by Patrick Fletcher.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="cf960-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="cf960-109">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="cf960-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cf960-110">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="cf960-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="cf960-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="cf960-112">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="cf960-112">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="cf960-113">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="cf960-113">Questions and comments</span></span>
> 
> <span data-ttu-id="cf960-114">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="cf960-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cf960-115">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="cf960-116">추적을 사용 하는 경우는 SignalR 응용 프로그램 이벤트에 대 한 로그 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="cf960-117">클라이언트와 서버 모두에서 이벤트를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="cf960-118">서버 로그를 연결, 확장 공급자 및 메시지 버스 이벤트에서 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="cf960-119">클라이언트 연결 이벤트는 추적 중입니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="cf960-120">SignalR 2.1 이상 버전에서는 추적이 클라이언트에 허브 호출 메시지의 전체 콘텐츠를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="cf960-121">목차</span><span class="sxs-lookup"><span data-stu-id="cf960-121">Contents</span></span>

- [<span data-ttu-id="cf960-122">서버에서 추적을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="cf960-123">텍스트 파일에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="cf960-124">서버 이벤트를 이벤트 로그에 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="cf960-125">.NET 클라이언트 (Windows 바탕 화면 앱)에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="cf960-126">콘솔에 데스크톱 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="cf960-127">텍스트 파일에 로깅 데스크톱 클라이언트 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="cf960-128">Windows Phone 8 클라이언트에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="cf960-129">UI에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="cf960-130">디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="cf960-131">JavaScript 클라이언트에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="cf960-132">서버에서 추적을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-132">Enabling tracing on the server</span></span>

<span data-ttu-id="cf960-133">응용 프로그램의 구성 파일 (App.config 또는 Web.config 프로젝트의 유형에 따라.) 서버에서 추적을 사용 하도록 설정 기록 하려는 이벤트의 범주를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="cf960-134">구성 파일도 지정 텍스트 파일, Windows 이벤트 로그 또는의 구현을 사용 하 여 사용자 지정 로그에 이벤트를 기록할 것인지 [TraceListener](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelistener(v=vs.110).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="cf960-135">서버 이벤트 범주에는 다음과 같은 메시지</span><span class="sxs-lookup"><span data-stu-id="cf960-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="cf960-136">소스</span><span class="sxs-lookup"><span data-stu-id="cf960-136">Source</span></span> | <span data-ttu-id="cf960-137">메시지</span><span class="sxs-lookup"><span data-stu-id="cf960-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="cf960-138">SignalR.SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="cf960-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="cf960-139">SQL 메시지 버스 확장 공급자를 설치, 데이터베이스 작업, 오류 및 제한 시간 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="cf960-140">SignalR.ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="cf960-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="cf960-141">서비스 버스 확장 공급자 항목 만들기 및 구독, 오류 및 메시징 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="cf960-142">SignalR.RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="cf960-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="cf960-143">Redis 확장 공급자 연결, 연결 끊기 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="cf960-144">SignalR.ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="cf960-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="cf960-145">메시징 이벤트 확장</span><span class="sxs-lookup"><span data-stu-id="cf960-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="cf960-146">SignalR.Transports.WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="cf960-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="cf960-147">WebSocket 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="cf960-148">SignalR.Transports.ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="cf960-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="cf960-149">ServerSentEvents 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="cf960-150">SignalR.Transports.ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="cf960-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="cf960-151">ForeverFrame 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="cf960-152">SignalR.Transports.LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="cf960-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="cf960-153">LongPolling 전송 연결, 연결 끊기, 메시징 및 오류 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="cf960-154">SignalR.Transports.TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="cf960-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="cf960-155">연결, 연결 끊기 및 keepalive 이벤트 전송</span><span class="sxs-lookup"><span data-stu-id="cf960-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="cf960-156">SignalR.ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="cf960-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="cf960-157">검색 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="cf960-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="cf960-158">텍스트 파일에 서버 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-158">Logging server events to text files</span></span>

<span data-ttu-id="cf960-159">다음 코드에는 각 범주의 이벤트에 대 한 추적을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="cf960-160">이 샘플에서는 텍스트 파일에 이벤트를 기록 하도록 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="cf960-161">**추적 사용에 대 한 XML 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="cf960-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="cf960-162">위의 코드에서는 `SignalRSwitch` 항목 지정는 [TraceLevel](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelevel(v=vs.110).aspx) 지정 된 로그로 전송 하는 이벤트에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="cf960-163">이 경우 설정 되어 `Verbose` 즉, 모든 디버깅 및 추적 메시지가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="cf960-164">다음과 같은 출력 항목을 보여 줍니다.는 `transports.log.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="cf960-165">새 표시 연결, 제거 된 연결 및 전송 하트 비트 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="cf960-166">서버 이벤트를 이벤트 로그에 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-166">Logging server events to the event log</span></span>

<span data-ttu-id="cf960-167">텍스트 파일이 아닌 이벤트 로그에 이벤트를 기록 하려면의 엔터티에 대 한 값을 변경는 `sharedListeners` 노드.</span><span class="sxs-lookup"><span data-stu-id="cf960-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="cf960-168">다음 코드에는 서버 이벤트를 이벤트 로그에 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="cf960-169">**이벤트 로그에 이벤트를 기록에 대 한 XML 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="cf960-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="cf960-170">이벤트 응용 프로그램 로그에 기록 되 고 아래 표시 된 것과 같이 이벤트 뷰어를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![SignalR 로그를 표시 하는 이벤트 뷰어](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="cf960-172">이벤트 로그를 사용할 때는 **TraceLevel** 를 **오류** 메시지 수를 관리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="cf960-173">.NET 클라이언트 (Windows 바탕 화면 앱)에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="cf960-174">.NET 클라이언트는 콘솔에 텍스트 파일 또는의 구현을 사용 하 여 사용자 지정 로그에 이벤트를 기록할 수 있습니다 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="cf960-175">.NET 클라이언트 로그인을 사용 하려면 연결의 설정 `TraceLevel` 속성을 한 [TraceLevels](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) 값 및 `TraceWriter` 속성을 유효한 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="cf960-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="cf960-176">콘솔에 데스크톱 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="cf960-177">다음 C# 코드에서.NET 클라이언트는 콘솔에 이벤트를 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="cf960-178">텍스트 파일에 로깅 데스크톱 클라이언트 이벤트</span><span class="sxs-lookup"><span data-stu-id="cf960-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="cf960-179">다음 C# 코드를 텍스트 파일로.NET 클라이언트에서 이벤트를 기록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="cf960-180">다음과 같은 출력 항목을 보여 줍니다.는 `ClientLog.txt` 위의 구성 파일을 사용 하 여 응용 프로그램에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="cf960-181">클라이언트 메서드를 호출할 허브 호출 및 서버에 연결 하는 클라이언트를 보여 주므로 `addMessage`:</span><span class="sxs-lookup"><span data-stu-id="cf960-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="cf960-182">Windows Phone 8 클라이언트에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="cf960-183">Windows Phone 앱 용 SignalR 응용 프로그램 같은.NET 클라이언트를 사용 하 여 데스크톱 응용 프로그램으로 하지만 [Console.Out](https://msdn.microsoft.com/en-us/library/system.console.out(v=vs.110).aspx) 및 사용 하 여 파일 쓰기 [StreamWriter](https://msdn.microsoft.com/en-us/library/system.io.streamwriter(v=vs.110).aspx) 는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/en-us/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/en-us/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="cf960-184">대신, 사용자 지정 구현을 만들 해야 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 추적에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span> 

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="cf960-185">UI에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="cf960-186">[SignalR 코드 베이스](https://github.com/SignalR/SignalR/archive/master.zip) 추적 출력을 작성 하는 Windows Phone 샘플이 포함 되어는 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 사용자 지정을 사용 하 여 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 호출 구현 `TextBlockWriter`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="cf960-187">이 클래스에서 확인할 수 있습니다는 **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="cf960-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="cf960-188">인스턴스를 만들 때 `TextBlockWriter`, 현재에서 전달 [SynchronizationContext](https://msdn.microsoft.com/en-us/library/system.threading.synchronizationcontext(v=vs.110).aspx), 및 [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 생성 됩니다는 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 추적에 사용할 출력:</span><span class="sxs-lookup"><span data-stu-id="cf960-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/en-us/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="cf960-189">그런 다음 새에 추적 출력을 기록 됩니다 [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 에서 만든는 [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) 에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="cf960-190">디버그 콘솔에 Windows Phone 클라이언트 이벤트 로깅</span><span class="sxs-lookup"><span data-stu-id="cf960-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="cf960-191">UI가 아닌 디버그 콘솔에 출력을 보내려면의 구현을 만드는 [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) 디버그 창에 기록 하 고이 연결의 할당 [TraceWriter](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) 속성:</span><span class="sxs-lookup"><span data-stu-id="cf960-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/en-us/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="cf960-192">그런 다음 Visual Studio의 디버그 창에 추적 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="cf960-193">JavaScript 클라이언트에서 추적 설정</span><span class="sxs-lookup"><span data-stu-id="cf960-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="cf960-194">클라이언트 쪽 로깅에 대 한 연결을 사용 하려면 설정는 `logging` 호출 하기 전에 연결 개체에 `start` 연결을 설정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="cf960-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="cf960-195">**생성 된 프록시) (사용 하 여 브라우저 콘솔에 대 한 추적을 사용 하기 위한 클라이언트 JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="cf960-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="cf960-196">**생성 된 프록시) (없이 브라우저 콘솔에 대 한 추적을 사용 하기 위한 클라이언트 JavaScript 코드**</span><span class="sxs-lookup"><span data-stu-id="cf960-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="cf960-197">추적을 사용 하는 경우 JavaScript 클라이언트 브라우저 콘솔에 이벤트를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="cf960-198">브라우저 콘솔에 액세스 하려면 참조 [모니터링 전송](../getting-started/introduction-to-signalr.md#MonitoringTransports)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="cf960-199">다음 스크린 샷에서 추적을 사용 하면서 SignalR JavaScript 클라이언트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="cf960-200">브라우저 콘솔의 연결 및 허브 호출 이벤트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cf960-200">It shows connection and hub invocation events in the browser console:</span></span>

![브라우저 콘솔에서 SignalR 추적 이벤트](enabling-signalr-tracing/_static/image4.png)