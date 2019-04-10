---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: Formatadores de mídia na API Web ASP.NET 2 - ASP.NET 4.x
author: MikeWasson
description: Mostra como dar suporte a formatos de mídia adicionais na API Web ASP.NET para ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418762"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a><span data-ttu-id="10bc8-103">Formatadores de mídia na API Web ASP.NET 2</span><span class="sxs-lookup"><span data-stu-id="10bc8-103">Media Formatters in ASP.NET Web API 2</span></span>

<span data-ttu-id="10bc8-104">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="10bc8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="10bc8-105">Este tutorial mostra como dar suporte a formatos de mídia adicionais na API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="10bc8-105">This tutorial shows how to support additional media formats in ASP.NET Web API.</span></span>

## <a name="internet-media-types"></a><span data-ttu-id="10bc8-106">Tipos de mídia da Internet</span><span class="sxs-lookup"><span data-stu-id="10bc8-106">Internet Media Types</span></span>

<span data-ttu-id="10bc8-107">Um tipo de mídia, também chamado de um tipo MIME, identifica o formato de uma parte dos dados.</span><span class="sxs-lookup"><span data-stu-id="10bc8-107">A media type, also called a MIME type, identifies the format of a piece of data.</span></span> <span data-ttu-id="10bc8-108">Em HTTP, os tipos de mídia descrevem o formato do corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="10bc8-108">In HTTP, media types describe the format of the message body.</span></span> <span data-ttu-id="10bc8-109">Um tipo de mídia consiste em duas cadeias de caracteres, um tipo e um subtipo.</span><span class="sxs-lookup"><span data-stu-id="10bc8-109">A media type consists of two strings, a type and a subtype.</span></span> <span data-ttu-id="10bc8-110">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="10bc8-110">For example:</span></span>

- <span data-ttu-id="10bc8-111">text/html</span><span class="sxs-lookup"><span data-stu-id="10bc8-111">text/html</span></span>
- <span data-ttu-id="10bc8-112">image/png</span><span class="sxs-lookup"><span data-stu-id="10bc8-112">image/png</span></span>
- <span data-ttu-id="10bc8-113">application/json</span><span class="sxs-lookup"><span data-stu-id="10bc8-113">application/json</span></span>

<span data-ttu-id="10bc8-114">Quando uma mensagem HTTP contém um corpo de entidade, o cabeçalho Content-Type especifica o formato do corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="10bc8-114">When an HTTP message contains an entity-body, the Content-Type header specifies the format of the message body.</span></span> <span data-ttu-id="10bc8-115">Isso informa ao destinatário como analisar o conteúdo do corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="10bc8-115">This tells the receiver how to parse the contents of the message body.</span></span>

<span data-ttu-id="10bc8-116">Por exemplo, se uma resposta HTTP contém uma imagem PNG, a resposta pode ter os seguintes cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="10bc8-116">For example, if an HTTP response contains a PNG image, the response might have the following headers.</span></span>

[!code-console[Main](media-formatters/samples/sample1.cmd)]

<span data-ttu-id="10bc8-117">Quando o cliente envia uma mensagem de solicitação, ele pode incluir um cabeçalho Accept.</span><span class="sxs-lookup"><span data-stu-id="10bc8-117">When the client sends a request message, it can include an Accept header.</span></span> <span data-ttu-id="10bc8-118">O cabeçalho Accept informa que deseja que o servidor no qual mídia tipo (s) o cliente do servidor.</span><span class="sxs-lookup"><span data-stu-id="10bc8-118">The Accept header tells the server which media type(s) the client wants from the server.</span></span> <span data-ttu-id="10bc8-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="10bc8-119">For example:</span></span>

[!code-console[Main](media-formatters/samples/sample2.cmd)]

<span data-ttu-id="10bc8-120">Esse cabeçalho informa ao servidor que o cliente deseja HTML, XHTML e XML.</span><span class="sxs-lookup"><span data-stu-id="10bc8-120">This header tells the server that the client wants either HTML, XHTML, or XML.</span></span>

