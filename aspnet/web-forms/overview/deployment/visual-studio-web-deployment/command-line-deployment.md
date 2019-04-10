---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Implantação da Web do ASP.NET usando o Visual Studio: Implantação de linha de comando | Microsoft Docs'
author: tdykstra
description: Esta série de tutoriais mostra como implantar (publicar) um ASP.NET web de aplicativo para aplicativos de Web do serviço de aplicativo do Azure ou para um provedor de hospedagem de terceiros, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: c9aadec642837953dde4cf3e89ec9a7d484b380e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59401329"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="75e4a-103">Implantação da Web do ASP.NET usando o Visual Studio: Implantação por linha de comando</span><span class="sxs-lookup"><span data-stu-id="75e4a-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="75e4a-104">por [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="75e4a-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="75e4a-105">Baixe o projeto inicial</span><span class="sxs-lookup"><span data-stu-id="75e4a-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="75e4a-106">Esta série de tutoriais mostra como implantar (publicar) um ASP.NET web application para aplicativos de Web do serviço de aplicativo do Azure ou para um provedor de hospedagem de terceiros, usando o Visual Studio 2012 ou Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="75e4a-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="75e4a-107">Para obter informações sobre a série, consulte [o primeiro tutorial na série](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75e4a-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="75e4a-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="75e4a-108">Overview</span></span>

<span data-ttu-id="75e4a-109">Este tutorial mostra como invocar a Visual Studio web publicar pipeline da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="75e4a-110">Isso é útil para cenários em que você deseja [automatizar o processo de implantação](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) em vez de fazê-lo manualmente no Visual Studio, geralmente, usando uma [sistema de controle de versão do código de origem](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span><span class="sxs-lookup"><span data-stu-id="75e4a-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="75e4a-111">Faça uma alteração para implantar</span><span class="sxs-lookup"><span data-stu-id="75e4a-111">Make a change to deploy</span></span>

<span data-ttu-id="75e4a-112">Atualmente, a página sobre exibirá o código de modelo.</span><span class="sxs-lookup"><span data-stu-id="75e4a-112">Currently the About page displays the template code.</span></span>

![Página sobre com código de modelo](command-line-deployment/_static/image1.png)

<span data-ttu-id="75e4a-114">Você irá substituí-lo com o código que exibe um resumo de registro de aluno.</span><span class="sxs-lookup"><span data-stu-id="75e4a-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="75e4a-115">Abra o *About* página, exclua todos a marcação dentro a `MainContent` `Content` elemento e inserir a marcação a seguir em seu lugar:</span><span class="sxs-lookup"><span data-stu-id="75e4a-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="75e4a-116">Execute o projeto e selecione o **sobre** página.</span><span class="sxs-lookup"><span data-stu-id="75e4a-116">Run the project and select the **About** page.</span></span>

![Página Sobre](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="75e4a-118">Implantar em teste usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="75e4a-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="75e4a-119">Você não implantar outra alteração de banco de dados, portanto, implantação de banco de dados dbDacFx desabilitar para o banco de dados do aspnet ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="75e4a-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="75e4a-120">Abra o **publicar na Web** do assistente e em cada um dos três perfis, claros de publicação a **Atualizar banco de dados** caixa de seleção na **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="75e4a-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="75e4a-121">Na página Iniciar do Windows 8, pesquise **Prompt de comando do desenvolvedor para VS2012**.</span><span class="sxs-lookup"><span data-stu-id="75e4a-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="75e4a-122">Clique com botão direito no ícone **Prompt de comando do desenvolvedor para VS2012** e clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="75e4a-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="75e4a-123">Digite o seguinte comando no prompt de comando, substituindo o caminho para o arquivo de solução com o caminho para o arquivo da solução:</span><span class="sxs-lookup"><span data-stu-id="75e4a-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="75e4a-124">O MSBuild compila a solução e implanta para o ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="75e4a-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![Saída da linha de comando](command-line-deployment/_static/image3.png)

<span data-ttu-id="75e4a-126">Abra um navegador e vá para `http://localhost/ContosoUniversity`, em seguida, clique em de **sobre** página para verificar se a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="75e4a-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="75e4a-127">Se você não tiver criado todos os alunos no teste, você verá uma página vazia sob o **estatísticas do corpo de aluno** título.</span><span class="sxs-lookup"><span data-stu-id="75e4a-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="75e4a-128">Vá para o **alunos** , clique em **adicionar aluno**e adicionar alguns alunos e, em seguida, retornar para o **sobre** página para ver as estatísticas de alunos.</span><span class="sxs-lookup"><span data-stu-id="75e4a-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![Sobre a página no ambiente de teste](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="75e4a-130">Opções de chave de linha de comando</span><span class="sxs-lookup"><span data-stu-id="75e4a-130">Key command line options</span></span>

<span data-ttu-id="75e4a-131">O comando que você inseriu passado duas propriedades e o caminho do arquivo de solução para o MSBuild:</span><span class="sxs-lookup"><span data-stu-id="75e4a-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="75e4a-132">Implantar a solução em vez de implantar projetos individuais</span><span class="sxs-lookup"><span data-stu-id="75e4a-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="75e4a-133">Especificar o arquivo de solução faz com que todos os projetos na solução a ser criado.</span><span class="sxs-lookup"><span data-stu-id="75e4a-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="75e4a-134">Se você tiver vários projetos da web na solução, o comportamento de MSBuild a seguir se aplica:</span><span class="sxs-lookup"><span data-stu-id="75e4a-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="75e4a-135">As propriedades que você especifica na linha de comando são passadas para cada projeto.</span><span class="sxs-lookup"><span data-stu-id="75e4a-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="75e4a-136">Portanto, cada projeto da web deve ter um perfil de publicação com o nome que você especificar.</span><span class="sxs-lookup"><span data-stu-id="75e4a-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="75e4a-137">Se você especificar `/p:PublishProfile=Test`, cada projeto da web deve ter um perfil de publicação denominado *teste*.</span><span class="sxs-lookup"><span data-stu-id="75e4a-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="75e4a-138">Com êxito, você pode publicar um projeto quando outro ainda não compila.</span><span class="sxs-lookup"><span data-stu-id="75e4a-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="75e4a-139">Para obter mais informações, consulte o thread de stackoverflow [MSBuild falha com dois pacotes](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span><span class="sxs-lookup"><span data-stu-id="75e4a-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="75e4a-140">Se você especificar um projeto individual, em vez de uma solução, você precisa adicionar um parâmetro que especifica a versão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75e4a-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="75e4a-141">Se você estiver usando o Visual Studio 2012 da linha de comando seria semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="75e4a-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="75e4a-142">O número de versão para Visual Studio 2010 é 10.0.</span><span class="sxs-lookup"><span data-stu-id="75e4a-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="75e4a-143">Para obter mais informações, consulte [compatibilidade de projeto do Visual Studio e VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) no blog do Sayed Hashimi.</span><span class="sxs-lookup"><span data-stu-id="75e4a-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="75e4a-144">Especificar o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="75e4a-144">Specifying the publish profile</span></span>

<span data-ttu-id="75e4a-145">Você pode especificar o perfil de publicação por nome ou o caminho completo para o *. pubxml* de arquivos, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="75e4a-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="75e4a-146">Métodos com suporte para publicação de linha de comando de publicar Web</span><span class="sxs-lookup"><span data-stu-id="75e4a-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="75e4a-147">Três métodos de publicação têm suporte para publicação de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="75e4a-147">Three publish methods are supported for command line publishing:</span></span>

- `MSDeploy` <span data-ttu-id="75e4a-148">-Publica usando a implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="75e4a-148">- Publish by using Web Deploy.</span></span>
- `Package` <span data-ttu-id="75e4a-149">-Publica, criando um pacote de implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="75e4a-149">- Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="75e4a-150">Você precisa instalar o pacote separadamente do comando MSBuild que o cria.</span><span class="sxs-lookup"><span data-stu-id="75e4a-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- `FileSystem` <span data-ttu-id="75e4a-151">-Publica copiando arquivos para uma pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="75e4a-151">- Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="75e4a-152">Especificando a configuração de compilação e plataforma</span><span class="sxs-lookup"><span data-stu-id="75e4a-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="75e4a-153">A configuração de compilação e a plataforma devem ser definidos no Visual Studio ou na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="75e4a-154">Os perfis de publicação incluem propriedades que são nomeadas `LastUsedBuildConfiguration` e `LastUsedPlatform`, mas você não pode definir essas propriedades para determinar como o projeto é compilado.</span><span class="sxs-lookup"><span data-stu-id="75e4a-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="75e4a-155">Para obter mais informações, consulte [MSBuild: como definir a propriedade de configuração](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) no blog do Sayed Hashimi.</span><span class="sxs-lookup"><span data-stu-id="75e4a-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="75e4a-156">Implantar no preparo</span><span class="sxs-lookup"><span data-stu-id="75e4a-156">Deploy to staging</span></span>

<span data-ttu-id="75e4a-157">Para implantar no Azure, você deve adicionar a senha para a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="75e4a-158">Se você salvou a senha no perfil de publicação no Visual Studio, ele foi armazenado em formato criptografado no seu *. pubxml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="75e4a-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="75e4a-159">Esse arquivo não é acessado pelo MSBuild, quando você fizer uma implantação de linha de comando, portanto, você precisa passar a senha em um parâmetro de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="75e4a-160">Copie a senha que você precisa do *. publishsettings* arquivo que você baixou anteriormente para o site de preparo.</span><span class="sxs-lookup"><span data-stu-id="75e4a-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="75e4a-161">A senha é o valor de `userPWD` atributo para a implantação da Web `publishProfile` elemento.</span><span class="sxs-lookup"><span data-stu-id="75e4a-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Senha de implantação da Web](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="75e4a-163">Na página Iniciar do Windows 8, pesquise **Prompt de comando do desenvolvedor para VS2012**e clique no ícone para abrir o prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="75e4a-164">(Você não precisa para abri-lo como administrador neste momento porque você não estiver implantando no IIS no computador local).</span><span class="sxs-lookup"><span data-stu-id="75e4a-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="75e4a-165">Digite o seguinte comando no prompt de comando, substituindo o caminho para o arquivo de solução com o caminho para o arquivo da solução e a senha com a sua senha:</span><span class="sxs-lookup"><span data-stu-id="75e4a-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="75e4a-166">Observe que essa linha de comando inclui um parâmetro extra: `/p:AllowUntrustedCertificate=true`.</span><span class="sxs-lookup"><span data-stu-id="75e4a-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="75e4a-167">Neste tutorial está sendo escrito, o `AllowUntrustedCertificate` propriedade deve ser definida quando você publica no Azure da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="75e4a-168">Quando a correção para esse bug for lançada, você não precisa desse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="75e4a-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="75e4a-169">Abra um navegador e vá para a URL do seu site de preparo e, em seguida, clique no **sobre** página para verificar se a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="75e4a-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="75e4a-170">Como você viu anteriormente para o ambiente de teste, talvez você precise criar alguns alunos para ver as estatísticas sobre o **sobre** página.</span><span class="sxs-lookup"><span data-stu-id="75e4a-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="75e4a-171">Implantar na produção</span><span class="sxs-lookup"><span data-stu-id="75e4a-171">Deploy to production</span></span>

<span data-ttu-id="75e4a-172">O processo de implantação para produção é semelhante ao processo de preparo.</span><span class="sxs-lookup"><span data-stu-id="75e4a-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="75e4a-173">Copie a senha que você precisa do *. publishsettings* arquivo que você baixou anteriormente para o site da web de produção.</span><span class="sxs-lookup"><span data-stu-id="75e4a-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="75e4a-174">Abra **Prompt de comando do desenvolvedor para VS2012**.</span><span class="sxs-lookup"><span data-stu-id="75e4a-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="75e4a-175">Digite o seguinte comando no prompt de comando, substituindo o caminho para o arquivo de solução com o caminho para o arquivo da solução e a senha com a sua senha:</span><span class="sxs-lookup"><span data-stu-id="75e4a-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="75e4a-176">Para um site de produção real, se também houve uma alteração de banco de dados, você normalmente copiaria os *app\_offline.htm* de arquivo para o site antes da implantação e excluí-lo após a implantação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="75e4a-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="75e4a-177">Abra um navegador e vá para a URL do seu site de preparo e, em seguida, clique no **sobre** página para verificar se a implantação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="75e4a-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="75e4a-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="75e4a-178">Summary</span></span>

<span data-ttu-id="75e4a-179">Agora você já implantou uma atualização de aplicativo usando a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="75e4a-179">You have now deployed an application update by using the command line.</span></span>

![Sobre a página no ambiente de teste](command-line-deployment/_static/image6.png)

<span data-ttu-id="75e4a-181">No próximo tutorial, você verá um exemplo de como estender a web publicar pipeline.</span><span class="sxs-lookup"><span data-stu-id="75e4a-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="75e4a-182">O exemplo mostra como implantar arquivos que não estão incluídos no projeto.</span><span class="sxs-lookup"><span data-stu-id="75e4a-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="75e4a-183">[Anterior](deploying-a-database-update.md)
> [Próximo](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="75e4a-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
