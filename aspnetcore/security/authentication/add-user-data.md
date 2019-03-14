---
title: Adicionar, baixar e excluir dados de usuário à identidade em um projeto ASP.NET Core
author: rick-anderson
description: Saiba como adicionar dados personalizados do usuário a identidade em um projeto ASP.NET Core. Exclua dados por GDPR.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 6/16/2018
ms.custom: seodec18
uid: security/authentication/add-user-data
ms.openlocfilehash: 5465117e5db880e8298e6c2075a27699e4081894
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057293"
---
# <a name="add-download-and-delete-custom-user-data-to-identity-in-an-aspnet-core-project"></a><span data-ttu-id="d2792-104">Adicionar, baixar e excluir dados de usuário personalizada à identidade em um projeto ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d2792-104">Add, download, and delete custom user data to Identity in an ASP.NET Core project</span></span>

<span data-ttu-id="d2792-105">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d2792-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d2792-106">Este artigo mostra como:</span><span class="sxs-lookup"><span data-stu-id="d2792-106">This article shows how to:</span></span>

* <span data-ttu-id="d2792-107">Adicione dados de usuário personalizada para um aplicativo web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2792-107">Add custom user data to an ASP.NET Core web app.</span></span>
* <span data-ttu-id="d2792-108">Decore o modelo de dados de usuário personalizada com o [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) para que ele fica automaticamente disponível para download e exclusão de atributo.</span><span class="sxs-lookup"><span data-stu-id="d2792-108">Decorate the custom user data model with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute so it's automatically available for download and deletion.</span></span> <span data-ttu-id="d2792-109">Tornando os dados capazes de ser baixado e excluído ajuda a cumprir [GDPR](xref:security/gdpr) requisitos.</span><span class="sxs-lookup"><span data-stu-id="d2792-109">Making the data able to be downloaded and deleted helps meet [GDPR](xref:security/gdpr) requirements.</span></span>

<span data-ttu-id="d2792-110">O exemplo de projeto é criado a partir de um aplicativo web páginas Razor, mas as instruções são semelhantes para um aplicativo web ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="d2792-110">The project sample is created from a Razor Pages web app, but the instructions are similar for a ASP.NET Core MVC web app.</span></span>

