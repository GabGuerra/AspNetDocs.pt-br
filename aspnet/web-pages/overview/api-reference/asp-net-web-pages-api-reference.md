---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: Referência rápida da API de (Razor) de páginas da Web ASP.NET | Microsoft Docs
author: Rick-Anderson
description: Esta página contém uma lista com breves exemplos de como os objetos mais usados, propriedades e métodos para a programação de páginas da Web ASP.NET com sintaxe do Razor.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: 656987f8a725f81dbca7a72594d7d03bc542fabe
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063853"
---
<a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="f6e18-103">Referência rápida da API de (Razor) de páginas da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f6e18-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>
====================
<span data-ttu-id="f6e18-104">por [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f6e18-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f6e18-105">Esta página contém uma lista com breves exemplos de como os objetos mais usados, propriedades e métodos para a programação de páginas da Web ASP.NET com sintaxe do Razor.</span><span class="sxs-lookup"><span data-stu-id="f6e18-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="f6e18-106">Descrições marcadas com "(v2)" foram introduzidas em páginas da Web do ASP.NET versão 2.</span><span class="sxs-lookup"><span data-stu-id="f6e18-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="f6e18-107">Para obter a documentação de referência de API, consulte o [documentação de referência de páginas da Web do ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6e18-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="f6e18-108">Versões de software</span><span class="sxs-lookup"><span data-stu-id="f6e18-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="f6e18-109">Páginas da Web do ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="f6e18-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="f6e18-110">Este tutorial também funciona com ASP.NET Web Pages 2 e páginas da Web de ASP.NET 1.0 (exceto para os recursos marcados v2).</span><span class="sxs-lookup"><span data-stu-id="f6e18-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>


<span data-ttu-id="f6e18-111">Esta página contém informações de referência para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f6e18-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="f6e18-112">Classes</span><span class="sxs-lookup"><span data-stu-id="f6e18-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="f6e18-113">Dados</span><span class="sxs-lookup"><span data-stu-id="f6e18-113">Data</span></span>](#Data)
- [<span data-ttu-id="f6e18-114">Auxiliares</span><span class="sxs-lookup"><span data-stu-id="f6e18-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="f6e18-115">Validação</span><span class="sxs-lookup"><span data-stu-id="f6e18-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="f6e18-116">Classes</span><span class="sxs-lookup"><span data-stu-id="f6e18-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="f6e18-117">Contém dados que podem ser compartilhados por todas as páginas no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6e18-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="f6e18-118">Você pode usar dinâmica `App` propriedade para acessar os mesmos dados, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e18-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="f6e18-119">Converte um valor de cadeia de caracteres em um valor booliano (true/false).</span><span class="sxs-lookup"><span data-stu-id="f6e18-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="f6e18-120">Retorna falso ou o valor especificado se a cadeia de caracteres não representar Verdadeiro/Falso.</span><span class="sxs-lookup"><span data-stu-id="f6e18-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="f6e18-121">Converte um valor de cadeia de caracteres em data/hora.</span><span class="sxs-lookup"><span data-stu-id="f6e18-121">Converts a string value to date/time.</span></span> <span data-ttu-id="f6e18-122">Retorna `DateTime.MinValue` ou o valor especificado se a cadeia de caracteres não representar uma data/hora.</span><span class="sxs-lookup"><span data-stu-id="f6e18-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="f6e18-123">Converte um valor de cadeia de caracteres em um valor decimal.</span><span class="sxs-lookup"><span data-stu-id="f6e18-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="f6e18-124">Retorna 0,0 ou o valor especificado se a cadeia de caracteres não representar um valor decimal.</span><span class="sxs-lookup"><span data-stu-id="f6e18-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="f6e18-125">Converte um valor de cadeia de caracteres em um float.</span><span class="sxs-lookup"><span data-stu-id="f6e18-125">Converts a string value to a float.</span></span> <span data-ttu-id="f6e18-126">Retorna 0,0 ou o valor especificado se a cadeia de caracteres não representar um valor decimal.</span><span class="sxs-lookup"><span data-stu-id="f6e18-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="f6e18-127">Converte um valor de cadeia de caracteres em um inteiro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-127">Converts a string value to an integer.</span></span> <span data-ttu-id="f6e18-128">Retorna 0 ou o valor especificado se a cadeia de caracteres não representar um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="f6e18-129">Cria uma URL compatível com o navegador de um caminho de arquivo local, com partes opcionais adicionais de caminho.</span><span class="sxs-lookup"><span data-stu-id="f6e18-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="f6e18-130">Renderiza *valor* como marcação HTML em vez de renderizá-lo como codificada em HTML de saída.</span><span class="sxs-lookup"><span data-stu-id="f6e18-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="f6e18-131">Retorna VERDADEIRO se o valor pode ser convertido de uma cadeia de caracteres no tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="f6e18-132">Retornará true se o objeto ou uma variável não tem nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="f6e18-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="f6e18-133">Retorna VERDADEIRO se a solicitação for uma POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="f6e18-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="f6e18-134">(Solicitações iniciais geralmente são um GET).</span><span class="sxs-lookup"><span data-stu-id="f6e18-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="f6e18-135">Especifica o caminho de uma página de layout para aplicar a esta página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="f6e18-136">Contém dados compartilhados entre a página, páginas de layout e páginas parciais na solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="f6e18-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="f6e18-137">Você pode usar dinâmica `Page` propriedade para acessar os mesmos dados, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6e18-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="f6e18-138">(Páginas de layout) Renderiza o conteúdo de uma página de conteúdo que não esteja em qualquer seção nomeada.</span><span class="sxs-lookup"><span data-stu-id="f6e18-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="f6e18-139">Renderiza uma página de conteúdo usando o caminho especificado e os dados extras opcionais.</span><span class="sxs-lookup"><span data-stu-id="f6e18-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="f6e18-140">Você pode obter os valores dos parâmetros extras de `PageData` por posição (exemplo 1) ou chave (exemplo 2).</span><span class="sxs-lookup"><span data-stu-id="f6e18-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="f6e18-141">(Páginas de layout) Renderiza uma seção de conteúdo que tem um nome.</span><span class="sxs-lookup"><span data-stu-id="f6e18-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="f6e18-142">Definir *necessária* como false para tornar uma seção opcional.</span><span class="sxs-lookup"><span data-stu-id="f6e18-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="f6e18-143">Obtém ou define o valor de um cookie HTTP.</span><span class="sxs-lookup"><span data-stu-id="f6e18-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="f6e18-144">Obtém os arquivos que foram carregados na solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="f6e18-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="f6e18-145">Obtém os dados que foi lançados em um formulário (como cadeias de caracteres).</span><span class="sxs-lookup"><span data-stu-id="f6e18-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="f6e18-146">`Request[key]` verifica tanto a `Request.Form` e o `Request.QueryString` coleções.</span><span class="sxs-lookup"><span data-stu-id="f6e18-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="f6e18-147">Obtém os dados que foi especificados na cadeia de caracteres de consulta da URL.</span><span class="sxs-lookup"><span data-stu-id="f6e18-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="f6e18-148">`Request[key]` verifica tanto a `Request.Form` e o `Request.QueryString` coleções.</span><span class="sxs-lookup"><span data-stu-id="f6e18-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="f6e18-149">Seletivamente desabilita a validação para um elemento de formulário, o valor de cadeia de caracteres de consulta, cookie ou valor de cabeçalho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="f6e18-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="f6e18-150">Validação de solicitação está habilitada por padrão e impede que os usuários de lançamento marcação ou outros tipos de conteúdo potencialmente perigoso.</span><span class="sxs-lookup"><span data-stu-id="f6e18-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="f6e18-151">Adiciona um cabeçalho de servidor HTTP à resposta.</span><span class="sxs-lookup"><span data-stu-id="f6e18-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="f6e18-152">Armazena a saída de página por um período especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="f6e18-153">Se desejar, defina *deslizante* para redefinir o tempo limite em cada página de acesso e *varyByParams* para armazenar em cache versões diferentes da página para cada cadeia de caracteres de consulta diferentes na solicitação de página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="f6e18-154">Redireciona a solicitação do navegador para um novo local.</span><span class="sxs-lookup"><span data-stu-id="f6e18-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="f6e18-155">Define o código de status HTTP enviado para o navegador.</span><span class="sxs-lookup"><span data-stu-id="f6e18-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="f6e18-156">Grava o conteúdo do *dados* à resposta com um tipo MIME opcional.</span><span class="sxs-lookup"><span data-stu-id="f6e18-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="f6e18-157">Grava o conteúdo de um arquivo de resposta.</span><span class="sxs-lookup"><span data-stu-id="f6e18-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="f6e18-158">(Páginas de layout) Define uma seção de conteúdo que tem um nome.</span><span class="sxs-lookup"><span data-stu-id="f6e18-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="f6e18-159">Decodifica uma cadeia de caracteres codificada em HTML.</span><span class="sxs-lookup"><span data-stu-id="f6e18-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="f6e18-160">Codifica uma cadeia de caracteres para renderização na marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="f6e18-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="f6e18-161">Retorna o caminho físico do servidor para o caminho virtual especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="f6e18-162">Decodifica o texto de uma URL.</span><span class="sxs-lookup"><span data-stu-id="f6e18-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="f6e18-163">Codifica o texto a ser colocado em uma URL.</span><span class="sxs-lookup"><span data-stu-id="f6e18-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="f6e18-164">Obtém ou define um valor que existe até que o usuário fechar o navegador.</span><span class="sxs-lookup"><span data-stu-id="f6e18-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="f6e18-165">Exibe uma representação de cadeia de caracteres do valor do objeto.</span><span class="sxs-lookup"><span data-stu-id="f6e18-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="f6e18-166">Obtém dados adicionais da URL (por exemplo, *MyPage/ExtraData*).</span><span class="sxs-lookup"><span data-stu-id="f6e18-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="f6e18-167">Altera a senha para o usuário especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="f6e18-168">Confirma uma conta usando o token de confirmação de conta.</span><span class="sxs-lookup"><span data-stu-id="f6e18-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="f6e18-169">Cria uma nova conta de usuário com o nome de usuário especificado e a senha.</span><span class="sxs-lookup"><span data-stu-id="f6e18-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="f6e18-170">Para exigir um token de confirmação, passe true para *requireConfirmationToken.*</span><span class="sxs-lookup"><span data-stu-id="f6e18-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="f6e18-171">Obtém o identificador de inteiro para o usuário conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="f6e18-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="f6e18-172">Obtém o nome do usuário conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="f6e18-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="f6e18-173">Gera um token de redefinição de senha que pode ser enviado por email a um usuário para que o usuário pode redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="f6e18-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="f6e18-174">Retorna a ID de usuário do nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="f6e18-175">Retornará true se o usuário atual está conectado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="f6e18-176">Retornará true se o usuário foi confirmado (por exemplo, por meio de um email de confirmação).</span><span class="sxs-lookup"><span data-stu-id="f6e18-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="f6e18-177">Retorna VERDADEIRO se o nome do usuário atual corresponde ao nome de usuário especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="f6e18-178">Conecta o usuário no definindo um token de autenticação no cookie.</span><span class="sxs-lookup"><span data-stu-id="f6e18-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="f6e18-179">Conecta o usuário de fora, removendo o cookie de autenticação de token.</span><span class="sxs-lookup"><span data-stu-id="f6e18-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="f6e18-180">Se o usuário não for autenticado, define o status HTTP como 401 (não autorizado).</span><span class="sxs-lookup"><span data-stu-id="f6e18-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="f6e18-181">Se o usuário atual não for um membro de uma das funções especificadas, define o status HTTP como 401 (não autorizado).</span><span class="sxs-lookup"><span data-stu-id="f6e18-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="f6e18-182">Se o usuário atual não é o usuário especificado por *nome de usuário*, define o status HTTP como 401 (não autorizado).</span><span class="sxs-lookup"><span data-stu-id="f6e18-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="f6e18-183">Se o token de redefinição de senha for válido, altera a senha do usuário para a nova senha.</span><span class="sxs-lookup"><span data-stu-id="f6e18-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="f6e18-184">Dados</span><span class="sxs-lookup"><span data-stu-id="f6e18-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="f6e18-185">Executa *SQLstatement* (com parâmetros opcionais), como INSERT, DELETE ou UPDATE e retorna uma contagem de registros afetados.</span><span class="sxs-lookup"><span data-stu-id="f6e18-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="f6e18-186">Retorna a coluna de identidade da linha inserida mais recentemente.</span><span class="sxs-lookup"><span data-stu-id="f6e18-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="f6e18-187">Abre o arquivo de banco de dados especificado ou o banco de dados especificado usando uma cadeia de caracteres de conexão nomeada a *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f6e18-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="f6e18-188">Abre um banco de dados usando a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="f6e18-188">Opens a database using the connection string.</span></span> <span data-ttu-id="f6e18-189">(Isso contrasta com `Database.Open`, que usa um nome de cadeia de caracteres de conexão.)</span><span class="sxs-lookup"><span data-stu-id="f6e18-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="f6e18-190">Consulta o banco de dados usando *SQLstatement* (opcionalmente passando parâmetros) e retorna os resultados como uma coleção.</span><span class="sxs-lookup"><span data-stu-id="f6e18-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="f6e18-191">Executa *SQLstatement* (com parâmetros opcionais) e retorna um único registro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="f6e18-192">Executa *SQLstatement* (com parâmetros opcionais) e retorna um valor único.</span><span class="sxs-lookup"><span data-stu-id="f6e18-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="f6e18-193">Auxiliares</span><span class="sxs-lookup"><span data-stu-id="f6e18-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="f6e18-194">Processa o código JavaScript do Google Analytics para a ID especificada.</span><span class="sxs-lookup"><span data-stu-id="f6e18-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="f6e18-195">Processa o código de JavaScript do Analytics StatCounter para o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="f6e18-196">Processa o código de JavaScript do Yahoo Analytics para a conta especificada.</span><span class="sxs-lookup"><span data-stu-id="f6e18-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="f6e18-197">Passa uma pesquisa ao Bing.</span><span class="sxs-lookup"><span data-stu-id="f6e18-197">Passes a search to Bing.</span></span> <span data-ttu-id="f6e18-198">Para especificar o site para pesquisa e um título para a caixa de pesquisa, você pode definir as `Bing.SiteUrl` e `Bing.SiteTitle` propriedades.</span><span class="sxs-lookup"><span data-stu-id="f6e18-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="f6e18-199">Normalmente você define essas propriedades na  *\_AppStart* página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="f6e18-200">Inicializa um gráfico.</span><span class="sxs-lookup"><span data-stu-id="f6e18-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="f6e18-201">Adiciona uma legenda para um gráfico.</span><span class="sxs-lookup"><span data-stu-id="f6e18-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="f6e18-202">Adiciona uma série de valores ao gráfico.</span><span class="sxs-lookup"><span data-stu-id="f6e18-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="f6e18-203">Retorna um hash de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="f6e18-204">O algoritmo padrão é `sha256`.</span><span class="sxs-lookup"><span data-stu-id="f6e18-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="f6e18-205">Permite que os usuários do Facebook faça uma conexão para páginas.</span><span class="sxs-lookup"><span data-stu-id="f6e18-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="f6e18-206">Renderiza a interface do usuário para carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="f6e18-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="f6e18-207">Renderiza a marca jogador do Xbox especificada.</span><span class="sxs-lookup"><span data-stu-id="f6e18-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="f6e18-208">Processa a imagem de Gravatar para o endereço de email especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="f6e18-209">Converte um objeto de dados em uma cadeia de caracteres no formato de notação JSON (JavaScript Object).</span><span class="sxs-lookup"><span data-stu-id="f6e18-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="f6e18-210">Converte uma cadeia de caracteres de entrada codificados por JSON em um objeto de dados que você pode iterar sobre ou inserir em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f6e18-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="f6e18-211">Renderiza os links de rede social usando o título especificado e a URL opcional.</span><span class="sxs-lookup"><span data-stu-id="f6e18-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="f6e18-212">Associa uma mensagem de erro com um campo de formulário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-212">Associates an error message with a form field.</span></span> <span data-ttu-id="f6e18-213">Use o `ModelState` auxiliar para acessar esse membro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="f6e18-214">Associa uma mensagem de erro com um formulário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-214">Associates an error message with a form.</span></span> <span data-ttu-id="f6e18-215">Use o `ModelState` auxiliar para acessar esse membro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="f6e18-216">Retorna VERDADEIRO se não houver nenhum erro de validação.</span><span class="sxs-lookup"><span data-stu-id="f6e18-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="f6e18-217">Use o `ModelState` auxiliar para acessar esse membro.</span><span class="sxs-lookup"><span data-stu-id="f6e18-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="f6e18-218">As propriedades e valores de um objeto e qualquer filho processa objetos.</span><span class="sxs-lookup"><span data-stu-id="f6e18-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="f6e18-219">Renderiza o teste de verificação reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="f6e18-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="f6e18-220">Define as chaves públicas e privadas para o serviço reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="f6e18-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="f6e18-221">Normalmente você define essas propriedades na  *\_AppStart* página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="f6e18-222">Retorna o resultado do teste reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="f6e18-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="f6e18-223">Processa as informações de status sobre páginas da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f6e18-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="f6e18-224">Renderiza um fluxo do Twitter para o usuário especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="f6e18-225">Renderiza um fluxo do Twitter para o texto de pesquisa especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="f6e18-226">Renderiza um player de vídeo Flash para o arquivo especificado com altura e largura opcional.</span><span class="sxs-lookup"><span data-stu-id="f6e18-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="f6e18-227">Renderiza um player de mídia do Windows para o arquivo especificado com altura e largura opcional.</span><span class="sxs-lookup"><span data-stu-id="f6e18-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="f6e18-228">Renderiza um player do Silverlight especificado *. xap* arquivo com a largura e altura exigidos.</span><span class="sxs-lookup"><span data-stu-id="f6e18-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="f6e18-229">Retorna o objeto especificado pelo *chave*, ou nulo se o objeto não for encontrado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="f6e18-230">Remove o objeto especificado por *chave* do cache.</span><span class="sxs-lookup"><span data-stu-id="f6e18-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="f6e18-231">Coloca *valor* para o cache sob o nome especificado por *chave*.</span><span class="sxs-lookup"><span data-stu-id="f6e18-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="f6e18-232">Cria um novo `WebGrid` usando dados de uma consulta de objeto.</span><span class="sxs-lookup"><span data-stu-id="f6e18-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="f6e18-233">Renderiza uma marcação para exibir dados em uma tabela HTML.</span><span class="sxs-lookup"><span data-stu-id="f6e18-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="f6e18-234">Renderiza um pager para o `WebGrid` objeto.</span><span class="sxs-lookup"><span data-stu-id="f6e18-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="f6e18-235">Carrega uma imagem do caminho especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="f6e18-236">Adiciona a imagem especificada como uma marca d'água.</span><span class="sxs-lookup"><span data-stu-id="f6e18-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="f6e18-237">Adiciona o texto especificado para a imagem.</span><span class="sxs-lookup"><span data-stu-id="f6e18-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="f6e18-238">Inverte a imagem horizontalmente ou verticalmente.</span><span class="sxs-lookup"><span data-stu-id="f6e18-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="f6e18-239">Carrega uma imagem quando uma imagem de uma página é postada durante um carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="f6e18-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="f6e18-240">Redimensiona uma imagem.</span><span class="sxs-lookup"><span data-stu-id="f6e18-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="f6e18-241">Gira a imagem à esquerda ou à direita.</span><span class="sxs-lookup"><span data-stu-id="f6e18-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="f6e18-242">Salva a imagem no caminho especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="f6e18-243">Define a senha para o servidor SMTP.</span><span class="sxs-lookup"><span data-stu-id="f6e18-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="f6e18-244">Normalmente você definir essa propriedade  *\_AppStart* página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="f6e18-245">Envia uma mensagem de email.</span><span class="sxs-lookup"><span data-stu-id="f6e18-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="f6e18-246">Define o nome do servidor SMTP.</span><span class="sxs-lookup"><span data-stu-id="f6e18-246">Sets the SMTP server name.</span></span> <span data-ttu-id="f6e18-247">Normalmente você definir essa propriedade<em>\_AppStart</em> página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-247">Normally you set this property in the<em>\_AppStart</em> page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="f6e18-248">Define o nome de usuário para o servidor SMTP.</span><span class="sxs-lookup"><span data-stu-id="f6e18-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="f6e18-249">Normalmente, você deve definir essa propriedade na  *\_AppStart* página.</span><span class="sxs-lookup"><span data-stu-id="f6e18-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="f6e18-250">Validação</span><span class="sxs-lookup"><span data-stu-id="f6e18-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="f6e18-251">(v2) Processa uma mensagem de erro de validação para o campo especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="f6e18-252">(v2) Exibe uma lista de todos os erros de validação.</span><span class="sxs-lookup"><span data-stu-id="f6e18-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="f6e18-253">(v2) Registra um elemento de entrada do usuário para o tipo de validação especificado.</span><span class="sxs-lookup"><span data-stu-id="f6e18-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="f6e18-254">(v2) Renderiza dinamicamente os atributos de classe CSS para validação do lado do cliente para que você pode formatar mensagens de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="f6e18-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="f6e18-255">(Requer que você referencie as bibliotecas de script de cliente apropriadas e que você define classes CSS).</span><span class="sxs-lookup"><span data-stu-id="f6e18-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="f6e18-256">(v2) Habilita a validação do lado do cliente para o campo de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="f6e18-257">(Requer que você referencie as bibliotecas de script de cliente apropriado.)</span><span class="sxs-lookup"><span data-stu-id="f6e18-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="f6e18-258">(v2) Retornará true se todos os elementos de entrada de usuário que estão registrado para a validação contêm valores válidos.</span><span class="sxs-lookup"><span data-stu-id="f6e18-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="f6e18-259">(v2) Especifica que os usuários devem fornecer um valor para o elemento de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="f6e18-260">(v2) Especifica que os usuários devem fornecer valores para cada um dos elementos de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="f6e18-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="f6e18-261">Esse método não permite que você especificar uma mensagem de erro personalizada.</span><span class="sxs-lookup"><span data-stu-id="f6e18-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="f6e18-262">(v2) Especifica um teste de validação quando você usar o `Validation.Add` método.</span><span class="sxs-lookup"><span data-stu-id="f6e18-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
