---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Hospedar OWIN em uma função de trabalho do Azure | Microsoft Docs
author: MikeWasson
description: Este tutorial mostra como hospedar internamente o OWIN em uma função de trabalho do Microsoft Azure. Open Web Interface para .NET (OWIN) define uma abstração entre o servidor de web do .NET...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 129b6a8f411d482de75e7e5edc5cc919b4d2de52
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419516"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="74591-104">Hospedar OWIN em uma função de trabalho do Azure</span><span class="sxs-lookup"><span data-stu-id="74591-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="74591-105">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="74591-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="74591-106">Este tutorial mostra como hospedar internamente o OWIN em uma função de trabalho do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="74591-107">[Open Web Interface para .NET](http://owin.org/) (OWIN) define uma abstração entre servidores de web do .NET e aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="74591-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="74591-108">OWIN separa o aplicativo web do servidor, o que torna o OWIN ideal para auto-hospedagem em um aplicativo web em seu próprio processo, fora do IIS – por exemplo, dentro de uma função de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="74591-109">Neste tutorial, você aprenderá como hospedar internamente um aplicativos OWIN dentro de uma função de trabalho do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="74591-110">Para saber mais sobre as funções de trabalho, consulte [modelos de execução do Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span><span class="sxs-lookup"><span data-stu-id="74591-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="74591-111">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="74591-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="74591-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="74591-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="74591-113">SDK do Azure para .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="74591-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="74591-114">Microsoft.Owin.Selfhost 2.1.0</span><span class="sxs-lookup"><span data-stu-id="74591-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)


## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="74591-115">Criar um projeto do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="74591-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="74591-116">Inicie o Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="74591-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="74591-117">Privilégios de administrador são necessárias para depurar o aplicativo localmente, usando o emulador de computação do Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-117">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="74591-118">No **arquivo** menu, clique em **New**, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="74591-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="74591-119">Partir **modelos instalados**, no Visual c#, clique em **nuvem** e, em seguida, clique em **serviço de nuvem do Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="74591-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="74591-120">Nomeie o projeto "AzureApp" e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="74591-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="74591-121">No **novo serviço de nuvem do Windows Azure** caixa de diálogo, clique duas vezes em **função de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="74591-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="74591-122">Deixe o nome padrão ("WorkerRole1").</span><span class="sxs-lookup"><span data-stu-id="74591-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="74591-123">Esta etapa adiciona uma função de trabalho à solução.</span><span class="sxs-lookup"><span data-stu-id="74591-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="74591-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="74591-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="74591-125">A solução do Visual Studio criado contém dois projetos:</span><span class="sxs-lookup"><span data-stu-id="74591-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="74591-126">&quot;AzureApp&quot; define as funções e a configuração para o aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="74591-127">&quot;WorkerRole1&quot; contém o código da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="74591-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="74591-128">Em geral, um aplicativo do Azure pode conter várias funções, embora este tutorial usa uma única função.</span><span class="sxs-lookup"><span data-stu-id="74591-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="74591-129">Adicione os pacotes de auto-hospedagem de OWIN</span><span class="sxs-lookup"><span data-stu-id="74591-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="74591-130">Do **ferramentas** menu, clique em **Gerenciador de pacotes NuGet**, em seguida, clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="74591-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="74591-131">Na janela do Console do Gerenciador de pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="74591-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="74591-132">Adicionar um ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="74591-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="74591-133">No Gerenciador de soluções, expanda o projeto AzureApp.</span><span class="sxs-lookup"><span data-stu-id="74591-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="74591-134">Expanda o nó funções, WorkerRole1 com o botão direito e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="74591-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="74591-135">Clique em **pontos de extremidade**e, em seguida, clique em **Adicionar ponto de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="74591-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="74591-136">No **protocolo** lista suspensa, selecione "http".</span><span class="sxs-lookup"><span data-stu-id="74591-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="74591-137">Na **porta pública** e **porta privada**, digite 80.</span><span class="sxs-lookup"><span data-stu-id="74591-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="74591-138">Esses números de porta podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="74591-138">These port numbers can be different.</span></span> <span data-ttu-id="74591-139">A porta pública é o que os clientes usam quando eles enviam uma solicitação para a função.</span><span class="sxs-lookup"><span data-stu-id="74591-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="74591-140">Criar a classe de inicialização OWIN</span><span class="sxs-lookup"><span data-stu-id="74591-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="74591-141">No Gerenciador de soluções, com o botão direito do mouse no projeto WorkerRole1 e selecione **Add** / **classe** para adicionar uma nova classe.</span><span class="sxs-lookup"><span data-stu-id="74591-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="74591-142">Nomeie a classe `Startup`.</span><span class="sxs-lookup"><span data-stu-id="74591-142">Name the class `Startup`.</span></span>

