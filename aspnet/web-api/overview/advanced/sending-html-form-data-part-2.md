---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'Enviando dados de formulário HTML na API Web ASP.NET: Upload de arquivo e com diversas partes MIME | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/21/2012
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 875f9ac62901dfbafc8224af2982c1daf3afc9c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028973"
---
<a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="cd917-102">Enviando dados de formulário HTML na API Web ASP.NET: Carregamento do arquivo e MIME com diversas partes</span><span class="sxs-lookup"><span data-stu-id="cd917-102">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>
====================
<span data-ttu-id="cd917-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cd917-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="cd917-104">Parte 2: Carregamento do arquivo e MIME com diversas partes</span><span class="sxs-lookup"><span data-stu-id="cd917-104">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="cd917-105">Este tutorial mostra como carregar arquivos para uma API da web.</span><span class="sxs-lookup"><span data-stu-id="cd917-105">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="cd917-106">Ele também descreve como processar dados com várias partes de MIME.</span><span class="sxs-lookup"><span data-stu-id="cd917-106">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="cd917-107">[Baixe o projeto concluído](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="cd917-107">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="cd917-108">Aqui está um exemplo de um formulário HTML para carregar um arquivo:</span><span class="sxs-lookup"><span data-stu-id="cd917-108">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="cd917-109">Este formulário contém um controle de entrada de texto e um controle de entrada do arquivo.</span><span class="sxs-lookup"><span data-stu-id="cd917-109">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="cd917-110">Quando um formulário contém um controle de entrada de arquivo, o **enctype** atributo deve ser sempre &quot;multipart/form-data&quot;, que especifica que o formulário será enviado como uma mensagem MIME de várias partes.</span><span class="sxs-lookup"><span data-stu-id="cd917-110">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="cd917-111">O formato de uma mensagem MIME de várias partes é mais fácil de entender examinando um exemplo de solicitação:</span><span class="sxs-lookup"><span data-stu-id="cd917-111">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="cd917-112">Esta mensagem é dividida em duas *partes*, uma para cada controle de formulário.</span><span class="sxs-lookup"><span data-stu-id="cd917-112">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="cd917-113">Limites de parte são indicados por linhas que começam com traços.</span><span class="sxs-lookup"><span data-stu-id="cd917-113">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="cd917-114">O limite de parte inclui um componente aleatório (&quot;41184676334&quot;) para garantir que a cadeia de caracteres de limite não acidentalmente aparece dentro de uma parte da mensagem.</span><span class="sxs-lookup"><span data-stu-id="cd917-114">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="cd917-115">Cada parte da mensagem contém um ou mais cabeçalhos, seguidos pelo conteúdo de parte.</span><span class="sxs-lookup"><span data-stu-id="cd917-115">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="cd917-116">O cabeçalho Content-Disposition inclui o nome do controle.</span><span class="sxs-lookup"><span data-stu-id="cd917-116">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="cd917-117">Para arquivos, ele também contém o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="cd917-117">For files, it also contains the file name.</span></span>
- <span data-ttu-id="cd917-118">O cabeçalho Content-Type descreve os dados na parte.</span><span class="sxs-lookup"><span data-stu-id="cd917-118">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="cd917-119">Se esse cabeçalho for omitido, o padrão é texto/simples.</span><span class="sxs-lookup"><span data-stu-id="cd917-119">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="cd917-120">No exemplo anterior, o usuário carregou um arquivo chamado GrandCanyon.jpg, com o tipo de conteúdo de imagem/jpeg; e o valor da entrada de texto era &quot;férias de verão&quot;.</span><span class="sxs-lookup"><span data-stu-id="cd917-120">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="cd917-121">Upload de arquivo</span><span class="sxs-lookup"><span data-stu-id="cd917-121">File Upload</span></span>