<span data-ttu-id="10bc8-121">O tipo de mídia determina como a API da Web serializa e desserializa o corpo da mensagem HTTP.</span><span class="sxs-lookup"><span data-stu-id="10bc8-121">The media type determines how Web API serializes and deserializes the HTTP message body.</span></span> <span data-ttu-id="10bc8-122">API da Web tem suporte interno para XML, JSON, BSON e dados de formulário urlencoded, e você pode dar suporte a tipos de mídia adicionais escrevendo uma *formatador de mídia*.</span><span class="sxs-lookup"><span data-stu-id="10bc8-122">Web API has built-in support for XML, JSON, BSON, and form-urlencoded data, and you can support additional media types by writing a *media formatter*.</span></span>

<span data-ttu-id="10bc8-123">Para criar um formatador de mídia, derive de uma dessas classes:</span><span class="sxs-lookup"><span data-stu-id="10bc8-123">To create a media formatter, derive from one of these classes:</span></span>

- <span data-ttu-id="10bc8-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="10bc8-124">[MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx).</span></span> <span data-ttu-id="10bc8-125">Esta leitura assíncrona de usos de classe e métodos de gravação.</span><span class="sxs-lookup"><span data-stu-id="10bc8-125">This class uses asynchronous read and write methods.</span></span>
- <span data-ttu-id="10bc8-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span><span class="sxs-lookup"><span data-stu-id="10bc8-126">[BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx).</span></span> <span data-ttu-id="10bc8-127">Essa classe deriva **MediaTypeFormatter** mas utiliza métodos de leitura/gravação síncrona.</span><span class="sxs-lookup"><span data-stu-id="10bc8-127">This class derives from **MediaTypeFormatter** but uses synchronous read/write methods.</span></span>

<span data-ttu-id="10bc8-128">Derivando de **BufferedMediaTypeFormatter** é mais simples, porque não há nenhum código assíncrono, mas isso também significa que o thread de chamada pode bloquear durante e/s.</span><span class="sxs-lookup"><span data-stu-id="10bc8-128">Deriving from **BufferedMediaTypeFormatter** is simpler, because there is no asynchronous code, but it also means the calling thread can block during I/O.</span></span>

## <a name="example-creating-a-csv-media-formatter"></a><span data-ttu-id="10bc8-129">Exemplo: Criando um formatador de mídia do CSV</span><span class="sxs-lookup"><span data-stu-id="10bc8-129">Example: Creating a CSV Media Formatter</span></span>

