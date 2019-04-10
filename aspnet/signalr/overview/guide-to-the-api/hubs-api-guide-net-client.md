---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR guia da API Hubs – cliente .NET (c#) | Microsoft Docs
author: bradygaster
description: Este documento fornece uma introdução ao uso da API de Hubs de SignalR versão 2 em clientes do .NET, como Windows Store (WinRT), WPF, Silverlight e contras...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 473c8dd14d639fb9f4ff9e11a4c3ffa2b1a3a81e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59396025"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="92a6f-103">ASP.NET SignalR guia da API Hubs – cliente .NET (c#)</span><span class="sxs-lookup"><span data-stu-id="92a6f-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>


[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="92a6f-104">Este documento fornece uma introdução ao uso da API de Hubs de SignalR versão 2 em clientes do .NET, como aplicativos de console, WPF, Silverlight e Store do Windows (WinRT).</span><span class="sxs-lookup"><span data-stu-id="92a6f-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="92a6f-105">A API de Hubs de SignalR permite que você faça chamadas de procedimento remoto (RPCs) de um servidor para clientes conectados e de clientes para o servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="92a6f-106">No código do servidor, você define métodos que podem ser chamados por clientes e você chamar métodos que são executados no cliente.</span><span class="sxs-lookup"><span data-stu-id="92a6f-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="92a6f-107">No código do cliente, você define métodos que podem ser chamados a partir do servidor e você chamar métodos que são executados no servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="92a6f-108">O SignalR é responsável por todos os detalhes de cliente-servidor para você.</span><span class="sxs-lookup"><span data-stu-id="92a6f-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="92a6f-109">O SignalR também oferece uma API de nível inferior chamada conexões persistentes.</span><span class="sxs-lookup"><span data-stu-id="92a6f-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="92a6f-110">Para obter uma introdução ao SignalR, Hubs e conexões persistentes, ou para um tutorial que mostra como criar um aplicativo completo do SignalR, consulte [SignalR - Introdução ao](../getting-started/index.md).</span><span class="sxs-lookup"><span data-stu-id="92a6f-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="92a6f-111">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="92a6f-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="92a6f-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="92a6f-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="92a6f-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="92a6f-113">.NET 4.5</span></span>
> - <span data-ttu-id="92a6f-114">Versão 2 do SignalR</span><span class="sxs-lookup"><span data-stu-id="92a6f-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="92a6f-115">Versões anteriores deste tópico</span><span class="sxs-lookup"><span data-stu-id="92a6f-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="92a6f-116">Para obter informações sobre versões anteriores do SignalR, consulte [versões mais antigas do SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="92a6f-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="92a6f-117">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="92a6f-117">Questions and comments</span></span>
>
> <span data-ttu-id="92a6f-118">Deixe comentários sobre como você gostou neste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="92a6f-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="92a6f-119">Se você tiver perguntas que não estão diretamente relacionadas para o tutorial, você pode postá-los para o [Fórum do ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="92a6f-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="92a6f-120">Visão geral</span><span class="sxs-lookup"><span data-stu-id="92a6f-120">Overview</span></span>

<span data-ttu-id="92a6f-121">Este documento contém as seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="92a6f-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="92a6f-122">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="92a6f-123">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="92a6f-124">Conexões entre domínios de clientes do Silverlight</span><span class="sxs-lookup"><span data-stu-id="92a6f-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="92a6f-125">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="92a6f-126">Como definir o número máximo de conexões simultâneas em clientes do WPF</span><span class="sxs-lookup"><span data-stu-id="92a6f-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="92a6f-127">Como especificar parâmetros de cadeia de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="92a6f-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="92a6f-128">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="92a6f-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="92a6f-129">Como especificar cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="92a6f-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="92a6f-130">Como especificar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="92a6f-131">Como criar o proxy do Hub</span><span class="sxs-lookup"><span data-stu-id="92a6f-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="92a6f-132">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="92a6f-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="92a6f-133">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="92a6f-134">Métodos com parâmetros, especificando os tipos de parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="92a6f-135">Métodos com parâmetros, especificando os objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="92a6f-136">Como remover um manipulador</span><span class="sxs-lookup"><span data-stu-id="92a6f-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="92a6f-137">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="92a6f-138">Como manipular eventos de tempo de vida da conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="92a6f-139">Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="92a6f-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="92a6f-140">Como habilitar o registro em log do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="92a6f-141">Exemplos de código de aplicativo de console para que o servidor pode chamar métodos do cliente, o Silverlight e WPF</span><span class="sxs-lookup"><span data-stu-id="92a6f-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="92a6f-142">Um exemplo .NET para projetos de cliente, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="92a6f-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="92a6f-143">[Gustavo armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) no GitHub.com (WinRT, Silverlight, exemplos de aplicativo de console).</span><span class="sxs-lookup"><span data-stu-id="92a6f-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="92a6f-144">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) no GitHub.com (exemplo do WPF).</span><span class="sxs-lookup"><span data-stu-id="92a6f-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="92a6f-145">[O SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) no GitHub.com (exemplo de aplicativo de Console).</span><span class="sxs-lookup"><span data-stu-id="92a6f-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="92a6f-146">Para obter documentação sobre como programar o servidor ou os clientes JavaScript, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="92a6f-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="92a6f-147">Guia de API de Hubs de SignalR – servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="92a6f-148">O SignalR guia da API Hubs – cliente JavaScript</span><span class="sxs-lookup"><span data-stu-id="92a6f-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="92a6f-149">Links para tópicos de referência de API são para a versão 4.5 do .NET da API.</span><span class="sxs-lookup"><span data-stu-id="92a6f-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="92a6f-150">Se você estiver usando o .NET 4, consulte [a versão do .NET 4 dos tópicos da API](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6f-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="92a6f-151">Configuração do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-151">Client setup</span></span>

<span data-ttu-id="92a6f-152">Instalar o [ASPNET](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) pacote do NuGet (não o [ASPNET](http://nuget.org/packages/microsoft.aspnet.signalr) pacote).</span><span class="sxs-lookup"><span data-stu-id="92a6f-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="92a6f-153">Este pacote suporta WinRT, Silverlight, WPF, o aplicativo de console e os clientes do Windows Phone, para .NET 4 e .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="92a6f-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="92a6f-154">Se a versão do SignalR que você tem no cliente é diferente da versão que você tem no servidor, o SignalR geralmente é capaz de se adaptar à diferença.</span><span class="sxs-lookup"><span data-stu-id="92a6f-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="92a6f-155">Por exemplo, um servidor que executa a versão 2 do SignalR será dar suporte a clientes que têm 1.1.x instalado, bem como os clientes que têm a versão 2 instalado.</span><span class="sxs-lookup"><span data-stu-id="92a6f-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="92a6f-156">Se a diferença entre a versão no servidor e a versão do cliente for muito grande, ou se o cliente mais recente do que o servidor, o SignalR gera um `InvalidOperationException` exceção quando o cliente tenta estabelecer uma conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="92a6f-157">A mensagem de erro é "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span><span class="sxs-lookup"><span data-stu-id="92a6f-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="92a6f-158">Como estabelecer uma conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-158">How to establish a connection</span></span>

<span data-ttu-id="92a6f-159">Antes de estabelecer uma conexão, você precisa criar um `HubConnection` de objeto e criar um proxy.</span><span class="sxs-lookup"><span data-stu-id="92a6f-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="92a6f-160">Para estabelecer a conexão, chame o `Start` método no `HubConnection` objeto.</span><span class="sxs-lookup"><span data-stu-id="92a6f-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="92a6f-161">Para clientes de JavaScript, você precisa registrar pelo menos um manipulador de eventos antes de chamar o `Start` método para estabelecer a conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="92a6f-162">Isso não é necessário para clientes .NET.</span><span class="sxs-lookup"><span data-stu-id="92a6f-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="92a6f-163">Para clientes de JavaScript, o código de proxy gerada automaticamente cria proxies para todos os Hubs que existem no servidor e registrar um manipulador é como você indica que os Hubs de seu cliente pretende usar.</span><span class="sxs-lookup"><span data-stu-id="92a6f-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="92a6f-164">Mas para um cliente .NET criar proxies Hub manualmente, portanto, o SignalR pressupõe que você usará o Hub que você cria um proxy para.</span><span class="sxs-lookup"><span data-stu-id="92a6f-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="92a6f-165">O código de exemplo usa o padrão "/ signalr" URL para se conectar ao seu serviço SignalR.</span><span class="sxs-lookup"><span data-stu-id="92a6f-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="92a6f-166">Para obter informações sobre como especificar uma URL de base diferente, consulte [o guia da API de Hubs de SignalR do ASP.NET - Server - URL /signalr](hubs-api-guide-server.md#signalrurl).</span><span class="sxs-lookup"><span data-stu-id="92a6f-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="92a6f-167">O `Start` método executa de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="92a6f-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="92a6f-168">Para certificar-se de que as linhas subsequentes do código não executam até depois que a conexão for estabelecida, use `await` em um método assíncrono do ASP.NET 4.5 ou `.Wait()` em um método síncrono.</span><span class="sxs-lookup"><span data-stu-id="92a6f-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="92a6f-169">Não use `.Wait()` em um cliente do WinRT.</span><span class="sxs-lookup"><span data-stu-id="92a6f-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="92a6f-170">Conexões entre domínios de clientes do Silverlight</span><span class="sxs-lookup"><span data-stu-id="92a6f-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="92a6f-171">Para obter informações sobre como habilitar conexões entre domínios de clientes do Silverlight, consulte [tornando um serviço disponível entre limites de domínio](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6f-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="92a6f-172">Como configurar a conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-172">How to configure the connection</span></span>

<span data-ttu-id="92a6f-173">Antes de estabelecer uma conexão, você pode especificar qualquer uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="92a6f-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="92a6f-174">Limite de conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="92a6f-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="92a6f-175">Parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="92a6f-175">Query string parameters.</span></span>
- <span data-ttu-id="92a6f-176">O método de transporte.</span><span class="sxs-lookup"><span data-stu-id="92a6f-176">The transport method.</span></span>
- <span data-ttu-id="92a6f-177">Cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="92a6f-177">HTTP headers.</span></span>
- <span data-ttu-id="92a6f-178">Certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="92a6f-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="92a6f-179">Como definir o número máximo de conexões simultâneas em clientes do WPF</span><span class="sxs-lookup"><span data-stu-id="92a6f-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="92a6f-180">Em clientes do WPF, você talvez precise aumentar o número máximo de conexões simultâneas de seu valor padrão de 2.</span><span class="sxs-lookup"><span data-stu-id="92a6f-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="92a6f-181">O valor recomendado é 10.</span><span class="sxs-lookup"><span data-stu-id="92a6f-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="92a6f-182">Para obter mais informações, consulte [ServicePointManager. Defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6f-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="92a6f-183">Como especificar parâmetros de cadeia de caracteres de consulta</span><span class="sxs-lookup"><span data-stu-id="92a6f-183">How to specify query string parameters</span></span>

<span data-ttu-id="92a6f-184">Se você quiser enviar dados para o servidor quando o cliente se conecta, você pode adicionar parâmetros de cadeia de caracteres de consulta para o objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="92a6f-185">O exemplo a seguir mostra como definir um parâmetro de cadeia de caracteres de consulta no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="92a6f-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="92a6f-186">O exemplo a seguir mostra como ler um parâmetro de cadeia de caracteres de consulta no código do servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="92a6f-187">Como especificar o método de transporte</span><span class="sxs-lookup"><span data-stu-id="92a6f-187">How to specify the transport method</span></span>

<span data-ttu-id="92a6f-188">Como parte do processo de conexão, um cliente SignalR normalmente negocia com o servidor para determinar o melhor transporte com suporte pelo cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="92a6f-189">Se você já souber qual transporte você deseja usar, você pode ignorar esse processo de negociação.</span><span class="sxs-lookup"><span data-stu-id="92a6f-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="92a6f-190">Para especificar o método de transporte, passe um objeto de transporte para o método Start.</span><span class="sxs-lookup"><span data-stu-id="92a6f-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="92a6f-191">O exemplo a seguir mostra como especificar o método de transporte no código do cliente.</span><span class="sxs-lookup"><span data-stu-id="92a6f-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="92a6f-192">O [Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace inclui as seguintes classes que você pode usar para especificar o transporte.</span><span class="sxs-lookup"><span data-stu-id="92a6f-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- [<span data-ttu-id="92a6f-193">LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="92a6f-193">LongPollingTransport</span></span>](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [<span data-ttu-id="92a6f-194">ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="92a6f-194">ServerSentEventsTransport</span></span>](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- <span data-ttu-id="92a6f-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (disponível somente quando o servidor e cliente usam o .NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="92a6f-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="92a6f-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (escolhe automaticamente o melhor transporte é compatível com o cliente e o servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="92a6f-197">Isso é o transporte padrão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-197">This is the default transport.</span></span> <span data-ttu-id="92a6f-198">Passar isso para o `Start` método tem o mesmo efeito que não está passando em nada.)</span><span class="sxs-lookup"><span data-stu-id="92a6f-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="92a6f-199">O transporte ForeverFrame não está incluído nesta lista, porque ele é usado somente pelos navegadores.</span><span class="sxs-lookup"><span data-stu-id="92a6f-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="92a6f-200">Para obter informações sobre como verificar o método de transporte no código do servidor, consulte [o guia da API de Hubs de SignalR do ASP.NET - Server - como obter informações sobre o cliente da propriedade de contexto](hubs-api-guide-server.md#contextproperty).</span><span class="sxs-lookup"><span data-stu-id="92a6f-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="92a6f-201">Para obter mais informações sobre os transportes e fallbacks, consulte [Introdução ao SignalR - transportes e Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span><span class="sxs-lookup"><span data-stu-id="92a6f-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="92a6f-202">Como especificar cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="92a6f-202">How to specify HTTP headers</span></span>

<span data-ttu-id="92a6f-203">Para definir cabeçalhos HTTP, use o `Headers` propriedade no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="92a6f-204">O exemplo a seguir mostra como adicionar um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="92a6f-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="92a6f-205">Como especificar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-205">How to specify client certificates</span></span>

<span data-ttu-id="92a6f-206">Para adicionar certificados de cliente, use o `AddClientCertificate` método no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="92a6f-207">Como criar o proxy do Hub</span><span class="sxs-lookup"><span data-stu-id="92a6f-207">How to create the Hub proxy</span></span>

<span data-ttu-id="92a6f-208">Para definir métodos no cliente que um Hub pode chamar a partir do servidor e invocar métodos em um Hub no servidor, criar um proxy para o Hub chamando `CreateHubProxy` no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="92a6f-209">A cadeia de caracteres para o qual você passa `CreateHubProxy` é o nome da sua classe Hub ou o nome especificado pelo `HubName` atributo se estava sendo usado no servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="92a6f-210">Correspondência de nome não diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="92a6f-210">Name matching is case-insensitive.</span></span>

**<span data-ttu-id="92a6f-211">Classe de Hub no servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-211">Hub class on server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**<span data-ttu-id="92a6f-212">Criar proxy de cliente para a classe Hub</span><span class="sxs-lookup"><span data-stu-id="92a6f-212">Create client proxy for the Hub class</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="92a6f-213">Se você decorar a classe Hub com um `HubName` de atributo, use esse nome.</span><span class="sxs-lookup"><span data-stu-id="92a6f-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

**<span data-ttu-id="92a6f-214">Classe de Hub no servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-214">Hub class on server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**<span data-ttu-id="92a6f-215">Criar proxy de cliente para a classe Hub</span><span class="sxs-lookup"><span data-stu-id="92a6f-215">Create client proxy for the Hub class</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="92a6f-216">Se você chamar `HubConnection.CreateHubProxy` várias vezes com o mesmo `hubName`, você obterá a mesma armazenados em cache `IHubProxy` objeto.</span><span class="sxs-lookup"><span data-stu-id="92a6f-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="92a6f-217">Como definir métodos no cliente que o servidor pode chamar</span><span class="sxs-lookup"><span data-stu-id="92a6f-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="92a6f-218">Para definir um método que o servidor pode chamar, use o proxy `On` método para registrar um manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="92a6f-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="92a6f-219">Correspondência de nomes do método diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="92a6f-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="92a6f-220">Por exemplo, `Clients.All.UpdateStockPrice` no servidor serão executadas `updateStockPrice`, `updatestockprice`, ou `UpdateStockPrice` no cliente.</span><span class="sxs-lookup"><span data-stu-id="92a6f-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="92a6f-221">Plataformas de cliente diferentes têm requisitos diferentes para como escrever o código do método para atualizar a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="92a6f-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="92a6f-222">Os exemplos mostrados são para clientes do WinRT (Windows Store .NET).</span><span class="sxs-lookup"><span data-stu-id="92a6f-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="92a6f-223">WPF, Silverlight e exemplos de aplicativos de console são fornecidos no [uma seção separada deste tópico](#wpfsl).</span><span class="sxs-lookup"><span data-stu-id="92a6f-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="92a6f-224">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-224">Methods without parameters</span></span>

<span data-ttu-id="92a6f-225">Se o método que está sendo manipulado não tiver parâmetros, use a sobrecarga de não-genérica do `On` método:</span><span class="sxs-lookup"><span data-stu-id="92a6f-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

**<span data-ttu-id="92a6f-226">Código do servidor chamando o método de cliente sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-226">Server code calling client method without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**<span data-ttu-id="92a6f-227">Código de cliente do WinRT para método de chamada do servidor sem parâmetros ([ver exemplos WPF e Silverlight neste tópico](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="92a6f-227">WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="92a6f-228">Métodos com parâmetros, especificando os tipos de parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="92a6f-229">Se o método que você está lidando tiver parâmetros, especifique os tipos dos parâmetros como os tipos genéricos do `On` método.</span><span class="sxs-lookup"><span data-stu-id="92a6f-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="92a6f-230">Há sobrecargas genéricas do `On` método para que você possa especificar os parâmetros de até 8 (4 no Windows Phone 7).</span><span class="sxs-lookup"><span data-stu-id="92a6f-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="92a6f-231">No exemplo a seguir, um parâmetro é enviado para o `UpdateStockPrice` método.</span><span class="sxs-lookup"><span data-stu-id="92a6f-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

**<span data-ttu-id="92a6f-232">Chamar o método de cliente com um parâmetro de código do servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-232">Server code calling client method with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**<span data-ttu-id="92a6f-233">A classe de estoque usada para o parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-233">The Stock class used for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**<span data-ttu-id="92a6f-234">Código do cliente do WinRT para um método chamado de servidor com um parâmetro ([ver exemplos WPF e Silverlight neste tópico](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="92a6f-234">WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="92a6f-235">Métodos com parâmetros, especificando os objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="92a6f-236">Como uma alternativa para especificar parâmetros como tipos genéricos do `On` método, você pode especificar parâmetros como objetos dinâmicos:</span><span class="sxs-lookup"><span data-stu-id="92a6f-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

**<span data-ttu-id="92a6f-237">Chamar o método de cliente com um parâmetro de código do servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-237">Server code calling client method with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**<span data-ttu-id="92a6f-238">A classe de estoque usada para o parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-238">The Stock class used for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**<span data-ttu-id="92a6f-239">Código do cliente do WinRT para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro ([ver exemplos WPF e Silverlight neste tópico](#wpfsl))</span><span class="sxs-lookup"><span data-stu-id="92a6f-239">WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="92a6f-240">Como remover um manipulador</span><span class="sxs-lookup"><span data-stu-id="92a6f-240">How to remove a handler</span></span>

<span data-ttu-id="92a6f-241">Para remover um manipulador, chame seu `Dispose` método.</span><span class="sxs-lookup"><span data-stu-id="92a6f-241">To remove a handler, call its `Dispose` method.</span></span>

**<span data-ttu-id="92a6f-242">Código do cliente para um método chamado de servidor</span><span class="sxs-lookup"><span data-stu-id="92a6f-242">Client code for a method called from server</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**<span data-ttu-id="92a6f-243">Para remover o manipulador de código do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-243">Client code to remove the handler</span></span>**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="92a6f-244">Como chamar métodos de servidor do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-244">How to call server methods from the client</span></span>

<span data-ttu-id="92a6f-245">Para chamar um método no servidor, use o `Invoke` método no proxy de Hub.</span><span class="sxs-lookup"><span data-stu-id="92a6f-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="92a6f-246">Se o método de servidor não tem nenhum valor de retorno, use a sobrecarga não genérico do `Invoke` método.</span><span class="sxs-lookup"><span data-stu-id="92a6f-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

**<span data-ttu-id="92a6f-247">Código de servidor para um método que não tem nenhum valor de retorno</span><span class="sxs-lookup"><span data-stu-id="92a6f-247">Server code for a method that has no return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**<span data-ttu-id="92a6f-248">Um método que não tem nenhum valor de retorno de chamada de código do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-248">Client code calling a method that has no return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="92a6f-249">Se o método de servidor tem um valor de retorno, especifique o tipo de retorno como o tipo genérico do `Invoke` método.</span><span class="sxs-lookup"><span data-stu-id="92a6f-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

**<span data-ttu-id="92a6f-250">Código de servidor para um método que tem um valor de retorno e usa um parâmetro de tipo complexo</span><span class="sxs-lookup"><span data-stu-id="92a6f-250">Server code for a method that has a return value and takes a complex type parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**<span data-ttu-id="92a6f-251">A classe de estoque usada para o parâmetro e valor de retorno</span><span class="sxs-lookup"><span data-stu-id="92a6f-251">The Stock class used for the parameter and return value</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**<span data-ttu-id="92a6f-252">Código do cliente chamar um método que tem um valor de retorno e usa um parâmetro de tipo complexo, em um método assíncrono de ASP.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="92a6f-252">Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**<span data-ttu-id="92a6f-253">Código do cliente chamar um método que tem um valor de retorno e usa um parâmetro de tipo complexo, em um método síncrono</span><span class="sxs-lookup"><span data-stu-id="92a6f-253">Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="92a6f-254">O `Invoke` método executa de forma assíncrona e retorna um `Task` objeto.</span><span class="sxs-lookup"><span data-stu-id="92a6f-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="92a6f-255">Se você não especificar `await` ou `.Wait()`, a próxima linha de código será executado antes que você invocar o método de execução foi concluída.</span><span class="sxs-lookup"><span data-stu-id="92a6f-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="92a6f-256">Como manipular eventos de tempo de vida da conexão</span><span class="sxs-lookup"><span data-stu-id="92a6f-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="92a6f-257">SignalR fornece eventos de tempo de vida que você pode manipular de conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="92a6f-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- `Received`<span data-ttu-id="92a6f-258">: Gerado quando nenhum dado for recebido na conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-258">: Raised when any data is received on the connection.</span></span> <span data-ttu-id="92a6f-259">Fornece os dados recebidos.</span><span class="sxs-lookup"><span data-stu-id="92a6f-259">Provides the received data.</span></span>
- `ConnectionSlow`<span data-ttu-id="92a6f-260">: Gerado quando o cliente detecta uma conexão lenta ou remoção com frequência.</span><span class="sxs-lookup"><span data-stu-id="92a6f-260">: Raised when the client detects a slow or frequently dropping connection.</span></span>
- `Reconnecting`<span data-ttu-id="92a6f-261">: Gerado quando o transporte subjacente inicia a reconexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-261">: Raised when the underlying transport begins reconnecting.</span></span>
- `Reconnected`<span data-ttu-id="92a6f-262">: Gerado quando o transporte subjacente foi reconectada.</span><span class="sxs-lookup"><span data-stu-id="92a6f-262">: Raised when the underlying transport has reconnected.</span></span>
- `StateChanged`<span data-ttu-id="92a6f-263">: Gerado quando o estado de conexão é alterado.</span><span class="sxs-lookup"><span data-stu-id="92a6f-263">: Raised when the connection state changes.</span></span> <span data-ttu-id="92a6f-264">Fornece o estado antigo e o novo estado.</span><span class="sxs-lookup"><span data-stu-id="92a6f-264">Provides the old state and the new state.</span></span> <span data-ttu-id="92a6f-265">Para obter informações sobre conexão ver valores de estado [enumeração ConnectionState](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6f-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- `Closed`<span data-ttu-id="92a6f-266">: Gerado quando a conexão foi desconectada.</span><span class="sxs-lookup"><span data-stu-id="92a6f-266">: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="92a6f-267">Por exemplo, se você quiser exibir mensagens de aviso para erros que não são fatais, mas causam problemas intermitentes de conexão, como lentidão ou frequentes descartando de conexão, manipular o `ConnectionSlow` eventos.</span><span class="sxs-lookup"><span data-stu-id="92a6f-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="92a6f-268">Para obter mais informações, consulte [Noções básicas e tratamento de eventos de tempo de vida de Conexão no SignalR](handling-connection-lifetime-events.md).</span><span class="sxs-lookup"><span data-stu-id="92a6f-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="92a6f-269">Como tratar erros</span><span class="sxs-lookup"><span data-stu-id="92a6f-269">How to handle errors</span></span>

<span data-ttu-id="92a6f-270">Se você não explicitamente habilitar mensagens de erro detalhadas no servidor, o objeto de exceção SignalR retorna após um erro contém algumas informações sobre o erro.</span><span class="sxs-lookup"><span data-stu-id="92a6f-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="92a6f-271">Por exemplo, se uma chamada para `newContosoChatMessage` falhar, a mensagem de erro no objeto de erro contém "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" envio de mensagens de erro detalhadas para clientes em produção não é recomendado por motivos de segurança, mas se você quiser habilitar mensagens de erro detalhadas para solução de problemas, use o seguinte código no servidor.</span><span class="sxs-lookup"><span data-stu-id="92a6f-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="92a6f-272">Para tratar erros que aciona o SignalR, você pode adicionar um manipulador para o `Error` evento no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="92a6f-273">Para tratar erros de invocações de método, encapsule o código em um bloco try-catch.</span><span class="sxs-lookup"><span data-stu-id="92a6f-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="92a6f-274">Como habilitar o registro em log do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="92a6f-274">How to enable client-side logging</span></span>

<span data-ttu-id="92a6f-275">Para habilitar o registro em log do lado do cliente, defina as `TraceLevel` e `TraceWriter` propriedades no objeto de conexão.</span><span class="sxs-lookup"><span data-stu-id="92a6f-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="92a6f-276">Exemplos de código de aplicativo de console para que o servidor pode chamar métodos do cliente, o Silverlight e WPF</span><span class="sxs-lookup"><span data-stu-id="92a6f-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="92a6f-277">Os exemplos de código mostrados anteriormente para definir métodos de cliente que o servidor pode chamar se aplicam aos clientes do WinRT.</span><span class="sxs-lookup"><span data-stu-id="92a6f-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="92a6f-278">Os exemplos a seguir mostram o código equivalente para WPF, Silverlight e clientes de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="92a6f-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="92a6f-279">Métodos sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-279">Methods without parameters</span></span>

**<span data-ttu-id="92a6f-280">Código de cliente do WPF para o método é chamado de servidor sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-280">WPF client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**<span data-ttu-id="92a6f-281">Código de cliente do Silverlight para o método é chamado de servidor sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-281">Silverlight client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**<span data-ttu-id="92a6f-282">Código de cliente do aplicativo de console para o método é chamado de servidor sem parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-282">Console application client code for method called from server without parameters</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="92a6f-283">Métodos com parâmetros, especificando os tipos de parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-283">Methods with parameters, specifying the parameter types</span></span>

**<span data-ttu-id="92a6f-284">Código do cliente do WPF para um método chamado de servidor com um parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-284">WPF client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**<span data-ttu-id="92a6f-285">Código do cliente do Silverlight para um método chamado de servidor com um parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-285">Silverlight client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**<span data-ttu-id="92a6f-286">Código de cliente do aplicativo de console para um método chamado de servidor com um parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-286">Console application client code for a method called from server with a parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="92a6f-287">Métodos com parâmetros, especificando os objetos dinâmicos para os parâmetros</span><span class="sxs-lookup"><span data-stu-id="92a6f-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

**<span data-ttu-id="92a6f-288">Código do cliente do WPF para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-288">WPF client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**<span data-ttu-id="92a6f-289">Código do cliente do Silverlight para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-289">Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**<span data-ttu-id="92a6f-290">Código de cliente do aplicativo de console para um método chamado de servidor com um parâmetro, usando um objeto dinâmico para o parâmetro</span><span class="sxs-lookup"><span data-stu-id="92a6f-290">Console application client code for a method called from server with a parameter, using a dynamic object for the parameter</span></span>**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
