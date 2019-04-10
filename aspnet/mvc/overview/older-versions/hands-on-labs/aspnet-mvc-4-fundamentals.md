---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: Conceitos básicos do ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: Este laboratório prático baseia-se na Store de música do MVC (Model View Controller), um aplicativo tutorial que apresenta e explica passo a passo de como usar a MV do ASP.NET...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 38aea3b3480dde6ec6182a45c4f61f44eea8e05e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59380217"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="f7502-103">Conceitos básicos do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="f7502-104">por [Web Camps equipe](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="f7502-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="f7502-105">Baixe o Kit de treinamento do Web Camps</span><span class="sxs-lookup"><span data-stu-id="f7502-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="f7502-106">Este laboratório prático baseia-se na Store de música do MVC (Model View Controller), um aplicativo tutorial que apresenta e explica passo a passo de como usar o ASP.NET MVC e o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="f7502-107">Em todo o laboratório, você aprenderá a simplicidade, ainda energia de uso dessas tecnologias em conjunto.</span><span class="sxs-lookup"><span data-stu-id="f7502-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="f7502-108">Você começará com um aplicativo simples e será compilá-lo até que você tenha um aplicativo de Web do ASP.NET MVC 4 totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="f7502-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="f7502-109">Este laboratório funciona com o ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7502-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="f7502-110">Se você quiser explorar a versão do ASP.NET MVC 3 do tutorial aplicativo, você pode encontrar na [MVC de música de Store](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="f7502-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="f7502-111">Este laboratório prático pressupõe que o desenvolvedor tenha experiência em tecnologias de desenvolvimento na Web, como HTML e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f7502-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="f7502-112">Todo o código de exemplo e trechos de código são incluídos no Web Camps treinamento Kit, disponível em [versões Web/Microsoft-WebCampTrainingKit](https://aka.ms/webcamps-training-kit).</span><span class="sxs-lookup"><span data-stu-id="f7502-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="f7502-113">O projeto específico para este laboratório está disponível em [conceitos básicos do ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span><span class="sxs-lookup"><span data-stu-id="f7502-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="f7502-114">O aplicativo de música Store</span><span class="sxs-lookup"><span data-stu-id="f7502-114">The Music Store application</span></span>

<span data-ttu-id="f7502-115">O aplicativo de web Store de música que será compilado em todo este laboratório consiste em três partes principais: compras, check-out e administração.</span><span class="sxs-lookup"><span data-stu-id="f7502-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="f7502-116">Os visitantes será capazes de procurar álbuns por gênero, adicionar álbuns ao seu carrinho, revise sua seleção e, por fim, vá para o check-out ao fazer logon e concluir o pedido.</span><span class="sxs-lookup"><span data-stu-id="f7502-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="f7502-117">Além disso, os administradores de armazenamento será capazes de gerenciar os álbuns disponíveis, bem como suas propriedades principais.</span><span class="sxs-lookup"><span data-stu-id="f7502-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="f7502-118">![Telas de Store de música](aspnet-mvc-4-fundamentals/_static/image1.png "telas do Music Store")</span><span class="sxs-lookup"><span data-stu-id="f7502-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

*<span data-ttu-id="f7502-119">Telas de Store de música</span><span class="sxs-lookup"><span data-stu-id="f7502-119">Music Store screens</span></span>*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="f7502-120">Conceitos básicos do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="f7502-121">Aplicativo de música Store será compilado usando **controlador MVC (Model View)**, um padrão de arquitetura que separa um aplicativo em três componentes principais:</span><span class="sxs-lookup"><span data-stu-id="f7502-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="f7502-122">**Modelos de**: Objetos de modelo são as partes do aplicativo que implementam a lógica do domínio.</span><span class="sxs-lookup"><span data-stu-id="f7502-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="f7502-123">Muitas vezes, os objetos de modelo também recuperar e armazenam o estado de modelo em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f7502-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="f7502-124">**Exibições:** As exibições são os componentes que exibem a interface do usuário do aplicativo (UI).</span><span class="sxs-lookup"><span data-stu-id="f7502-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="f7502-125">Normalmente, essa interface do usuário é criado a partir de dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="f7502-126">Um exemplo seria a exibição de edição de álbuns que exibe as caixas de texto e uma lista suspensa com base no estado atual de um objeto de álbum.</span><span class="sxs-lookup"><span data-stu-id="f7502-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="f7502-127">**Controladores:** Os controladores são os componentes que manipular a interação do usuário, manipulam o modelo e, por fim, selecionam um modo de exibição para renderizar a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7502-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="f7502-128">Em um aplicativo MVC, a exibição mostra apenas informações; o controlador manipula e responde à entrada e à interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7502-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="f7502-129">O padrão MVC ajuda a criar aplicativos que separam os diferentes aspectos do aplicativo (lógica de entrada, lógica de negócios e lógica de interface do usuário), enquanto fornece um acoplamento flexível entre esses elementos.</span><span class="sxs-lookup"><span data-stu-id="f7502-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="f7502-130">Essa separação ajuda você a gerenciar a complexidade ao compilar um aplicativo, pois permite que você se concentre em um aspecto da implementação por vez.</span><span class="sxs-lookup"><span data-stu-id="f7502-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="f7502-131">Além disso, o padrão MVC torna mais fácil testar aplicativos, também incentivar o uso de desenvolvimento orientado por testes (TDD) para a criação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f7502-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="f7502-132">O **ASP.NET MVC** framework fornece uma alternativa ao padrão de Web Forms do ASP.NET para a criação de aplicativos Web baseados em ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f7502-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="f7502-133">O **ASP.NET MVC** framework é uma estrutura de apresentação leve e altamente testável que (assim como acontece com aplicativos baseados em Web forms) é integrado aos recursos ASP.NET existentes, como páginas mestras e baseada em associação autenticação para que você obtenha todo o poder do .NET framework core.</span><span class="sxs-lookup"><span data-stu-id="f7502-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="f7502-134">Isso é útil se você já estiver familiarizado com o Web Forms do ASP.NET porque todas as bibliotecas que você já usa também estão disponíveis no ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7502-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="f7502-135">Além disso, o acoplamento flexível entre os três componentes principais de um aplicativo MVC também promove o desenvolvimento paralelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="f7502-136">Por exemplo, um desenvolvedor pode trabalhar no modo de exibição, um segundo desenvolvedor pode trabalhar na lógica do controlador e um terceiro desenvolvedor pode se concentrar na lógica de negócios no modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f7502-137">Objetivos</span><span class="sxs-lookup"><span data-stu-id="f7502-137">Objectives</span></span>

<span data-ttu-id="f7502-138">Neste laboratório prático, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f7502-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="f7502-139">Criar um aplicativo MVC do ASP.NET do zero com base no tutorial do aplicativo de Store de música</span><span class="sxs-lookup"><span data-stu-id="f7502-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="f7502-140">Adicionar controladores para tratar URLs para a Home page do site e para navegação sua funcionalidade principal</span><span class="sxs-lookup"><span data-stu-id="f7502-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="f7502-141">Adicionar um modo de exibição para personalizar o conteúdo exibido juntamente com seu estilo</span><span class="sxs-lookup"><span data-stu-id="f7502-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="f7502-142">Adicionar classes de modelo para conter e gerenciar dados e lógica de domínio</span><span class="sxs-lookup"><span data-stu-id="f7502-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="f7502-143">Use o padrão de modelo de exibição para passar informações de ações do controlador para os modelos de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="f7502-144">Explore o novo modelo de ASP.NET MVC 4 para aplicativos da internet</span><span class="sxs-lookup"><span data-stu-id="f7502-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f7502-145">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f7502-145">Prerequisites</span></span>

<span data-ttu-id="f7502-146">Você deve ter os seguintes itens para concluir este laboratório:</span><span class="sxs-lookup"><span data-stu-id="f7502-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f7502-147">[Visual Studio 2012 Express para Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (leia [Apêndice A](#AppendixA) para obter instruções sobre como instalá-la)</span><span class="sxs-lookup"><span data-stu-id="f7502-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f7502-148">Configuração</span><span class="sxs-lookup"><span data-stu-id="f7502-148">Setup</span></span>

**<span data-ttu-id="f7502-149">Instalando os trechos de código</span><span class="sxs-lookup"><span data-stu-id="f7502-149">Installing Code Snippets</span></span>**

<span data-ttu-id="f7502-150">Para sua conveniência, grande parte do código que você estiver gerenciando ao longo deste laboratório está disponível como trechos de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f7502-151">Para instalar os trechos de código executados **.\Source\Setup\CodeSnippets.vsi** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f7502-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f7502-152">Se você não estiver familiarizado com os trechos de código do Visual Studio e aprender como usá-los, consulte o Apêndice deste documento &quot; [apêndice c: Usar trechos de código](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="f7502-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f7502-153">Exercícios</span><span class="sxs-lookup"><span data-stu-id="f7502-153">Exercises</span></span>

<span data-ttu-id="f7502-154">Este laboratório prático é composto pelos seguintes exercícios:</span><span class="sxs-lookup"><span data-stu-id="f7502-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="f7502-155">Exercício 1: Criando o projeto de aplicativo Web do MusicStore ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7502-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="f7502-156">Exercício 2: Criando um controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="f7502-157">Exercício 3: Passando parâmetros para um controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="f7502-158">Exercício 4: Criando uma exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="f7502-159">Exercício 5: Criando um modelo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="f7502-160">Exercício 6: Usando parâmetros no modo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="f7502-161">Exercício 7: Uma visão geral do novo modelo do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="f7502-162">Cada exercício é acompanhado por um **final** pasta que contém a solução resultante, você deve obter depois de concluir os exercícios.</span><span class="sxs-lookup"><span data-stu-id="f7502-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f7502-163">Você pode usar essa solução como um guia se você precisar trabalhar com os exercícios de ajuda adicional.</span><span class="sxs-lookup"><span data-stu-id="f7502-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="f7502-164">Tempo estimado para concluir este laboratório: **60 minutos**.</span><span class="sxs-lookup"><span data-stu-id="f7502-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="f7502-165">Exercício 1: Criando o projeto de aplicativo Web do MusicStore ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7502-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="f7502-166">Neste exercício, você aprenderá como criar um aplicativo ASP.NET MVC no Visual Studio 2012 Express para Web, bem como sua organização da pasta principal.</span><span class="sxs-lookup"><span data-stu-id="f7502-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="f7502-167">Além disso, você aprenderá como adicionar um novo controlador e torná-lo a exibir uma cadeia de caracteres simple na página inicial do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="f7502-168">Tarefa 1 - criar o projeto de aplicativo Web ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7502-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="f7502-169">Nesta tarefa, você criará um projeto de aplicativo do ASP.NET MVC vazio usando o modelo MVC Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="f7502-170">Inicie **VS Express para Web**.</span><span class="sxs-lookup"><span data-stu-id="f7502-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="f7502-171">No menu **Arquivo**, clique em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="f7502-172">No **novo projeto** caixa de diálogo, selecione o **aplicativo Web do ASP.NET MVC 4** tipo, localizado no projeto **Visual c#** **Web** modelo lista.</span><span class="sxs-lookup"><span data-stu-id="f7502-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="f7502-173">Alterar o **nome** à *MvcMusicStore*.</span><span class="sxs-lookup"><span data-stu-id="f7502-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="f7502-174">Defina o local da solução dentro de um novo **começar** na pasta de origem neste exercício, por exemplo **\Source\Ex01-CreatingMusicStoreProject\Begin [YOUR-CHOL-PATH]**.</span><span class="sxs-lookup"><span data-stu-id="f7502-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="f7502-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7502-175">Click **OK**.</span></span>

    <span data-ttu-id="f7502-176">![Criar caixa de diálogo Novo projeto](aspnet-mvc-4-fundamentals/_static/image2.png "criar caixa de diálogo Novo projeto")</span><span class="sxs-lookup"><span data-stu-id="f7502-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    *<span data-ttu-id="f7502-177">Criar caixa de diálogo Novo projeto</span><span class="sxs-lookup"><span data-stu-id="f7502-177">Create New Project Dialog Box</span></span>*
6. <span data-ttu-id="f7502-178">No **novo projeto ASP.NET MVC 4** caixa de diálogo, selecione o **básica** modelo e certifique-se de que o **mecanismo de exibição** selecionado é **Razor**.</span><span class="sxs-lookup"><span data-stu-id="f7502-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="f7502-179">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7502-179">Click **OK**.</span></span>

    <span data-ttu-id="f7502-180">![Caixa de diálogo Novo projeto ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image3.png "caixa de diálogo Novo projeto ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="f7502-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    *<span data-ttu-id="f7502-181">Caixa de diálogo Novo projeto ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-181">New ASP.NET MVC 4 Project Dialog Box</span></span>*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="f7502-182">Tarefa 2 - explorar a estrutura da solução</span><span class="sxs-lookup"><span data-stu-id="f7502-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="f7502-183">A estrutura ASP.NET MVC inclui um modelo de projeto do Visual Studio que ajuda a criar aplicativos Web que dão suporte ao padrão MVC.</span><span class="sxs-lookup"><span data-stu-id="f7502-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="f7502-184">Este modelo cria um novo aplicativo Web ASP.NET MVC com pastas obrigatórias, modelos de item e as entradas do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f7502-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="f7502-185">Nesta tarefa, você examinará a estrutura da solução para compreender os elementos que estão envolvidos e suas relações.</span><span class="sxs-lookup"><span data-stu-id="f7502-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="f7502-186">As seguintes pastas estão incluídas em todos os aplicativos ASP.NET MVC, porque a estrutura ASP.NET MVC, por padrão usa um &quot;convenção em detrimento da configuração&quot; abordagem e faz algumas suposições padrão com base na nomenclatura de pasta convenções.</span><span class="sxs-lookup"><span data-stu-id="f7502-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="f7502-187">Quando o projeto é criado, examine a estrutura de pasta que foi criada no Gerenciador de soluções, no lado direito:</span><span class="sxs-lookup"><span data-stu-id="f7502-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="f7502-188">![Estrutura de pastas de MVC do ASP.NET no Gerenciador de soluções](aspnet-mvc-4-fundamentals/_static/image4.png "estrutura de pastas de MVC do ASP.NET no Gerenciador de soluções")</span><span class="sxs-lookup"><span data-stu-id="f7502-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    *<span data-ttu-id="f7502-189">Estrutura de pastas de MVC do ASP.NET no Gerenciador de soluções</span><span class="sxs-lookup"><span data-stu-id="f7502-189">ASP.NET MVC Folder structure in Solution Explorer</span></span>*

   1. <span data-ttu-id="f7502-190">**Controladores**.</span><span class="sxs-lookup"><span data-stu-id="f7502-190">**Controllers**.</span></span> <span data-ttu-id="f7502-191">Essa pasta contém as classes do controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="f7502-192">Em um aplicativo MVC com base, os controladores são responsáveis por manipular a interação do usuário final, manipular o modelo e, por fim, escolhendo um modo de exibição para renderizar a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7502-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="f7502-193">A estrutura do MVC requer que os nomes de todos os controladores para terminar com &quot;controlador&quot;-por exemplo, o HomeController, LoginController ou ProductController.</span><span class="sxs-lookup"><span data-stu-id="f7502-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="f7502-194">**Modelos de**.</span><span class="sxs-lookup"><span data-stu-id="f7502-194">**Models**.</span></span> <span data-ttu-id="f7502-195">Essa pasta é fornecida para as classes que representam o modelo de aplicativo para o aplicativo Web do MVC.</span><span class="sxs-lookup"><span data-stu-id="f7502-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="f7502-196">Isso geralmente inclui o código que define objetos e a lógica para interagir com o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f7502-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="f7502-197">Normalmente, os objetos de modelo real será nas bibliotecas de classe separada.</span><span class="sxs-lookup"><span data-stu-id="f7502-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="f7502-198">No entanto, quando você cria um novo aplicativo, você pode incluir classes e, em seguida, movê-los para bibliotecas de classe separada em um momento posterior no ciclo de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f7502-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="f7502-199">**Modos de exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-199">**Views**.</span></span> <span data-ttu-id="f7502-200">Essa pasta é o local recomendado para modos de exibição, os componentes responsáveis por exibir a interface do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="f7502-201">Exibições usam arquivos. aspx,. ascx,. cshtml e. master, além de quaisquer outros arquivos que estão relacionados aos modos de exibição de renderização.</span><span class="sxs-lookup"><span data-stu-id="f7502-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="f7502-202">Pasta de modos de exibição contém uma pasta para cada controlador; a pasta é nomeada com o prefixo do nome do controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="f7502-203">Por exemplo, se você tiver um controlador chamado **HomeController**, a pasta de modos de exibição conterá uma pasta chamada página inicial.</span><span class="sxs-lookup"><span data-stu-id="f7502-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="f7502-204">Por padrão, quando a estrutura ASP.NET MVC carrega uma exibição, ele procura um arquivo. aspx com o nome de exibição solicitada na pasta Views\controllerName (**modos de exibição [Nomedocontrolador] [ação]. aspx**) ou (**exibições [Nomedocontrolador] . [Action] cshtml**) para modos de exibição do Razor.</span><span class="sxs-lookup"><span data-stu-id="f7502-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-205">Além das pastas listadas anteriormente, um aplicativo Web MVC usa o **global. asax** padrões de arquivo para definir o roteamento de URL global e usa o **Web. config** arquivo para configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="f7502-206">Tarefa 3: adicionando um HomeController</span><span class="sxs-lookup"><span data-stu-id="f7502-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="f7502-207">Em aplicativos ASP.NET que não usam a estrutura do MVC, a interação do usuário é organizada em torno de páginas e gerando e manipulando eventos a partir dessas páginas.</span><span class="sxs-lookup"><span data-stu-id="f7502-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="f7502-208">Por outro lado, a interação do usuário com aplicativos ASP.NET MVC é organizada em torno de controladores e seus métodos de ação.</span><span class="sxs-lookup"><span data-stu-id="f7502-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="f7502-209">Por outro lado, o ASP.NET MVC framework mapeia as URLs para classes que são chamadas de controladores.</span><span class="sxs-lookup"><span data-stu-id="f7502-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="f7502-210">Controladores de processar solicitações de entrada, lidar com a entrada do usuário e interações, executar a lógica do aplicativo apropriado e determinar a resposta para enviar de volta para o cliente (exibição de HTML, baixar um arquivo, redirecionar para uma URL diferente, etc.).</span><span class="sxs-lookup"><span data-stu-id="f7502-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="f7502-211">No caso de exibição de HTML, uma classe de controlador normalmente chama um componente de exibição separados para gerar a marcação HTML para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="f7502-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="f7502-212">Em um aplicativo MVC, a exibição mostra apenas informações; o controlador manipula e responde à entrada e à interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7502-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="f7502-213">Nesta tarefa, você adicionará uma classe de controlador que tratará as URLs para a Home page do site do Music Store.</span><span class="sxs-lookup"><span data-stu-id="f7502-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="f7502-214">Clique com botão direito **controladores** pasta dentro do Gerenciador de soluções, selecione **Add** e, em seguida, **controlador** comando:</span><span class="sxs-lookup"><span data-stu-id="f7502-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="f7502-215">![Adicionar um comando do controlador](aspnet-mvc-4-fundamentals/_static/image5.png "adicionar um comando de controlador")</span><span class="sxs-lookup"><span data-stu-id="f7502-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    *<span data-ttu-id="f7502-216">Adicionar comando de controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-216">Add Controller Command</span></span>*
2. <span data-ttu-id="f7502-217">O **Adicionar controlador** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="f7502-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="f7502-218">Nomeie o controlador *HomeController* e pressione **Add**.</span><span class="sxs-lookup"><span data-stu-id="f7502-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="f7502-219">![Adicionar caixa de diálogo do controlador](aspnet-mvc-4-fundamentals/_static/image6.png "Adicionar caixa de diálogo do controlador")</span><span class="sxs-lookup"><span data-stu-id="f7502-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    *<span data-ttu-id="f7502-220">Adicionar caixa de diálogo do controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-220">Add Controller Dialog</span></span>*
3. <span data-ttu-id="f7502-221">O arquivo **HomeController.cs** é criado na **controladores** pasta.</span><span class="sxs-lookup"><span data-stu-id="f7502-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="f7502-222">Para ter o **HomeController** retornar uma cadeia de caracteres em sua ação de índice, substitua o **índice** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="f7502-223">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex1 HomeController índice*)</span><span class="sxs-lookup"><span data-stu-id="f7502-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f7502-224">Tarefa 4 - execução do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="f7502-225">Nesta tarefa, você irá testar o aplicativo em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f7502-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="f7502-226">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="f7502-227">O projeto é compilado e inicia o servidor Web do IIS local.</span><span class="sxs-lookup"><span data-stu-id="f7502-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="f7502-228">O local no servidor Web do IIS será aberto automaticamente um navegador da web apontando para a URL do servidor Web.</span><span class="sxs-lookup"><span data-stu-id="f7502-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="f7502-229">![Aplicativo em execução em um navegador da web](aspnet-mvc-4-fundamentals/_static/image7.png "aplicativo em execução em um navegador da web")</span><span class="sxs-lookup"><span data-stu-id="f7502-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    *<span data-ttu-id="f7502-230">Aplicativo em execução em um navegador da web</span><span class="sxs-lookup"><span data-stu-id="f7502-230">Application running in a web browser</span></span>*

    > [!NOTE]
    > <span data-ttu-id="f7502-231">Servidor Web do IIS local executarão o site em um número de porta aleatório de gratuito.</span><span class="sxs-lookup"><span data-stu-id="f7502-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="f7502-232">Na figura acima, o site está em execução no `http://localhost:50103/`, de modo que ele está usando a porta 50103.</span><span class="sxs-lookup"><span data-stu-id="f7502-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="f7502-233">Seu número de porta pode variar.</span><span class="sxs-lookup"><span data-stu-id="f7502-233">Your port number may vary.</span></span>
2. <span data-ttu-id="f7502-234">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="f7502-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="f7502-235">Exercício 2: Criando um controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="f7502-236">Neste exercício, você aprenderá como atualizar o controlador para implementar a funcionalidade simple do aplicativo Store de música.</span><span class="sxs-lookup"><span data-stu-id="f7502-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="f7502-237">Esse controlador irá definir métodos de ação para lidar com cada uma das seguintes solicitações específicas:</span><span class="sxs-lookup"><span data-stu-id="f7502-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="f7502-238">Uma página de listagem de gêneros música no Store de música</span><span class="sxs-lookup"><span data-stu-id="f7502-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="f7502-239">Uma página de navegação que lista todos os álbuns de música para um gênero específico</span><span class="sxs-lookup"><span data-stu-id="f7502-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="f7502-240">Uma página de detalhes que mostra informações sobre um álbum de música específico</span><span class="sxs-lookup"><span data-stu-id="f7502-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="f7502-241">Para o escopo deste exercício, essas ações simplesmente retornará uma cadeia de caracteres até o momento.</span><span class="sxs-lookup"><span data-stu-id="f7502-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="f7502-242">Tarefa 1 - adicionar uma nova classe StoreController</span><span class="sxs-lookup"><span data-stu-id="f7502-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="f7502-243">Nesta tarefa, você adicionará um novo controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="f7502-244">Se não estiver aberto, inicie **VS Express para Web 2012**.</span><span class="sxs-lookup"><span data-stu-id="f7502-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="f7502-245">No **arquivo** menu, escolha **Abrir projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="f7502-246">Na caixa de diálogo Abrir projeto, navegue até **Source\Ex02 CreatingAController\Begin**, selecione **Begin.sln** e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="f7502-247">Como alternativa, você pode continuar com a solução que você obteve depois de concluir o exercício anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="f7502-248">Se você abriu fornecido **começar** solução, você precisará baixar alguns pacotes do NuGet ausentes antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f7502-249">Para fazer isso, clique o **Project** menu e selecione **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="f7502-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f7502-250">No **gerenciar pacotes NuGet** caixa de diálogo, clique em **restaurar** para baixar os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f7502-251">Por fim, compile a solução clicando **construir** | **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="f7502-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-252">Uma das vantagens de usar o NuGet é que você não precisa enviar todas as bibliotecas em seu projeto, reduzindo o tamanho do projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f7502-253">Com o NuGet Power Tools, especificando as versões do pacote no arquivo Packages. config, você será capaz de baixar todas as bibliotecas necessárias na primeira vez em que você executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f7502-254">É por isso você terá que executar essas etapas depois de abrir uma solução existente neste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="f7502-255">Adicione o novo controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-255">Add the new controller.</span></span> <span data-ttu-id="f7502-256">Para fazer isso, clique com botão direito a **controladores** pasta dentro do Gerenciador de soluções, selecione **Add** e, em seguida, o **controlador** comando.</span><span class="sxs-lookup"><span data-stu-id="f7502-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="f7502-257">Alterar o **nome do controlador** à *StoreController*e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="f7502-258">![Adicionar caixa de diálogo do controlador](aspnet-mvc-4-fundamentals/_static/image8.png "Adicionar caixa de diálogo do controlador")</span><span class="sxs-lookup"><span data-stu-id="f7502-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    *<span data-ttu-id="f7502-259">Adicionar caixa de diálogo do controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-259">Add Controller Dialog</span></span>*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="f7502-260">Tarefa 2 – modificar as ações do StoreController</span><span class="sxs-lookup"><span data-stu-id="f7502-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="f7502-261">Nesta tarefa, você modificará os métodos do controlador que são chamados **ações**.</span><span class="sxs-lookup"><span data-stu-id="f7502-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="f7502-262">As ações são responsáveis por gerenciar solicitações de URL e determinar o conteúdo que deve ser enviado de volta para o navegador ou o usuário que invocou a URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="f7502-263">O **StoreController** classe já tiver um **índice** método.</span><span class="sxs-lookup"><span data-stu-id="f7502-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="f7502-264">Você irá usá-lo posteriormente neste laboratório para implementar a página que lista todos os gêneros de loja de música.</span><span class="sxs-lookup"><span data-stu-id="f7502-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="f7502-265">Por enquanto, basta substituir a **índice** método com o código a seguir que retorna uma cadeia de caracteres &quot;Olá do Store.Index()&quot;:</span><span class="sxs-lookup"><span data-stu-id="f7502-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="f7502-266">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - o Ex2 StoreController índice*)</span><span class="sxs-lookup"><span data-stu-id="f7502-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="f7502-267">Adicione **navegue** e **detalhes** métodos.</span><span class="sxs-lookup"><span data-stu-id="f7502-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="f7502-268">Para fazer isso, adicione o seguinte código para o **StoreController**:</span><span class="sxs-lookup"><span data-stu-id="f7502-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="f7502-269">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - o Ex2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="f7502-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="f7502-270">Tarefa 3: executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="f7502-271">Nesta tarefa, você irá testar o aplicativo em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f7502-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="f7502-272">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-273">O projeto é iniciado **Home** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="f7502-274">Altere a URL para verificar se a implementação de cada ação.</span><span class="sxs-lookup"><span data-stu-id="f7502-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="f7502-275">**/ Store**.</span><span class="sxs-lookup"><span data-stu-id="f7502-275">**/Store**.</span></span> <span data-ttu-id="f7502-276">Você verá  **&quot;Olá do Store.Index()&quot;**.</span><span class="sxs-lookup"><span data-stu-id="f7502-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="f7502-277">**/ Store/procura**.</span><span class="sxs-lookup"><span data-stu-id="f7502-277">**/Store/Browse**.</span></span> <span data-ttu-id="f7502-278">Você verá  **&quot;Olá do Store.Browse()&quot;**.</span><span class="sxs-lookup"><span data-stu-id="f7502-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="f7502-279">**/ Store/detalhes**.</span><span class="sxs-lookup"><span data-stu-id="f7502-279">**/Store/Details**.</span></span> <span data-ttu-id="f7502-280">Você verá  **&quot;Olá do Store.Details()&quot;**.</span><span class="sxs-lookup"><span data-stu-id="f7502-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="f7502-281">![Navegação StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse de navegação")</span><span class="sxs-lookup"><span data-stu-id="f7502-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        *<span data-ttu-id="f7502-282">Navegação /Store/Browse</span><span class="sxs-lookup"><span data-stu-id="f7502-282">Browsing /Store/Browse</span></span>*
3. <span data-ttu-id="f7502-283">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="f7502-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="f7502-284">Exercício 3: Passando parâmetros para um controlador</span><span class="sxs-lookup"><span data-stu-id="f7502-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="f7502-285">Até agora, você tê sido retornando cadeias de caracteres constantes nos controladores de.</span><span class="sxs-lookup"><span data-stu-id="f7502-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="f7502-286">Neste exercício, você aprenderá como passar parâmetros para um controlador usando a URL e a cadeia de consulta e, em seguida, fazendo com que as ações de método responder com o texto para o navegador.</span><span class="sxs-lookup"><span data-stu-id="f7502-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="f7502-287">Tarefa 1 - a parâmetro adicionando gênero StoreController</span><span class="sxs-lookup"><span data-stu-id="f7502-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="f7502-288">Nesta tarefa, você aprenderá a usar o **querystring** para enviar parâmetros para o **procurar** método de ação a **StoreController**.</span><span class="sxs-lookup"><span data-stu-id="f7502-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="f7502-289">Se não estiver aberto, inicie **VS Express para Web**.</span><span class="sxs-lookup"><span data-stu-id="f7502-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="f7502-290">No **arquivo** menu, escolha **Abrir projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="f7502-291">Na caixa de diálogo Abrir projeto, navegue até **Source\Ex03 PassingParametersToAController\Begin**, selecione **Begin.sln** e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="f7502-292">Como alternativa, você pode continuar com a solução que você obteve depois de concluir o exercício anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="f7502-293">Se você abriu fornecido **começar** solução, você precisará baixar alguns pacotes do NuGet ausentes antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f7502-294">Para fazer isso, clique o **Project** menu e selecione **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="f7502-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f7502-295">No **gerenciar pacotes NuGet** caixa de diálogo, clique em **restaurar** para baixar os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f7502-296">Por fim, compile a solução clicando **construir** | **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="f7502-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-297">Uma das vantagens de usar o NuGet é que você não precisa enviar todas as bibliotecas em seu projeto, reduzindo o tamanho do projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f7502-298">Com o NuGet Power Tools, especificando as versões do pacote no arquivo Packages. config, você será capaz de baixar todas as bibliotecas necessárias na primeira vez em que você executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f7502-299">É por isso você terá que executar essas etapas depois de abrir uma solução existente neste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="f7502-300">Abra **StoreController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-300">Open **StoreController** class.</span></span> <span data-ttu-id="f7502-301">Para fazer isso, na **Gerenciador de soluções**, expanda o **controladores** pasta e clique duas vezes em **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="f7502-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="f7502-302">Alterar o **procurar** método, adicionando um parâmetro de cadeia de caracteres para solicitar um gênero específico.</span><span class="sxs-lookup"><span data-stu-id="f7502-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="f7502-303">ASP.NET MVC será automaticamente passar qualquer cadeia de consulta ou parâmetros nomeados de postagem de formulário **gênero** para esse método de ação quando invocado.</span><span class="sxs-lookup"><span data-stu-id="f7502-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="f7502-304">Para fazer isso, substitua os **procurar** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="f7502-305">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="f7502-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="f7502-306">Você está usando o **HttpUtility** método de utilitário para impede que os usuários injetando Javascript para o modo de exibição com um link como   **/Store/procurar? Gênero =&lt;script&gt;Window '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span><span class="sxs-lookup"><span data-stu-id="f7502-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="f7502-307">Para obter mais explicações, visite [este artigo do msdn](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span><span class="sxs-lookup"><span data-stu-id="f7502-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="f7502-308">Tarefa 2 - executando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="f7502-309">Nesta tarefa, você irá testar o aplicativo em um navegador da web e usar o **gênero** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f7502-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="f7502-310">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-311">O projeto é iniciado **Home** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="f7502-312">Altere a URL para   */Store/procurar? Gênero = Disco* para verificar se a ação recebe o parâmetro de gênero.</span><span class="sxs-lookup"><span data-stu-id="f7502-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="f7502-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span><span class="sxs-lookup"><span data-stu-id="f7502-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    *<span data-ttu-id="f7502-314">Browsing /Store/Browse?Genre=Disco</span><span class="sxs-lookup"><span data-stu-id="f7502-314">Browsing /Store/Browse?Genre=Disco</span></span>*
3. <span data-ttu-id="f7502-315">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="f7502-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="f7502-316">Tarefa 3: adicionando um parâmetro de Id inserido na URL</span><span class="sxs-lookup"><span data-stu-id="f7502-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="f7502-317">Nesta tarefa, você aprenderá a usar o **URL** para passar um **Id** parâmetro para o **detalhes** o método de ação do **StoreController**.</span><span class="sxs-lookup"><span data-stu-id="f7502-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="f7502-318">Padrão de ASP.NET MVC convenção de roteamento é tratar o segmento de URL após o nome do método de ação como um parâmetro denominado **Id**. Se seu método de ação tem um parâmetro chamado Id, em seguida, ASP.NET MVC automaticamente passará o segmento de URL para você como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f7502-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="f7502-319">Na URL **Store/detalhes/5**, **Id** será interpretado como **5**.</span><span class="sxs-lookup"><span data-stu-id="f7502-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="f7502-320">Alterar o **detalhes** método da **StoreController**, adicionar um **int** parâmetro chamado **id**. Para fazer isso, substitua os **detalhes** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="f7502-321">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="f7502-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="f7502-322">Tarefa 4 - execução do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="f7502-323">Nesta tarefa, você irá testar o aplicativo em um navegador da web e usar o **Id** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f7502-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="f7502-324">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-325">O projeto é iniciado **Home** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="f7502-326">Altere a URL para */Store/Details/5* para verificar se a ação recebe o parâmetro de id.</span><span class="sxs-lookup"><span data-stu-id="f7502-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="f7502-327">![Navegação StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 de navegação")</span><span class="sxs-lookup"><span data-stu-id="f7502-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    *<span data-ttu-id="f7502-328">Navegação /Store/Details/5</span><span class="sxs-lookup"><span data-stu-id="f7502-328">Browsing /Store/Details/5</span></span>*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="f7502-329">Exercício 4: Criando uma exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="f7502-330">Até agora você tê sido retornar cadeias de caracteres de ações do controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="f7502-331">Embora isso seja uma maneira útil de entender como funcionam os controladores, ele não é como seus aplicativos Web reais são criados.</span><span class="sxs-lookup"><span data-stu-id="f7502-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="f7502-332">Modos de exibição são componentes que fornecem uma abordagem melhor para gerar HTML volta para o navegador com o uso de arquivos de modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="f7502-333">Neste exercício, você aprenderá como adicionar uma página de layout mestre para configurar um modelo de conteúdo HTML comum, uma folha de estilos para aprimorar a aparência do site e, finalmente, um modelo de exibição para habilitar o HomeController retornar HTML.</span><span class="sxs-lookup"><span data-stu-id="f7502-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a><span data-ttu-id="f7502-334">Tarefa 1: modificar o arquivo \_layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="f7502-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="f7502-335">O arquivo **~/Views/Shared/\_layout. cshtml** permite configurar um modelo para HTML comuns para usar em todo o site.</span><span class="sxs-lookup"><span data-stu-id="f7502-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="f7502-336">Nesta tarefa, você adicionará uma página de layout mestre com um cabeçalho comum com links para a área de Home page e Store.</span><span class="sxs-lookup"><span data-stu-id="f7502-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="f7502-337">Se não estiver aberto, inicie **VS Express para Web**.</span><span class="sxs-lookup"><span data-stu-id="f7502-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="f7502-338">No **arquivo** menu, escolha **Abrir projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="f7502-339">Na caixa de diálogo Abrir projeto, navegue até **Source\Ex04 CreatingAView\Begin**, selecione **Begin.sln** e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="f7502-340">Como alternativa, você pode continuar com a solução que você obteve depois de concluir o exercício anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="f7502-341">Se você abriu fornecido **começar** solução, você precisará baixar alguns pacotes do NuGet ausentes antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f7502-342">Para fazer isso, clique o **Project** menu e selecione **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="f7502-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f7502-343">No **gerenciar pacotes NuGet** caixa de diálogo, clique em **restaurar** para baixar os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f7502-344">Por fim, compile a solução clicando **construir** | **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="f7502-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-345">Uma das vantagens de usar o NuGet é que você não precisa enviar todas as bibliotecas em seu projeto, reduzindo o tamanho do projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f7502-346">Com o NuGet Power Tools, especificando as versões do pacote no arquivo Packages. config, você será capaz de baixar todas as bibliotecas necessárias na primeira vez em que você executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f7502-347">É por isso você terá que executar essas etapas depois de abrir uma solução existente neste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="f7502-348">O arquivo  <strong>\_layout. cshtml</strong> contém o layout de contêiner HTML para todas as páginas no site.</span><span class="sxs-lookup"><span data-stu-id="f7502-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="f7502-349">Ele inclui o <strong>&lt;html&gt;</strong> elemento para a resposta HTML, bem como o <strong>&lt;head&gt;</strong> e <strong>&lt;corpo&gt;</strong> elementos.</span><span class="sxs-lookup"><span data-stu-id="f7502-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="f7502-350"><strong>@RenderBody()</strong> o HTML dentro do corpo identificar regiões dessa exibição modelos poderão ser preenchidos com conteúdo dinâmico.</span><span class="sxs-lookup"><span data-stu-id="f7502-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="f7502-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="f7502-352">Adicione um cabeçalho comum com links para a área de Home page e Store em todas as páginas no site.</span><span class="sxs-lookup"><span data-stu-id="f7502-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="f7502-353">Para fazer isso, adicione o seguinte código abaixo &lt;corpo&gt; instrução.</span><span class="sxs-lookup"><span data-stu-id="f7502-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="f7502-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="f7502-355">Inclua um div para renderizar a seção de corpo de cada página.</span><span class="sxs-lookup"><span data-stu-id="f7502-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="f7502-356">Substitua  <strong>@RenderBody()</strong> com o seguinte código realçado: (C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-356">Replace <strong>@RenderBody()</strong> with the following highlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="f7502-357">Você sabia?</span><span class="sxs-lookup"><span data-stu-id="f7502-357">Did you know?</span></span> <span data-ttu-id="f7502-358">Visual Studio 2012 tem trechos de código que tornam fácil adicionar código comumente usado em HTML, arquivos de código e muito mais!</span><span class="sxs-lookup"><span data-stu-id="f7502-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="f7502-359">Testá-lo, digitando **&lt;div&gt;** e pressionando **guia** duas vezes para inserir uma completa **div** marca.</span><span class="sxs-lookup"><span data-stu-id="f7502-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="f7502-360">Tarefa 2 - adicionar folha de estilos CSS</span><span class="sxs-lookup"><span data-stu-id="f7502-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="f7502-361">O modelo de projeto vazio inclui um arquivo CSS muito simplificado que inclui apenas os estilos usados para exibir mensagens de validação e formas básicas.</span><span class="sxs-lookup"><span data-stu-id="f7502-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="f7502-362">Você usará o CSS e imagens (potencialmente fornecidas por um designer) adicionais para aprimorar a aparência do site.</span><span class="sxs-lookup"><span data-stu-id="f7502-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="f7502-363">Nesta tarefa, você irá adicionar uma folha de estilos CSS para definir os estilos do site.</span><span class="sxs-lookup"><span data-stu-id="f7502-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="f7502-364">O arquivo CSS e imagens são incluídas na **Source\Assets\Content** pasta deste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="f7502-365">Para adicioná-las para o aplicativo, arraste seu conteúdo de um **Windows Explorer** janela para o **Gerenciador de soluções** no Visual Studio Express para Web, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="f7502-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="f7502-366">![Arrastar conteúdo de estilo](aspnet-mvc-4-fundamentals/_static/image12.png "arrastar conteúdo de estilo")</span><span class="sxs-lookup"><span data-stu-id="f7502-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    *<span data-ttu-id="f7502-367">Arrastar conteúdo de estilo</span><span class="sxs-lookup"><span data-stu-id="f7502-367">Dragging style contents</span></span>*
2. <span data-ttu-id="f7502-368">Uma caixa de diálogo de aviso será exibido, solicitando a confirmação substituir **CSS** de arquivo e algumas imagens existentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="f7502-369">Verifique **aplicar a todos os itens** e clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f7502-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="f7502-370">Tarefa 3: adicionando um modelo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="f7502-371">Nesta tarefa, você adicionará um modelo de exibição para gerar a resposta HTML que usará a página mestra do layout e CSS adicionados neste exercício.</span><span class="sxs-lookup"><span data-stu-id="f7502-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="f7502-372">Para usar um modelo de exibição quando a navegação na home page do site, você primeiro precisará indicar que em vez de retornar uma cadeia de caracteres, o **índice HomeController** método será retornado um **exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="f7502-373">Abra **HomeController** classe e altere seu **índice** método para retornar um **ActionResult**, e que ele retorne **View()**.</span><span class="sxs-lookup"><span data-stu-id="f7502-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="f7502-374">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex4 HomeController índice*)</span><span class="sxs-lookup"><span data-stu-id="f7502-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="f7502-375">Agora, você precisará adicionar um modelo de exibição apropriado.</span><span class="sxs-lookup"><span data-stu-id="f7502-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="f7502-376">Para fazer isso, **com o botão direito** dentro de **índice** método de ação e selecione **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="f7502-377">Isso abrirá o **adicionar exibição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7502-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="f7502-378">![Adicionando uma exibição de dentro do método de índice](aspnet-mvc-4-fundamentals/_static/image13.png "adicionando uma exibição de dentro do método Index")</span><span class="sxs-lookup"><span data-stu-id="f7502-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    *<span data-ttu-id="f7502-379">Adicionando uma exibição de dentro do método Index</span><span class="sxs-lookup"><span data-stu-id="f7502-379">Adding a View from within the Index method</span></span>*
3. <span data-ttu-id="f7502-380">O **adicionar exibição** caixa de diálogo será exibida para gerar um arquivo de modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="f7502-381">Por padrão, essa caixa de diálogo preenche previamente o nome do modelo de exibição para que ele corresponda ao método de ação que irá usá-lo.</span><span class="sxs-lookup"><span data-stu-id="f7502-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="f7502-382">Como você usou o **adicionar exibição** menu de contexto dentro a **índice** método de ação dentro do HomeController, o **adicionar exibição** caixa de diálogo tem um índice como o nome de exibição padrão.</span><span class="sxs-lookup"><span data-stu-id="f7502-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="f7502-383">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-383">Click **Add**.</span></span>

    <span data-ttu-id="f7502-384">![Adicionar caixa de diálogo de exibição](aspnet-mvc-4-fundamentals/_static/image14.png "Adicionar caixa de diálogo de exibição")</span><span class="sxs-lookup"><span data-stu-id="f7502-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    *<span data-ttu-id="f7502-385">Adicionar caixa de diálogo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-385">Add View Dialog</span></span>*
4. <span data-ttu-id="f7502-386">O Visual Studio gera uma **index. cshtml** modelo de exibição dentro de **Views\Home** pasta e, em seguida, abre.</span><span class="sxs-lookup"><span data-stu-id="f7502-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="f7502-387">![Página inicial de exibição de índice criada](aspnet-mvc-4-fundamentals/_static/image15.png "exibição Home índice criado")</span><span class="sxs-lookup"><span data-stu-id="f7502-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    *<span data-ttu-id="f7502-388">Exibição de índice inicial criada</span><span class="sxs-lookup"><span data-stu-id="f7502-388">Home Index view created</span></span>*

    > [!NOTE]
    > <span data-ttu-id="f7502-389">nome e local a **index. cshtml** arquivo é relevante e segue as convenções de nomenclatura padrão ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f7502-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="f7502-390">A pasta \Views\**página inicial*\* corresponde ao nome do controlador (**Home** controlador).</span><span class="sxs-lookup"><span data-stu-id="f7502-390">The folder \Views\**Home*\* matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="f7502-391">O nome do modelo de exibição (**índice**), corresponde ao método de ação de controlador que deseja exibir o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="f7502-392">Dessa forma, o ASP.NET MVC evita a necessidade de especificar explicitamente o nome ou local de um modelo de exibição ao usar essa convenção de nomenclatura para retornar uma exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="f7502-393">O modelo de exibição gerado se baseia a  **\_layout. cshtml** template definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7502-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="f7502-394">Atualizar a propriedade ViewBag Title para **página inicial**e altere o conteúdo principal **esta é a Home Page**, conforme mostrado no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="f7502-395">Selecione **MvcMusicStore** projeto no Gerenciador de soluções e pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="f7502-396">Tarefa 4: Verificação</span><span class="sxs-lookup"><span data-stu-id="f7502-396">Task 4: Verification</span></span>

<span data-ttu-id="f7502-397">Para verificar que você realizou corretamente todas as etapas no exercício anterior, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7502-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="f7502-398">Com o aplicativo aberto em um navegador, você deve observar que:</span><span class="sxs-lookup"><span data-stu-id="f7502-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="f7502-399">Método de ação de índice do HomeController encontrado e exibidos a **\Views\Home\Index.cshtml** exibir modelo, mesmo que o código chamado **retornar View()**, porque o modelo de exibição seguido de convenção de nomenclatura padrão.</span><span class="sxs-lookup"><span data-stu-id="f7502-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="f7502-400">A Home Page exibe a mensagem de boas-vinda definida dentro de **\Views\Home\Index.cshtml** modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="f7502-401">A Home Page é usando o  **\_layout. cshtml** modelo, e, portanto, a mensagem de boas-vinda está contida o layout do site padrão HTML.</span><span class="sxs-lookup"><span data-stu-id="f7502-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="f7502-402">![Página inicial usando o LayoutPage definido e o estilo de exibição de índice](aspnet-mvc-4-fundamentals/_static/image16.png "índice visualização inicial usando o LayoutPage e o estilo definido")</span><span class="sxs-lookup"><span data-stu-id="f7502-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    *<span data-ttu-id="f7502-403">Usando o LayoutPage definido e o estilo de exibição de índice inicial</span><span class="sxs-lookup"><span data-stu-id="f7502-403">Home Index View using the defined LayoutPage and style</span></span>*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="f7502-404">Exercício 5: Criando um modelo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="f7502-405">Até agora, feitas seus modos de exibição exibem inserido no código HTML, mas, para criar aplicativos web dinâmicos, o modelo de exibição deve receber informações do controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="f7502-406">Uma técnica comum a ser usado para essa finalidade é a **ViewModel** padrão, que permite que um controlador empacotar todas as informações necessárias para gerar a resposta HTML apropriada.</span><span class="sxs-lookup"><span data-stu-id="f7502-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="f7502-407">Neste exercício, você aprenderá como criar uma classe ViewModel e adicionar as propriedades necessárias: o número de gêneros no armazenamento e uma lista desses gêneros.</span><span class="sxs-lookup"><span data-stu-id="f7502-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="f7502-408">Também atualizará o StoreController para usar o ViewModel criado e, por fim, você criará um novo modelo de exibição que exibirá as propriedades mencionadas na página.</span><span class="sxs-lookup"><span data-stu-id="f7502-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="f7502-409">Tarefa 1 - criação de uma classe ViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="f7502-410">Nesta tarefa, você criará uma classe ViewModel que implementará o cenário de listagem de gênero de Store.</span><span class="sxs-lookup"><span data-stu-id="f7502-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="f7502-411">Se não estiver aberto, inicie **VS Express para Web**.</span><span class="sxs-lookup"><span data-stu-id="f7502-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="f7502-412">No **arquivo** menu, escolha **Abrir projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="f7502-413">Na caixa de diálogo Abrir projeto, navegue até **Source\Ex05 CreatingAViewModel\Begin**, selecione **Begin.sln** e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="f7502-414">Como alternativa, você pode continuar com a solução que você obteve depois de concluir o exercício anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="f7502-415">Se você abriu fornecido **começar** solução, você precisará baixar alguns pacotes do NuGet ausentes antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f7502-416">Para fazer isso, clique o **Project** menu e selecione **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="f7502-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f7502-417">No **gerenciar pacotes NuGet** caixa de diálogo, clique em **restaurar** para baixar os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f7502-418">Por fim, compile a solução clicando **construir** | **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="f7502-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-419">Uma das vantagens de usar o NuGet é que você não precisa enviar todas as bibliotecas em seu projeto, reduzindo o tamanho do projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f7502-420">Com o NuGet Power Tools, especificando as versões do pacote no arquivo Packages. config, você será capaz de baixar todas as bibliotecas necessárias na primeira vez em que você executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f7502-421">É por isso você terá que executar essas etapas depois de abrir uma solução existente neste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="f7502-422">Criar uma **ViewModels** pasta usada para armazenar o ViewModel.</span><span class="sxs-lookup"><span data-stu-id="f7502-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="f7502-423">Para fazer isso, clique com botão direito superior **MvcMusicStore** projeto, selecione **Add** e, em seguida, **nova pasta**.</span><span class="sxs-lookup"><span data-stu-id="f7502-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="f7502-424">![Adicionando uma nova pasta](aspnet-mvc-4-fundamentals/_static/image17.png "adicionando uma nova pasta")</span><span class="sxs-lookup"><span data-stu-id="f7502-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    *<span data-ttu-id="f7502-425">Adicionando uma nova pasta</span><span class="sxs-lookup"><span data-stu-id="f7502-425">Adding a new folder</span></span>*
4. <span data-ttu-id="f7502-426">Nomeie a pasta *ViewModels*.</span><span class="sxs-lookup"><span data-stu-id="f7502-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="f7502-427">![Pasta ViewModels no Gerenciador de soluções](aspnet-mvc-4-fundamentals/_static/image18.png "pasta ViewModels no Gerenciador de soluções")</span><span class="sxs-lookup"><span data-stu-id="f7502-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    *<span data-ttu-id="f7502-428">Pasta ViewModels no Gerenciador de soluções</span><span class="sxs-lookup"><span data-stu-id="f7502-428">ViewModels folder in Solution Explorer</span></span>*
5. <span data-ttu-id="f7502-429">Criar uma **ViewModel** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="f7502-430">Para fazer isso, clique com botão direito no **ViewModels** pasta recentemente criada, selecione **Add** e, em seguida, **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f7502-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="f7502-431">Sob **código**, escolha o **classe** item e nomeie o arquivo *StoreIndexViewModel.cs*, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="f7502-432">![Adicionando uma nova classe](aspnet-mvc-4-fundamentals/_static/image19.png "adicionando uma nova classe")</span><span class="sxs-lookup"><span data-stu-id="f7502-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    *<span data-ttu-id="f7502-433">Adicionando uma nova classe</span><span class="sxs-lookup"><span data-stu-id="f7502-433">Adding a new Class</span></span>*

    <span data-ttu-id="f7502-434">![Criando classe StoreIndexViewModel](aspnet-mvc-4-fundamentals/_static/image20.png "StoreIndexViewModel de criação de classe")</span><span class="sxs-lookup"><span data-stu-id="f7502-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    *<span data-ttu-id="f7502-435">Criando classe StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-435">Creating StoreIndexViewModel class</span></span>*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="f7502-436">Tarefa 2: Adicionando propriedades à classe ViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="f7502-437">Há dois parâmetros a serem passados do StoreController para o modelo de exibição para gerar a resposta esperada do HTML: o número de gêneros no armazenamento e uma lista desses gêneros.</span><span class="sxs-lookup"><span data-stu-id="f7502-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="f7502-438">Nesta tarefa, você adicionará as propriedades, 2 para o **StoreIndexViewModel** classe: **NumberOfGenres** (um inteiro) e **gêneros** (uma lista de cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="f7502-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="f7502-439">Adicione **NumberOfGenres** e **gêneros** as propriedades para o **StoreIndexViewModel** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="f7502-440">Para fazer isso, adicione as seguintes linhas de 2 à definição de classe:</span><span class="sxs-lookup"><span data-stu-id="f7502-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="f7502-441">(Código de trecho de código – *ASP.NET MVC 4 conceitos básicos - propriedades de Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="f7502-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="f7502-442">O **{get; definir;}**  notação faz uso de C# recurso de propriedades implementadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f7502-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="f7502-443">Ele fornece os benefícios de uma propriedade sem a necessidade de nós declarar um campo de suporte.</span><span class="sxs-lookup"><span data-stu-id="f7502-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="f7502-444">Tarefa 3: atualização StoreController para usar o StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="f7502-445">O **StoreIndexViewModel** classe encapsula as informações necessárias para passar de **StoreController**do **índice** método para um modelo de exibição para gerar uma resposta .</span><span class="sxs-lookup"><span data-stu-id="f7502-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="f7502-446">Nesta tarefa, você atualizará o **StoreController** usar o **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="f7502-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="f7502-447">Abra **StoreController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="f7502-448">![Abrindo a classe StoreController](aspnet-mvc-4-fundamentals/_static/image21.png "StoreController de abertura de classe")</span><span class="sxs-lookup"><span data-stu-id="f7502-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    *<span data-ttu-id="f7502-449">Classe de StoreController de abertura</span><span class="sxs-lookup"><span data-stu-id="f7502-449">Opening StoreController class</span></span>*
2. <span data-ttu-id="f7502-450">Para usar o **StoreIndexViewModel** classe a **StoreController**, adicione o namespace a seguir na parte superior da **StoreController** código:</span><span class="sxs-lookup"><span data-stu-id="f7502-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="f7502-451">(Código de trecho de código – *ASP.NET MVC 4 conceitos básicos - StoreIndexViewModel Ex5 usando ViewModels*)</span><span class="sxs-lookup"><span data-stu-id="f7502-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="f7502-452">Alterar o **StoreController**do **índice** método de ação para que ele cria e preenche uma **StoreIndexViewModel** de objeto e, em seguida, passa-o para um modelo de exibição para gere uma resposta HTML com ele.</span><span class="sxs-lookup"><span data-stu-id="f7502-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7502-453">Laboratório &quot;acesso a dados e modelos do ASP.NET MVC&quot; você irá escrever código que recupera a lista de gêneros de repositório de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f7502-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="f7502-454">O código a seguir, você aprenderá a criar uma **lista** de gêneros dados fictícios que preencherão o **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="f7502-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="f7502-455">Depois de criar e configurar o **StoreIndexViewModel** do objeto, ele será passado como um argumento para o **exibição** método.</span><span class="sxs-lookup"><span data-stu-id="f7502-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="f7502-456">Isso indica que o modelo de exibição usará esse objeto para gerar uma resposta HTML com ele.</span><span class="sxs-lookup"><span data-stu-id="f7502-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="f7502-457">Substitua os **índice** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="f7502-458">(Código de trecho de código – *ASP.NET MVC 4 conceitos básicos - método Ex5 StoreController Index*)</span><span class="sxs-lookup"><span data-stu-id="f7502-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="f7502-459">Se você estiver familiarizado com c#, você pode presumir que usar **var** significa que o **viewModel** variável é a associação tardia.</span><span class="sxs-lookup"><span data-stu-id="f7502-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="f7502-460">Que não estiver correta – o compilador c# está usando com base em atribuir à variável de inferência de tipo para determinar que **viewModel** é do tipo **StoreIndexViewModel**.</span><span class="sxs-lookup"><span data-stu-id="f7502-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="f7502-461">Além disso, ao compilar local **viewModel** variável como um **StoreIndexViewModel** tipo de verificação de tempo de compilação get e suporte de editor de códigos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="f7502-462">Tarefa 4 - criar um modelo de exibição que usa StoreIndexViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="f7502-463">Nesta tarefa, você criará um modelo de exibição que usará um objeto StoreIndexViewModel passado do controlador para exibir uma lista de gêneros.</span><span class="sxs-lookup"><span data-stu-id="f7502-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="f7502-464">Antes de criar o novo modelo de exibição, vamos criar o projeto para que o **caixa de diálogo Adicionar modo de exibição** sabe sobre o **StoreIndexViewModel** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="f7502-465">Compile o projeto selecionando o **construir** item de menu e, em seguida, **MvcMusicStore Build**.</span><span class="sxs-lookup"><span data-stu-id="f7502-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="f7502-466">![Compilar o projeto](aspnet-mvc-4-fundamentals/_static/image22.png "compilar o projeto")</span><span class="sxs-lookup"><span data-stu-id="f7502-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    *<span data-ttu-id="f7502-467">Compilar o projeto</span><span class="sxs-lookup"><span data-stu-id="f7502-467">Building the project</span></span>*
2. <span data-ttu-id="f7502-468">Crie um novo modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-468">Create a new View template.</span></span> <span data-ttu-id="f7502-469">Para fazer isso, clique com botão direito dentro do **índice** método e selecione **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="f7502-470">![Adicionando uma exibição](aspnet-mvc-4-fundamentals/_static/image23.png "adicionando uma exibição")</span><span class="sxs-lookup"><span data-stu-id="f7502-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    *<span data-ttu-id="f7502-471">Adicionar uma exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-471">Adding a View</span></span>*
3. <span data-ttu-id="f7502-472">Porque o **caixa de diálogo Adicionar modo de exibição** foi invocado a partir o **StoreController**, ele adicionará o modelo de exibição por padrão em um **\Views\Store\Index.cshtml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f7502-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="f7502-473">Verifique as **criar um fortemente tipada-modo de exibição** caixa de seleção e, em seguida, selecione **StoreIndexViewModel** como o **classe de modelo**.</span><span class="sxs-lookup"><span data-stu-id="f7502-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="f7502-474">Além disso, certifique-se de que o mecanismo de exibição selecionado **Razor**.</span><span class="sxs-lookup"><span data-stu-id="f7502-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="f7502-475">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-475">Click **Add**.</span></span>

    <span data-ttu-id="f7502-476">![Adicionar caixa de diálogo de exibição](aspnet-mvc-4-fundamentals/_static/image24.png "Adicionar caixa de diálogo de exibição")</span><span class="sxs-lookup"><span data-stu-id="f7502-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    *<span data-ttu-id="f7502-477">Adicionar caixa de diálogo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-477">Add View Dialog</span></span>*

    <span data-ttu-id="f7502-478">O **\Views\Store\Index.cshtml** arquivo de modelo de exibição é criado e aberto.</span><span class="sxs-lookup"><span data-stu-id="f7502-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="f7502-479">Com base nas informações fornecidas para o **adicionar exibição** caixa de diálogo na última etapa, a exibição de modelo espera que um **StoreIndexViewModel** instância como os dados a serem usados para gerar uma resposta HTML.</span><span class="sxs-lookup"><span data-stu-id="f7502-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="f7502-480">Você observará que o modelo herda um `ViewPage<musicstore.viewmodels.storeindexviewmodel>` em c#.</span><span class="sxs-lookup"><span data-stu-id="f7502-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="f7502-481">Tarefa 5 – atualizar o modelo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="f7502-482">Nesta tarefa, você atualizará o modelo de exibição criado na última tarefa para recuperar o número de gêneros e seus nomes dentro da página.</span><span class="sxs-lookup"><span data-stu-id="f7502-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="f7502-483">Você usará a sintaxe @ (também conhecido como &quot;nuggets de código&quot;) para executar o código dentro do modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="f7502-484">No **index. cshtml** do arquivo, dentro de **Store** pasta, substitua o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. <span data-ttu-id="f7502-485">Loop através da lista de gênero em **StoreIndexViewModel** e criar um HTML **&lt;ul&gt;** listar usando um **foreach** loop.</span><span class="sxs-lookup"><span data-stu-id="f7502-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="f7502-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="f7502-487">Pressione **F5** para executar o aplicativo e procure **/Store**.</span><span class="sxs-lookup"><span data-stu-id="f7502-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="f7502-488">Você verá a lista de gêneros passado a **StoreIndexViewModel** objeto o **StoreController** para o modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="f7502-489">![Modo de exibição exibindo uma lista de gêneros](aspnet-mvc-4-fundamentals/_static/image26.png "exibindo uma lista de gêneros de exibição")</span><span class="sxs-lookup"><span data-stu-id="f7502-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    *<span data-ttu-id="f7502-490">Exibindo uma lista de gêneros de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-490">View displaying a list of genres</span></span>*
4. <span data-ttu-id="f7502-491">Feche o navegador.</span><span class="sxs-lookup"><span data-stu-id="f7502-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="f7502-492">Exercício 6: Usando parâmetros no modo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="f7502-493">No Exercício 3, você aprendeu como passar parâmetros para o controlador.</span><span class="sxs-lookup"><span data-stu-id="f7502-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="f7502-494">Neste exercício, você aprenderá como usar esses parâmetros no modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="f7502-495">Para essa finalidade, você será apresentado pela primeira vez para classes de modelo que ajudarão você a gerenciar seu dados e lógica de domínio.</span><span class="sxs-lookup"><span data-stu-id="f7502-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="f7502-496">Além disso, você aprenderá como criar links para páginas dentro do aplicativo ASP.NET MVC sem se preocupar de coisas como a codificação de caminhos de URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="f7502-497">Tarefa 1: Adicionar Classes de modelo</span><span class="sxs-lookup"><span data-stu-id="f7502-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="f7502-498">Ao contrário de ViewModels, que são criados apenas para passar informações do controlador para o modo de exibição, classes de modelo são criadas para conter e gerenciar dados e lógica de domínio.</span><span class="sxs-lookup"><span data-stu-id="f7502-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="f7502-499">Nesta tarefa, você adicionará duas classes de modelo para representar esses conceitos: **Gênero** e **álbum**.</span><span class="sxs-lookup"><span data-stu-id="f7502-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="f7502-500">Se não estiver aberto, inicie **VS Express para Web**</span><span class="sxs-lookup"><span data-stu-id="f7502-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="f7502-501">No **arquivo** menu, escolha **Abrir projeto**.</span><span class="sxs-lookup"><span data-stu-id="f7502-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="f7502-502">Na caixa de diálogo Abrir projeto, navegue até **Source\Ex06 UsingParametersInView\Begin**, selecione **Begin.sln** e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="f7502-503">Como alternativa, você pode continuar com a solução que você obteve depois de concluir o exercício anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="f7502-504">Se você abriu fornecido **começar** solução, você precisará baixar alguns pacotes do NuGet ausentes antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f7502-505">Para fazer isso, clique o **Project** menu e selecione **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="f7502-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f7502-506">No **gerenciar pacotes NuGet** caixa de diálogo, clique em **restaurar** para baixar os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f7502-507">Por fim, compile a solução clicando **construir** | **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="f7502-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f7502-508">Uma das vantagens de usar o NuGet é que você não precisa enviar todas as bibliotecas em seu projeto, reduzindo o tamanho do projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f7502-509">Com o NuGet Power Tools, especificando as versões do pacote no arquivo Packages. config, você será capaz de baixar todas as bibliotecas necessárias na primeira vez em que você executar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f7502-510">É por isso você terá que executar essas etapas depois de abrir uma solução existente neste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="f7502-511">Adicionar um **gênero** classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="f7502-512">Para fazer isso, clique com botão direito do **modelos** pasta na **Gerenciador de soluções**, selecione **adicionar** e, em seguida, o **Novo Item** opção.</span><span class="sxs-lookup"><span data-stu-id="f7502-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="f7502-513">Sob **código**, escolha o **classe** item e nomeie o arquivo *Genre.cs*, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="f7502-514">![Adicionando uma classe](aspnet-mvc-4-fundamentals/_static/image27.png "adicionando uma classe")</span><span class="sxs-lookup"><span data-stu-id="f7502-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    *<span data-ttu-id="f7502-515">Adicionando um novo item</span><span class="sxs-lookup"><span data-stu-id="f7502-515">Adding a new item</span></span>*

    <span data-ttu-id="f7502-516">![Adicionar classe de modelo de gênero](aspnet-mvc-4-fundamentals/_static/image28.png "Adicionar classe de modelo de gênero")</span><span class="sxs-lookup"><span data-stu-id="f7502-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    *<span data-ttu-id="f7502-517">Adicionar classe de modelo de gênero</span><span class="sxs-lookup"><span data-stu-id="f7502-517">Add Genre Model Class</span></span>*
4. <span data-ttu-id="f7502-518">Adicionar um **nome** propriedade para a classe de gênero.</span><span class="sxs-lookup"><span data-stu-id="f7502-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="f7502-519">Para fazer isso, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f7502-519">To do this, add the following code:</span></span>

    <span data-ttu-id="f7502-520">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 gênero*)</span><span class="sxs-lookup"><span data-stu-id="f7502-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="f7502-521">Seguindo o mesmo procedimento como antes, adicione uma **álbum** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="f7502-522">Para fazer isso, clique com botão direito do **modelos** pasta na **Gerenciador de soluções**, selecione **adicionar** e, em seguida, o **Novo Item** opção.</span><span class="sxs-lookup"><span data-stu-id="f7502-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="f7502-523">Sob **código**, escolha o **classe** item e nomeie o arquivo *Album.cs*, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="f7502-524">Adicione duas propriedades à classe álbum: **Gênero** e **título**.</span><span class="sxs-lookup"><span data-stu-id="f7502-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="f7502-525">Para fazer isso, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f7502-525">To do this, add the following code:</span></span>

    <span data-ttu-id="f7502-526">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - álbum Ex6*)</span><span class="sxs-lookup"><span data-stu-id="f7502-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="f7502-527">Tarefa 2 - adicionando um StoreBrowseViewModel</span><span class="sxs-lookup"><span data-stu-id="f7502-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="f7502-528">Um **StoreBrowseViewModel** será usado nessa tarefa para mostrar os álbuns que correspondem a um gênero selecionado.</span><span class="sxs-lookup"><span data-stu-id="f7502-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="f7502-529">Nesta tarefa, você criará essa classe e, em seguida, adicione duas propriedades para lidar com o **gênero** e seu **álbum**da lista.</span><span class="sxs-lookup"><span data-stu-id="f7502-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="f7502-530">Adicionar um **StoreBrowseViewModel** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="f7502-531">Para fazer isso, clique com botão direito do **ViewModels** pasta na **Gerenciador de soluções**, selecione **adicionar** e, em seguida, o **Novo Item** opção.</span><span class="sxs-lookup"><span data-stu-id="f7502-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="f7502-532">Sob **código**, escolha o **classe** item e nomeie o arquivo *StoreBrowseViewModel.cs*, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="f7502-533">Adicione uma referência para os modelos no **StoreBrowseViewModel** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="f7502-534">Para fazer isso, adicione o seguinte usando o namespace:</span><span class="sxs-lookup"><span data-stu-id="f7502-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="f7502-535">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="f7502-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="f7502-536">Adicionar duas propriedades a serem **StoreBrowseViewModel** classe: **Gênero** e **álbuns**.</span><span class="sxs-lookup"><span data-stu-id="f7502-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="f7502-537">Para fazer isso, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f7502-537">To do this, add the following code:</span></span>

    <span data-ttu-id="f7502-538">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="f7502-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="f7502-539">O que é **lista&lt;álbum&gt;**  ?: Essa definição é usando o **lista&lt;T&gt;**  tipo, onde **T** restringe o tipo ao qual os elementos disso **lista** pertence, nesse caso **Álbum** (ou qualquer um dos seus descendentes).</span><span class="sxs-lookup"><span data-stu-id="f7502-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="f7502-540">Essa capacidade de criar classes e métodos que adiam a especificação de um ou mais tipos até que a classe ou método é declarado e instanciado pelo código do cliente é um recurso da linguagem c# chamado **genéricos**.</span><span class="sxs-lookup"><span data-stu-id="f7502-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="f7502-541">**Lista&lt;T&gt;**  é o equivalente genérico a **ArrayList** digite e está disponível na **Collections** namespace.</span><span class="sxs-lookup"><span data-stu-id="f7502-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="f7502-542">Um dos benefícios de usar **genéricos** é que, como o tipo é especificado, você não precisa cuidar da verificação de operações como converter os elementos de tipo **álbum** como você faria com um **ArrayList**.</span><span class="sxs-lookup"><span data-stu-id="f7502-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="f7502-543">Tarefa 3: usando o novo ViewModel no StoreController</span><span class="sxs-lookup"><span data-stu-id="f7502-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="f7502-544">Nesta tarefa, você modificará o **StoreController**do **procurar** e **detalhes** métodos de ação para usar o novo **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="f7502-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="f7502-545">Adicione uma referência para a pasta de modelos no **StoreController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="f7502-546">Para fazer isso, expanda o **controladores** pasta o **Gerenciador de soluções** e abra o **StoreController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="f7502-547">Em seguida, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f7502-547">Then add the following code:</span></span>

    <span data-ttu-id="f7502-548">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="f7502-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="f7502-549">Substitua o **navegue** método de ação para usar o **StoreViewBrowseController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="f7502-550">Você criará um gênero e dois novos objetos de álbuns com dados fictícios (no próximo laboratório prático, você irá consumir dados reais de um banco de dados).</span><span class="sxs-lookup"><span data-stu-id="f7502-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="f7502-551">Para fazer isso, substitua os **procurar** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="f7502-552">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="f7502-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="f7502-553">Substitua os **detalhes** método de ação para usar o **StoreViewBrowseController** classe.</span><span class="sxs-lookup"><span data-stu-id="f7502-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="f7502-554">Você criará uma nova **álbum** objeto a ser retornado para o **exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="f7502-555">Para fazer isso, substitua os **detalhes** método com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="f7502-556">(Código de trecho de código – *conceitos básicos do ASP.NET MVC 4 - Ex6 DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="f7502-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="f7502-557">Tarefa 4 - adicionando um modelo de exibição de navegação</span><span class="sxs-lookup"><span data-stu-id="f7502-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="f7502-558">Nesta tarefa, você adicionará uma **procurar** modo de exibição para mostrar os álbuns encontrados para um gênero específico.</span><span class="sxs-lookup"><span data-stu-id="f7502-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="f7502-559">Antes de criar o novo modelo de exibição, você deve compilar o projeto para que o **adicionar exibição** caixa de diálogo sabe sobre o **ViewModel** classe a ser usada.</span><span class="sxs-lookup"><span data-stu-id="f7502-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="f7502-560">Compile o projeto selecionando o **construir** item de menu e, em seguida, **MvcMusicStore Build**.</span><span class="sxs-lookup"><span data-stu-id="f7502-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="f7502-561">Adicionar um **procurar** modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-561">Add a **Browse** View.</span></span> <span data-ttu-id="f7502-562">Para fazer isso, clique com botão direito no **navegue** método de ação do **StoreController** e clique em **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="f7502-563">No **adicionar exibição** diálogo caixa, verifique se o nome da exibição **procurar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="f7502-564">Verifique as **criar uma exibição fortemente tipada** caixa de seleção e selecione **StoreBrowseViewModel** do **classe de modelo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="f7502-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="f7502-565">Deixe os outros campos com seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="f7502-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="f7502-566">Em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-566">Then click **Add**.</span></span>

    <span data-ttu-id="f7502-567">![Adicionando uma exibição de navegação](aspnet-mvc-4-fundamentals/_static/image29.png "adicionando uma exibição de navegação")</span><span class="sxs-lookup"><span data-stu-id="f7502-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    *<span data-ttu-id="f7502-568">Adicionando uma exibição de navegação</span><span class="sxs-lookup"><span data-stu-id="f7502-568">Adding a Browse View</span></span>*
4. <span data-ttu-id="f7502-569">Modificar a **Browse.cshtml** para exibir informações do gênero, acessando a **StoreBrowseViewModel** objeto que é passado para o modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="f7502-570">Para fazer isso, substitua o conteúdo pelo seguinte: (C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="f7502-571">Tarefa 5 – executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="f7502-572">Nesta tarefa, você testará que a **navegue** método recupera álbuns da **procurar** ação do método.</span><span class="sxs-lookup"><span data-stu-id="f7502-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="f7502-573">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-574">O projeto é iniciado na Home page.</span><span class="sxs-lookup"><span data-stu-id="f7502-574">The project starts in the Home page.</span></span> <span data-ttu-id="f7502-575">Altere a URL para   **/Store/procurar? Gênero = Disco** para verificar se a ação retorna dois álbuns.</span><span class="sxs-lookup"><span data-stu-id="f7502-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="f7502-576">![Navegação Store álbuns de discoteca](aspnet-mvc-4-fundamentals/_static/image30.png "navegação álbuns de discoteca Store")</span><span class="sxs-lookup"><span data-stu-id="f7502-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    *<span data-ttu-id="f7502-577">Navegação álbuns de discoteca Store</span><span class="sxs-lookup"><span data-stu-id="f7502-577">Browsing Store Disco Albums</span></span>*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="f7502-578">Tarefa 6 - exibindo informações sobre um álbum específico</span><span class="sxs-lookup"><span data-stu-id="f7502-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="f7502-579">Nesta tarefa, você implementará o **Store/detalhes** modo de exibição para exibir informações sobre um álbum específico.</span><span class="sxs-lookup"><span data-stu-id="f7502-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="f7502-580">Neste laboratório prático, tudo o que você irá exibir sobre o álbum já está contido na **exibição** modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="f7502-581">Então, em vez de criar uma **StoreDetailsViewModel** classe, você usará atual **StoreBrowseViewModel** modelo passando-lhe o álbum.</span><span class="sxs-lookup"><span data-stu-id="f7502-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="f7502-582">Feche o navegador, se necessário, para retornar à janela do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f7502-583">Adicione um novo **detalhes** exibir para o **StoreController**do **detalhes** método de ação.</span><span class="sxs-lookup"><span data-stu-id="f7502-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="f7502-584">Para fazer isso, clique com botão direito do **detalhes** método na **StoreController** classe e clique em **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="f7502-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="f7502-585">No **adicionar exibição** caixa de diálogo, verifique se que o **nome da exibição** é **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="f7502-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="f7502-586">Verifique a **criar uma exibição fortemente tipada** caixa de seleção e selecione **álbum** do **classe de modelo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="f7502-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="f7502-587">Deixe os outros campos com seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="f7502-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="f7502-588">Em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-588">Then click **Add**.</span></span> <span data-ttu-id="f7502-589">Isso criará e abrirá uma **\Views\Store\Details.cshtml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f7502-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="f7502-590">![Adicionando uma exibição de detalhes](aspnet-mvc-4-fundamentals/_static/image31.png "adicionando uma exibição de detalhes")</span><span class="sxs-lookup"><span data-stu-id="f7502-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    *<span data-ttu-id="f7502-591">Adicionando uma exibição de detalhes</span><span class="sxs-lookup"><span data-stu-id="f7502-591">Adding a Details View</span></span>*
3. <span data-ttu-id="f7502-592">Modificar a **details. cshtml** arquivo para exibir informações do álbum, acessando a **álbum** objeto que é passado para o modelo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="f7502-593">Para fazer isso, substitua o conteúdo pelo seguinte: (C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="f7502-594">Tarefa 7 – executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="f7502-595">Nesta tarefa, você testará que a **detalhes** View recupera informações do álbum da **fornece detalhes sobre a ação** método.</span><span class="sxs-lookup"><span data-stu-id="f7502-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="f7502-596">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-597">O projeto é iniciado **Home** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="f7502-598">Altere a URL para **/Store/Details/5** para verificar as informações do álbum.</span><span class="sxs-lookup"><span data-stu-id="f7502-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="f7502-599">![Navegação de detalhes de álbuns](aspnet-mvc-4-fundamentals/_static/image32.png "navegação álbuns detalhes")</span><span class="sxs-lookup"><span data-stu-id="f7502-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    *<span data-ttu-id="f7502-600">Detalhes do álbum de navegação</span><span class="sxs-lookup"><span data-stu-id="f7502-600">Browsing Album's Detail</span></span>*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="f7502-601">Tarefa 8 - adicionando Links entre páginas</span><span class="sxs-lookup"><span data-stu-id="f7502-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="f7502-602">Nesta tarefa, você irá adicionar um link no modo de exibição Store tem um link no cada nome de gênero ao apropriado **/Store/procurar** URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="f7502-603">Dessa forma, quando você clica em um gênero, por exemplo **Disco**, ele vai navegar para **/Store/procurar? genre = Disco** URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="f7502-604">Feche o navegador, se necessário, para retornar à janela do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f7502-605">Atualizar o **índice** página para adicionar um link para o **procurar** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="f7502-606">Para fazer isso, na **Gerenciador de soluções** expandir o **modos de exibição** pasta, em seguida, a **Store** pasta e clique duas vezes o **index. cshtml** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="f7502-607">Adicione um link para o modo de exibição de navegador que indica o gênero selecionado.</span><span class="sxs-lookup"><span data-stu-id="f7502-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="f7502-608">Para fazer isso, substitua o seguinte código realçado dentro de **&lt;li&gt;** marcas: (C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="f7502-609">outra abordagem seria estar vinculando diretamente para a página, com um código semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7502-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="f7502-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="f7502-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="f7502-611">Embora essa abordagem funciona, depende de uma cadeia de caracteres codificada.</span><span class="sxs-lookup"><span data-stu-id="f7502-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="f7502-612">Se você renomear o controlador mais tarde, você precisará alterar essa instrução manualmente.</span><span class="sxs-lookup"><span data-stu-id="f7502-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="f7502-613">Uma alternativa melhor é usar um **auxiliar HTML** método.</span><span class="sxs-lookup"><span data-stu-id="f7502-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="f7502-614">O ASP.NET MVC inclui um método auxiliar HTML que está disponível para essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="f7502-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="f7502-615">O **Html.ActionLink()** método auxiliar torna fácil criar HTML **&lt;um&gt;** links, certificando-se de caminhos de URL sejam corretamente codificados de URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="f7502-616">HTML. ActionLink tem várias sobrecargas.</span><span class="sxs-lookup"><span data-stu-id="f7502-616">Html.ActionLink has several overloads.</span></span> <span data-ttu-id="f7502-617">Neste exercício você usará uma que usa três parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f7502-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="f7502-618">Texto do link, que exibirá o nome de gênero</span><span class="sxs-lookup"><span data-stu-id="f7502-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="f7502-619">Nome da ação de controlador (**procurar**)</span><span class="sxs-lookup"><span data-stu-id="f7502-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="f7502-620">Valores de parâmetro, especificando o nome de rota (**gênero**) e o valor (**nome de gênero**)</span><span class="sxs-lookup"><span data-stu-id="f7502-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="f7502-621">Tarefa 9 - executando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="f7502-622">Nesta tarefa, você testará que cada gênero é exibido com um link para o apropriada **/Store/procurar** URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="f7502-623">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-624">O projeto é iniciado na Home page.</span><span class="sxs-lookup"><span data-stu-id="f7502-624">The project starts in the Home page.</span></span> <span data-ttu-id="f7502-625">Altere a URL para **/Store** para verificar cada gênero vincula-se ao apropriado **/Store/procurar** URL.</span><span class="sxs-lookup"><span data-stu-id="f7502-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="f7502-626">![Navegação gêneros com links para a página de navegação](aspnet-mvc-4-fundamentals/_static/image33.png "gêneros de navegação com links para a página Procurar")</span><span class="sxs-lookup"><span data-stu-id="f7502-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    *<span data-ttu-id="f7502-627">Navegação gêneros com links para a página Procurar</span><span class="sxs-lookup"><span data-stu-id="f7502-627">Browsing Genres with links to Browse page</span></span>*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="f7502-628">Tarefa 10 - usando a coleção de ViewModel dinâmico para passar valores</span><span class="sxs-lookup"><span data-stu-id="f7502-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="f7502-629">Nesta tarefa, você aprenderá a um método simples e poderoso para passar valores entre o controlador e o modo de exibição sem fazer nenhuma alteração no modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="f7502-630">ASP.NET MVC 4 fornece a coleção &quot;ViewModel&quot;, que pode ser atribuído a qualquer valor dinâmico e acessado dentro de controladores e exibições também.</span><span class="sxs-lookup"><span data-stu-id="f7502-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="f7502-631">Agora você usará a coleção de dinâmica de ViewBag para passar uma lista de &quot; **estrelado gêneros** &quot; do controlador para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="f7502-632">O modo de exibição de índice Store acessará a **ViewModel** e exibir as informações.</span><span class="sxs-lookup"><span data-stu-id="f7502-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="f7502-633">Feche o navegador, se necessário, para retornar à janela do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="f7502-634">Abra **StoreController.cs** e modifique **índice** método para criar uma lista de gêneros de estrelado na coleção ViewModel:</span><span class="sxs-lookup"><span data-stu-id="f7502-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="f7502-635">Você também pode usar a sintaxe **ViewBag [&quot;Starred&quot;]** para acessar as propriedades.</span><span class="sxs-lookup"><span data-stu-id="f7502-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="f7502-636">O ícone de estrela **&quot;starred.png&quot;** está incluído no **Source\Assets\Images** pasta deste laboratório.</span><span class="sxs-lookup"><span data-stu-id="f7502-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="f7502-637">Para adicioná-lo ao aplicativo, arraste seu conteúdo de um **Windows Explorer** janela para o **Gerenciador de soluções** no Visual Web Developer Express, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="f7502-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="f7502-638">![Adicionar imagem de estrela à solução](aspnet-mvc-4-fundamentals/_static/image34.png "adicionar imagem de estrela à solução")</span><span class="sxs-lookup"><span data-stu-id="f7502-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    *<span data-ttu-id="f7502-639">Adicionar imagem de estrela para a solução</span><span class="sxs-lookup"><span data-stu-id="f7502-639">Adding star image to the solution</span></span>*
3. <span data-ttu-id="f7502-640">Abra o modo de exibição **Store/Index.cshtml** e modificar o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f7502-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="f7502-641">Você lerá os &quot;estrelado&quot; propriedade no **ViewBag** coleção e pergunte se o nome do gênero atual está na lista.</span><span class="sxs-lookup"><span data-stu-id="f7502-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="f7502-642">Nesse caso, você mostrará um ícone de estrela à direita para o link do gênero.</span><span class="sxs-lookup"><span data-stu-id="f7502-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="f7502-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="f7502-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="f7502-644">Tarefa 11: executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f7502-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="f7502-645">Nesta tarefa, você testará que gêneros destacados exibem um ícone de estrela.</span><span class="sxs-lookup"><span data-stu-id="f7502-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="f7502-646">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="f7502-647">O projeto é iniciado **Home** página.</span><span class="sxs-lookup"><span data-stu-id="f7502-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="f7502-648">Altere a URL para **/Store** para verificar se cada gênero em destaque tem o rótulo a respeito próprio:</span><span class="sxs-lookup"><span data-stu-id="f7502-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="f7502-649">![Navegação gêneros com elementos destacados](aspnet-mvc-4-fundamentals/_static/image35.png "gêneros navegando com elementos destacados")</span><span class="sxs-lookup"><span data-stu-id="f7502-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    *<span data-ttu-id="f7502-650">Navegação gêneros com elementos destacados</span><span class="sxs-lookup"><span data-stu-id="f7502-650">Browsing Genres with starred elements</span></span>*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="f7502-651">Exercício 7: Uma visão geral do novo modelo do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="f7502-652">Neste exercício, você irá explorar os aprimoramentos nos modelos de projeto do ASP.NET MVC 4, dar uma olhada recursos mais relevantes do novo modelo.</span><span class="sxs-lookup"><span data-stu-id="f7502-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="f7502-653">Tarefa 1: Explorando o modelo de aplicativo de Internet do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="f7502-654">Se não estiver aberto, inicie **VS Express para Web**</span><span class="sxs-lookup"><span data-stu-id="f7502-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="f7502-655">Selecione o **arquivo | Novo | Projeto** comando de menu.</span><span class="sxs-lookup"><span data-stu-id="f7502-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="f7502-656">No **novo projeto** caixa de diálogo, selecione o **Visual c# | Web** modelo no painel à esquerda de árvore e, em seguida, escolha o **aplicativo Web do ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="f7502-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="f7502-657">**Nome da** o projeto *MusicStore* e atualize o **nome da solução** para *começar*, em seguida, selecione um local (ou deixe o padrão) e clique em **Okey** .</span><span class="sxs-lookup"><span data-stu-id="f7502-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="f7502-658">![Criando um novo projeto ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image36.png "criando um novo projeto ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="f7502-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    *<span data-ttu-id="f7502-659">Criando um novo projeto ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-659">Creating a new ASP.NET MVC 4 Project</span></span>*
3. <span data-ttu-id="f7502-660">No **novo projeto ASP.NET MVC 4** caixa de diálogo, selecione o **aplicativo de Internet** modelo de projeto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f7502-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="f7502-661">Observe que você pode selecionar o Razor ou ASPX como o mecanismo de exibição.</span><span class="sxs-lookup"><span data-stu-id="f7502-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="f7502-662">![Criando um novo aplicativo ASP.NET MVC 4 da Internet](aspnet-mvc-4-fundamentals/_static/image37.png "criando um novo aplicativo ASP.NET MVC 4 da Internet")</span><span class="sxs-lookup"><span data-stu-id="f7502-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    *<span data-ttu-id="f7502-663">Criando um novo aplicativo ASP.NET MVC 4 da Internet</span><span class="sxs-lookup"><span data-stu-id="f7502-663">Creating a new ASP.NET MVC 4 Internet Application</span></span>*

    > [!NOTE]
    > <span data-ttu-id="f7502-664">Sintaxe do Razor foi introduzido no ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="f7502-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="f7502-665">Sua meta é minimizar o número de caracteres e pressionamentos de teclas necessários em um arquivo, permitindo um rápido e fluido fluxo de trabalho de codificação.</span><span class="sxs-lookup"><span data-stu-id="f7502-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="f7502-666">Aproveita o Razor existente C# /VB (ou outro) habilidades linguísticas e fornece uma sintaxe de marcação de modelo que permite que um fluxo de trabalho de construção de HTML incrível.</span><span class="sxs-lookup"><span data-stu-id="f7502-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="f7502-667">Pressione **F5** para executar a solução e ver o modelo renovado.</span><span class="sxs-lookup"><span data-stu-id="f7502-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="f7502-668">Você pode conferir os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7502-668">You can check out the following features:</span></span>

    1. **<span data-ttu-id="f7502-669">Modelos de estilo moderno</span><span class="sxs-lookup"><span data-stu-id="f7502-669">Modern-style templates</span></span>**

        <span data-ttu-id="f7502-670">Os modelos têm sido renovados, fornecendo mais estilos de aparência moderna.</span><span class="sxs-lookup"><span data-stu-id="f7502-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="f7502-671">![Modelos do ASP.NET MVC 4 remodelado](aspnet-mvc-4-fundamentals/_static/image38.png "remodelado modelos do ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="f7502-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        *<span data-ttu-id="f7502-672">Modelos do ASP.NET MVC 4 remodelado</span><span class="sxs-lookup"><span data-stu-id="f7502-672">ASP.NET MVC 4 restyled templates</span></span>*
    2. **<span data-ttu-id="f7502-673">Renderização adaptável</span><span class="sxs-lookup"><span data-stu-id="f7502-673">Adaptive Rendering</span></span>**

        <span data-ttu-id="f7502-674">Fazer check-out de redimensionamento da janela do navegador e observe como o layout da página se adapte dinamicamente para o novo tamanho de janela.</span><span class="sxs-lookup"><span data-stu-id="f7502-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="f7502-675">Esses modelos de usam a técnica de renderização adaptável para renderizar corretamente em plataformas móveis e da área de trabalho sem nenhuma personalização.</span><span class="sxs-lookup"><span data-stu-id="f7502-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="f7502-676">![Modelo de projeto do ASP.NET MVC 4 em tamanhos de navegador diferente](aspnet-mvc-4-fundamentals/_static/image39.png "modelo de projeto do ASP.NET MVC 4 em tamanhos de navegador diferente")</span><span class="sxs-lookup"><span data-stu-id="f7502-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        *<span data-ttu-id="f7502-677">Modelo de projeto do ASP.NET MVC 4 em tamanhos de navegador diferente</span><span class="sxs-lookup"><span data-stu-id="f7502-677">ASP.NET MVC 4 project template in different browser sizes</span></span>*
5. <span data-ttu-id="f7502-678">Feche o navegador para interromper o depurador e retorne ao Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="f7502-679">Agora, você será capaz de explorar a solução e fazer check-out de alguns dos novos recursos introduzidos pelo ASP.NET MVC 4 no modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f7502-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="f7502-680">![ASP.NET MVC4-internet---modelo de projeto aplicativo](aspnet-mvc-4-fundamentals/_static/image40.png "o modelo de projeto de aplicativo de Internet do ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="f7502-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    *<span data-ttu-id="f7502-681">O modelo de projeto de aplicativo de Internet do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-681">The ASP.NET MVC 4 Internet Application Project Template</span></span>*

   1. **<span data-ttu-id="f7502-682">Marcação HTML5</span><span class="sxs-lookup"><span data-stu-id="f7502-682">HTML5 markup</span></span>**

       <span data-ttu-id="f7502-683">Procurar exibições de modelo para descobrir a nova marcação de tema, por exemplo aberta **About. cshtml** exibir dentro **Home** pasta.</span><span class="sxs-lookup"><span data-stu-id="f7502-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="f7502-684">![Novo modelo, usando a marcação do Razor e o HTML5](aspnet-mvc-4-fundamentals/_static/image41.png "novo modelo, usando a marcação do Razor e o HTML5")</span><span class="sxs-lookup"><span data-stu-id="f7502-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       *<span data-ttu-id="f7502-685">Novo modelo, usando a marcação do Razor e o HTML5</span><span class="sxs-lookup"><span data-stu-id="f7502-685">New template, using Razor and HTML5 markup</span></span>*
   2. **<span data-ttu-id="f7502-686">Bibliotecas JavaScript incluídas</span><span class="sxs-lookup"><span data-stu-id="f7502-686">JavaScript libraries included</span></span>**

      1. <span data-ttu-id="f7502-687">**jQuery**: jQuery simplifica a percorrer de documento HTML, manipulação de eventos, animação e interações de Ajax.</span><span class="sxs-lookup"><span data-stu-id="f7502-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="f7502-688">**jQuery UI**: Esta biblioteca fornece abstrações para interação de baixo nível e animação, efeitos avançados e widgets passíveis de tema, criados sobre a biblioteca JavaScript jQuery.</span><span class="sxs-lookup"><span data-stu-id="f7502-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="f7502-689">Você pode aprender sobre o jQuery e o jQuery UI no [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="f7502-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="f7502-690">**KnockoutJS**: O modelo de padrão do ASP.NET MVC 4 agora inclui **KnockoutJS**, uma estrutura MVVM do JavaScript que permite que você crie aplicativos web avançados e altamente responsivos usando JavaScript e HTML.</span><span class="sxs-lookup"><span data-stu-id="f7502-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="f7502-691">Como no ASP.NET MVC 3, o jQuery e bibliotecas de interface do usuário do jQuery também estão incluídas no ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7502-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="f7502-692">Você pode obter mais informações sobre a biblioteca KnockOutJS presentes neste link: [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="f7502-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="f7502-693">**Modernizr**: Essa biblioteca é executado automaticamente, tornando seu site compatível com navegadores mais antigos, ao usar as tecnologias do HTML5 e CSS3.</span><span class="sxs-lookup"><span data-stu-id="f7502-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="f7502-694">Você pode obter mais informações sobre a biblioteca do Modernizr presentes neste link: [ http://www.modernizr.com/ ](http://www.modernizr.com/).</span><span class="sxs-lookup"><span data-stu-id="f7502-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. **<span data-ttu-id="f7502-695">SimpleMembership incluído na solução</span><span class="sxs-lookup"><span data-stu-id="f7502-695">SimpleMembership included in the solution</span></span>**

       <span data-ttu-id="f7502-696">SimpleMembership foi projetado como uma substituição para o sistema de provedor de função do ASP.NET e a associação anterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="f7502-697">Ele tem muitos recursos novos que tornam mais fácil para o desenvolvedor de páginas da web seguras de forma mais flexível.</span><span class="sxs-lookup"><span data-stu-id="f7502-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="f7502-698">O modelo de Internet já tiver configurado algumas coisas a integrar o SimpleMembership, por exemplo, o controlador é preparado para usar o OAuthWebSecurity (para o registro de conta OAuth, login, gerenciamento, etc.) e segurança da Web.</span><span class="sxs-lookup"><span data-stu-id="f7502-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="f7502-699">![SimpleMembership incluído na solução](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership incluído na solução")</span><span class="sxs-lookup"><span data-stu-id="f7502-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       *<span data-ttu-id="f7502-700">SimpleMembership incluído na solução</span><span class="sxs-lookup"><span data-stu-id="f7502-700">SimpleMembership Included in the solution</span></span>*

       > [!NOTE]
       > <span data-ttu-id="f7502-701">Para obter mais informações sobre [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="f7502-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="f7502-702">Além disso, você pode implantar esse aplicativo para Windows Azure Web Sites seguinte [apêndice b: Publicando um aplicativo ASP.NET MVC 4 usando a implantação da Web](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="f7502-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f7502-703">Resumo</span><span class="sxs-lookup"><span data-stu-id="f7502-703">Summary</span></span>

<span data-ttu-id="f7502-704">Ao concluir este laboratório prático, você aprendeu os conceitos básicos do ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="f7502-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="f7502-705">Os principais elementos de um aplicativo MVC e como eles interagem</span><span class="sxs-lookup"><span data-stu-id="f7502-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="f7502-706">Como criar um aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7502-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="f7502-707">Como adicionar e configurar os controladores para lidar com os parâmetros passados por meio da URL e a querystring</span><span class="sxs-lookup"><span data-stu-id="f7502-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="f7502-708">Como adicionar uma página de layout mestre para configurar um modelo de conteúdo HTML comum, uma folha de estilos para aprimorar a aparência e um modelo de exibição para exibir o conteúdo HTML</span><span class="sxs-lookup"><span data-stu-id="f7502-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="f7502-709">Como usar o padrão de ViewModel para passar as propriedades para o modelo de exibição para exibir informações dinâmicas</span><span class="sxs-lookup"><span data-stu-id="f7502-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="f7502-710">Como usar os parâmetros passados para controladores no modelo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="f7502-711">Como adicionar links para páginas dentro do aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f7502-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="f7502-712">Como adicionar e usar propriedades dinâmicas em um modo de exibição</span><span class="sxs-lookup"><span data-stu-id="f7502-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="f7502-713">Os aprimoramentos nos modelos de projeto do ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="f7502-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f7502-714">Apêndice a: Instalar o Visual Studio Express 2012 para Web</span><span class="sxs-lookup"><span data-stu-id="f7502-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f7502-715">Você pode instalar **Microsoft Visual Studio Express 2012 para Web** ou outra &quot;Express&quot; versão usando o **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f7502-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f7502-716">As instruções a seguir guia você pelas etapas necessárias para instalar *Visual studio Express 2012 para Web* usando *Microsoft Web Platform Installer*.</span><span class="sxs-lookup"><span data-stu-id="f7502-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f7502-717">Vá para [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="f7502-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f7502-718">Como alternativa, se você já tiver instalado o Web Platform Installer, você pode abri-lo e pesquisar o produto &quot; <em>Visual Studio Express 2012 para Web com o SDK do Windows Azure</em>&quot;.</span><span class="sxs-lookup"><span data-stu-id="f7502-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f7502-719">Clique em **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="f7502-719">Click on **Install Now**.</span></span> <span data-ttu-id="f7502-720">Se você não tiver **Web Platform Installer** você será redirecionado para baixar e instalá-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="f7502-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f7502-721">Uma vez **Web Platform Installer** é aberto, clique em **instalar** para iniciar a instalação.</span><span class="sxs-lookup"><span data-stu-id="f7502-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f7502-722">![Instalar o Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "instalar o Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="f7502-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    *<span data-ttu-id="f7502-723">Instalar o Visual Studio Express</span><span class="sxs-lookup"><span data-stu-id="f7502-723">Install Visual Studio Express</span></span>*
4. <span data-ttu-id="f7502-724">Leia os termos e licenças de todos os produtos e clique em **aceito** para continuar.</span><span class="sxs-lookup"><span data-stu-id="f7502-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Aceitar os termos de licença](aspnet-mvc-4-fundamentals/_static/image44.png)

    *<span data-ttu-id="f7502-726">Aceitar os termos de licença</span><span class="sxs-lookup"><span data-stu-id="f7502-726">Accepting the license terms</span></span>*
5. <span data-ttu-id="f7502-727">Aguarde até que o processo de download e instalação for concluído.</span><span class="sxs-lookup"><span data-stu-id="f7502-727">Wait until the downloading and installation process completes.</span></span>

    ![Progresso da instalação](aspnet-mvc-4-fundamentals/_static/image45.png)

    *<span data-ttu-id="f7502-729">Progresso da instalação</span><span class="sxs-lookup"><span data-stu-id="f7502-729">Installation progress</span></span>*
6. <span data-ttu-id="f7502-730">Quando a instalação for concluída, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="f7502-730">When the installation completes, click **Finish**.</span></span>

    ![Instalação concluída](aspnet-mvc-4-fundamentals/_static/image46.png)

    *<span data-ttu-id="f7502-732">Instalação concluída</span><span class="sxs-lookup"><span data-stu-id="f7502-732">Installation completed</span></span>*
7. <span data-ttu-id="f7502-733">Clique em **Exit** para fechar o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f7502-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f7502-734">Para abrir o Visual Studio Express para Web, vá para o **iniciar** de tela e comece a escrever &quot; **VS Express**&quot;, em seguida, clique no **VS Express para Web** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="f7502-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express para o bloco da Web](aspnet-mvc-4-fundamentals/_static/image47.png)

    *<span data-ttu-id="f7502-736">VS Express para o bloco da Web</span><span class="sxs-lookup"><span data-stu-id="f7502-736">VS Express for Web tile</span></span>*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f7502-737">Apêndice b: Publicando um aplicativo ASP.NET MVC 4 usando a implantação da Web</span><span class="sxs-lookup"><span data-stu-id="f7502-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f7502-738">Este apêndice mostram como criar um novo site do Portal de gerenciamento do Windows Azure e publicar o aplicativo que você obteve seguindo o ambiente de laboratório, aproveitando o recurso de publicação de implantação da Web fornecido pelo Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f7502-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="f7502-739">Tarefa 1 - criar um novo Site do Windows Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7502-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="f7502-740">Vá para o [Portal de gerenciamento do Windows Azure](https://manage.windowsazure.com/) e entre usando as credenciais da Microsoft associadas à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f7502-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7502-741">Com o Windows Azure, você pode hospedar 10 Sites da Web ASP.NET gratuitamente e, em seguida, dimensione conforme seu tráfego aumenta.</span><span class="sxs-lookup"><span data-stu-id="f7502-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f7502-742">Você pode se inscrever [aqui](https://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="f7502-742">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f7502-743">![Faça logon no portal do Windows Azure](aspnet-mvc-4-fundamentals/_static/image48.png "faça logon no portal do Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="f7502-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    *<span data-ttu-id="f7502-744">Faça logon no Portal de gerenciamento do Azure do Windows</span><span class="sxs-lookup"><span data-stu-id="f7502-744">Log on to Windows Azure Management Portal</span></span>*
2. <span data-ttu-id="f7502-745">Clique em **New** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="f7502-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f7502-746">![Criando um novo Site](aspnet-mvc-4-fundamentals/_static/image49.png "criando um novo Site")</span><span class="sxs-lookup"><span data-stu-id="f7502-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    *<span data-ttu-id="f7502-747">Criando um novo Site</span><span class="sxs-lookup"><span data-stu-id="f7502-747">Creating a new Web Site</span></span>*
3. <span data-ttu-id="f7502-748">Clique em **Compute** | **Site da Web**.</span><span class="sxs-lookup"><span data-stu-id="f7502-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f7502-749">Em seguida, selecione **criação rápida** opção.</span><span class="sxs-lookup"><span data-stu-id="f7502-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="f7502-750">Forneça uma URL disponível para o novo site da web e clique em **Criar Site**.</span><span class="sxs-lookup"><span data-stu-id="f7502-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7502-751">Um Site do Windows Azure é o host para um aplicativo web em execução na nuvem que você pode controlar e gerenciar.</span><span class="sxs-lookup"><span data-stu-id="f7502-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f7502-752">A opção criação rápida permite que você implantar um aplicativo web completo para o Windows Azure Site de fora do portal.</span><span class="sxs-lookup"><span data-stu-id="f7502-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="f7502-753">Ele não inclui as etapas para configurar um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f7502-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f7502-754">![Criando um novo Site usando a criação rápida](aspnet-mvc-4-fundamentals/_static/image50.png "criando um novo Site usando a criação rápida")</span><span class="sxs-lookup"><span data-stu-id="f7502-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    *<span data-ttu-id="f7502-755">Criando um novo Site usando a criação rápida</span><span class="sxs-lookup"><span data-stu-id="f7502-755">Creating a new Web Site using Quick Create</span></span>*
4. <span data-ttu-id="f7502-756">Aguarde até que o novo **Site da Web** é criado.</span><span class="sxs-lookup"><span data-stu-id="f7502-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f7502-757">Depois que o Site da Web é criado, clique no link sob a **URL** coluna.</span><span class="sxs-lookup"><span data-stu-id="f7502-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f7502-758">Verifique se o novo Site da Web está funcionando.</span><span class="sxs-lookup"><span data-stu-id="f7502-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f7502-759">![Navegando até o novo site](aspnet-mvc-4-fundamentals/_static/image51.png "navegando até o novo site da web")</span><span class="sxs-lookup"><span data-stu-id="f7502-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    *<span data-ttu-id="f7502-760">Navegando até o novo site da web</span><span class="sxs-lookup"><span data-stu-id="f7502-760">Browsing to the new web site</span></span>*

    <span data-ttu-id="f7502-761">![Site da Web em execução](aspnet-mvc-4-fundamentals/_static/image52.png "site da Web em execução")</span><span class="sxs-lookup"><span data-stu-id="f7502-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    *<span data-ttu-id="f7502-762">Site da Web em execução</span><span class="sxs-lookup"><span data-stu-id="f7502-762">Web site running</span></span>*
6. <span data-ttu-id="f7502-763">Volte para o portal e clique no nome do site da web sob o **nome** coluna para exibir as páginas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f7502-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f7502-764">![Abrir as páginas de gerenciamento do site da web](aspnet-mvc-4-fundamentals/_static/image53.png "abrir as páginas de gerenciamento do site da web")</span><span class="sxs-lookup"><span data-stu-id="f7502-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    *<span data-ttu-id="f7502-765">Abrir as páginas de gerenciamento do Site da Web</span><span class="sxs-lookup"><span data-stu-id="f7502-765">Opening the Web Site management pages</span></span>*
7. <span data-ttu-id="f7502-766">No **Dashboard** página na **visão geral rápida** seção, clique no **baixar perfil de publicação** link.</span><span class="sxs-lookup"><span data-stu-id="f7502-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7502-767">O *perfil de publicação* contém todas as informações necessárias para publicar um aplicativo web para um site do Windows Azure para cada método de publicação habilitado.</span><span class="sxs-lookup"><span data-stu-id="f7502-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="f7502-768">O perfil de publicação contém as URLs, as credenciais do usuário e cadeias de caracteres de banco de dados necessárias para conectar e autenticar em relação a cada um dos pontos de extremidade para o qual um método de publicação está habilitado.</span><span class="sxs-lookup"><span data-stu-id="f7502-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f7502-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio para Web Express** e **Microsoft Visual Studio 2012** oferecem suporte à leitura perfis de publicação para automatizar a configuração desses programas para publicação de aplicativos web nos sites do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f7502-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="f7502-770">![Baixando o site da web de perfil de publicação](aspnet-mvc-4-fundamentals/_static/image54.png "baixando o site da web de perfil de publicação")</span><span class="sxs-lookup"><span data-stu-id="f7502-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    *<span data-ttu-id="f7502-771">Baixando o Site da Web de perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="f7502-771">Downloading the Web Site publish profile</span></span>*
8. <span data-ttu-id="f7502-772">Baixe o arquivo de perfil de publicação em um local conhecido.</span><span class="sxs-lookup"><span data-stu-id="f7502-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f7502-773">Ainda mais neste exercício, você verá como usar esse arquivo para publicar um aplicativo web para um Windows Azure Web Sites do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7502-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="f7502-774">![Salvando o arquivo de perfil de publicação](aspnet-mvc-4-fundamentals/_static/image55.png "salvar o perfil de publicação")</span><span class="sxs-lookup"><span data-stu-id="f7502-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    *<span data-ttu-id="f7502-775">Salvando o arquivo de perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="f7502-775">Saving the publish profile file</span></span>*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f7502-776">Tarefa 2 – Configurando o servidor de banco de dados</span><span class="sxs-lookup"><span data-stu-id="f7502-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f7502-777">Se seu aplicativo faz uso do SQL Server você precisará criar um servidor de banco de dados SQL de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="f7502-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f7502-778">Se você quiser implantar um aplicativo simples que não usa o SQL Server, você pode ignorar esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="f7502-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f7502-779">Você precisará de um servidor de banco de dados SQL para armazenar o banco de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7502-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f7502-780">Você pode exibir os servidores de banco de dados SQL na sua assinatura no portal de gerenciamento do Windows Azure em **bancos de dados Sql** | **servidores** | **do servidor Painel**.</span><span class="sxs-lookup"><span data-stu-id="f7502-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f7502-781">Se você não tiver um servidor criado, você pode criar uma usando o **adicionar** botão na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="f7502-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f7502-782">Anote o **nome do servidor e o URL, o nome de logon de administrador e senha**, pois você usará nas próximas tarefas.</span><span class="sxs-lookup"><span data-stu-id="f7502-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f7502-783">Não crie o banco de dados ainda, ele será criado em um estágio posterior.</span><span class="sxs-lookup"><span data-stu-id="f7502-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f7502-784">![Painel do servidor de banco de dados SQL](aspnet-mvc-4-fundamentals/_static/image56.png "painel de banco de dados do SQL Server")</span><span class="sxs-lookup"><span data-stu-id="f7502-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    *<span data-ttu-id="f7502-785">Painel de banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f7502-785">SQL Database Server Dashboard</span></span>*
2. <span data-ttu-id="f7502-786">A próxima tarefa, você testará a conexão de banco de dados do Visual Studio, por esse motivo, você precisa incluir seu endereço IP local na lista do servidor **endereços IP permitidos**.</span><span class="sxs-lookup"><span data-stu-id="f7502-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f7502-787">Para fazer isso, clique em **configurar**, selecione o endereço IP do **endereço de IP do cliente atual** e cole-o na **endereço IP inicial** e **oendereçoIPfinal** caixas de texto e clique em de ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) botão.</span><span class="sxs-lookup"><span data-stu-id="f7502-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![Adicionar endereço IP do cliente](aspnet-mvc-4-fundamentals/_static/image58.png)

    *<span data-ttu-id="f7502-789">Adicionar endereço IP do cliente</span><span class="sxs-lookup"><span data-stu-id="f7502-789">Adding Client IP Address</span></span>*
3. <span data-ttu-id="f7502-790">Uma vez a **endereço IP do cliente** é adicionado para endereços IP, clique em **salvar** para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="f7502-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Confirmar alterações](aspnet-mvc-4-fundamentals/_static/image59.png)

    *<span data-ttu-id="f7502-792">Confirmar alterações</span><span class="sxs-lookup"><span data-stu-id="f7502-792">Confirm Changes</span></span>*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f7502-793">Tarefa 3 – publicar um aplicativo ASP.NET MVC 4 usando a implantação da Web</span><span class="sxs-lookup"><span data-stu-id="f7502-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f7502-794">Volte para a solução do ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="f7502-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f7502-795">No **Gerenciador de soluções**, clique com botão direito no projeto de site da web e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f7502-796">![O aplicativo de publicação](aspnet-mvc-4-fundamentals/_static/image60.png "publicando o aplicativo")</span><span class="sxs-lookup"><span data-stu-id="f7502-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    *<span data-ttu-id="f7502-797">Publicar o site da web</span><span class="sxs-lookup"><span data-stu-id="f7502-797">Publishing the web site</span></span>*
2. <span data-ttu-id="f7502-798">Importe o perfil de publicação que você salvou na primeira tarefa.</span><span class="sxs-lookup"><span data-stu-id="f7502-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f7502-799">![Importando o perfil de publicação](aspnet-mvc-4-fundamentals/_static/image61.png "importando o perfil de publicação")</span><span class="sxs-lookup"><span data-stu-id="f7502-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    *<span data-ttu-id="f7502-800">Importando o perfil de publicação</span><span class="sxs-lookup"><span data-stu-id="f7502-800">Importing publish profile</span></span>*
3. <span data-ttu-id="f7502-801">Clique em **validar Conexão**.</span><span class="sxs-lookup"><span data-stu-id="f7502-801">Click **Validate Connection**.</span></span> <span data-ttu-id="f7502-802">Depois que a validação estiver concluída, clique em **próxima**.</span><span class="sxs-lookup"><span data-stu-id="f7502-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7502-803">A validação é concluída quando você vir uma marca de seleção verde aparecer ao lado do botão Validar Conexão.</span><span class="sxs-lookup"><span data-stu-id="f7502-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f7502-804">![Validar conexão](aspnet-mvc-4-fundamentals/_static/image62.png "validar conexão")</span><span class="sxs-lookup"><span data-stu-id="f7502-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    *<span data-ttu-id="f7502-805">Validando a conexão</span><span class="sxs-lookup"><span data-stu-id="f7502-805">Validating connection</span></span>*
4. <span data-ttu-id="f7502-806">No **as configurações** página na **bancos de dados** seção, clique no botão ao lado da caixa de texto do sua conexão banco de dados (ou seja, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="f7502-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f7502-807">![Configuração de implantação da Web](aspnet-mvc-4-fundamentals/_static/image63.png "configuração de implantação da Web")</span><span class="sxs-lookup"><span data-stu-id="f7502-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    *<span data-ttu-id="f7502-808">Configuração de implantação da Web</span><span class="sxs-lookup"><span data-stu-id="f7502-808">Web deploy configuration</span></span>*
5. <span data-ttu-id="f7502-809">Configure a conexão de banco de dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f7502-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f7502-810">No **nome do servidor** digite sua URL de servidor de banco de dados SQL usando o *tcp:* prefixo.</span><span class="sxs-lookup"><span data-stu-id="f7502-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f7502-811">Na **nome de usuário** digite seu nome de logon de administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="f7502-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f7502-812">Na **senha** digite sua senha de logon de administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="f7502-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f7502-813">Digite um novo nome de banco de dados, por exemplo: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="f7502-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="f7502-814">![Configurando a cadeia de caracteres de conexão de destino](aspnet-mvc-4-fundamentals/_static/image64.png "Configurando a cadeia de caracteres de conexão de destino")</span><span class="sxs-lookup"><span data-stu-id="f7502-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     *<span data-ttu-id="f7502-815">Configurando a cadeia de caracteres de conexão de destino</span><span class="sxs-lookup"><span data-stu-id="f7502-815">Configuring destination connection string</span></span>*
6. <span data-ttu-id="f7502-816">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7502-816">Then click **OK**.</span></span> <span data-ttu-id="f7502-817">Quando for solicitado a criar o banco de dados, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="f7502-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f7502-818">![Criando o banco de dados](aspnet-mvc-4-fundamentals/_static/image65.png "criando a cadeia de caracteres de banco de dados")</span><span class="sxs-lookup"><span data-stu-id="f7502-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    *<span data-ttu-id="f7502-819">Criando o banco de dados</span><span class="sxs-lookup"><span data-stu-id="f7502-819">Creating the database</span></span>*
7. <span data-ttu-id="f7502-820">A cadeia de caracteres de conexão que você usará para se conectar ao banco de dados SQL no Windows Azure é mostrada na caixa de texto de Conexão padrão.</span><span class="sxs-lookup"><span data-stu-id="f7502-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f7502-821">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-821">Then click **Next**.</span></span>

    <span data-ttu-id="f7502-822">![Cadeia de caracteres de Conexão que aponta para o banco de dados SQL](aspnet-mvc-4-fundamentals/_static/image66.png "cadeia de caracteres de Conexão que aponta para o banco de dados SQL")</span><span class="sxs-lookup"><span data-stu-id="f7502-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    *<span data-ttu-id="f7502-823">Cadeia de caracteres de Conexão que aponta para o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="f7502-823">Connection string pointing to SQL Database</span></span>*
8. <span data-ttu-id="f7502-824">No **versão prévia** , clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f7502-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f7502-825">![Publicando o aplicativo web](aspnet-mvc-4-fundamentals/_static/image67.png "publicando o aplicativo web")</span><span class="sxs-lookup"><span data-stu-id="f7502-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    *<span data-ttu-id="f7502-826">Publicar o aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="f7502-826">Publishing the web application</span></span>*
9. <span data-ttu-id="f7502-827">Quando o processo de publicação for concluído, o navegador padrão abrirá o site publicado.</span><span class="sxs-lookup"><span data-stu-id="f7502-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="f7502-828">![Aplicativo publicado no Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "aplicativo publicado no Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="f7502-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    *<span data-ttu-id="f7502-829">Aplicativo publicado para o Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f7502-829">Application published to Windows Azure</span></span>*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="f7502-830">Apêndice c: Usar trechos de código</span><span class="sxs-lookup"><span data-stu-id="f7502-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="f7502-831">Com trechos de código, você tem todo o código que necessário ao seu alcance.</span><span class="sxs-lookup"><span data-stu-id="f7502-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f7502-832">O documento de laboratório lhe dirá exatamente quando você pode usá-los, conforme mostrado na figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7502-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f7502-833">![Usar trechos de código do Visual Studio para inserir código em seu projeto](aspnet-mvc-4-fundamentals/_static/image69.png "trechos de código usando o Visual Studio para inserir código em seu projeto")</span><span class="sxs-lookup"><span data-stu-id="f7502-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

*<span data-ttu-id="f7502-834">Usar trechos de código do Visual Studio para inserir código em seu projeto</span><span class="sxs-lookup"><span data-stu-id="f7502-834">Using Visual Studio code snippets to insert code into your project</span></span>*

***<span data-ttu-id="f7502-835">Para adicionar um trecho de código usando o teclado (somente c#)</span><span class="sxs-lookup"><span data-stu-id="f7502-835">To add a code snippet using the keyboard (C# only)</span></span>***

1. <span data-ttu-id="f7502-836">Coloque o cursor onde você deseja inserir o código.</span><span class="sxs-lookup"><span data-stu-id="f7502-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f7502-837">Comece a digitar o nome do trecho de código (sem espaços ou hifens).</span><span class="sxs-lookup"><span data-stu-id="f7502-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f7502-838">Assista como o IntelliSense exibe os nomes dos trechos de código correspondentes.</span><span class="sxs-lookup"><span data-stu-id="f7502-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f7502-839">Selecione o trecho de código correto (ou continue digitando até que o nome do trecho toda está selecionado).</span><span class="sxs-lookup"><span data-stu-id="f7502-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f7502-840">Pressione a tecla Tab duas vezes para inserir o trecho de código no local do cursor.</span><span class="sxs-lookup"><span data-stu-id="f7502-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f7502-841">![Comece a digitar o nome do trecho](aspnet-mvc-4-fundamentals/_static/image70.png "comece a digitar o nome do trecho de código")</span><span class="sxs-lookup"><span data-stu-id="f7502-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

*<span data-ttu-id="f7502-842">Comece a digitar o nome do trecho de código</span><span class="sxs-lookup"><span data-stu-id="f7502-842">Start typing the snippet name</span></span>*

<span data-ttu-id="f7502-843">![Pressione Tab para selecionar o trecho de código realçado](aspnet-mvc-4-fundamentals/_static/image71.png "pressione Tab para selecionar o trecho de código realçado")</span><span class="sxs-lookup"><span data-stu-id="f7502-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

*<span data-ttu-id="f7502-844">Pressione Tab para selecionar o trecho de código realçado</span><span class="sxs-lookup"><span data-stu-id="f7502-844">Press Tab to select the highlighted snippet</span></span>*

<span data-ttu-id="f7502-845">![Pressione Tab novamente e o trecho de código serão expandido](aspnet-mvc-4-fundamentals/_static/image72.png "pressione Tab novamente e o trecho de código serão expandido")</span><span class="sxs-lookup"><span data-stu-id="f7502-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

*<span data-ttu-id="f7502-846">Pressione Tab novamente e o trecho de código serão expandido</span><span class="sxs-lookup"><span data-stu-id="f7502-846">Press Tab again and the snippet will expand</span></span>*

<span data-ttu-id="f7502-847">***Para adicionar um trecho de código usando o mouse (c#, Visual Basic e XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="f7502-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f7502-848">Clique com botão direito no qual você deseja inserir o trecho de código.</span><span class="sxs-lookup"><span data-stu-id="f7502-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f7502-849">Selecione **Inserir trecho** seguido **Meus trechos de código**.</span><span class="sxs-lookup"><span data-stu-id="f7502-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f7502-850">Selecione o trecho relevante na lista, clicando nele.</span><span class="sxs-lookup"><span data-stu-id="f7502-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f7502-851">![Clique com botão direito no qual você deseja inserir o trecho de código e selecione Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "botão direito do mouse em que você deseja inserir o trecho de código e selecione Insert Snippet")</span><span class="sxs-lookup"><span data-stu-id="f7502-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

*<span data-ttu-id="f7502-852">Clique com botão direito no qual você deseja inserir o trecho de código e selecione Insert Snippet</span><span class="sxs-lookup"><span data-stu-id="f7502-852">Right-click where you want to insert the code snippet and select Insert Snippet</span></span>*

<span data-ttu-id="f7502-853">![Escolher o trecho relevante na lista, clicando nele](aspnet-mvc-4-fundamentals/_static/image74.png "escolher o trecho relevante na lista, clicando nele")</span><span class="sxs-lookup"><span data-stu-id="f7502-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

*<span data-ttu-id="f7502-854">Escolher o trecho relevante na lista, clicando nele</span><span class="sxs-lookup"><span data-stu-id="f7502-854">Pick the relevant snippet from the list, by clicking on it</span></span>*
