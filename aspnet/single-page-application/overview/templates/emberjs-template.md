---
uid: single-page-application/overview/templates/emberjs-template
title: Modelo EmberJS | Microsoft Docs
author: xqiu
description: Modelo EmberJS
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 69331dc1cf2aacf306b55b49402f7df90f5e2c99
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421968"
---
<a name="emberjs-template"></a><span data-ttu-id="bf610-103">Modelo EmberJS</span><span class="sxs-lookup"><span data-stu-id="bf610-103">EmberJS template</span></span>
====================
<span data-ttu-id="bf610-104">por [Xinyang Qiu](https://github.com/xqiu)</span><span class="sxs-lookup"><span data-stu-id="bf610-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="bf610-105">O modelo MVC EmberJS é gravado por Nathan Totten, Thiago Santos e Xinyang Qiu.</span><span class="sxs-lookup"><span data-stu-id="bf610-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="bf610-106">Baixe o modelo MVC EmberJS</span><span class="sxs-lookup"><span data-stu-id="bf610-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)


<span data-ttu-id="bf610-107">O modelo EmberJS SPA é projetado para ajudá-lo a começar a criar rapidamente aplicativos web interativos do lado do cliente usando o EmberJS.</span><span class="sxs-lookup"><span data-stu-id="bf610-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="bf610-108">"Aplicativo de página única" (SPA) é o termo geral para um aplicativo web que carrega uma página HTML única e, em seguida, atualiza a página dinamicamente, em vez de carregar novas páginas.</span><span class="sxs-lookup"><span data-stu-id="bf610-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="bf610-109">Após o carregamento de página inicial, o SPA se comunica com o servidor por meio de solicitações AJAX.</span><span class="sxs-lookup"><span data-stu-id="bf610-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="bf610-110">AJAX não é novidade, mas hoje em dia há estruturas de JavaScript que facilitam criar e manter um grande aplicativo SPA sofisticado.</span><span class="sxs-lookup"><span data-stu-id="bf610-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="bf610-111">Além disso, HTML 5 e CSS3 são tornando mais fácil criar interfaces do usuário avançadas.</span><span class="sxs-lookup"><span data-stu-id="bf610-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="bf610-112">O modelo de SPA EmberJS usa o [Ember](http://emberjs.com/) biblioteca de JavaScript para manipular atualizações de página de solicitações AJAX.</span><span class="sxs-lookup"><span data-stu-id="bf610-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="bf610-113">Ember usa associação de dados para sincronizar a página com os dados mais recentes.</span><span class="sxs-lookup"><span data-stu-id="bf610-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="bf610-114">Dessa forma, você não precisa escrever nenhum código que percorre os dados JSON e atualiza o DOM.</span><span class="sxs-lookup"><span data-stu-id="bf610-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="bf610-115">Em vez disso, você deve colocar atributos declarativos em HTML que informam o ember como apresentar os dados.</span><span class="sxs-lookup"><span data-stu-id="bf610-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="bf610-116">No lado do servidor, o modelo EmberJS é quase idêntico do [modelo KnockoutJS SPA](../introduction/knockoutjs-template.md).</span><span class="sxs-lookup"><span data-stu-id="bf610-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="bf610-117">Ele usa o ASP.NET MVC para servir de documentos HTML e a API Web do ASP.NET para manipular solicitações AJAX do cliente.</span><span class="sxs-lookup"><span data-stu-id="bf610-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="bf610-118">Para obter mais informações sobre esses aspectos do modelo, consulte o [modelo KnockoutJS](../introduction/knockoutjs-template.md) documentação.</span><span class="sxs-lookup"><span data-stu-id="bf610-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="bf610-119">Este tópico enfoca as diferenças entre o modelo do Knockout e o modelo EmberJS.</span><span class="sxs-lookup"><span data-stu-id="bf610-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="bf610-120">Criar um projeto de modelo do SPA EmberJS</span><span class="sxs-lookup"><span data-stu-id="bf610-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="bf610-121">Baixe e instale o modelo clicando no botão de Download acima.</span><span class="sxs-lookup"><span data-stu-id="bf610-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="bf610-122">Talvez você precise reiniciar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf610-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="bf610-123">No painel **Modelos**, selecione **Modelos Instalados** e expanda o nó **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="bf610-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="bf610-124">Em **Visual C#**, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="bf610-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="bf610-125">Na lista de modelos de projeto, selecione **aplicativo Web do ASP.NET MVC 4**.</span><span class="sxs-lookup"><span data-stu-id="bf610-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="bf610-126">Nomeie o projeto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="bf610-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="bf610-127">No **novo projeto** assistente, selecione **projeto do SPA ember**.</span><span class="sxs-lookup"><span data-stu-id="bf610-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="bf610-128">Visão geral do modelo EmberJS SPA</span><span class="sxs-lookup"><span data-stu-id="bf610-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="bf610-129">O modelo EmberJS usa uma combinação de jQuery, ember, Handlebars.js para criar uma interface de usuário interativa suave.</span><span class="sxs-lookup"><span data-stu-id="bf610-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="bf610-130">Ember é uma biblioteca de JavaScript que usa um padrão MVC do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="bf610-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="bf610-131">Um *modelo*escrito na linguagem de modelagem Handlebars, descreve a interface de usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf610-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="bf610-132">No modo de versão, o [compilador Handlebars](https://github.com/Myslik/csharp-ember-handlebars) é usado para agrupar e compilar o modelo handlebars.</span><span class="sxs-lookup"><span data-stu-id="bf610-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="bf610-133">Um *modelo* armazena os dados de aplicativo que ele obtém do servidor (listas de tarefas pendentes e itens de tarefas).</span><span class="sxs-lookup"><span data-stu-id="bf610-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="bf610-134">Um *controlador* armazena o estado do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bf610-134">A *controller* stores application state.</span></span> <span data-ttu-id="bf610-135">Controladores geralmente apresentam dados de modelo para os modelos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="bf610-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="bf610-136">Um *exibição* converte primitivos eventos do aplicativo e os passa para o controlador.</span><span class="sxs-lookup"><span data-stu-id="bf610-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="bf610-137">Um *roteador* gerencia o estado do aplicativo, mantendo as URLs e modelos em sincronia.</span><span class="sxs-lookup"><span data-stu-id="bf610-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="bf610-138">Além disso, a biblioteca Ember dados pode ser usada para sincronizar objetos JSON (obtidos do servidor por meio de uma API RESTful) e os modelos de cliente.</span><span class="sxs-lookup"><span data-stu-id="bf610-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="bf610-139">O modelo EmberJS SPA organiza os scripts em oito camadas:</span><span class="sxs-lookup"><span data-stu-id="bf610-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="bf610-140">webapi\_adapter.js, webapi\_serializer.js: Estende a biblioteca Ember dados para trabalhar com a API Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bf610-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="bf610-141">Scripts/helpers.js: Define os auxiliares de Handlebars Ember novo.</span><span class="sxs-lookup"><span data-stu-id="bf610-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="bf610-142">Scripts/app.js: Cria o aplicativo e configura o adaptador e o serializador.</span><span class="sxs-lookup"><span data-stu-id="bf610-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="bf610-143">App/scripts/modelos/\*. js: Define os modelos.</span><span class="sxs-lookup"><span data-stu-id="bf610-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="bf610-144">Scripts/app/exibições/\*. js: Define os modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="bf610-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="bf610-145">App/scripts/controladores/\*. js: Define os controladores.</span><span class="sxs-lookup"><span data-stu-id="bf610-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="bf610-146">Scripts/app/routes, Scripts/app/router.js: Define as rotas.</span><span class="sxs-lookup"><span data-stu-id="bf610-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="bf610-147">Modelos /\*.hbs: Define os modelos handlebars.</span><span class="sxs-lookup"><span data-stu-id="bf610-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="bf610-148">Vamos examinar alguns desses scripts mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="bf610-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="bf610-149">Modelos</span><span class="sxs-lookup"><span data-stu-id="bf610-149">Models</span></span>

<span data-ttu-id="bf610-150">Os modelos são definidos na pasta Scripts/app/modelos.</span><span class="sxs-lookup"><span data-stu-id="bf610-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="bf610-151">Existem dois arquivos de modelo: todoitem. js e todoList.js.</span><span class="sxs-lookup"><span data-stu-id="bf610-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="bf610-152">**todo.Model.js** define os modelos do lado do cliente (navegador) para as listas de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="bf610-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="bf610-153">Há duas classes de modelo: todoItem e lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="bf610-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="bf610-154">No Ember, os modelos são subclasses de DS. Modelo.</span><span class="sxs-lookup"><span data-stu-id="bf610-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="bf610-155">Um modelo pode ter propriedades com atributos:</span><span class="sxs-lookup"><span data-stu-id="bf610-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="bf610-156">Modelos podem definir relações com outros modelos:</span><span class="sxs-lookup"><span data-stu-id="bf610-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="bf610-157">Modelos podem ter propriedades que se associam a outras propriedades computadas:</span><span class="sxs-lookup"><span data-stu-id="bf610-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="bf610-158">Modelos podem ter funções de observador, que são chamadas quando uma propriedade observada ser alterada:</span><span class="sxs-lookup"><span data-stu-id="bf610-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="bf610-159">Exibições</span><span class="sxs-lookup"><span data-stu-id="bf610-159">Views</span></span>

<span data-ttu-id="bf610-160">As exibições são definidas na pasta Scripts/app/exibições.</span><span class="sxs-lookup"><span data-stu-id="bf610-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="bf610-161">Um modo de exibição converte os eventos do aplicativo da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="bf610-161">A view translates events from the application UI.</span></span> <span data-ttu-id="bf610-162">Um manipulador de eventos pode chamada de retorno para funções de controlador ou simplesmente chamar o contexto de dados diretamente.</span><span class="sxs-lookup"><span data-stu-id="bf610-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="bf610-163">Por exemplo, o código a seguir é de views/TodoItemEditView.js.</span><span class="sxs-lookup"><span data-stu-id="bf610-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="bf610-164">Ele define o manipulação de eventos para um campo de texto de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf610-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="bf610-165">Controlador</span><span class="sxs-lookup"><span data-stu-id="bf610-165">Controller</span></span>

<span data-ttu-id="bf610-166">Os controladores são definidos na pasta Scripts/app/controladores.</span><span class="sxs-lookup"><span data-stu-id="bf610-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="bf610-167">Para representar um único modelo, estender `Ember.ObjectController`:</span><span class="sxs-lookup"><span data-stu-id="bf610-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="bf610-168">Um controlador também pode representar uma coleção de modelos, estendendo `Ember.ArrayController`.</span><span class="sxs-lookup"><span data-stu-id="bf610-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="bf610-169">Por exemplo, o TodoListController representa uma matriz de `todoList` objetos.</span><span class="sxs-lookup"><span data-stu-id="bf610-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="bf610-170">O controlador classifica por ID de lista de tarefas pendentes, em ordem decrescente:</span><span class="sxs-lookup"><span data-stu-id="bf610-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="bf610-171">O controlador define uma função chamada `addTodoList`, que cria uma nova lista de tarefas e o adiciona à matriz.</span><span class="sxs-lookup"><span data-stu-id="bf610-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="bf610-172">Para ver como essa função é chamada, abra o arquivo de modelo chamado todoListTemplate.html, na pasta modelos.</span><span class="sxs-lookup"><span data-stu-id="bf610-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="bf610-173">O código de modelo a seguir associa um botão para o `addTodoList` função:</span><span class="sxs-lookup"><span data-stu-id="bf610-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="bf610-174">O controlador também contém um `error` propriedade, que contém uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="bf610-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="bf610-175">Aqui está o código de modelo para exibir a mensagem de erro (também em todoListTemplate.html):</span><span class="sxs-lookup"><span data-stu-id="bf610-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="bf610-176">Rotas</span><span class="sxs-lookup"><span data-stu-id="bf610-176">Routes</span></span>

<span data-ttu-id="bf610-177">Router.js define as rotas e o modelo padrão para exibir conjuntos de backup do estado do aplicativo e corresponde a URLs às rotas:</span><span class="sxs-lookup"><span data-stu-id="bf610-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="bf610-178">TodoListRoute.js carrega dados para o TodoListRoute, substituindo a função setupController:</span><span class="sxs-lookup"><span data-stu-id="bf610-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="bf610-179">O ember usa as convenções de nomenclatura para corresponder a URLs, nomes de rotas, controladores e modelos.</span><span class="sxs-lookup"><span data-stu-id="bf610-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="bf610-180">Para obter mais informações, consulte [ http://emberjs.com/guides/routing/defining-your-routes/ ](http://emberjs.com/guides/routing/defining-your-routes/) na documentação EmberJS.</span><span class="sxs-lookup"><span data-stu-id="bf610-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="bf610-181">Modelos</span><span class="sxs-lookup"><span data-stu-id="bf610-181">Templates</span></span>

<span data-ttu-id="bf610-182">A pasta Modelos contém quatro modelos:</span><span class="sxs-lookup"><span data-stu-id="bf610-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="bf610-183">Application.HBS: O modelo padrão que é renderizado quando o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="bf610-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="bf610-184">About.HBS: O modelo de rota "/ sobre".</span><span class="sxs-lookup"><span data-stu-id="bf610-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="bf610-185">index.hbs: O modelo para a raiz "/" rota.</span><span class="sxs-lookup"><span data-stu-id="bf610-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="bf610-186">todoList.hbs: O modelo para o "/ todo" rota.</span><span class="sxs-lookup"><span data-stu-id="bf610-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="bf610-187">\_navbar.hbs: O modelo define o menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="bf610-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="bf610-188">O modelo de aplicativo funciona como uma página mestra.</span><span class="sxs-lookup"><span data-stu-id="bf610-188">The application template acts like a master page.</span></span> <span data-ttu-id="bf610-189">Ele contém um cabeçalho, um rodapé e uma "{{outlet}}" para inserir outros modelos no dependendo da rota.</span><span class="sxs-lookup"><span data-stu-id="bf610-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="bf610-190">Para obter mais informações sobre modelos de aplicativo no Ember, consulte [ http://guides.emberjs.com/v1.10.0/templates/the-application-template// ](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="bf610-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="bf610-191">O "/ lista de tarefas pendentes" modelo contém duas expressões de loop.</span><span class="sxs-lookup"><span data-stu-id="bf610-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="bf610-192">O loop externo é `{{#each controller}}`e o loop é `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="bf610-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="bf610-193">O código a seguir mostra uma interna `Ember.Checkbox` exibir, um personalizado `App.TodoItemEditView`e um link com um `deleteTodo` ação.</span><span class="sxs-lookup"><span data-stu-id="bf610-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="bf610-194">O `HtmlHelperExtensions` classe, definida na Controllers/HtmlHelperExtensions.cs, define um auxiliar de função em cache e inserir modelo arquivos ao **debug** é definido como **true** no arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="bf610-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="bf610-195">Essa função é chamada do arquivo de exibição do MVC do ASP.NET definido no Views/Home/App.cshtml:</span><span class="sxs-lookup"><span data-stu-id="bf610-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="bf610-196">A função chamado sem argumentos, processa todos os arquivos de modelo na pasta modelos.</span><span class="sxs-lookup"><span data-stu-id="bf610-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="bf610-197">Você também pode especificar uma subpasta ou um arquivo de modelo específico.</span><span class="sxs-lookup"><span data-stu-id="bf610-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="bf610-198">Quando **debug** é **falso** no Web. config, o aplicativo inclui o item de pacote "~/bundles/templates".</span><span class="sxs-lookup"><span data-stu-id="bf610-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="bf610-199">Este item de pacote for adicionado no BundleConfig.cs, usando a biblioteca de compilador Handlebars:</span><span class="sxs-lookup"><span data-stu-id="bf610-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
