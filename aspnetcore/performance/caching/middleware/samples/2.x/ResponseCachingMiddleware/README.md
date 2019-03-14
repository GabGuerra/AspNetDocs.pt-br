---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062713"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="9b81d-101">Exemplo de cache de resposta do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9b81d-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="9b81d-102">Este exemplo ilustra o uso do ASP.NET Core [Middleware de cache de resposta](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="9b81d-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="9b81d-103">O aplicativo responde com a página de índice, incluindo um `Cache-Control` cabeçalho para configurar o comportamento do cache.</span><span class="sxs-lookup"><span data-stu-id="9b81d-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="9b81d-104">O aplicativo também define o `Vary` cabeçalho para configurar o cache para servir a resposta somente se o `Accept-Encoding` cabeçalho das solicitações subsequentes corresponde da solicitação original.</span><span class="sxs-lookup"><span data-stu-id="9b81d-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="9b81d-105">Ao executar o exemplo, a página de índice for atendida do cache quando armazenados e armazenado em cache por até 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="9b81d-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