<span data-ttu-id="10bc8-130">O exemplo a seguir mostra um formatador de tipo de mídia que pode serializar um objeto de produto para um formato de valores separados por vírgulas (CSV).</span><span class="sxs-lookup"><span data-stu-id="10bc8-130">The following example shows a media type formatter that can serialize a Product object to a comma-separated values (CSV) format.</span></span> <span data-ttu-id="10bc8-131">Este exemplo usa o tipo de produto definido no tutorial [criando uma API da Web que dá suporte a operações de CRUD](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span><span class="sxs-lookup"><span data-stu-id="10bc8-131">This example uses the Product type defined in the tutorial [Creating a Web API that Supports CRUD Operations](../older-versions/creating-a-web-api-that-supports-crud-operations.md).</span></span> <span data-ttu-id="10bc8-132">Aqui está a definição do objeto Product:</span><span class="sxs-lookup"><span data-stu-id="10bc8-132">Here is the definition of the Product object:</span></span>

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

<span data-ttu-id="10bc8-133">Para implementar um formatador CSV, defina uma classe que deriva de **BufferedMediaTypeFormatter**:</span><span class="sxs-lookup"><span data-stu-id="10bc8-133">To implement a CSV formatter, define a class that derives from **BufferedMediaTypeFormatter**:</span></span>

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

<span data-ttu-id="10bc8-134">No construtor, adicione os tipos de mídia que o formatador suporta.</span><span class="sxs-lookup"><span data-stu-id="10bc8-134">In the constructor, add the media types that the formatter supports.</span></span> <span data-ttu-id="10bc8-135">Neste exemplo, o formatador dá suporte a um único tipo de mídia, &quot;texto/csv&quot;:</span><span class="sxs-lookup"><span data-stu-id="10bc8-135">In this example, the formatter supports a single media type, &quot;text/csv&quot;:</span></span>

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

<span data-ttu-id="10bc8-136">Substituir a **CanWriteType** método para indicar quais tipos o formatador pode serializar:</span><span class="sxs-lookup"><span data-stu-id="10bc8-136">Override the **CanWriteType** method to indicate which types the formatter can serialize:</span></span>

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

<span data-ttu-id="10bc8-137">Neste exemplo, o formatador pode serializar única `Product` objetos, bem como coleções de `Product` objetos.</span><span class="sxs-lookup"><span data-stu-id="10bc8-137">In this example, the formatter can serialize single `Product` objects as well as collections of `Product` objects.</span></span>

<span data-ttu-id="10bc8-138">Substituir da mesma forma, o **CanReadType** método para indicar quais tipos o formatador pode desserializar.</span><span class="sxs-lookup"><span data-stu-id="10bc8-138">Similarly, override the **CanReadType** method to indicate which types the formatter can deserialize.</span></span> <span data-ttu-id="10bc8-139">Neste exemplo, o formatador não oferece suporte a desserialização, então o método simplesmente retorna **falsos**.</span><span class="sxs-lookup"><span data-stu-id="10bc8-139">In this example, the formatter does not support deserialization, so the method simply returns **false**.</span></span>

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

<span data-ttu-id="10bc8-140">Por fim, substitua os **WriteToStream** método.</span><span class="sxs-lookup"><span data-stu-id="10bc8-140">Finally, override the **WriteToStream** method.</span></span> <span data-ttu-id="10bc8-141">Esse método serializa um tipo por meio da gravação em um fluxo.</span><span class="sxs-lookup"><span data-stu-id="10bc8-141">This method serializes a type by writing it to a stream.</span></span> <span data-ttu-id="10bc8-142">Se o formatador dá suporte à desserialização, também substituir as **ReadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="10bc8-142">If your formatter supports deserialization, also override the **ReadFromStream** method.</span></span>

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a><span data-ttu-id="10bc8-143">Adicionando um formatador de mídia ao Pipeline da API da Web</span><span class="sxs-lookup"><span data-stu-id="10bc8-143">Adding a Media Formatter to the Web API Pipeline</span></span>

<span data-ttu-id="10bc8-144">Para adicionar um tipo de mídia formatador para o pipeline da API da Web, use o **formatadores** propriedade sobre o **HttpConfiguration** objeto.</span><span class="sxs-lookup"><span data-stu-id="10bc8-144">To add a media type formatter to the Web API pipeline, use the **Formatters** property on the **HttpConfiguration** object.</span></span>

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a><span data-ttu-id="10bc8-145">Codificações de caracteres</span><span class="sxs-lookup"><span data-stu-id="10bc8-145">Character Encodings</span></span>

<span data-ttu-id="10bc8-146">Opcionalmente, um formatador de mídia pode dar suporte a várias codificações de caracteres, como UTF-8 ou ISO 8859-1.</span><span class="sxs-lookup"><span data-stu-id="10bc8-146">Optionally, a media formatter can support multiple character encodings, such as UTF-8 or ISO 8859-1.</span></span>

<span data-ttu-id="10bc8-147">No construtor, adicione um ou mais [Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) tipos para o **SupportedEncodings** coleção.</span><span class="sxs-lookup"><span data-stu-id="10bc8-147">In the constructor, add one or more [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) types to the **SupportedEncodings** collection.</span></span> <span data-ttu-id="10bc8-148">Coloque a primeira de codificação padrão.</span><span class="sxs-lookup"><span data-stu-id="10bc8-148">Put the default encoding first.</span></span>

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

<span data-ttu-id="10bc8-149">No **WriteToStream** e **ReadFromStream** métodos, chame [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) para selecionar a codificação de caractere preferencial.</span><span class="sxs-lookup"><span data-stu-id="10bc8-149">In the **WriteToStream** and **ReadFromStream** methods, call [MediaTypeFormatter.SelectCharacterEncoding](https://msdn.microsoft.com/library/hh969054.aspx) to select the preferred character encoding.</span></span> <span data-ttu-id="10bc8-150">Esse método corresponde os cabeçalhos de solicitação em relação à lista de codificações com suporte.</span><span class="sxs-lookup"><span data-stu-id="10bc8-150">This method matches the request headers against the list of supported encodings.</span></span> <span data-ttu-id="10bc8-151">Usar retornado **Encoding** quando você ler ou gravar no fluxo:</span><span class="sxs-lookup"><span data-stu-id="10bc8-151">Use the returned **Encoding** when you read or write from the stream:</span></span>

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
