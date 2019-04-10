---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Roteamento na API Web ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419230"
---
# <a name="routing-in-aspnet-web-api"></a>Roteamento na API Web ASP.NET

por [Mike Wasson](https://github.com/MikeWasson)

Este artigo descreve como o API Web ASP.NET encaminha solicitações HTTP para controladores.

> [!NOTE]
> Se você estiver familiarizado com o ASP.NET MVC, roteamento API Web é muito semelhante ao roteamento MVC. A principal diferença é que a API Web usa o verbo HTTP, não o caminho URI, para selecionar a ação. Você também pode usar o roteamento na API Web no estilo MVC. Este artigo não assume nenhum conhecimento do ASP.NET MVC.

## <a name="routing-tables"></a>Tabelas de roteamento

Na API Web ASP.NET, uma *controlador* é uma classe que manipula as solicitações HTTP. Os métodos públicos do controlador são chamados *métodos de ação* ou simplesmente *ações*. Quando a estrutura da API Web recebe uma solicitação, ele encaminha a solicitação para uma ação.

Para determinar qual ação a ser invocada, a estrutura usa um *tabela de roteamento*. O modelo de projeto do Visual Studio para API da Web cria uma rota padrão:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Essa rota é definida na *WebApiConfig.cs* arquivo, que é colocado na *App\_iniciar* diretório:

![](routing-in-aspnet-web-api/_static/image1.png)

Para obter mais informações sobre o `WebApiConfig` classe, consulte [Configurando o ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).

Se você hospedar internamente o API da Web, você deve definir a tabela de roteamento diretamente no `HttpSelfHostConfiguration` objeto. Para obter mais informações, consulte [hospedar internamente uma API Web](../older-versions/self-host-a-web-api.md).

Cada entrada na tabela de roteamento contém um *modelo de rota*. É o modelo de rota padrão para a API da Web &quot;api / {controller} / {id}&quot;. Neste modelo, &quot;api&quot; é um segmento de caminho literal e {controlador} e {id} são variáveis de espaço reservado.

Quando a estrutura da API Web recebe uma solicitação HTTP, ele tenta corresponder o URI em relação a um dos modelos de rota na tabela de roteamento. Se nenhuma rota corresponde, o cliente recebe um erro 404. Por exemplo, os URIs a seguir corresponde a rota padrão:

- /api/contacts
- /api/contacts/1
- /api/products/gizmo1

No entanto, o seguinte URI não corresponde, porque ele não tem o &quot;api&quot; segmento:

- /contacts/1

> [!NOTE]
> O motivo para usar "api" na rota é evitar colisões com o roteamento do ASP.NET MVC. Dessa forma, você pode ter &quot;/entra em contato com&quot; vá para um controlador MVC, e &quot;/api/contatos&quot; vá para um controlador de API da Web. É claro que, se você não gostar essa convenção, você pode alterar a tabela de rotas padrão.

Depois que uma rota correspondente for encontrada, a API da Web seleciona o controlador e a ação:

- Para localizar o controlador, a API da Web adiciona &quot;controlador&quot; para o valor da *{controlador}* variável.
- Para encontrar a ação, a API Web examina o verbo HTTP e, em seguida, procura por uma ação cujo nome começa com esse nome do verbo HTTP. Por exemplo, com uma solicitação GET, API da Web procura por uma ação prefixados com &quot;Obtenha&quot;, como &quot;GetContact&quot; ou &quot;GetAllContacts&quot;. Essa convenção aplica-se somente para obter, POST, PUT, DELETE, HEAD, opções e verbos de PATCH. Você pode habilitar outros verbos HTTP por meio de atributos em seu controlador. Veremos um exemplo disso mais tarde.
- Outras variáveis de espaço reservado no modelo de rota, como *{id},* são mapeados para parâmetros de ação.

Vamos examinar um exemplo. Suponha que você defina o controlador a seguir:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Aqui estão algumas solicitações HTTP possíveis, junto com a ação que é invocado para cada:

| HTTP Verb | Caminho de URI | Ação | Parâmetro |
| --- | --- | --- | --- |
| OBTER | API/produtos | GetAllProducts | *(nenhum)* |
| OBTER | produtos/API/4 | GetProductById | 4 |
| DELETE | produtos/API/4 | DeleteProduct | 4 |
| POSTAR | API/produtos | *(nenhuma correspondência)* |  |

Observe que o *{id}* segmento do URI, se presente, é mapeado para o *id* parâmetro da ação. Neste exemplo, o controlador define dois métodos GET com um *id* parâmetro e um sem parâmetros.

Além disso, observe que a solicitação POST falhará, pois o controlador não define uma &quot;Post... &quot; método.

## <a name="routing-variations"></a>Variações de roteamentos

A seção anterior descreveu o mecanismo de roteamento básico de API Web do ASP.NET. Esta seção descreve algumas variações.

### <a name="http-verbs"></a>Verbos HTTP

Em vez de usar a convenção de nomenclatura para verbos HTTP, você pode especificar explicitamente o verbo HTTP para uma ação decorando o método de ação com um dos seguintes atributos:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

No exemplo a seguir, o `FindProduct` método é mapeado para solicitações GET:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Para permitir que vários verbos HTTP para uma ação, ou para permitir verbos HTTP diferente de GET, PUT, POST, DELETE, HEAD, opções e PATCH, use o `[AcceptVerbs]` atributo, que utiliza uma lista de verbos HTTP.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Roteamento pelo nome da ação

Com o modelo de roteamento padrão, a API Web usa o verbo HTTP para selecionar a ação. No entanto, você também pode criar uma rota em que o nome da ação está incluído no URI:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

Neste modelo de rota, o *{action}* nomes de parâmetro de método de ação no controlador. Com esse estilo de roteamento, use atributos para especificar os verbos HTTP permitidos. Por exemplo, suponha que seu controlador tem o seguinte método:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

Nesse caso, uma solicitação GET para "api/produtos/detalhes/1" seria mapeados para o `Details` método. Esse estilo de roteamento é semelhante ao ASP.NET MVC e pode ser apropriado para uma API de estilo RPC.

Você pode substituir o nome da ação usando o `[ActionName]` atributo. No exemplo a seguir, há duas ações que mapeiam &quot;produtos/api/miniatura/*id*. Um oferece suporte a GET e o outro oferece suporte a POSTAGEM:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Não ações

Para impedir que um método sendo invocada como uma ação, use o `[NonAction]` atributo. Isso sinaliza para o framework que o método não é uma ação, mesmo que ele tenha correspondência as regras de roteamento.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Leitura adicional

Este tópico forneceu uma visão geral do roteamento. Para obter mais detalhes, consulte [roteamento e seleção de ação](routing-and-action-selection.md), que descreve exatamente como o framework corresponde a um URI para uma rota, seleciona um controlador e, em seguida, seleciona a ação a ser invocada.
