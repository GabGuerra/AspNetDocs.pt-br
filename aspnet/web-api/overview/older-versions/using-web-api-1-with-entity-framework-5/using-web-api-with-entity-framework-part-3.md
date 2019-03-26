---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'Parte 3: Criando um controlador de administrador | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: 0fc533fb3673639769ecdfa8b3d02ff40133cb27
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421617"
---
<a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="b0224-102">Parte 3: Criação de um controlador de administrador</span><span class="sxs-lookup"><span data-stu-id="b0224-102">Part 3: Creating an Admin Controller</span></span>
====================
<span data-ttu-id="b0224-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b0224-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b0224-104">Baixe o projeto concluído</span><span class="sxs-lookup"><span data-stu-id="b0224-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="b0224-105">Adicionar um controlador de administrador</span><span class="sxs-lookup"><span data-stu-id="b0224-105">Add an Admin Controller</span></span>

<span data-ttu-id="b0224-106">Nesta seção, vamos adicionar um controlador de API da Web que dá suporte ao CRUD (criar, ler, atualizar e excluir) operações em produtos.</span><span class="sxs-lookup"><span data-stu-id="b0224-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="b0224-107">O controlador usará o Entity Framework para se comunicar com a camada de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="b0224-108">Somente os administradores poderão usar esse controlador.</span><span class="sxs-lookup"><span data-stu-id="b0224-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="b0224-109">Os clientes poderão acessar os produtos por meio de outro controlador.</span><span class="sxs-lookup"><span data-stu-id="b0224-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="b0224-110">No Gerenciador de soluções, clique com botão direito na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="b0224-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="b0224-111">Selecione **adicione** e, em seguida **controlador**.</span><span class="sxs-lookup"><span data-stu-id="b0224-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="b0224-112">No **Adicionar controlador** caixa de diálogo, nomeie o controlador `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="b0224-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="b0224-113">Sob **modelo**, selecione &quot;controlador API com ações de leitura/gravação, usando o Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="b0224-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="b0224-114">Sob **classe de modelo**, selecione "Product (ProductStore.Models)".</span><span class="sxs-lookup"><span data-stu-id="b0224-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="b0224-115">Sob **contexto de dados**, selecione "&lt;novo contexto de dados&gt;".</span><span class="sxs-lookup"><span data-stu-id="b0224-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="b0224-116">Se o **classe de modelo** suspensa não mostra as classes de modelo, verifique se você tiver compilado o projeto.</span><span class="sxs-lookup"><span data-stu-id="b0224-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="b0224-117">Entity Framework usa a reflexão, portanto, ele precisa que o assembly compilado.</span><span class="sxs-lookup"><span data-stu-id="b0224-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>


