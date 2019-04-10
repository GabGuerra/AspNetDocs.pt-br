---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Implantando um aplicativo da Web ASP.NET com o SQL Server Compact usando o Visual Studio ou Visual Web Developer: Implantando uma atualização somente de código – 8 de 12 | Microsoft Docs'
author: tdykstra
description: Esta série de tutoriais mostra como implantar (publicar) um ASP.NET projeto de aplicativo web que inclui um banco de dados do SQL Server Compact usando o Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: f06fd5d28613ba8f881df2d1422fead2fff8c35f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59399886"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="06718-103">Implantando um aplicativo da Web ASP.NET com o SQL Server Compact usando o Visual Studio ou Visual Web Developer: Implantando uma atualização somente de código – 8 de 12</span><span class="sxs-lookup"><span data-stu-id="06718-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="06718-104">por [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="06718-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="06718-105">Baixe o projeto inicial</span><span class="sxs-lookup"><span data-stu-id="06718-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="06718-106">Esta série de tutoriais mostra como implantar (publicar) um ASP.NET projeto de aplicativo web que inclui um banco de dados do SQL Server Compact usando o Visual Studio 2012 RC ou Visual Studio Express 2012 RC para Web.</span><span class="sxs-lookup"><span data-stu-id="06718-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="06718-107">Você também pode usar o Visual Studio 2010 se você instalar a atualização de publicação na Web.</span><span class="sxs-lookup"><span data-stu-id="06718-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="06718-108">Para obter uma introdução à série, consulte [o primeiro tutorial na série](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="06718-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="06718-109">Para obter um tutorial que mostra os recursos de implantação introduzidos após a versão RC do Visual Studio 2012, mostra como implantar as edições do SQL Server que não seja o SQL Server Compact e mostra como implantar aplicativos de Web do serviço de aplicativo do Azure, consulte [implantação da Web do ASP.NET usando o Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06718-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="06718-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="06718-110">Overview</span></span>

<span data-ttu-id="06718-111">Após a implantação inicial, continua seu trabalho de manutenção e desenvolvimento de seu site da web e pouco tempo você deseja implantar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="06718-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="06718-112">Este tutorial o guiará durante o processo de implantação de uma atualização para o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06718-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="06718-113">Esta atualização não envolve uma alteração de banco de dados; Você verá o que é diferente sobre como implantar uma alteração de banco de dados no próximo tutorial.</span><span class="sxs-lookup"><span data-stu-id="06718-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="06718-114">Lembrete: Se você receber uma mensagem de erro ou se algo não funciona ao percorrer o tutorial, certifique-se de verificar a [página de solução de problemas](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="06718-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="06718-115">Fazer uma alteração de código</span><span class="sxs-lookup"><span data-stu-id="06718-115">Making a Code Change</span></span>

<span data-ttu-id="06718-116">Como um exemplo simples de uma atualização para o seu aplicativo, você adicionará a **instrutores** página uma lista de cursos ministrados pelo instrutor selecionado.</span><span class="sxs-lookup"><span data-stu-id="06718-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="06718-117">Se você executar o **instrutores** página, você observará que há **selecione** links na grade, mas eles não fazem nada diferente de marca a linha cinza de turno em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="06718-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

[![I<span data-ttu-id="06718-118">nstructors_page]</span><span class="sxs-lookup"><span data-stu-id="06718-118">nstructors_page]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

<span data-ttu-id="06718-119">Agora você adicionará código que é executada quando o **selecionar** link é clicado e exibe uma lista de cursos ministrados pelo instrutor selecionado.</span><span class="sxs-lookup"><span data-stu-id="06718-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="06718-120">Na *Instructors.aspx*, adicione a seguinte marcação imediatamente após o **ErrorMessageLabel** `Label` controle:</span><span class="sxs-lookup"><span data-stu-id="06718-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="06718-121">Execute a página e selecione um instrutor.</span><span class="sxs-lookup"><span data-stu-id="06718-121">Run the page and select an instructor.</span></span> <span data-ttu-id="06718-122">Você ver uma lista de cursos ministrados por instrutor.</span><span class="sxs-lookup"><span data-stu-id="06718-122">You see a list of courses taught by that instructor.</span></span>

[![I<span data-ttu-id="06718-123">nstructors_page_with_courses]</span><span class="sxs-lookup"><span data-stu-id="06718-123">nstructors_page_with_courses]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="06718-124">Implantar a atualização de código para o ambiente de teste</span><span class="sxs-lookup"><span data-stu-id="06718-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="06718-125">A implantação no ambiente de teste é uma simples questão de execução em um único clique publique novamente.</span><span class="sxs-lookup"><span data-stu-id="06718-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="06718-126">Para tornar esse processo mais rápido, você pode usar o **publicação Web com um clique** barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="06718-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="06718-127">No **modo de exibição** menu, escolha **barras de ferramentas** e, em seguida, selecione **publicação Web com um clique**.</span><span class="sxs-lookup"><span data-stu-id="06718-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="06718-129">Na **Gerenciador de soluções**, selecione o projeto ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="06718-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="06718-130">o **publicação Web com um clique em** barra de ferramentas, escolha o **teste** perfil de publicação e, em seguida, clique em **publicar na Web** (o ícone com setas apontando para a esquerda e direita).</span><span class="sxs-lookup"><span data-stu-id="06718-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="06718-132">O Visual Studio implanta o aplicativo atualizado e o navegador é aberto automaticamente para a home page.</span><span class="sxs-lookup"><span data-stu-id="06718-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="06718-133">Execute a página instrutores e selecione um instrutor para verificar se a atualização foi implantada com êxito.</span><span class="sxs-lookup"><span data-stu-id="06718-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

[![I<span data-ttu-id="06718-134">nstructors_page_with_courses_Test]</span><span class="sxs-lookup"><span data-stu-id="06718-134">nstructors_page_with_courses_Test]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

<span data-ttu-id="06718-135">Você faria normalmente também fazer testes de regressão (ou seja, teste o restante do site para certificar-se de que a nova alteração não quebra nenhuma funcionalidade existente).</span><span class="sxs-lookup"><span data-stu-id="06718-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="06718-136">Mas para este tutorial, você vai ignorar essa etapa e continuar para implantar a atualização para a produção.</span><span class="sxs-lookup"><span data-stu-id="06718-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="06718-137">Impedindo a reimplantação do estado inicial do banco de dados para a produção</span><span class="sxs-lookup"><span data-stu-id="06718-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="06718-138">Em um aplicativo real, os usuários interagem com seu site de produção após a implantação inicial e os bancos de dados são preenchidos com dados dinâmicos.</span><span class="sxs-lookup"><span data-stu-id="06718-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="06718-139">Portanto, você não deseja reimplantar o banco de dados de associação em seu estado inicial, o que seria apagar todos os dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="06718-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="06718-140">Já que os bancos de dados do SQL Server Compact são arquivos no *App\_dados* pasta, você precisa evitar isso, alterando as configurações de implantação para que arquivos no *App\_dados* pasta não são implantados.</span><span class="sxs-lookup"><span data-stu-id="06718-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="06718-141">Abra o **propriedades do projeto** janela para o projeto ContosoUniversity e selecione o **pacote/Publicar Web** guia. Certifique-se de que o **Configuration** caixa suspensa foi **Active Directory (versão)** ou **versão** selecionado, selecione **excluir arquivos do aplicativo\_Pasta de dados**.</span><span class="sxs-lookup"><span data-stu-id="06718-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="06718-143">No caso de você optar por implantar uma compilação de depuração no futuro, é uma boa ideia fazer a mesma alteração para a configuração de build de depuração: altere **Configuration** para **Debug** e, em seguida, selecione **excluir arquivos do aplicativo\_pasta de dados**.</span><span class="sxs-lookup"><span data-stu-id="06718-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="06718-144">Salve e feche o **empacotar/Publicar Web** guia.</span><span class="sxs-lookup"><span data-stu-id="06718-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="06718-145">Certifique-se de que você não tem **remover arquivos adicionais no destino** selecionado em seus perfis de publicação.</span><span class="sxs-lookup"><span data-stu-id="06718-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="06718-146">Se você selecionar essa opção, o processo de implantação excluirá os bancos de dados que você tem no aplicativo\_dados no site implantado e ele excluirá o aplicativo\_própria pasta de dados.</span><span class="sxs-lookup"><span data-stu-id="06718-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>


## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="06718-147">Impedindo o acesso de usuário ao Site de produção durante a atualização</span><span class="sxs-lookup"><span data-stu-id="06718-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="06718-148">Agora, a alteração que você está implantando é uma alteração simple em uma única página.</span><span class="sxs-lookup"><span data-stu-id="06718-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="06718-149">Mas, às vezes, você pode implantar alterações maiores e, nesse caso, o site pode se comportar de forma estranha se um usuário solicita uma página antes da implantação for concluída.</span><span class="sxs-lookup"><span data-stu-id="06718-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="06718-150">Para evitar isso, você pode usar um *app\_offline.htm* arquivo.</span><span class="sxs-lookup"><span data-stu-id="06718-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="06718-151">Quando você colocar um arquivo chamado *app\_offline.htm* na pasta raiz do seu aplicativo, o IIS exibe automaticamente esse arquivo em vez de executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06718-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="06718-152">Então, para impedir o acesso durante a implantação, coloque *app\_offline.htm* na pasta raiz, execute o processo de implantação e, em seguida, remova *app\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="06718-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="06718-153">Na **Gerenciador de soluções**, a solução (não um dos projetos) com o botão direito e selecione **nova pasta de solução**.</span><span class="sxs-lookup"><span data-stu-id="06718-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="06718-155">Nomeie a pasta *SolutionFiles*.</span><span class="sxs-lookup"><span data-stu-id="06718-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="06718-156">Na nova pasta, crie uma página HTML chamada *app\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="06718-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="06718-157">Substitua o conteúdo existente com a seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="06718-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="06718-158">Você pode copiar o *app\_offline.htm* arquivo para o site usando uma conexão de FTP ou o **Gerenciador de arquivos** utilitário no painel de controle do provedor de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="06718-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="06718-159">Para este tutorial, você usará o **Gerenciador de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="06718-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="06718-160">Abra o painel de controle e selecione **Gerenciador de arquivos** como fez na [implantando no ambiente de produção](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="06718-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="06718-161">Selecione **contosouniversity.com** e, em seguida **wwwroot** para obter a pasta raiz do seu aplicativo e, em seguida, clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="06718-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

[![U<span data-ttu-id="06718-162">pload_button_in_File_Manager]</span><span class="sxs-lookup"><span data-stu-id="06718-162">pload_button_in_File_Manager]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

<span data-ttu-id="06718-163">No **carregar arquivo** caixa de diálogo, selecione o *app\_offline.htm* de arquivo e, em seguida, clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="06718-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

[![U<span data-ttu-id="06718-164">pload_dialog_box_in_File_Manager]</span><span class="sxs-lookup"><span data-stu-id="06718-164">pload_dialog_box_in_File_Manager]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

<span data-ttu-id="06718-165">Navegue até a URL do site.</span><span class="sxs-lookup"><span data-stu-id="06718-165">Browse to your site's URL.</span></span> <span data-ttu-id="06718-166">Você verá que o *app\_offline.htm* página agora é exibida em vez de sua home page.</span><span class="sxs-lookup"><span data-stu-id="06718-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

[![A<span data-ttu-id="06718-167">pp_offline.htm_page_in_production]</span><span class="sxs-lookup"><span data-stu-id="06718-167">pp_offline.htm_page_in_production]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

<span data-ttu-id="06718-168">Agora você está pronto para implantar em produção.</span><span class="sxs-lookup"><span data-stu-id="06718-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="06718-169">Implantar a atualização de código para o ambiente de produção</span><span class="sxs-lookup"><span data-stu-id="06718-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="06718-170">No **publicação Web com um clique em** barra de ferramentas, escolha o **produção** perfil de publicação e, em seguida, clique em **publicar na Web**.</span><span class="sxs-lookup"><span data-stu-id="06718-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="06718-171">Visual Studio implanta o aplicativo atualizado e abre o navegador para a home page do site.</span><span class="sxs-lookup"><span data-stu-id="06718-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="06718-172">O *app\_offline.htm* arquivo é exibido.</span><span class="sxs-lookup"><span data-stu-id="06718-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="06718-173">Antes de poder testar para verificar a implantação bem-sucedida, você deve remover o *app\_offline.htm* arquivo.</span><span class="sxs-lookup"><span data-stu-id="06718-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="06718-174">Volte para o **Gerenciador de arquivos** aplicativo no painel de controle.</span><span class="sxs-lookup"><span data-stu-id="06718-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="06718-175">Selecione **contosouniversity.com** e **wwwroot**, selecione **aplicativo\_offline.htm**e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="06718-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

[![D<span data-ttu-id="06718-176">eleting_app_offline.htm]</span><span class="sxs-lookup"><span data-stu-id="06718-176">eleting_app_offline.htm]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

<span data-ttu-id="06718-177">No navegador, abra a página instrutores no site público e selecione um instrutor para verificar se a atualização foi implantada com êxito.</span><span class="sxs-lookup"><span data-stu-id="06718-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

[![I<span data-ttu-id="06718-178">nstructors_page_with_courses_Prod]</span><span class="sxs-lookup"><span data-stu-id="06718-178">nstructors_page_with_courses_Prod]</span></span>(deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

<span data-ttu-id="06718-179">Agora, você implantou uma atualização de aplicativo que envolve uma alteração de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="06718-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="06718-180">O próximo tutorial mostra como implantar uma alteração de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="06718-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="06718-181">[Anterior](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [Próximo](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="06718-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
