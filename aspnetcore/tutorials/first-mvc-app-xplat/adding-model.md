---
title: ASP.NET Core MVC 앱에 모델 추가
author: rick-anderson
description: 간단한 ASP.NET Core 앱에 모델을 추가합니다.
ms.author: riande
ms.date: 09/18/2017
uid: tutorials/first-mvc-app-xplat/adding-model
ms.openlocfilehash: 82b8338f10cb4d58ae06bdb70583e1563c2e6b64
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961427"
---
[!INCLUDE [adding-model1](../../includes/mvc-intro/adding-model1.md)]

* *Models* 폴더에 *Movie.cs* 클래스를 추가합니다.
* *Models/Movie.cs* 파일에 다음 코드를 추가합니다.

[!code-csharp[](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

`ID` 필드는 데이터베이스에서 기본 키 대신 필요합니다. 

앱을 빌드하여 오류가 없고 마지막으로 **모**델을 **M**VC 앱에 추가했는지 확인합니다.

## <a name="prepare-the-project-for-scaffolding"></a>프로젝트에서 스캐폴딩을 준비합니다.

- 다음 강조 표시된 NuGet 패키지를 *MvcMovie.csproj* 파일에 추가합니다.
             
   [!code-csharp[](start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- 파일을 저장하고 다음 **정보** 메시지에 대해 **복원**을 선택합니다. “확인되지 않은 종속성이 있습니다.”
- *Models/MvcMovieContext.cs* 파일을 만들고 다음 `MvcMovieContext` 클래스를 추가합니다.

   [!code-csharp[](start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]
   
- *Startup.cs* 파일을 열고 두 개의 using을 추가합니다.

   [!code-csharp[](start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]

- 데이터베이스 컨텍스트를 *Startup.cs* 파일에 추가합니다.

   [!code-csharp[](start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  이 코드는 데이터 모델에 포함되는 모델 클래스를 Entity Framework에 알립니다. 데이터베이스에서 Movie 테이블을 표현할 Movie 개체의 *엔터티 집합* 하나를 정의하고 있습니다.

- 프로젝트를 빌드하여 오류가 없는지 확인합니다.

## <a name="scaffold-the-moviecontroller"></a>MovieController 스캐폴드

프로젝트 폴더에서 터미널 창을 열고 다음 명령을 실행합니다.

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
스캐폴딩 엔진은 다음을 만듭니다.

* 동영상 컨트롤러(*Controllers/MoviesController.cs*)
* 만들기, 삭제, 세부 정보, 편집 및 인덱스 페이지에 대한 Razor 뷰 파일(*Views/Movies/\*.cshtml*)

[CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)(만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 자동으로 만드는 작업을 *스캐폴딩*이라고 합니다. 동영상 데이터베이스를 관리할 수 있는 완벽하게 작동하는 웹 응용 프로그램이 곧 제공됩니다.

[!INCLUDE [adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE [adding-model](../../includes/mvc-intro/adding-model3.md)]

이제 데이터를 표시, 편집, 업데이트 및 삭제할 데이터베이스 및 페이지가 제공됩니다. 다음 자습서에서는 데이터베이스 작업을 수행합니다.

### <a name="additional-resources"></a>추가 자료

* [태그 도우미](xref:mvc/views/tag-helpers/intro)
* [전역화 및 지역화](xref:fundamentals/localization)

> [!div class="step-by-step"]
> [이전 - 뷰 추가](adding-view.md)
> [다음 - SQLite 사용](working-with-sql.md)