<span data-ttu-id="74591-143">Substitua todo o código clichê com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="74591-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="74591-144">O `UseWelcomePage` método de extensão adiciona uma página HTML simples ao seu aplicativo, para verificar se o site está funcionando.</span><span class="sxs-lookup"><span data-stu-id="74591-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="74591-145">Iniciar o Host OWIN</span><span class="sxs-lookup"><span data-stu-id="74591-145">Start the OWIN Host</span></span>

<span data-ttu-id="74591-146">Abra o arquivo WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="74591-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="74591-147">Essa classe define o código que é executado quando a função de trabalho é iniciada e parada.</span><span class="sxs-lookup"><span data-stu-id="74591-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="74591-148">Adicione a seguinte instrução using:</span><span class="sxs-lookup"><span data-stu-id="74591-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="74591-149">Adicionar um **IDisposable** membro para o `WorkerRole` classe:</span><span class="sxs-lookup"><span data-stu-id="74591-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="74591-150">No `OnStart` método, adicione o seguinte código para iniciar o host:</span><span class="sxs-lookup"><span data-stu-id="74591-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="74591-151">O **WebApp.Start** método inicia o host do OWIN.</span><span class="sxs-lookup"><span data-stu-id="74591-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="74591-152">O nome da `Startup` classe é um parâmetro de tipo para o método.</span><span class="sxs-lookup"><span data-stu-id="74591-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="74591-153">Por convenção, o host chamará o `Configure` método dessa classe.</span><span class="sxs-lookup"><span data-stu-id="74591-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="74591-154">Substituir a `OnStop` descartar o  *\_aplicativo* instância:</span><span class="sxs-lookup"><span data-stu-id="74591-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="74591-155">Aqui está o código completo para WorkerRole.cs:</span><span class="sxs-lookup"><span data-stu-id="74591-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="74591-156">Compile a solução e pressione F5 para executar o aplicativo localmente no emulador de computação do Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="74591-157">Dependendo de suas configurações de firewall, você precisa permitir que o emulador através do firewall.</span><span class="sxs-lookup"><span data-stu-id="74591-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="74591-158">O emulador de computação atribui um endereço IP local para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="74591-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="74591-159">Você pode encontrar o endereço IP, exibindo a interface de usuário do emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="74591-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="74591-160">Clique com botão direito no ícone do emulador na tarefa de área de notificação da barra e, em seguida, selecione **mostrar IU do emulador de computação**.</span><span class="sxs-lookup"><span data-stu-id="74591-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="74591-161">Localize o endereço IP em implantações de serviços de implantação [id], detalhes do serviço.</span><span class="sxs-lookup"><span data-stu-id="74591-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="74591-162">Abra um navegador da web e navegue para http:\/\/*endereço*, onde *endereço* é o endereço IP atribuído pelo emulador de computação; por exemplo, `http://127.0.0.1:80`.</span><span class="sxs-lookup"><span data-stu-id="74591-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="74591-163">Você verá a página de boas-vinda do OWIN:</span><span class="sxs-lookup"><span data-stu-id="74591-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="74591-164">Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="74591-164">Deploy to Azure</span></span>

<span data-ttu-id="74591-165">Para esta etapa, você deve ter uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="74591-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="74591-166">Se você ainda não tiver uma, você pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="74591-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="74591-167">Para obter detalhes, consulte [avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="74591-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="74591-168">No Gerenciador de soluções, clique com botão direito no projeto AzureApp.</span><span class="sxs-lookup"><span data-stu-id="74591-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="74591-169">Selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="74591-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="74591-170">Se você não estiver conectado à sua conta do Azure, clique em **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="74591-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="74591-171">Depois que você está conectado, escolha uma assinatura e clique em **próxima**.</span><span class="sxs-lookup"><span data-stu-id="74591-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="74591-172">Insira um nome para o serviço de nuvem e escolha uma região.</span><span class="sxs-lookup"><span data-stu-id="74591-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="74591-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="74591-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="74591-174">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="74591-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="74591-175">A janela de Log de atividades do Azure mostra o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="74591-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="74591-176">Quando o aplicativo é implantado, navegue até `http://appname.cloudapp.net/`, onde *appname* é o nome do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="74591-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74591-177">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="74591-177">Additional Resources</span></span>

- [<span data-ttu-id="74591-178">Uma visão geral do projeto Katana</span><span class="sxs-lookup"><span data-stu-id="74591-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="74591-179">Projeto Katana no GitHub</span><span class="sxs-lookup"><span data-stu-id="74591-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