<span data-ttu-id="b0224-118">Selecionando "&lt;novo contexto de dados&gt;" abrirá o **novo contexto de dados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0224-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="b0224-119">Nomeie o contexto de dados `ProductStore.Models.OrdersContext`.</span><span class="sxs-lookup"><span data-stu-id="b0224-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="b0224-120">Clique em **Okey** para ignorar a **novo contexto de dados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b0224-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="b0224-121">No **Adicionar controlador** caixa de diálogo, clique em **Add**.</span><span class="sxs-lookup"><span data-stu-id="b0224-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="b0224-122">Aqui está o que foi adicionado ao projeto:</span><span class="sxs-lookup"><span data-stu-id="b0224-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="b0224-123">Uma classe chamada `OrdersContext` que deriva de **DbContext**.</span><span class="sxs-lookup"><span data-stu-id="b0224-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="b0224-124">Essa classe fornece a cola entre os modelos POCO e o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="b0224-125">Um controlador de API da Web chamado `AdminController`.</span><span class="sxs-lookup"><span data-stu-id="b0224-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="b0224-126">Esse controlador dá suporte a operações CRUD em `Product` instâncias.</span><span class="sxs-lookup"><span data-stu-id="b0224-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="b0224-127">Ele usa o `OrdersContext` classe para se comunicar com o Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="b0224-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="b0224-128">Uma nova cadeia de conexão de banco de dados no arquivo Web. config.</span><span class="sxs-lookup"><span data-stu-id="b0224-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="b0224-129">Abra o arquivo OrdersContext.cs.</span><span class="sxs-lookup"><span data-stu-id="b0224-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="b0224-130">Observe que o construtor Especifica o nome da cadeia de caracteres de conexão de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="b0224-131">Esse nome se refere à cadeia de conexão que foi adicionada ao Web. config.</span><span class="sxs-lookup"><span data-stu-id="b0224-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="b0224-132">Adicione as seguintes propriedades à classe `OrdersContext`:</span><span class="sxs-lookup"><span data-stu-id="b0224-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="b0224-133">Um **DbSet** representa um conjunto de entidades que podem ser consultados.</span><span class="sxs-lookup"><span data-stu-id="b0224-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="b0224-134">Aqui está a listagem completa para o `OrdersContext` classe:</span><span class="sxs-lookup"><span data-stu-id="b0224-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="b0224-135">O `AdminController` classe define cinco métodos que implementam a funcionalidade básica de CRUD.</span><span class="sxs-lookup"><span data-stu-id="b0224-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="b0224-136">Cada método corresponde a um URI que o cliente pode invocar:</span><span class="sxs-lookup"><span data-stu-id="b0224-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="b0224-137">Método do controlador</span><span class="sxs-lookup"><span data-stu-id="b0224-137">Controller Method</span></span> | <span data-ttu-id="b0224-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="b0224-138">Description</span></span> | <span data-ttu-id="b0224-139">URI</span><span class="sxs-lookup"><span data-stu-id="b0224-139">URI</span></span> | <span data-ttu-id="b0224-140">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="b0224-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b0224-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="b0224-141">GetProducts</span></span> | <span data-ttu-id="b0224-142">Obtém todos os produtos.</span><span class="sxs-lookup"><span data-stu-id="b0224-142">Gets all products.</span></span> | <span data-ttu-id="b0224-143">API/produtos</span><span class="sxs-lookup"><span data-stu-id="b0224-143">api/products</span></span> | <span data-ttu-id="b0224-144">OBTER</span><span class="sxs-lookup"><span data-stu-id="b0224-144">GET</span></span> |
| <span data-ttu-id="b0224-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="b0224-145">GetProduct</span></span> | <span data-ttu-id="b0224-146">Localiza um produto por ID.</span><span class="sxs-lookup"><span data-stu-id="b0224-146">Finds a product by ID.</span></span> | <span data-ttu-id="b0224-147">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b0224-147">api/products/*id*</span></span> | <span data-ttu-id="b0224-148">OBTER</span><span class="sxs-lookup"><span data-stu-id="b0224-148">GET</span></span> |
| <span data-ttu-id="b0224-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="b0224-149">PutProduct</span></span> | <span data-ttu-id="b0224-150">Atualiza um produto.</span><span class="sxs-lookup"><span data-stu-id="b0224-150">Updates a product.</span></span> | <span data-ttu-id="b0224-151">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b0224-151">api/products/*id*</span></span> | <span data-ttu-id="b0224-152">PUT</span><span class="sxs-lookup"><span data-stu-id="b0224-152">PUT</span></span> |
| <span data-ttu-id="b0224-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="b0224-153">PostProduct</span></span> | <span data-ttu-id="b0224-154">Cria um novo produto.</span><span class="sxs-lookup"><span data-stu-id="b0224-154">Creates a new product.</span></span> | <span data-ttu-id="b0224-155">API/produtos</span><span class="sxs-lookup"><span data-stu-id="b0224-155">api/products</span></span> | <span data-ttu-id="b0224-156">POSTAR</span><span class="sxs-lookup"><span data-stu-id="b0224-156">POST</span></span> |
| <span data-ttu-id="b0224-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="b0224-157">DeleteProduct</span></span> | <span data-ttu-id="b0224-158">Exclui um produto.</span><span class="sxs-lookup"><span data-stu-id="b0224-158">Deletes a product.</span></span> | <span data-ttu-id="b0224-159">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b0224-159">api/products/*id*</span></span> | <span data-ttu-id="b0224-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="b0224-160">DELETE</span></span> |

<span data-ttu-id="b0224-161">Chama cada método `OrdersContext` para consultar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="b0224-162">Chamam os métodos que modificam a coleção (PUT, POST e DELETE) `db.SaveChanges` para manter as alterações no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="b0224-163">Controladores são criados por solicitação HTTP e, em seguida, descartados, portanto, é necessário manter as alterações antes de um método retorna.</span><span class="sxs-lookup"><span data-stu-id="b0224-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="b0224-164">Adicionar um inicializador de banco de dados</span><span class="sxs-lookup"><span data-stu-id="b0224-164">Add a Database Initializer</span></span>

<span data-ttu-id="b0224-165">Entity Framework tem um recurso interessante que permite que você preencher o banco de dados na inicialização e recriar automaticamente o banco de dados sempre que alterar os modelos.</span><span class="sxs-lookup"><span data-stu-id="b0224-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="b0224-166">Esse recurso é útil durante o desenvolvimento, porque você sempre tem alguns dados de teste, mesmo se você alterar os modelos.</span><span class="sxs-lookup"><span data-stu-id="b0224-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="b0224-167">No Gerenciador de soluções, clique com botão direito na pasta modelos e criar uma nova classe chamada `OrdersContextInitializer`.</span><span class="sxs-lookup"><span data-stu-id="b0224-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="b0224-168">Cole a seguinte implementação:</span><span class="sxs-lookup"><span data-stu-id="b0224-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="b0224-169">Herdando a **DropCreateDatabaseIfModelChanges** classe, estamos informando o Entity Framework para descartar o banco de dados sempre que modificamos as classes de modelo.</span><span class="sxs-lookup"><span data-stu-id="b0224-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="b0224-170">Quando o Entity Framework cria (ou recria) o banco de dados, ele chama o **semente** para popular as tabelas.</span><span class="sxs-lookup"><span data-stu-id="b0224-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="b0224-171">Podemos usar o **semente** método para adicionar alguns produtos de exemplo mais de um pedido de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b0224-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="b0224-172">Esse recurso é ótimo para teste, mas não use o **DropCreateDatabaseIfModelChanges** classe em produção, pois você poderá perder seus dados se alguém alterar uma classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="b0224-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="b0224-173">Em seguida, abra o global. asax e adicione o seguinte código para o **Application\_iniciar** método:</span><span class="sxs-lookup"><span data-stu-id="b0224-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="b0224-174">Envie uma solicitação para o controlador</span><span class="sxs-lookup"><span data-stu-id="b0224-174">Send a Request to the Controller</span></span>

<span data-ttu-id="b0224-175">Neste ponto, nunca escrevemos qualquer código de cliente, mas você pode chamar a web API usando um navegador da web ou uma depuração de HTTP, como ferramenta [Fiddler](http://www.fiddler2.com/fiddler2/).</span><span class="sxs-lookup"><span data-stu-id="b0224-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="b0224-176">No Visual Studio, pressione F5 para iniciar a depuração.</span><span class="sxs-lookup"><span data-stu-id="b0224-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="b0224-177">Seu navegador da web abrirá `http://localhost:*portnum*/`, onde *portnum* é um número de porta.</span><span class="sxs-lookup"><span data-stu-id="b0224-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="b0224-178">Enviar uma solicitação HTTP para "`http://localhost:*portnum*/api/admin`.</span><span class="sxs-lookup"><span data-stu-id="b0224-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="b0224-179">A primeira solicitação pode ser lenta para ser concluída, pois o Entity Framework precisa para criar e propagar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0224-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="b0224-180">A resposta deverá algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="b0224-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="b0224-181">[Anterior](using-web-api-with-entity-framework-part-2.md)
> [Próximo](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="b0224-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
