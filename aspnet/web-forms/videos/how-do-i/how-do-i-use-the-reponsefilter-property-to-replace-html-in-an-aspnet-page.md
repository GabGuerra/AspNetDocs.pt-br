---
uid: web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
title: '[Como fazer:] Use a propriedade reponse. Filter para substituir o HTML em uma página ASP.NET | Microsoft Docs'
author: rick-anderson
description: Neste vídeo, Chris Pels mostra como usar a propriedade reponse. Filter para interceptar e alterar o HTML que está sendo enviado para uma página. Primeiro, uma página de exemplo é criada w...
ms.author: riande
ms.date: 01/29/2009
ms.assetid: 3e5ae74a-9798-47d8-a2b3-0d8ad42dd4bc
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page
msc.type: video
ms.openlocfilehash: 2ebd9162f81f5270c92c6b8d55e2d2dad4660701
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59403422"
---
# <a name="how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page"></a>[Como fazer:] Use a propriedade reponse. Filter para substituir o HTML em uma página ASP.NET

por [Chris Pels](https://twitter.com/chrispels)

Neste vídeo, Chris Pels mostra como usar a propriedade reponse. Filter para interceptar e alterar o HTML que está sendo enviado para uma página. Primeiro, uma página de exemplo é criada com um texto simples. Em seguida, uma classe Stream personalizada é criada que serve como o fluxo de substituição para o fluxo atual que está sendo enviado para o navegador do usuário. Essa classe de fluxos personalizados o conteúdo da página é recuperado do fluxo, alterados e, em seguida, gravada no fluxo de resposta. Nessa classe Stream personalizado o método de gravação é personalizado para substituir o HTML no fluxo de resposta de base, alterando assim que for enviado para o navegador do usuário. Por fim, a nova classe de fluxo é atribuída à propriedade Response na página\_evento de carregamento, assim, fornecendo o mecanismo para alterar o conteúdo da página.

[&#9654;Assista ao vídeo (13 minutos)](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-reponsefilter-property-to-replace-html-in-an-aspnet-page)
