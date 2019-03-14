---
ms.openlocfilehash: e5c80c80380dadfce9cff5ec268535076258d980
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041113"
---
<span data-ttu-id="1e4c9-101">Execute o scaffolder de identidade:</span><span class="sxs-lookup"><span data-stu-id="1e4c9-101">Run the Identity scaffolder:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1e4c9-102">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e4c9-102">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="1e4c9-103">Partir **Gerenciador de soluções**, clique com botão direito no projeto > **Add** > **New Scaffolded Item**.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-103">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="1e4c9-104">No painel à esquerda do **adicionar Scaffold** caixa de diálogo, selecione **identidade** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-104">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="1e4c9-105">No **identidade de adição** caixa de diálogo, selecione as opções desejadas.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-105">In the **ADD Identity** dialog, select the options you want.</span></span>
  * <span data-ttu-id="1e4c9-106">Selecione a página de layout existente ou seu arquivo de layout será substituído pela marcação incorreta.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-106">Select your existing layout page, or your layout file will be overwritten with incorrect markup.</span></span> <span data-ttu-id="1e4c9-107">Por exemplo `~/Pages/Shared/_Layout.cshtml` para as páginas Razor `~/Views/Shared/_Layout.cshtml` para projetos MVC</span><span class="sxs-lookup"><span data-stu-id="1e4c9-107">For example `~/Pages/Shared/_Layout.cshtml` for Razor Pages `~/Views/Shared/_Layout.cshtml` for MVC projects</span></span>
  * <span data-ttu-id="1e4c9-108">Selecione o **+** botão para criar um novo **classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-108">Select the **+** button to create a new **Data context class**.</span></span>
* <span data-ttu-id="1e4c9-109">Selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-109">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="1e4c9-110">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="1e4c9-110">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="1e4c9-111">Se você já não tiver instalado o scaffolder de ASP.NET Core, instale-o agora:</span><span class="sxs-lookup"><span data-stu-id="1e4c9-111">If you have not previously installed the ASP.NET Core scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="1e4c9-112">Adicione uma referência de pacote ao [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) ao projeto (\*. csproj) arquivos.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-112">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (\*.csproj) file.</span></span> <span data-ttu-id="1e4c9-113">Execute o seguinte comando no diretório do projeto:</span><span class="sxs-lookup"><span data-stu-id="1e4c9-113">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="1e4c9-114">Execute o seguinte comando para listar as opções de scaffolder de identidade:</span><span class="sxs-lookup"><span data-stu-id="1e4c9-114">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="1e4c9-115">Na pasta do projeto, execute o scaffolder de identidade com as opções desejadas.</span><span class="sxs-lookup"><span data-stu-id="1e4c9-115">In the project folder, run the Identity scaffolder with the options you want.</span></span> <span data-ttu-id="1e4c9-116">Por exemplo, para configurar a identidade com a interface do usuário padrão e o número mínimo de arquivos, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="1e4c9-116">For example, to setup identity with the default UI and the minimum number of files, run the following command:</span></span>

```cli
dotnet aspnet-codegenerator identity --useDefaultUI
```

-------------
