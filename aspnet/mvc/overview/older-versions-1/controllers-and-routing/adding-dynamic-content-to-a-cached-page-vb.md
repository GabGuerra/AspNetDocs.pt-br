---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: Adicionando conteúdo dinâmico a uma página em cache (VB) | Microsoft Docs
author: microsoft
description: Saiba como a combinação de conteúdo dinâmico e armazenados em cache na mesma página. Substituição do pós-cache de permite que você exiba o conteúdo dinâmico, como faixa anúncios s...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: b361470c769b61a7b407797158eb695fe5084eda
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423488"
---
<a name="adding-dynamic-content-to-a-cached-page-vb"></a>Adicionar conteúdo dinâmico a uma página em cache (VB)
====================
por [Microsoft](https://github.com/microsoft)

> Saiba como a combinação de conteúdo dinâmico e armazenados em cache na mesma página. Substituição do pós-cache de permite que você exiba o conteúdo dinâmico, como anúncios de banner ou itens de notícias, dentro de uma página que tem sido a saída armazenada em cache.


Aproveitando o cache de saída, você pode melhorar consideravelmente o desempenho de um aplicativo ASP.NET MVC. Em vez de regenerar uma página de cada vez que a página é solicitada, a página pode ser gerada uma vez e armazenado em cache na memória para vários usuários.

Mas há um problema. E se você precisa exibir o conteúdo dinâmico na página? Por exemplo, imagine que você deseja exibir uma faixa de anúncio na página. Você não quer o anúncio em faixa sejam armazenados em cache para que cada usuário vê o anúncio do mesmo. Você não faria qualquer dinheiro dessa maneira!

Felizmente, há uma solução fácil. Você pode tirar proveito de um recurso da estrutura do ASP.NET chamado *pós-cache substituição*. Substituição do pós-cache de permite que você substitua o conteúdo dinâmico em uma página que foi armazenado em cache na memória.


Normalmente, quando você emitir armazenar em cache uma página usando o &lt;OutputCache&gt; atributo, a página é armazenada em cache no servidor e o cliente (navegador da web). Quando você usa a substituição do cache de postagem, uma página é armazenada em cache apenas no servidor.


#### <a name="using-post-cache-substitution"></a>Usando a substituição do Cache de postagem

Usando a substituição de POST-cache requer duas etapas. Primeiro, você precisa definir um método que retorna uma cadeia de caracteres que representa o conteúdo dinâmico que você deseja exibir na página em cache. Em seguida, você chamar o método de HttpResponse.WriteSubstitution() para inserir o conteúdo dinâmico na página.

Por exemplo, imagine que você deseja exibir aleatoriamente os itens de notícias diferentes em uma página em cache. A classe na listagem 1 expõe um único método, chamado RenderNews(), que retorna aleatoriamente um item de notícias de uma lista de três itens de notícias.

**Listagem 1 – Models\News.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

Para tirar proveito de substituição do cache de postagem, você chamar o método HttpResponse.WriteSubstitution(). O método WriteSubstitution() define o código para substituir uma região da página em cache com conteúdo dinâmico. O método WriteSubstitution() é usado para exibir o item de notícias aleatório no modo de exibição na listagem 2.

**Listagem 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

O método RenderNews é passado para o método WriteSubstitution(). Observe que o método RenderNews não é chamado. Em vez disso, uma referência para o método é passada para WriteSubstitution() com a Ajuda do operador AddressOf.

O modo de exibição de índice é armazenado em cache. O modo de exibição é retornado pelo controlador na listagem 3. Observe que a ação Index () é decorada com um &lt;OutputCache&gt; atributo que faz com que o modo de exibição de índice a ser armazenado em cache por 60 segundos.

**Listagem 3 – Controllers\HomeController.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

Mesmo que o modo de exibição de índice é armazenado em cache, os itens de notícias aleatórios diferentes são exibidos quando você solicita a página de índice. Quando você solicita a página de índice, não altera a hora exibida pela página por 60 segundos (veja a Figura 1). O fato de que o tempo não é alterado prova que a página é armazenada em cache. No entanto, o conteúdo é injetado pelas alterações de método – o item de notícias aleatório – WriteSubstitution() com cada solicitação.

**Figura 1 – injetando itens de notícias dinâmico em uma página em cache**

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>Usar substituição POST-Cache em métodos auxiliares

Uma maneira mais fácil para tirar proveito de substituição do cache de postagem é encapsular a chamada ao método WriteSubstitution() dentro de um método auxiliar personalizado. Essa abordagem é ilustrada pelo método auxiliar na listagem 4.

**Listagem 4 – Helpers\AdHelper.vb**

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

Listagem 4 contém um módulo do Visual Basic que expõe dois métodos: RenderBanner() e RenderBannerInternal(). O método RenderBanner() representa o método auxiliar real. Este método estende a classe HtmlHelper do ASP.NET MVC padrão para que você possa chamar Html.RenderBanner() em uma exibição exatamente como qualquer outro método auxiliar.

O método RenderBanner() chama o método de HttpResponse.WriteSubstitution() passando o método RenderBannerInternal() para o método WriteSubstitution().

O método RenderBannerInternal() é um método particular. Esse método não sejam exposto como um método auxiliar. O método RenderBannerInternal() aleatoriamente retorna uma imagem de anúncio da faixa de uma lista de três imagens de anúncio de faixa.

O modo de exibição do índice modificado na listagem 5 ilustra como você pode usar o método auxiliar RenderBanner(). Observe que adicional &lt;% @ % importação&gt; diretiva está incluída na parte superior do modo de exibição para importar o namespace MvcApplication1.Helpers. Se você não importar esse namespace, o método RenderBanner() não aparecerá como um método em que a propriedade de Html.

**Listagem 5 – Views\Home\Index.aspx (com o método RenderBanner())**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

Quando você solicita a página renderizada pela exibição na listagem 5, uma faixa diferente de anúncio é exibido com cada solicitação (veja a Figura 2). A página é armazenada em cache, mas a faixa de anúncio é injetada dinamicamente pelo método auxiliar RenderBanner().

**Figura 2 – o modo de exibição de índice exibindo um anúncio em faixa aleatório**

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a>Resumo

Este tutorial explicou como você pode atualizar dinamicamente o conteúdo em uma página em cache. Você aprendeu como usar o método HttpResponse.WriteSubstitution() para habilitar o conteúdo dinâmico a ser injetado em uma página em cache. Você também aprendeu como encapsular a chamada ao método WriteSubstitution() dentro de um método auxiliar HTML.

Tirar proveito do armazenamento em cache sempre que possível – ele pode ter um impacto significativo sobre o desempenho de seus aplicativos web. Conforme explicado neste tutorial, você pode tirar proveito do armazenamento em cache, mesmo quando você precisa exibir o conteúdo dinâmico em suas páginas.

> [!div class="step-by-step"]
> [Anterior](improving-performance-with-output-caching-vb.md)
> [Próximo](creating-a-controller-vb.md)