<span data-ttu-id="d2792-111">[Exibir ou baixar código de exemplo](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) ([como baixar](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="d2792-111">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2792-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2792-112">Prerequisites</span></span>

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="d2792-113">Criar um aplicativo Web do Razor</span><span class="sxs-lookup"><span data-stu-id="d2792-113">Create a Razor web app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d2792-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2792-114">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="d2792-115">No menu **Arquivo** do Visual Studio, selecione **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="d2792-115">From the Visual Studio **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="d2792-116">Nomeie o projeto **WebApp1** se você deseja corresponder ao namespace da [baixar exemplo](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) código.</span><span class="sxs-lookup"><span data-stu-id="d2792-116">Name the project **WebApp1** if you want to it match the namespace of the [download sample](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample) code.</span></span>
* <span data-ttu-id="d2792-117">Selecione **aplicativo Web ASP.NET Core** > **Okey**</span><span class="sxs-lookup"><span data-stu-id="d2792-117">Select **ASP.NET Core Web Application** > **OK**</span></span>
* <span data-ttu-id="d2792-118">Selecione **ASP.NET Core 2.1** na lista suspensa</span><span class="sxs-lookup"><span data-stu-id="d2792-118">Select **ASP.NET Core 2.1** in the dropdown</span></span>
* <span data-ttu-id="d2792-119">Selecione **aplicativo Web**  > **Okey**</span><span class="sxs-lookup"><span data-stu-id="d2792-119">Select **Web Application**  > **OK**</span></span>
* <span data-ttu-id="d2792-120">Compile e execute o projeto.</span><span class="sxs-lookup"><span data-stu-id="d2792-120">Build and run the project.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="d2792-121">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="d2792-121">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet new webapp -o WebApp1
```

---

## <a name="run-the-identity-scaffolder"></a><span data-ttu-id="d2792-122">Execute o scaffolder de identidade</span><span class="sxs-lookup"><span data-stu-id="d2792-122">Run the Identity scaffolder</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d2792-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2792-123">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="d2792-124">Partir **Gerenciador de soluções**, clique com botão direito no projeto > **Add** > **New Scaffolded Item**.</span><span class="sxs-lookup"><span data-stu-id="d2792-124">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="d2792-125">No painel à esquerda do **adicionar Scaffold** caixa de diálogo, selecione **identidade** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d2792-125">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="d2792-126">No **identidade de adição** caixa de diálogo, as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="d2792-126">In the **ADD Identity** dialog, the following options:</span></span>
  * <span data-ttu-id="d2792-127">Selecione o arquivo de layout existente *~/Pages/Shared/_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="d2792-127">Select the existing layout  file  *~/Pages/Shared/_Layout.cshtml*</span></span>
  * <span data-ttu-id="d2792-128">Selecione os arquivos a seguir para substituir:</span><span class="sxs-lookup"><span data-stu-id="d2792-128">Select the following files to override:</span></span>
    * <span data-ttu-id="d2792-129">**Conta/registro**</span><span class="sxs-lookup"><span data-stu-id="d2792-129">**Account/Register**</span></span>
    * <span data-ttu-id="d2792-130">**Conta/gerenciar/índice**</span><span class="sxs-lookup"><span data-stu-id="d2792-130">**Account/Manage/Index**</span></span>
  * <span data-ttu-id="d2792-131">Selecione o **+** botão para criar um novo **classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="d2792-131">Select the **+** button to create a new **Data context class**.</span></span> <span data-ttu-id="d2792-132">Aceite o tipo (**WebApp1.Models.WebApp1Context** se o projeto é denominado **WebApp1**).</span><span class="sxs-lookup"><span data-stu-id="d2792-132">Accept the type (**WebApp1.Models.WebApp1Context** if the project is named **WebApp1**).</span></span>
  * <span data-ttu-id="d2792-133">Selecione o **+** botão para criar um novo **classe User**.</span><span class="sxs-lookup"><span data-stu-id="d2792-133">Select the **+** button to create a new **User class**.</span></span> <span data-ttu-id="d2792-134">Aceite o tipo (**WebApp1User** se o projeto é denominado **WebApp1**) > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d2792-134">Accept the type (**WebApp1User** if the project is named **WebApp1**) > **Add**.</span></span>
* <span data-ttu-id="d2792-135">Selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d2792-135">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="d2792-136">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="d2792-136">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="d2792-137">Se você já não tiver instalado o scaffolder de ASP.NET Core, instale-o agora:</span><span class="sxs-lookup"><span data-stu-id="d2792-137">If you have not previously installed the ASP.NET Core scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="d2792-138">Adicione uma referência de pacote ao [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) ao arquivo de projeto (. csproj).</span><span class="sxs-lookup"><span data-stu-id="d2792-138">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (.csproj) file.</span></span> <span data-ttu-id="d2792-139">Execute o seguinte comando no diretório do projeto:</span><span class="sxs-lookup"><span data-stu-id="d2792-139">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="d2792-140">Execute o seguinte comando para listar as opções de scaffolder de identidade:</span><span class="sxs-lookup"><span data-stu-id="d2792-140">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="d2792-141">Na pasta do projeto, execute o scaffolder de identidade:</span><span class="sxs-lookup"><span data-stu-id="d2792-141">In the project folder, run the Identity scaffolder:</span></span>

```cli
dotnet aspnet-codegenerator identity -u WebApp1User -fi Account.Register;Account.Manage.Index
```

-------------

<span data-ttu-id="d2792-142">Siga as instruções da [migrações, UseAuthentication e layout](xref:security/authentication/scaffold-identity#efm) para executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d2792-142">Follow the instruction in [Migrations, UseAuthentication, and layout](xref:security/authentication/scaffold-identity#efm) to perform the following steps:</span></span>

* <span data-ttu-id="d2792-143">Criar uma migração e atualizar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d2792-143">Create a migration and update the database.</span></span>
* <span data-ttu-id="d2792-144">Adicione `UseAuthentication` a `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="d2792-144">Add `UseAuthentication` to `Startup.Configure`.</span></span>
* <span data-ttu-id="d2792-145">Adicionar `<partial name="_LoginPartial" />` ao arquivo de layout.</span><span class="sxs-lookup"><span data-stu-id="d2792-145">Add `<partial name="_LoginPartial" />` to the layout file.</span></span>
* <span data-ttu-id="d2792-146">Teste o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d2792-146">Test the app:</span></span>
  * <span data-ttu-id="d2792-147">Registrar um usuário</span><span class="sxs-lookup"><span data-stu-id="d2792-147">Register a user</span></span>
  * <span data-ttu-id="d2792-148">Selecione o novo nome de usuário (ao lado de **Logout** link).</span><span class="sxs-lookup"><span data-stu-id="d2792-148">Select the new user name (next to the **Logout** link).</span></span> <span data-ttu-id="d2792-149">Talvez você precise expandir a janela ou selecione o ícone da barra de navegação para mostrar o nome de usuário e outros links.</span><span class="sxs-lookup"><span data-stu-id="d2792-149">You might need to expand the window or select the navigation bar icon to show the user name and other links.</span></span>
  * <span data-ttu-id="d2792-150">Selecione o **dados pessoais** guia.</span><span class="sxs-lookup"><span data-stu-id="d2792-150">Select the **Personal Data** tab.</span></span>
  * <span data-ttu-id="d2792-151">Selecione o **Baixe** botão e examinado o *PersonalData.json* arquivo.</span><span class="sxs-lookup"><span data-stu-id="d2792-151">Select the **Download** button and examined the *PersonalData.json* file.</span></span>
  * <span data-ttu-id="d2792-152">Teste o **excluir** botão, que exclui o fez logon de usuário.</span><span class="sxs-lookup"><span data-stu-id="d2792-152">Test the **Delete** button, which deletes the logged on user.</span></span>

## <a name="add-custom-user-data-to-the-identity-db"></a><span data-ttu-id="d2792-153">Adicionar dados de usuário personalizada para o banco de dados de identidade</span><span class="sxs-lookup"><span data-stu-id="d2792-153">Add custom user data to the Identity DB</span></span>

<span data-ttu-id="d2792-154">Atualização de `IdentityUser` derivado da classe com propriedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d2792-154">Update the `IdentityUser` derived class with custom properties.</span></span> <span data-ttu-id="d2792-155">Se você nomeou o projeto WebApp1, o arquivo é nomeado *Areas/Identity/Data/WebApp1User.cs*.</span><span class="sxs-lookup"><span data-stu-id="d2792-155">If you named the project WebApp1, the file is named *Areas/Identity/Data/WebApp1User.cs*.</span></span> <span data-ttu-id="d2792-156">Atualize o arquivo com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2792-156">Update the file with the following code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Data/WebApp1User.cs)]

