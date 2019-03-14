---
ms.openlocfilehash: 6ceb4bd6580d11ee5d6ff57a895c499308035858
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064033"
---
# <a name="aspnet-core-authorization-sample"></a>Amostra de autorização do ASP.NET Core

Este exemplo ilustra o uso de autorização de páginas do Razor por convenções. Este exemplo demonstra os recursos descritos a [convenções de autorização de páginas do Razor](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization) tópico.

Autorização de usuário neste exemplo usa a autenticação de cookie recursos descritos a [usar a autenticação de cookie sem o ASP.NET Core Identity](https://docs.microsoft.com/aspnet/core/security/authentication/cookie) tópico. Para obter informações sobre como usar o ASP.NET Core Identity, consulte <xref:security/authentication/identity>.

Ao executar o exemplo, use o endereço de email **maria.rodriguez@contoso.com** para autenticar o usuário.

## <a name="examples-in-this-sample"></a>Exemplos desta amostra

| Recurso | Descrição |
| --- | --- |
| [AuthorizePage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage) | Adiciona uma [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) para a página com o caminho especificado. |
| [AuthorizeFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizefolder) | Adiciona uma [AuthorizeFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter) para todas as páginas em uma pasta com o caminho especificado. |
| [AllowAnonymousToPage](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustopage) | Adiciona uma [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) para uma página com o caminho especificado. |
| [AllowAnonymousToFolder](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.allowanonymoustofolder) | Adiciona uma [AllowAnonymousFilter](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.authorization.allowanonymousfilter) para todas as páginas em uma pasta com o caminho especificado. |