<span data-ttu-id="cd917-122">Agora vamos dar uma olhada em um controlador de API da Web que lê arquivos de uma mensagem MIME de várias partes.</span><span class="sxs-lookup"><span data-stu-id="cd917-122">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="cd917-123">O controlador lerá os arquivos de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="cd917-123">The controller will read the files asynchronously.</span></span> <span data-ttu-id="cd917-124">API da Web dá suporte a ações assíncronas usando o [modelo de programação baseado em tarefa](https://msdn.microsoft.com/library/dd460693.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd917-124">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="cd917-125">Primeiro, aqui está o código se você estiver direcionando o .NET Framework 4.5, que oferece suporte a **async** e **await** palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="cd917-125">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="cd917-126">Observe que a ação do controlador não leva nenhum parâmetro.</span><span class="sxs-lookup"><span data-stu-id="cd917-126">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="cd917-127">Isso ocorre porque podemos processar o corpo da solicitação dentro da ação, sem invocar um formatador de tipo de mídia.</span><span class="sxs-lookup"><span data-stu-id="cd917-127">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="cd917-128">O **IsMultipartContent** método verifica se a solicitação contém uma mensagem MIME de várias partes.</span><span class="sxs-lookup"><span data-stu-id="cd917-128">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="cd917-129">Caso contrário, o controlador retorna o código de status HTTP 415 (tipo de mídia sem suporte).</span><span class="sxs-lookup"><span data-stu-id="cd917-129">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="cd917-130">O **MultipartFormDataStreamProvider** classe é um objeto auxiliar que aloca fluxos de arquivos para arquivos carregados.</span><span class="sxs-lookup"><span data-stu-id="cd917-130">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="cd917-131">Para ler a mensagem MIME de várias partes, chame o **ReadAsMultipartAsync** método.</span><span class="sxs-lookup"><span data-stu-id="cd917-131">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="cd917-132">Esse método extrai todas as partes da mensagem e grava-os em fluxos fornecidos pelo **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="cd917-132">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="cd917-133">Quando o método for concluído, você pode obter informações sobre os arquivos a partir de **FileData** propriedade, que é uma coleção de **MultipartFileData** objetos.</span><span class="sxs-lookup"><span data-stu-id="cd917-133">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="cd917-134">**MultipartFileData.FileName** é o nome de arquivo local no servidor, onde o arquivo foi salvo.</span><span class="sxs-lookup"><span data-stu-id="cd917-134">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="cd917-135">**MultipartFileData.Headers** contém o cabeçalho da parte (*não* o cabeçalho de solicitação).</span><span class="sxs-lookup"><span data-stu-id="cd917-135">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="cd917-136">Você pode usar isso para acessar o conteúdo\_cabeçalhos Disposition e Content-Type.</span><span class="sxs-lookup"><span data-stu-id="cd917-136">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="cd917-137">Como o nome sugere, **ReadAsMultipartAsync** é um método assíncrono.</span><span class="sxs-lookup"><span data-stu-id="cd917-137">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="cd917-138">Para executar o trabalho depois que o método for concluído, use uma [tarefa de continuação](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) ou o **await** palavra-chave (.NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="cd917-138">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="cd917-139">Aqui está a versão do .NET Framework 4.0 do código anterior:</span><span class="sxs-lookup"><span data-stu-id="cd917-139">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="cd917-140">Leitura de dados de controle de formulário</span><span class="sxs-lookup"><span data-stu-id="cd917-140">Reading Form Control Data</span></span>

<span data-ttu-id="cd917-141">O formulário HTML que mostrei anteriormente tinha um controle de entrada de texto.</span><span class="sxs-lookup"><span data-stu-id="cd917-141">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="cd917-142">Você pode obter o valor do controle do **FormData** propriedade da **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="cd917-142">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="cd917-143">**FormData** é um **NameValueCollection** que contém pares nome/valor para os controles de formulário.</span><span class="sxs-lookup"><span data-stu-id="cd917-143">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="cd917-144">A coleção pode conter chaves duplicadas.</span><span class="sxs-lookup"><span data-stu-id="cd917-144">The collection can contain duplicate keys.</span></span> <span data-ttu-id="cd917-145">Considere este formulário:</span><span class="sxs-lookup"><span data-stu-id="cd917-145">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="cd917-146">O corpo da solicitação pode ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cd917-146">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="cd917-147">Nesse caso, o **FormData** coleção conteria os seguintes pares chave/valor:</span><span class="sxs-lookup"><span data-stu-id="cd917-147">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="cd917-148">viagem: ida e volta</span><span class="sxs-lookup"><span data-stu-id="cd917-148">trip: round-trip</span></span>
- <span data-ttu-id="cd917-149">options: nonstop</span><span class="sxs-lookup"><span data-stu-id="cd917-149">options: nonstop</span></span>
- <span data-ttu-id="cd917-150">opções: datas</span><span class="sxs-lookup"><span data-stu-id="cd917-150">options: dates</span></span>
- <span data-ttu-id="cd917-151">estação: janela</span><span class="sxs-lookup"><span data-stu-id="cd917-151">seat: window</span></span>