<span data-ttu-id="d2792-157">As propriedades decoradas com o [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) atributo são:</span><span class="sxs-lookup"><span data-stu-id="d2792-157">Properties decorated with the [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1) attribute are:</span></span>

* <span data-ttu-id="d2792-158">Excluído, quando o *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* página do Razor chama `UserManager.Delete`.</span><span class="sxs-lookup"><span data-stu-id="d2792-158">Deleted when the *Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor Page calls `UserManager.Delete`.</span></span>
* <span data-ttu-id="d2792-159">Incluído nos dados baixados pela *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* página do Razor.</span><span class="sxs-lookup"><span data-stu-id="d2792-159">Included in the downloaded data by the *Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor Page.</span></span>

### <a name="update-the-accountmanageindexcshtml-page"></a><span data-ttu-id="d2792-160">Atualizar a página Account/Manage/Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d2792-160">Update the Account/Manage/Index.cshtml page</span></span>

<span data-ttu-id="d2792-161">Atualizar o `InputModel` na *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* com o seguinte código realçado:</span><span class="sxs-lookup"><span data-stu-id="d2792-161">Update the `InputModel` in *Areas/Identity/Pages/Account/Manage/Index.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml.cs?name=snippet&highlight=28-36,63-64,87-95,120)]

<span data-ttu-id="d2792-162">Atualizar o *Areas/Identity/Pages/Account/Manage/Index.cshtml* com a seguinte marcação realçada:</span><span class="sxs-lookup"><span data-stu-id="d2792-162">Update the *Areas/Identity/Pages/Account/Manage/Index.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml?highlight=34-41)]

### <a name="update-the-accountregistercshtml-page"></a><span data-ttu-id="d2792-163">Atualizar a página Register</span><span class="sxs-lookup"><span data-stu-id="d2792-163">Update the Account/Register.cshtml page</span></span>

<span data-ttu-id="d2792-164">Atualizar o `InputModel` na *Areas/Identity/Pages/Account/Register.cshtml.cs* com o seguinte código realçado:</span><span class="sxs-lookup"><span data-stu-id="d2792-164">Update the `InputModel` in *Areas/Identity/Pages/Account/Register.cshtml.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=8-16,43,44)]

<span data-ttu-id="d2792-165">Atualizar o *Areas/Identity/Pages/Account/Register.cshtml* com a seguinte marcação realçada:</span><span class="sxs-lookup"><span data-stu-id="d2792-165">Update the *Areas/Identity/Pages/Account/Register.cshtml* with the following highlighted markup:</span></span>

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml?highlight=16-25)]

<span data-ttu-id="d2792-166">Compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="d2792-166">Build the project.</span></span>

### <a name="add-a-migration-for-the-custom-user-data"></a><span data-ttu-id="d2792-167">Adicionar uma migração para os dados de usuário personalizada</span><span class="sxs-lookup"><span data-stu-id="d2792-167">Add a migration for the custom user data</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d2792-168">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2792-168">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="d2792-169">No Visual Studio **Package Manager Console**:</span><span class="sxs-lookup"><span data-stu-id="d2792-169">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CustomUserData
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="d2792-170">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="d2792-170">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CustomUserData
dotnet ef database update
```

------

## <a name="test-create-view-download-delete-custom-user-data"></a><span data-ttu-id="d2792-171">Teste de criar, exibir, baixar, excluir dados de usuário personalizada</span><span class="sxs-lookup"><span data-stu-id="d2792-171">Test create, view, download, delete custom user data</span></span>

<span data-ttu-id="d2792-172">Teste o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d2792-172">Test the app:</span></span>

* <span data-ttu-id="d2792-173">Registre um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="d2792-173">Register a new user.</span></span>
* <span data-ttu-id="d2792-174">Exibir os dados de usuário personalizada no `/Identity/Account/Manage` página.</span><span class="sxs-lookup"><span data-stu-id="d2792-174">View the custom user data on the `/Identity/Account/Manage` page.</span></span>
* <span data-ttu-id="d2792-175">Baixar e exibir os dados pessoais de usuários da `/Identity/Account/Manage/PersonalData` página.</span><span class="sxs-lookup"><span data-stu-id="d2792-175">Download and view the users personal data from the `/Identity/Account/Manage/PersonalData` page.</span></span>
