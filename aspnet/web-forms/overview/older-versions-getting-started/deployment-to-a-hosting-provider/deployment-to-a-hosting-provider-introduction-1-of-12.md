---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'Implantando um aplicativo da Web ASP.NET com o SQL Server Compact usando o Visual Studio: Introdução - 1 de 12 | Microsoft Docs'
author: tdykstra
description: Esta série de tutoriais mostra como implantar (publicar) um ASP.NET projeto de aplicativo web que inclui um banco de dados do SQL Server Compact usando o Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: 9dacafaacdab12b8005cb6073647ae526cefcfb4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029673"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a><span data-ttu-id="e3ebe-103">Implantando um aplicativo da Web ASP.NET com o SQL Server Compact usando o Visual Studio: Introdução - 1 de 12</span><span class="sxs-lookup"><span data-stu-id="e3ebe-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio: Introduction - 1 of 12</span></span>
====================
<span data-ttu-id="e3ebe-104">por [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e3ebe-105">Baixe o projeto inicial</span><span class="sxs-lookup"><span data-stu-id="e3ebe-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="e3ebe-106">Esta série de tutoriais mostra como implantar (publicar) um ASP.NET projeto de aplicativo web que inclui um banco de dados do SQL Server Compact usando o Visual Studio 2012 RC ou Visual Studio Express 2012 RC para Web.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="e3ebe-107">Você também pode usar o Visual Studio 2010 se você instalar a atualização de publicação na Web.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span>
> 
> <span data-ttu-id="e3ebe-108">Para obter um tutorial que mostra os recursos de implantação introduzidos após a versão RC do Visual Studio 2012, mostra como implantar as edições do SQL Server que não seja o SQL Server Compact e mostra como implantar aplicativos de Web do serviço de aplicativo do Azure, consulte [implantação da Web do ASP.NET usando o Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-108">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>
> 
> <span data-ttu-id="e3ebe-109">Esses tutoriais orientá-lo Implantando primeiro ao IIS no seu computador de desenvolvimento local para teste e, em seguida, em um provedor de hospedagem de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-109">These tutorials guide you through deploying first to IIS on your local development computer for testing, and then to a third-party hosting provider.</span></span> <span data-ttu-id="e3ebe-110">O aplicativo que você implantará usa um banco de dados do aplicativo e um banco de dados de associação do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-110">The application that you'll deploy uses an application database and an ASP.NET membership database.</span></span> <span data-ttu-id="e3ebe-111">Você começa usando o SQL Server Compact e a implantação para o SQL Server Compact e tutoriais posteriores mostram como implantar as alterações do banco de dados e como migrar para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-111">You start off using SQL Server Compact and deploying to SQL Server Compact, and later tutorials show you how to deploy database changes and how to migrate to SQL Server.</span></span>
> 
> <span data-ttu-id="e3ebe-112">Os tutoriais presumem que você sabe como trabalhar com o ASP.NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-112">The tutorials assume you know how to work with ASP.NET in Visual Studio.</span></span> <span data-ttu-id="e3ebe-113">Se você não fizer isso, um bom lugar para começar é um [básica Tutorial do ASP.NET Web Forms](../tailspin-spyworks/tailspin-spyworks-part-1.md) ou um [Tutorial básico do ASP.NET MVC](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-113">If you don't, a good place to start is a [basic ASP.NET Web Forms Tutorial](../tailspin-spyworks/tailspin-spyworks-part-1.md) or a [basic ASP.NET MVC Tutorial](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md).</span></span>
> 
> <span data-ttu-id="e3ebe-114">Se você tiver perguntas que não estão diretamente relacionadas para o tutorial, você pode postá-los para o [Fórum de implantação do ASP.NET](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET Deployment forum](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment).</span></span>


## <a name="overview"></a><span data-ttu-id="e3ebe-115">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e3ebe-115">Overview</span></span>

<span data-ttu-id="e3ebe-116">Esses tutoriais orientá-lo Implantando primeiro ao IIS no seu computador de desenvolvimento local para teste e, em seguida, em um provedor de hospedagem de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-116">These tutorials guide you through deploying first to IIS on your local development computer for testing, and then to a third-party hosting provider.</span></span> <span data-ttu-id="e3ebe-117">O aplicativo que você implantará usa um banco de dados do aplicativo e um banco de dados de associação do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-117">The application that you'll deploy uses an application database and an ASP.NET membership database.</span></span> <span data-ttu-id="e3ebe-118">Você começa usando o SQL Server Compact e a implantação para o SQL Server Compact e tutoriais posteriores mostram como implantar as alterações do banco de dados e como migrar para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-118">You start off using SQL Server Compact and deploying to SQL Server Compact, and later tutorials show you how to deploy database changes and how to migrate to SQL Server.</span></span>

<span data-ttu-id="e3ebe-119">O número de tutoriais – 11 em todas as mais de uma página de solução de problemas pode tornar o processo de implantação parecer assustadora.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-119">The number of tutorials – 11 in all plus a troubleshooting page – might make the deployment process seem daunting.</span></span> <span data-ttu-id="e3ebe-120">Na verdade, os procedimentos básicos para implantar um site compõem uma parte relativamente pequena do conjunto de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-120">In fact, the basic procedures for deploying a site make up a relatively small part of the tutorial set.</span></span> <span data-ttu-id="e3ebe-121">No entanto, em situações do mundo real, geralmente precisar de informações sobre algum aspecto extra pequena, mas importante da implantação — por exemplo, definindo permissões de pasta no servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-121">However, in real-world situations, you often need information about some small but important extra aspect of deployment — for example, setting folder permissions on the target server.</span></span> <span data-ttu-id="e3ebe-122">Há muitas dessas técnicas adicionais nos tutoriais, na esperança de que os tutoriais de não deixar as informações que podem impedir que você implantar um aplicativo real.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-122">We've included many of these additional techniques in the tutorials, with the hope that the tutorials don't leave out information that might prevent you from successfully deploying a real application.</span></span>

<span data-ttu-id="e3ebe-123">Os tutoriais são projetados para executar em sequência, e cada parte se baseia na parte anterior.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-123">The tutorials are designed to run in sequence, and each part builds on the previous part.</span></span> <span data-ttu-id="e3ebe-124">No entanto, você poderá ignorar as partes que não são relevantes para sua situação.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-124">However, you can skip parts that aren't relevant to your situation.</span></span> <span data-ttu-id="e3ebe-125">(Ignorar partes pode exigir que você ajustar os procedimentos em tutoriais posteriores.)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-125">(Skipping parts might require you to adjust the procedures in later tutorials.)</span></span>

## <a name="intended-audience"></a><span data-ttu-id="e3ebe-126">Público-alvo</span><span class="sxs-lookup"><span data-stu-id="e3ebe-126">Intended Audience</span></span>

<span data-ttu-id="e3ebe-127">Os tutoriais são destinados a desenvolvedores do ASP.NET que trabalham em organizações de pequenas porte ou em outros ambientes em que:</span><span class="sxs-lookup"><span data-stu-id="e3ebe-127">The tutorials are aimed at ASP.NET developers who work in small organizations or other environments where:</span></span>

- <span data-ttu-id="e3ebe-128">Um processo de integração contínua (compilações automatizadas e implantação) não é usado.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-128">A continuous integration process (automated builds and deployment) is not used.</span></span>
- <span data-ttu-id="e3ebe-129">O ambiente de produção é um provedor de hospedagem de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-129">The production environment is a third-party hosting provider.</span></span>
- <span data-ttu-id="e3ebe-130">Uma pessoa normalmente executa várias funções (a mesma pessoa desenvolve, testa e implanta).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-130">One person typically fills multiple roles (the same person develops, tests, and deploys).</span></span>

<span data-ttu-id="e3ebe-131">Em ambientes empresariais, é mais comum para implementar processos de integração contínua e o ambiente de produção é geralmente hospedado pelos servidores da empresa.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-131">In enterprise environments, it's more typical to implement continuous integration processes, and the production environment is usually hosted by the company's own servers.</span></span> <span data-ttu-id="e3ebe-132">Pessoas diferentes também geralmente executam funções diferentes.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-132">Different people also typically perform different roles.</span></span> <span data-ttu-id="e3ebe-133">Para obter informações sobre implantação corporativa, consulte [implantação de aplicativos Web em cenários empresariais](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-133">For information about enterprise deployment, see [Deploying Web Applications in Enterprise Scenarios](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span>

<span data-ttu-id="e3ebe-134">As organizações de todos os tamanhos também podem implantar aplicativos web no Azure e a maioria dos procedimentos mostradas nos tutoriais também se aplicam a aplicativos de Web de serviços de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-134">Organizations of all sizes can also deploy web applications to Azure, and most of the procedures shown in these tutorials apply also to Azure App Services Web Apps.</span></span> <span data-ttu-id="e3ebe-135">Para obter uma introdução ao Azure, consulte [ https://azure.microsoft.com ](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-135">For an introduction to Azure, see [https://azure.microsoft.com](https://azure.microsoft.com).</span></span>

## <a name="the-hosting-provider-shown-in-the-tutorials"></a><span data-ttu-id="e3ebe-136">O provedor de hospedagem mostrado nos tutoriais</span><span class="sxs-lookup"><span data-stu-id="e3ebe-136">The Hosting Provider Shown in the Tutorials</span></span>

<span data-ttu-id="e3ebe-137">Os tutoriais guiarão você pelo processo de configuração de uma conta com uma empresa de hospedagem e implantação do aplicativo para esse provedor de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-137">The tutorials take you through the process of setting up an account with a hosting company and deploying the application to that hosting provider.</span></span> <span data-ttu-id="e3ebe-138">Uma empresa de hospedagem específica foi escolhida para que os tutoriais poderiam ilustram a experiência completa de implantação em um site ao vivo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-138">A specific hosting company was chosen so that the tutorials could illustrate the complete experience of deploying to a live website.</span></span> <span data-ttu-id="e3ebe-139">Cada empresa de hospedagem fornece recursos diferentes, e a experiência de implantação para seus servidores varia um pouco; No entanto, o processo descrito neste tutorial é típico para o processo geral.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-139">Each hosting company provides different features, and the experience of deploying to their servers varies somewhat; however, the process described in this tutorial is typical for the overall process.</span></span>

<span data-ttu-id="e3ebe-140">O provedor de hospedagem usado para este tutorial, Cytanium.com, é um dos muitos que estão disponíveis e seu uso neste tutorial não constitui um endosso ou recomendação.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-140">The hosting provider used for this tutorial, Cytanium.com, is one of many that are available, and its use in this tutorial does not constitute an endorsement or recommendation.</span></span>

## <a name="deploying-web-site-projects"></a><span data-ttu-id="e3ebe-141">Implantação de projetos de Site da Web</span><span class="sxs-lookup"><span data-stu-id="e3ebe-141">Deploying Web Site Projects</span></span>

<span data-ttu-id="e3ebe-142">Contoso University é um projeto de aplicativo web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-142">Contoso University is a Visual Studio web application project.</span></span> <span data-ttu-id="e3ebe-143">Não se aplicam à maioria dos métodos de implantação e ferramentas demonstradas neste tutorial [projetos de Site](https://msdn.microsoft.com/library/dd547590.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-143">Most of the deployment methods and tools demonstrated in this tutorial do not apply to [Web Site Projects](https://msdn.microsoft.com/library/dd547590.aspx).</span></span> <span data-ttu-id="e3ebe-144">Para obter informações sobre como implantar projetos de site, consulte [mapa de conteúdo de implantação do ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-144">For information about how to deploy web site projects, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects).</span></span>

## <a name="deploying-aspnet-mvc-projects"></a><span data-ttu-id="e3ebe-145">Implantação de projetos do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e3ebe-145">Deploying ASP.NET MVC Projects</span></span>

<span data-ttu-id="e3ebe-146">Para este tutorial, você implanta um projeto de Web Forms do ASP.NET, mas tudo o que você aprenderá a fazer é aplicável ao ASP.NET MVC também.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-146">For this tutorial you deploy an ASP.NET Web Forms project, but everything you learn how to do is applicable to ASP.NET MVC as well.</span></span> <span data-ttu-id="e3ebe-147">Um projeto do MVC do Visual Studio é apenas outra forma de projeto de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-147">A Visual Studio MVC project is just another form of web application project.</span></span> <span data-ttu-id="e3ebe-148">A única diferença é que se você estiver implantando em um provedor de hospedagem que não dão suporte ao ASP.NET MVC ou sua versão de destino dele, certifique-se de que você tenha instalado o apropriada ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) ou [MVC 4](http://nuget.org/packages/aspnetmvc)) O pacote NuGet em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-148">The only difference is that if you're deploying to a hosting provider that does not support ASP.NET MVC or your target version of it, you must make sure that you have installed the appropriate ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) or [MVC 4](http://nuget.org/packages/aspnetmvc)) NuGet package in your project.</span></span>

## <a name="programming-language"></a><span data-ttu-id="e3ebe-149">Linguagem de programação</span><span class="sxs-lookup"><span data-stu-id="e3ebe-149">Programming Language</span></span>

<span data-ttu-id="e3ebe-150">O aplicativo de exemplo usa c#, mas os tutoriais não exigem conhecimento do c# e mostradas nos tutoriais de técnicas de implantação não são específicas do idioma.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-150">The sample application uses C# but the tutorials do not require knowledge of C#, and the deployment techniques shown by the tutorials are not language-specific.</span></span>

## <a name="troubleshooting-during-this-tutorial"></a><span data-ttu-id="e3ebe-151">Solução de problemas durante este Tutorial</span><span class="sxs-lookup"><span data-stu-id="e3ebe-151">Troubleshooting During this Tutorial</span></span>

<span data-ttu-id="e3ebe-152">Quando ocorrer um erro durante a implantação, ou se o site implantado não é executado corretamente, as mensagens de erro sempre não fornecem uma solução.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-152">When an error happens during deployment, or if the deployed site does not run correctly, the error messages don't always provide a solution.</span></span> <span data-ttu-id="e3ebe-153">Para ajudá-lo com alguns cenários comuns de problema, uma [página de referência de solução de problemas](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) está disponível.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-153">To help you with some common problem scenarios, a [troubleshooting reference page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) is available.</span></span> <span data-ttu-id="e3ebe-154">Se você receber uma mensagem de erro ou se algo não funciona ao percorrer os tutoriais, certifique-se de verificar a página de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-154">If you get an error message or something doesn't work as you go through the tutorials, be sure to check the troubleshooting page.</span></span>

## <a name="comments-welcome"></a><span data-ttu-id="e3ebe-155">Bem-vindo de comentários</span><span class="sxs-lookup"><span data-stu-id="e3ebe-155">Comments Welcome</span></span>

<span data-ttu-id="e3ebe-156">Comentários sobre os tutoriais são boas-vindos e quando o tutorial será atualizado todos os esforços serão feito para correções de conta ou sugestões de melhorias que são fornecidas nos comentários do tutoriais.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-156">Comments on the tutorials are welcome, and when the tutorial is updated every effort will be made to take into account corrections or suggestions for improvements that are provided in tutorial comments.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3ebe-157">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3ebe-157">Prerequisites</span></span>

<span data-ttu-id="e3ebe-158">Antes de começar, certifique-se de que você tenha o Windows 7 ou posterior e um dos seguintes produtos instalados no seu computador:</span><span class="sxs-lookup"><span data-stu-id="e3ebe-158">Before you start, make sure that you have Windows 7 or later and one of the following products installed on your computer:</span></span>

- [<span data-ttu-id="e3ebe-159">Visual Studio 2010 SP1</span><span class="sxs-lookup"><span data-stu-id="e3ebe-159">Visual Studio 2010 SP1</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [<span data-ttu-id="e3ebe-160">Visual Web Developer Express 2010 SP1</span><span class="sxs-lookup"><span data-stu-id="e3ebe-160">Visual Web Developer Express 2010 SP1</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [<span data-ttu-id="e3ebe-161">Visual Studio 2012 RC ou Visual Studio Express 2012 RC para Web</span><span class="sxs-lookup"><span data-stu-id="e3ebe-161">Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web</span></span>](https://go.microsoft.com/fwlink/?LinkId=240162)

<span data-ttu-id="e3ebe-162">Se você tiver o Visual Studio 2010 SP1 ou Visual Web Developer Express 2010 SP1, instale os seguintes produtos também:</span><span class="sxs-lookup"><span data-stu-id="e3ebe-162">If you have Visual Studio 2010 SP1 or Visual Web Developer Express 2010 SP1, install the following products also:</span></span>

- <span data-ttu-id="e3ebe-163">[SDK do Azure para .NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (inclui a atualização de publicação na Web)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-163">[Azure SDK for .NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (includes the Web Publish Update)</span></span>
- [<span data-ttu-id="e3ebe-164">Microsoft Visual Studio 2010 SP1 Tools para SQL Server Compact 4.0</span><span class="sxs-lookup"><span data-stu-id="e3ebe-164">Microsoft Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

<span data-ttu-id="e3ebe-165">Qualquer outro software é necessário para concluir o tutorial, mas você não precisa ter que carregado ainda.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-165">Some other software is required in order to complete the tutorial, but you don't have to have that loaded yet.</span></span> <span data-ttu-id="e3ebe-166">O tutorial o orientará pelas etapas para instalá-lo quando necessário.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-166">The tutorial will walk you through the steps for installing it when you need it.</span></span>

## <a name="downloading-the-sample-application"></a><span data-ttu-id="e3ebe-167">Baixar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="e3ebe-167">Downloading the Sample Application</span></span>

<span data-ttu-id="e3ebe-168">O aplicativo que você vai implantar é denominado Contoso University e já foi criado para você.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-168">The application you'll deploy is named Contoso University and has already been created for you.</span></span> <span data-ttu-id="e3ebe-169">É uma versão simplificada de um site de Universidade, vagamente baseado no aplicativo Contoso University descrito na [tutoriais do Entity Framework no site do ASP.NET](https://asp.net/entity-framework/tutorials).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-169">It's a simplified version of a university web site, based loosely on the Contoso University application described in the [Entity Framework tutorials on the ASP.NET site](https://asp.net/entity-framework/tutorials).</span></span>

<span data-ttu-id="e3ebe-170">Quando você tem os pré-requisitos instalados, baixe o [aplicativo web Contoso University](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-170">When you have the prerequisites installed, download the [Contoso University web application](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b).</span></span> <span data-ttu-id="e3ebe-171">O *. zip* arquivo contém várias versões do projeto e um arquivo PDF que contém todos os tutoriais de 12.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-171">The *.zip* file contains multiple versions of the project and a PDF file that contains all 12 tutorials.</span></span> <span data-ttu-id="e3ebe-172">Para trabalhar com as etapas do tutorial, comece com Begin ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-172">To work through the steps of the tutorial, start with ContosoUniversity-Begin.</span></span> <span data-ttu-id="e3ebe-173">Para ver a aparência de projeto no final dos tutoriais, abra ContosoUniversity-End.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-173">To see what the project looks like at the end of the tutorials, open ContosoUniversity-End.</span></span> <span data-ttu-id="e3ebe-174">Para ver a aparência de projeto antes da migração para o SQL Server completo Tutorial 10, abra AfterTutorial09 ContosoUniversity.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-174">To see what the project looks like before the migration to full SQL Server in tutorial 10, open ContosoUniversity-AfterTutorial09.</span></span>

<span data-ttu-id="e3ebe-175">Para preparar a percorrer as etapas do tutorial, início do salvamento ContosoUniversity-até a pasta em que você pode usar para trabalhar com projetos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-175">To prepare to work through the tutorial steps, save ContosoUniversity-Begin to whatever folder you use for working with Visual Studio projects.</span></span> <span data-ttu-id="e3ebe-176">Por padrão, essa é a pasta a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3ebe-176">By default this is the following folder:</span></span>

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

<span data-ttu-id="e3ebe-177">(Para as capturas de tela neste tutorial, a pasta do projeto está localizada no diretório raiz no `C`: drive.)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-177">(For the screen shots in this tutorial, the project folder is located in the root directory on the `C`: drive.)</span></span>

<span data-ttu-id="e3ebe-178">Inicie o Visual Studio, abra o projeto e pressione CTRL-F5 para executá-lo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-178">Start Visual Studio, open the project, and press CTRL-F5 to run it.</span></span>

<span data-ttu-id="e3ebe-179">[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-179">[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)</span></span>

<span data-ttu-id="e3ebe-180">As páginas do site são acessíveis na barra de menus e permitem que você realize as seguintes funções:</span><span class="sxs-lookup"><span data-stu-id="e3ebe-180">The website pages are accessible from the menu bar and let you perform the following functions:</span></span>

- <span data-ttu-id="e3ebe-181">Exibir estatísticas de alunos (a página sobre).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-181">Display student statistics (the About page).</span></span>
- <span data-ttu-id="e3ebe-182">Exibir, editar, excluir e adicionar alunos.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-182">Display, edit, delete, and add students.</span></span>
- <span data-ttu-id="e3ebe-183">Exibir e editar cursos.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-183">Display and edit courses.</span></span>
- <span data-ttu-id="e3ebe-184">Exibir e editar instrutores.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-184">Display and edit instructors.</span></span>
- <span data-ttu-id="e3ebe-185">Exibir e editar os departamentos.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-185">Display and edit departments.</span></span>

<span data-ttu-id="e3ebe-186">A seguir estão as capturas de tela de algumas páginas representativas.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-186">Following are screen shots of a few representative pages.</span></span>

<span data-ttu-id="e3ebe-187">[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-187">[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)</span></span>

<span data-ttu-id="e3ebe-188">[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-188">[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)</span></span>

## <a name="reviewing-application-features-that-affect-deployment"></a><span data-ttu-id="e3ebe-189">Revisar recursos de aplicativos que afetam a implantação</span><span class="sxs-lookup"><span data-stu-id="e3ebe-189">Reviewing Application Features that Affect Deployment</span></span>

<span data-ttu-id="e3ebe-190">Os seguintes recursos do aplicativo afetam como implantá-lo ou o que você precisa fazer para implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-190">The following features of the application affect how you deploy it or what you have to do to deploy it.</span></span> <span data-ttu-id="e3ebe-191">Cada um deles é explicada mais detalhadamente nos tutoriais a seguir na série.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-191">Each of these is explained in more detail in the following tutorials in the series.</span></span>

- <span data-ttu-id="e3ebe-192">Contoso University usa um banco de dados do SQL Server Compact para armazenar dados de aplicativo, como nomes de aluno e instrutor.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-192">Contoso University uses a SQL Server Compact database to store application data such as student and instructor names.</span></span> <span data-ttu-id="e3ebe-193">O banco de dados contiver uma mistura de dados de teste e dados de produção e, quando você implanta em produção, você precisará excluir os dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-193">The database contains a mix of test data and production data, and when you deploy to production you need to exclude the test data.</span></span> <span data-ttu-id="e3ebe-194">Posteriormente na série de tutoriais, você vai migrar do SQL Server Compact para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-194">Later in the tutorial series you'll migrate from SQL Server Compact to SQL Server.</span></span>
- <span data-ttu-id="e3ebe-195">O aplicativo usa o sistema de associação do ASP.NET, que armazena informações de conta de usuário em um banco de dados do SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-195">The application uses the ASP.NET membership system, which stores user account information in a SQL Server Compact database.</span></span> <span data-ttu-id="e3ebe-196">O aplicativo define um usuário de administrador que tenha acesso a algumas informações restritas.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-196">The application defines an administrator user who has access to some restricted information.</span></span> <span data-ttu-id="e3ebe-197">Você precisará implantar o banco de dados de associação sem contas de teste, mas com uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-197">You need to deploy the membership database without test accounts but with one administrator account.</span></span>
- <span data-ttu-id="e3ebe-198">Como o banco de dados do aplicativo e o banco de dados de associação usam SQL Server Compact como o mecanismo de banco de dados, você precisa implantar o mecanismo de banco de dados para o provedor de hospedagem, bem como os bancos de dados em si.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-198">Because the application database and the membership database use SQL Server Compact as the database engine, you have to deploy the database engine to the hosting provider, as well as the databases themselves.</span></span>
- <span data-ttu-id="e3ebe-199">O aplicativo usa provedores de universal de associação ASP.NET para que o sistema de associação pode armazenar seus dados em um banco de dados do SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-199">The application uses ASP.NET universal membership providers so that the membership system can store its data in a SQL Server Compact database.</span></span> <span data-ttu-id="e3ebe-200">O assembly que contém os provedores de associação universal deve ser implantado com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-200">The assembly that contains the universal membership providers must be deployed with the application.</span></span>
- <span data-ttu-id="e3ebe-201">O aplicativo usa o Entity Framework 5.0 para acessar dados no banco de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-201">The application uses the Entity Framework 5.0 to access data in the application database.</span></span> <span data-ttu-id="e3ebe-202">O assembly que contém o Entity Framework 5.0 deve ser implantado com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-202">The assembly that contains Entity Framework 5.0 must be deployed with the application.</span></span>
- <span data-ttu-id="e3ebe-203">O aplicativo usa o utilitário de relatório e registro em log um erro de terceiros.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-203">The application uses a third-party error logging and reporting utility.</span></span> <span data-ttu-id="e3ebe-204">Esse utilitário é fornecido em um assembly que deve ser implantado com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-204">This utility is provided in an assembly which must be deployed with the application.</span></span>
- <span data-ttu-id="e3ebe-205">O utilitário de registro em log de erro grava informações de erro em arquivos XML para uma pasta de arquivos.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-205">The error logging utility writes error information in XML files to a file folder.</span></span> <span data-ttu-id="e3ebe-206">Você precisa certificar-se de que a conta que o ASP.NET é executado no site implantado tem permissão de gravação nessa pasta, e você precisará excluir essa pasta de implantação.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-206">You have to make sure that the account that ASP.NET runs under in the deployed site has write permission to this folder, and you have to exclude this folder from deployment.</span></span> <span data-ttu-id="e3ebe-207">(Caso contrário, os dados de log de erros do ambiente de teste podem ser implantados em produção e/ou arquivos de log de erros de produção podem ter sido excluídos.)</span><span class="sxs-lookup"><span data-stu-id="e3ebe-207">(Otherwise, error log data from the test environment might be deployed to production and/or production error log files might be deleted.)</span></span>
- <span data-ttu-id="e3ebe-208">O aplicativo inclui algumas configurações que devem ser alteradas em implantado *Web. config* arquivo dependendo do ambiente de destino (teste ou produção) e outras configurações que devem ser alteradas dependendo da compilação configuração (Debug ou Release).</span><span class="sxs-lookup"><span data-stu-id="e3ebe-208">The application includes some settings that must be changed in the deployed *Web.config* file depending on the destination environment (test or production), and other settings that must be changed depending on the build configuration (Debug or Release).</span></span>
- <span data-ttu-id="e3ebe-209">A solução do Visual Studio inclui um projeto de biblioteca de classes.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-209">The Visual Studio solution includes a class library project.</span></span> <span data-ttu-id="e3ebe-210">Somente o assembly que gera este projeto deve ser implantado, não o próprio projeto.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-210">Only the assembly that this project generates should be deployed, not the project itself.</span></span>

<span data-ttu-id="e3ebe-211">Neste tutorial primeiro da série, você baixou o projeto do Visual Studio e revisado recursos de site que afetam como você pode implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-211">In this first tutorial in the series, you have downloaded the sample Visual Studio project and reviewed site features that affect how you deploy the application.</span></span> <span data-ttu-id="e3ebe-212">Nos tutoriais a seguir, você prepara para implantação, configurando a algumas dessas coisas a serem manipulados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-212">In the following tutorials, you prepare for deployment by setting up some of these things to be handled automatically.</span></span> <span data-ttu-id="e3ebe-213">Outras pessoas que você cuidar manualmente.</span><span class="sxs-lookup"><span data-stu-id="e3ebe-213">Others you take care of manually.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e3ebe-214">Avançar</span><span class="sxs-lookup"><span data-stu-id="e3ebe-214">Next</span></span>](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)