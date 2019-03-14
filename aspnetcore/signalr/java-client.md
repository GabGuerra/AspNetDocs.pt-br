---
title: Cliente de Java do SignalR Core ASP.NET
author: mikaelm12
description: Saiba como usar o cliente de Java de SignalR do ASP.NET Core.
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 11/07/2018
uid: signalr/java-client
ms.openlocfilehash: d0eff38c1f622b896ed1dc3002238aec7b6bfd38
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030063"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="f0616-103">Cliente de Java do SignalR Core ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0616-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="f0616-104">Por [Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="f0616-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="f0616-105">O cliente de Java permite se conectar a um servidor do SignalR do ASP.NET Core do código Java, incluindo aplicativos Android.</span><span class="sxs-lookup"><span data-stu-id="f0616-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="f0616-106">Como o [cliente JavaScript](xref:signalr/javascript-client) e o [cliente .NET](xref:signalr/dotnet-client), o cliente de Java permite que você receber e enviar mensagens a um hub em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f0616-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="f0616-107">O cliente de Java está disponível no ASP.NET Core 2.2 e posterior.</span><span class="sxs-lookup"><span data-stu-id="f0616-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="f0616-108">O aplicativo de console do Java de exemplo referenciado neste artigo usa o cliente de Java do SignalR.</span><span class="sxs-lookup"><span data-stu-id="f0616-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="f0616-109">[Exibir ou baixar código de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([como baixar](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="f0616-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="f0616-110">Instalar o pacote de cliente Java do SignalR</span><span class="sxs-lookup"><span data-stu-id="f0616-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="f0616-111">O *1.0.0 signalr* arquivo JAR permite que os clientes se conectem aos hubs de SignalR.</span><span class="sxs-lookup"><span data-stu-id="f0616-111">The *signalr-1.0.0* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="f0616-112">Para localizar o número de versão de arquivo JAR mais recente, consulte o [resultados da pesquisa Maven](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span><span class="sxs-lookup"><span data-stu-id="f0616-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="f0616-113">Se usando o Gradle, adicione a seguinte linha para o `dependencies` seção do seu *Build. gradle* arquivo:</span><span class="sxs-lookup"><span data-stu-id="f0616-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0'
```

<span data-ttu-id="f0616-114">Se usando o Maven, adicione as seguintes linhas dentro de `<dependencies>` elemento da sua *POM. XML* arquivo:</span><span class="sxs-lookup"><span data-stu-id="f0616-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="f0616-115">Conectar a um hub</span><span class="sxs-lookup"><span data-stu-id="f0616-115">Connect to a hub</span></span>

<span data-ttu-id="f0616-116">Para estabelecer uma `HubConnection`, o `HubConnectionBuilder` deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="f0616-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="f0616-117">O nível de log e a URL do hub pode ser configurado durante a criação de uma conexão.</span><span class="sxs-lookup"><span data-stu-id="f0616-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="f0616-118">Configurar as opções necessárias chamando o `HubConnectionBuilder` métodos antes `build`.</span><span class="sxs-lookup"><span data-stu-id="f0616-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="f0616-119">Iniciar a conexão com `start`.</span><span class="sxs-lookup"><span data-stu-id="f0616-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="f0616-120">Chamar métodos de hub do cliente</span><span class="sxs-lookup"><span data-stu-id="f0616-120">Call hub methods from client</span></span>

<span data-ttu-id="f0616-121">Uma chamada para `send` invoca um método de hub.</span><span class="sxs-lookup"><span data-stu-id="f0616-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="f0616-122">Passe o nome do método de hub e quaisquer argumentos definidos no método de hub para `send`.</span><span class="sxs-lookup"><span data-stu-id="f0616-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="f0616-123">Chamar métodos de cliente do hub</span><span class="sxs-lookup"><span data-stu-id="f0616-123">Call client methods from hub</span></span>

<span data-ttu-id="f0616-124">Use `hubConnection.on` para definir métodos no cliente que o hub pode chamar.</span><span class="sxs-lookup"><span data-stu-id="f0616-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="f0616-125">Defina os métodos depois de criar, mas antes de iniciar a conexão.</span><span class="sxs-lookup"><span data-stu-id="f0616-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="f0616-126">Adicionar registro em log</span><span class="sxs-lookup"><span data-stu-id="f0616-126">Add logging</span></span>

<span data-ttu-id="f0616-127">O cliente SignalR Java usa a [SLF4J](https://www.slf4j.org/) biblioteca para registro em log.</span><span class="sxs-lookup"><span data-stu-id="f0616-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="f0616-128">É uma API de alto nível de log que permite aos usuários da biblioteca de escolher sua própria implementação de log específico, colocando em uma dependência de log específico.</span><span class="sxs-lookup"><span data-stu-id="f0616-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="f0616-129">O trecho de código a seguir mostra como usar `java.util.logging` com o cliente de Java do SignalR.</span><span class="sxs-lookup"><span data-stu-id="f0616-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="f0616-130">Se você não configurar o registro em log em suas dependências, SLF4J carrega um agente de operação não padrão com a seguinte mensagem de aviso:</span><span class="sxs-lookup"><span data-stu-id="f0616-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="f0616-131">Isso pode ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="f0616-131">This can safely be ignored.</span></span>

## <a name="android-development-notes"></a><span data-ttu-id="f0616-132">Notas de desenvolvimento do Android</span><span class="sxs-lookup"><span data-stu-id="f0616-132">Android development notes</span></span>

<span data-ttu-id="f0616-133">Com relação à compatibilidade do SDK do Android para os recursos de cliente do SignalR, considere os seguintes itens ao especificar sua versão do SDK do Android de destino:</span><span class="sxs-lookup"><span data-stu-id="f0616-133">With regards to Android SDK compatibility for the SignalR client features, consider the following items when specifying your target Android SDK version:</span></span>

* <span data-ttu-id="f0616-134">O cliente de Java do SignalR será executado no nível da API Android 16 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="f0616-134">The SignalR Java Client will run on Android API Level 16 and later.</span></span>
* <span data-ttu-id="f0616-135">Conectar-se por meio do serviço Azure SignalR exigirá o nível da API Android 20 e posterior porque a [serviço do Azure SignalR](/azure/azure-signalr/signalr-overview) requer o TLS 1.2 e não dá suporte a conjuntos de codificação baseado em SHA-1.</span><span class="sxs-lookup"><span data-stu-id="f0616-135">Connecting through the Azure SignalR Service will require Android API Level 20 and later because the [Azure SignalR Service](/azure/azure-signalr/signalr-overview) requires TLS 1.2 and doesn't support SHA-1-based cipher suites.</span></span> <span data-ttu-id="f0616-136">Android [adicionou suporte para SHA-256 (e superior) conjuntos de codificação](https://developer.android.com/reference/javax/net/ssl/SSLSocket) no nível da API 20.</span><span class="sxs-lookup"><span data-stu-id="f0616-136">Android [added support for SHA-256 (and above) cipher suites](https://developer.android.com/reference/javax/net/ssl/SSLSocket) in API Level 20.</span></span>

## <a name="configure-bearer-token-authentication"></a><span data-ttu-id="f0616-137">Configurar a autenticação de token de portador</span><span class="sxs-lookup"><span data-stu-id="f0616-137">Configure bearer token authentication</span></span>

<span data-ttu-id="f0616-138">No cliente de Java do SignalR, você pode configurar um token de portador para usar para autenticação, fornecendo uma "access token fábrica" para o [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span><span class="sxs-lookup"><span data-stu-id="f0616-138">In the SignalR Java client, you can configure a bearer token to use for authentication by providing an "access token factory" to the [HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java).</span></span> <span data-ttu-id="f0616-139">Use [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) para fornecer uma [RxJava](https://github.com/ReactiveX/RxJava) [único<String>](http://reactivex.io/documentation/single.html).</span><span class="sxs-lookup"><span data-stu-id="f0616-139">Use [withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__) to provide an [RxJava](https://github.com/ReactiveX/RxJava) [Single<String>](http://reactivex.io/documentation/single.html).</span></span> <span data-ttu-id="f0616-140">Com uma chamada para [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), você pode escrever a lógica para gerar tokens de acesso do cliente.</span><span class="sxs-lookup"><span data-stu-id="f0616-140">With a call to [Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-), you can write logic to produce access tokens for your client.</span></span>

```java
HubConnection hubConnection = HubConnectionBuilder.create("YOUR HUB URL HERE")
    .withAccessTokenProvider(Single.defer(() -> {
        // Your logic here.
        return Single.just("An Access Token");
    })).build();
```

## <a name="known-limitations"></a><span data-ttu-id="f0616-141">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="f0616-141">Known limitations</span></span>

* <span data-ttu-id="f0616-142">Há suporte para apenas o protocolo JSON.</span><span class="sxs-lookup"><span data-stu-id="f0616-142">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="f0616-143">Há suporte para apenas o transporte de WebSockets.</span><span class="sxs-lookup"><span data-stu-id="f0616-143">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="f0616-144">Streaming ainda não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="f0616-144">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0616-145">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f0616-145">Additional resources</span></span>

* [<span data-ttu-id="f0616-146">Referência de API Java</span><span class="sxs-lookup"><span data-stu-id="f0616-146">Java API reference</span></span>](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
