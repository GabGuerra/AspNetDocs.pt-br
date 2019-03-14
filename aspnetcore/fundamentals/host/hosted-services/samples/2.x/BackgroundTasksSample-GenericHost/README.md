---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056483"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="a02b0-101">Exemplo de tarefas em segundo plano do ASP.NET Core (host genérico)</span><span class="sxs-lookup"><span data-stu-id="a02b0-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="a02b0-102">Este exemplo ilustra o uso de [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span><span class="sxs-lookup"><span data-stu-id="a02b0-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="a02b0-103">Este exemplo demonstra os recursos descritos no tópico [Tarefas em segundo plano com serviços hospedados no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services).</span><span class="sxs-lookup"><span data-stu-id="a02b0-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="a02b0-104">Ao executar o exemplo no [Visual Studio Code](https://code.visualstudio.com/), defina o valor **console** da configuração de console em *.vscode/launch.json* como `externalTerminal` ou `integratedTerminal`.</span><span class="sxs-lookup"><span data-stu-id="a02b0-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="a02b0-105">Usar o `internalConsole` é incompatível com a entrada por pressionamento de tecla do console que o aplicativo usa para enfileirar itens de trabalho em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a02b0-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
