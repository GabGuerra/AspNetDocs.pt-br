---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: Rastreamento na API Web ASP.NET 2 | Microsoft Docs
author: MikeWasson
description: Mostra como habilitar o rastreamento na API Web ASP.NET.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59405892"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="18fee-103">Rastreamento na API Web ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="18fee-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="18fee-104">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="18fee-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="18fee-105">Quando você está tentando depurar um aplicativo baseado na web, não há nenhum substituto para um bom conjunto de logs de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="18fee-106">Este tutorial mostra como habilitar o rastreamento na API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18fee-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="18fee-107">Você pode usar esse recurso para rastrear o que faz a estrutura da API da Web antes e depois que ela invoca seu controlador.</span><span class="sxs-lookup"><span data-stu-id="18fee-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="18fee-108">Você também pode usá-lo para rastrear o seu próprio código.</span><span class="sxs-lookup"><span data-stu-id="18fee-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="18fee-109">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="18fee-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="18fee-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (também funciona com o Visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="18fee-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="18fee-111">API Web 2</span><span class="sxs-lookup"><span data-stu-id="18fee-111">Web API 2</span></span>
> - [<span data-ttu-id="18fee-112">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="18fee-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="18fee-113">Habilitar o rastreamento na API Web de System. Diagnostics</span><span class="sxs-lookup"><span data-stu-id="18fee-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="18fee-114">Primeiro, vamos criar um novo projeto de aplicativo Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18fee-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="18fee-115">No Visual Studio, do **arquivo** menu, selecione **New** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="18fee-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="18fee-116">Sob **modelos**, **Web**, selecione **aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="18fee-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="18fee-117">Escolha o modelo de projeto de API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="18fee-118">Do **ferramentas** menu, selecione **Gerenciador de pacotes NuGet**, em seguida, **Console de gerenciamento de pacote**.</span><span class="sxs-lookup"><span data-stu-id="18fee-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="18fee-119">Na janela do Console do Gerenciador de pacotes, digite os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="18fee-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="18fee-120">O primeiro comando instala o pacote mais recente de rastreamento de API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="18fee-121">Ele também atualiza os pacotes de API da Web principal.</span><span class="sxs-lookup"><span data-stu-id="18fee-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="18fee-122">O segundo comando atualiza o pacote de WebApi.WebHost para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="18fee-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="18fee-123">Se você quiser direcionar uma versão específica de API da Web, use o - sinalizador de versão quando você instala o pacote de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="18fee-124">Abra o arquivo WebApiConfig.cs no aplicativo\_pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="18fee-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="18fee-125">Adicione o seguinte código para o **registrar** método.</span><span class="sxs-lookup"><span data-stu-id="18fee-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="18fee-126">Esse código adiciona o [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) classe para o pipeline da API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="18fee-127">O **SystemDiagnosticsTraceWriter** classe grava rastreamentos [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span><span class="sxs-lookup"><span data-stu-id="18fee-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="18fee-128">Para ver os rastreamentos, execute o aplicativo no depurador.</span><span class="sxs-lookup"><span data-stu-id="18fee-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="18fee-129">No navegador, navegue até `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="18fee-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="18fee-130">As instruções de rastreamento são gravadas na janela de saída no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18fee-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="18fee-131">(Da **modo de exibição** menu, selecione **saída**).</span><span class="sxs-lookup"><span data-stu-id="18fee-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="18fee-132">Porque **SystemDiagnosticsTraceWriter** grava rastreamentos **Trace**, você pode registrar ouvintes de rastreamento adicionais; por exemplo, para gravar rastreamentos em um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="18fee-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="18fee-133">Para obter mais informações sobre os gravadores de rastreamento, consulte o [ouvintes de rastreamento](https://msdn.microsoft.com/library/4y5y10s7.aspx) tópico no MSDN.</span><span class="sxs-lookup"><span data-stu-id="18fee-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="18fee-134">Configurando o SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="18fee-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="18fee-135">O código a seguir mostra como configurar o gravador de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="18fee-136">Há duas configurações que você pode controlar:</span><span class="sxs-lookup"><span data-stu-id="18fee-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="18fee-137">IsVerbose: Se for falso, cada rastreamento contém informações mínimas.</span><span class="sxs-lookup"><span data-stu-id="18fee-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="18fee-138">Se for true, os rastreamentos incluem mais informações.</span><span class="sxs-lookup"><span data-stu-id="18fee-138">If true, traces include more information.</span></span>
- <span data-ttu-id="18fee-139">MinimumLevel: Define o nível mínimo de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="18fee-140">Níveis de rastreamento, em ordem, são Debug, Info, Warn, erro e Fatal.</span><span class="sxs-lookup"><span data-stu-id="18fee-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="18fee-141">Adicionar rastreamentos ao seu aplicativo de API da Web</span><span class="sxs-lookup"><span data-stu-id="18fee-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="18fee-142">Adicionar um gravador de rastreamento fornece acesso imediato aos rastreamentos criados pelo pipeline da API Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="18fee-143">Você também pode usar o gravador de rastreamento para seu próprio código de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="18fee-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="18fee-144">Para obter o gravador de rastreamento, chame **HttpConfiguration.Services.GetTraceWriter**.</span><span class="sxs-lookup"><span data-stu-id="18fee-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="18fee-145">De um controlador, esse método é acessível por meio de **ApiController.Configuration** propriedade.</span><span class="sxs-lookup"><span data-stu-id="18fee-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="18fee-146">Para gravar um rastreamento, você pode chamar o **ITraceWriter.Trace** método diretamente, mas o [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) classe define alguns métodos de extensão que são mais amigáveis.</span><span class="sxs-lookup"><span data-stu-id="18fee-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="18fee-147">Por exemplo, o **Info** método mostrado acima cria um rastreamento com nível de rastreamento **informações**.</span><span class="sxs-lookup"><span data-stu-id="18fee-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="18fee-148">Infraestrutura de rastreamento de API da Web</span><span class="sxs-lookup"><span data-stu-id="18fee-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="18fee-149">Esta seção descreve como escrever um gravador de rastreamento personalizado para a API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="18fee-150">O pacote Microsoft.AspNet.WebApi.Tracing baseia-se em uma infraestrutura de rastreamento mais geral na API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="18fee-151">Em vez de usar Microsoft.AspNet.WebApi.Tracing, você também pode usar alguma outra biblioteca de rastreamento/registro em log, tal como [NLog](http://nlog-project.org/) ou [log4net](http://logging.apache.org/log4net/).</span><span class="sxs-lookup"><span data-stu-id="18fee-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="18fee-152">Para coletar rastreamentos, implementar o **ITraceWriter** interface.</span><span class="sxs-lookup"><span data-stu-id="18fee-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="18fee-153">Aqui está um exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="18fee-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="18fee-154">O **ITraceWriter.Trace** método cria um rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="18fee-155">O chamador Especifica um nível de categoria e de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="18fee-156">A categoria pode ser qualquer cadeia de caracteres definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="18fee-156">The category can be any user-defined string.</span></span> <span data-ttu-id="18fee-157">Sua implementação de **rastreamento** deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="18fee-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="18fee-158">Criar um novo **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="18fee-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="18fee-159">Inicializá-lo com a solicitação, a categoria e o nível de rastreamento, conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="18fee-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="18fee-160">Esses valores são fornecidos pelo chamador.</span><span class="sxs-lookup"><span data-stu-id="18fee-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="18fee-161">Invocar o *traceAction* delegar.</span><span class="sxs-lookup"><span data-stu-id="18fee-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="18fee-162">Dentro desse delegado, o chamador deve preencher o restante dos **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="18fee-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="18fee-163">Gravar o **TraceRecord**, usando qualquer técnica de registro em log que você deseja.</span><span class="sxs-lookup"><span data-stu-id="18fee-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="18fee-164">O exemplo mostrado aqui chama simplesmente **Trace**.</span><span class="sxs-lookup"><span data-stu-id="18fee-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="18fee-165">Definindo o gravador de rastreamento</span><span class="sxs-lookup"><span data-stu-id="18fee-165">Setting the Trace Writer</span></span>

<span data-ttu-id="18fee-166">Para habilitar o rastreamento, você deve configurar a API da Web para usar sua **ITraceWriter** implementação.</span><span class="sxs-lookup"><span data-stu-id="18fee-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="18fee-167">Você fazer isso por meio de **HttpConfiguration** do objeto, conforme mostrado no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="18fee-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="18fee-168">Gravador de rastreamento apenas uma pode estar ativo.</span><span class="sxs-lookup"><span data-stu-id="18fee-168">Only one trace writer can be active.</span></span> <span data-ttu-id="18fee-169">Por padrão, a API Web define um &quot;inoperante&quot; rastreamento que não faz nada.</span><span class="sxs-lookup"><span data-stu-id="18fee-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="18fee-170">(O &quot;inoperante&quot; rastreamento existe para que o código de rastreamento não precisa verificar se o gravador de rastreamento é **nulo** antes de gravar um rastreamento.)</span><span class="sxs-lookup"><span data-stu-id="18fee-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="18fee-171">Como funciona o rastreamento de API de Web</span><span class="sxs-lookup"><span data-stu-id="18fee-171">How Web API Tracing Works</span></span>

<span data-ttu-id="18fee-172">Rastreamento na API Web usa um *fachada* padrão: Quando o rastreamento está habilitado, API da Web envolve várias partes do pipeline de solicitação com classes que executam chamadas de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="18fee-173">Por exemplo, ao selecionar um controlador, o pipeline usa o **IHttpControllerSelector** interface.</span><span class="sxs-lookup"><span data-stu-id="18fee-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="18fee-174">Com o rastreamento habilitado, o pipeline insere uma classe que implementa **IHttpControllerSelector** mas chamadas por meio de para a implementação real:</span><span class="sxs-lookup"><span data-stu-id="18fee-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Rastreamento de API da Web usa o padrão de fachada.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="18fee-176">Os benefícios desse design incluem:</span><span class="sxs-lookup"><span data-stu-id="18fee-176">The benefits of this design include:</span></span>

- <span data-ttu-id="18fee-177">Se você não adicionar um gravador de rastreamento, os componentes de rastreamento não serão instanciados e não tem nenhum impacto no desempenho.</span><span class="sxs-lookup"><span data-stu-id="18fee-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="18fee-178">Se você substituir os serviços padrão como **IHttpControllerSelector** com sua própria implementação personalizada, os rastreamento não é afetado, pois o rastreamento é feito pelo objeto de wrapper.</span><span class="sxs-lookup"><span data-stu-id="18fee-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="18fee-179">Você também pode substituir a estrutura de rastreamento de API da Web inteira com sua própria estrutura personalizada, substituindo o padrão **ITraceManager** serviço:</span><span class="sxs-lookup"><span data-stu-id="18fee-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="18fee-180">Implemente **ITraceManager.Initialize** para inicializar o sistema de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="18fee-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="18fee-181">Lembre-se de que ele substitui o *inteira* framework de rastreamento, incluindo todo o código de rastreamento que está embutido no API da Web.</span><span class="sxs-lookup"><span data-stu-id="18fee-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
