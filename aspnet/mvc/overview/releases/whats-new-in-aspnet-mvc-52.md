---
uid: mvc/overview/releases/whats-new-in-aspnet-mvc-52
title: ASP.NET MVC 5.2의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 12/25/2014
ms.assetid: 97972587-2720-48b4-b158-f35f2e855fbf
msc.legacyurl: /mvc/overview/releases/whats-new-in-aspnet-mvc-52
msc.type: authoredcontent
ms.openlocfilehash: 8c3c5de55396635d2e7f2b7726f54be1c06bb691
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823816"
---
<a name="whats-new-in-aspnet-mvc-52"></a>ASP.NET MVC 5.2의에서 새로운 기능
====================
[Microsoft](https://github.com/microsoft)

이 항목에서는 ASP.NET MVC 5.2의 새로운 기능에 대해 설명 합니다. [Microsoft.AspNet.MVC 5.2.2](#52) 고 [ASP.NET MVC 5.2.3 베타](#mvc523Beta)

- [소프트웨어 요구 사항](#softRequire)
- [다운로드](#download)
- [문서](#documentation)
- [ASP.NET MVC 5.2의에서 새로운 기능](#new-features)

    - [특성 라우팅 기능 향상](#attributerouting)
- [알려진된 문제 및 주요 변경 내용](#knownbreakingchanges)
- [버그 수정](#bug-fixes)
- [Microsoft.AspNet.MVC 5.2.2](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

- Visual Studio 2012: 다운로드 [ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용](https://go.microsoft.com/fwlink/?LinkId=390062)합니다.
- Visual Studio 2013: 다운로드 [Visual Studio 2013 업데이트](https://go.microsoft.com/fwlink/?LinkId=390064) 이상. 이 업데이트는 ASP.NET MVC 5.2 Razor 뷰를 편집 하기 위해 필요 합니다.

<a id="download"></a>
## <a name="download"></a>다운로드

NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다. 모든 런타임 패키지를 수행 합니다 [유의 적 버전](http://semver.org/) 사양입니다. 다음 버전이 최신 ASP.NET MVC 5.2 패키지: "5.2.0"입니다. 설치 하거나 이러한 패키지를 통해 업데이트할 수 있습니다 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)합니다. 릴리스에 NuGet의 해당 지역화 된 패키지도 포함 됩니다.

설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.

Install-package Microsoft.AspNet.Mvc-버전 5.2.0

<a id="documentation"></a>
## <a name="documentation"></a>설명서

자습서 및 ASP.NET MVC 5.2에 대 한 다른 정보는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ([https://www.asp.net/mvc](../../index.md)).

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a>ASP.NET MVC 5.2의에서 새로운 기능

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a>특성 라우팅 기능 향상

특성 라우팅은 이제 호출 IDirectRouteProvider 특성 경로 검색 하 고 구성 하는 방법을 완전히 제어할 수 있는 확장성 지점을 제공 합니다. IDirectRouteProvider는 작업 및 해당 작업에 대 한 라우팅 구성이 필요한 정확 하 게 지정 하려면 연결 된 경로 정보와 함께 컨트롤러의 목록을 제공 하는 일을 담당 합니다. IDirectRouteProvider 구현은 MapAttributes/MapHttpAttributeRoutes를 호출할 때 지정할 수 있습니다.

IDirectRouteProvider 사용자 지정이 기본 구현 DefaultDirectRouteProvider를 확장 하 여 가장 쉬운 방법은 수 있습니다. 이 클래스는 특성을 검색, 경로 항목을 만들고, 경로 접두사 및 영역 접두사 검색에 대 한 논리를 변경 하는 별도 재정의 가능한 가상 메서드를 제공 합니다.

새 특성 라우팅의 확장성 IDirectRouteProvider 사용 하 여 사용자 다음을 수행할 수 있습니다.

1. 특성 경로 상속을 지원 합니다. 예를 들어, 다음 시나리오에서는 BaseController 정의한는 특성 경로 규칙 블로그 및 저장소 컨트롤러에 사용 하는 합니다. 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. 특성 경로 대 한 경로 이름을 자동으로 생성 합니다. 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. 경로 경로 테이블에 추가 되기 전에 하나의 중앙 위치에서 경로 접두사를 수정 합니다.
4. 검색할 특성 라우팅 하려는 컨트롤러를 필터링 합니다. 바랍니다 3 및 4에 대 한 블로그를 곧.

### <a name="facebook-fixes-for-changed-api-surface"></a>Facebook은 API 화면 변경된에 대 한 수정

MVC Facebook 패키지 [끊기기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) Facebook에서 몇 가지 API 변경으로 인해 합니다. 새 Facebook 패키지 (Microsoft.AspNet.Facebook 1.0.0) 이러한 문제를 해결 하려면 릴리스할 수도 있습니다.

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a>5.2.0 사용 하 여 프로젝트에 스 캐 폴딩 MVC/웹 API 프로젝트에 이미 존재 하지 않는 것에 대 한 5.1.2에서 패키지가 결과 패키지

ASP.NET MVC 5.2.0에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩와 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다. 이전 버전의 ASP.NET 런타임 패키지 (예: 업데이트 2에서 5.1.2)를 사용합니다. 결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (예: 업데이트 2에서 5.1.2)으로 설치 됩니다. 그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩 프로젝트에서 최신 패키지를 덮어쓰지 않습니다. ASP.NET Web API 2.2에 ASP.NET MVC 5.2 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우 Web API 및 ASP.NET MVC의 버전이 일치 하는지 확인 합니다.

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a>JQuery 1.4.1 호환 Microsoft.jQuery.Unobtrusive.Validation의 버전을 찾을 수 없기 때문에 Microsoft.jQuery.Unobtrusive.Validation NuGet 패키지 설치 실패

Microsoft.jQuery.Unobtrusive.Validation 필요한 jQuery &gt;1.8 및 jQuery.Validation = &gt;1.8 =. But,jQuery.Validation (1.8) 필요한 jQuery (&#8805; 1.3.2 &amp; &amp; &#8804; 1.6). 이 인해 NuGet 동시에, JQuery 1.8 및 jQuery.Validation 1.8 설치 하는 경우 실패 합니다. 이 문제를 표시 하는 경우에 jQuery.Validation 버전 간단히 업데이트할 수 있습니다 &gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) 고정 jQuery cap가 먼저 있어야 설치 하려면 Microsoft.jQuery.Unobtrusive.Validation 합니다.

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a>Jquery 합니다. 유효성 검사 nuget 패키지 버전 1.13.0 일부 국제 전자 메일 주소를 인식 하지 않습니다.

1.11.1 jQuery.Validation nuget 패키지 버전에 따라 유효한 전자 메일 주소를 인식 하는 마지막 알려진된 버전이입니다. 모든 이후 버전에서 인식할 수 있도록 못할 수 있습니다. 예를 들어:

전자 메일 주소 국제화 EAI () 표준 (예를 들어 [ &#29992; &#25143; @domain.com ](mailto:&#29992;&#25143;@domain.com))   
 EAI + 국제 리소스 식별자 (IRIs) (예:., [ &#29992; &#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088; &#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))

문제에 보고 됩니다. [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a>Visual Studio 2013의 Razor 보기에 대 한 구문 강조 표시

Visual Studio 2013 업데이트 하지 않고 ASP.NET MVC 5.2를 업데이트 하는 경우 Razor 뷰를 편집 하는 동안 구문 강조 표시에 대 한 Visual Studio 편집기 지원이 제공 되지 않습니다. 이 지원을 받으려면 Visual Studio 2013 업데이트 해야 합니다.

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a>버그 수정 및 사소한 기능 업데이트

여러 버그 수정 및 사소한 기능에도이 릴리스에서 업데이트 합니다. 여기서 전체 목록을 찾을 수 있습니다.

- [5.2 패키지](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a>Microsoft.AspNet.MVC 5.2.2

이 릴리스에 MVC의 모든 새로운 기능이 나 버그 수정은 포함 되어 있지 않습니다. 했습니다를 [웹 페이지의 변경 내용](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) 성능이 크게 향상에 대 한 모든 기타 종속 패키지가 웹 페이지의이 새 버전에 따라 달라 집니다 소유한 것 이후에 업데이트.

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a>ASP.NET MVC 5.2.3 베타

릴리스에 대 한 읽을 수 있습니다 [여기](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)합니다. 이 릴리스에 버그 수정만 포함 됩니다. 사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 해결 된 문제 목록을 확인 합니다.
