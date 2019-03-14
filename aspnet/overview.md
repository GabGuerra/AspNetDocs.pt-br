---
uid: overview
title: Visão geral do ASP.NET | Microsoft Docs
author: rick-anderson
description: Introdução ao ASP.NET, uma estrutura gratuita para a criação de sites, aplicativos web e APIs da web.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 03/12/2010
ms.technology: aspnet
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 2dc48e1262b1807a77a9889f7e0e62c9b9ea463e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054633"
---
# <a name="aspnet-overview"></a>Visão geral do ASP.NET

O ASP.NET é um framework web grátis para a criação de ótimos sites e aplicativos web usando HTML, CSS e JavaScript. Você também pode criar APIs da Web e usar tecnologias em tempo real como Web Sockets.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) é uma alternativa ao ASP.NET.  Consulte a [orientações sobre como escolher entre ASP.NET e ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).

## <a name="get-started"></a>Introdução

Instale [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community edition, um IDE gratuito para o ASP.NET no Windows.

## <a name="websites-and-web-applications"></a>Sites e aplicativos web

 O ASP.NET oferece três estruturas para a criação de aplicativos da web: Web Forms, ASP.NET MVC e páginas da Web ASP.NET. Todas as três estruturas são estáveis e maduro e você pode criar aplicativos de sucesso da web com qualquer um deles. Não importa qual estrutura escolhida, você obterá todos os benefícios e recursos do ASP.NET em todos os lugares.

Cada estrutura tem como alvo um estilo de desenvolvimento diferentes. Aquele que você escolha depende de uma combinação de seus ativos de programação (dados de Conhecimento, habilidades e experiência de desenvolvimento), o tipo de aplicativo que você está criando e você se sentir confortável com a abordagem de desenvolvimento.

Abaixo está uma visão geral de cada uma das estruturas e algumas ideias para como escolher entre eles. Se você preferir um vídeo de Introdução, consulte [tornando sites com o ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) e [What ' s ferramentas da Web?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | Se você tiver experiência em | Estilo de desenvolvimento | Experiência |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms | Win Forms, WPF, .NET | Rápido desenvolvimento usando uma vasta biblioteca de controles que encapsulam a marcação HTML | Mid-Level, Advanced RAD |
| MVC       | Ruby on Rails, .NET  | Obter controle total sobre a marcação HTML, código e marcação separada e fáceis de escrever testes. A melhor opção para aplicativos móveis e de página única (SPA). | Mid-Level, Advanced |
| Páginas da Web  | Clássico ASP, PHP     | Marcação HTML e seu código junto no mesmo arquivo | Novo, de nível médio |

### <a name="web-forms"></a>Web Forms

Com Web Forms do ASP.NET, você pode criar sites dinâmicos usando um modelo familiar de arrastar e soltar, controlada por evento. Uma superfície de design e centenas de controles e componentes permitem que você crie rapidamente sofisticados, poderosos sites baseados em UI com acesso a dados.

[Saiba mais sobre Web Forms](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC lhe oferece uma maneira eficiente com base em padrões para criar sites dinâmicos que habilitam uma separação limpa de preocupações e que lhe dá controle total sobre a marcação para o desenvolvimento ágil e divertido. O ASP.NET MVC inclui muitos recursos que permitem o desenvolvimento rápido e amigável a TDD para criar aplicativos sofisticados que usam os últimos padrões da web.

[Saiba mais sobre o MVC](mvc/index.md)

### <a name="aspnet-web-pages"></a>Páginas da Web do ASP.NET

Páginas da Web ASP.NET e a sintaxe do Razor fornecem uma maneira rápida, acessível e leve de combinar código de servidor com HTML para criar conteúdo dinâmico da web. Conectar-se aos bancos de dados, adicionar um vídeo, vincular a sites de rede social e incluem muitos mais recursos que ajudam você a criam belos sites que estão em conformidade com os padrões da web mais recente.

[Saiba mais sobre as páginas da Web](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Observações sobre Web Forms, MVC e páginas da Web

Todas as três estruturas do ASP.NET são baseadas no .NET Framework e compartilham a funcionalidade de núcleo do .NET e do ASP.NET. Por exemplo, todas as três estruturas oferecem um modelo de segurança de logon com base em torno de associação, e todos os três compartilham os mesmos recursos para o gerenciamento de solicitações, manipulação de sessões e assim por diante que fazem parte da principal funcionalidade do ASP.NET.

Além disso, as três estruturas não são totalmente independentes e escolhendo um não evita que usando outro. Uma vez que as estruturas podem coexistir no mesmo aplicativo web, não é incomum ver componentes individuais dos aplicativos escritos usando estruturas diferentes. Por exemplo, voltado para o cliente de partes de um aplicativo podem ser desenvolvidas no MVC para otimizar a marcação, enquanto o acesso a dados e partes administrativas são desenvolvidas em Web Forms para tirar proveito dos controles de dados e acesso a dados simples.

## <a name="web-apis"></a>APIs da Web

API Web ASP.NET é uma estrutura que torna mais fácil criar serviços HTTP que alcançam uma ampla gama de clientes, incluindo navegadores e dispositivos móveis. O ASP.NET Web API é uma plataforma ideal para o desenvolvimento de aplicativos RESTful no .NET Framework.

[Saiba mais sobre a API da Web](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>Tecnologias em tempo real

SignalR do ASP.NET é uma nova biblioteca para desenvolvedores do ASP.NET que facilita a funcionalidade de desenvolvimento da web em tempo real. O SignalR permite a comunicação bidirecional entre servidor e cliente. Servidores podem enviar conteúdos para clientes conectados imediatamente conforme ficam disponível. O SignalR dá suporte a soquetes da Web e reverterá para outras técnicas compatíveis para navegadores mais antigos. O SignalR inclui APIs para o gerenciamento de conexão (por exemplo, conexão e eventos de desconexão), agrupamento de conexões e autorização.

[Saiba mais sobre o SignalR](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>Sites e aplicativos móveis

ASP.NET pode potencializar aplicativos móveis nativos com um back-end de API da Web, bem como os sites para celular usando estruturas de design dinâmico como o Twitter Bootstrap. Se você estiver criando um aplicativo móvel nativo, é fácil criar uma API da Web baseado em JSON para o identificador de acesso a dados, autenticação e notificações por push para seu aplicativo. Se você estiver criando um site para celular responsivo, você pode usar qualquer estrutura CSS ou o sistema de grade aberta preferem, ou selecione um sistema móvel poderoso como ótimos aplicativos móveis com o PhoneGap e Sencha ou o jQuery Mobile.

[Saiba mais sobre o desenvolvimento de site e aplicativo móvel](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>Aplicativos de página única

Aplicativo de página ASP.NET única (SPA) ajuda a criar aplicativos que incluam significativas interações do lado do cliente usando HTML 5, 3 de CSS e JavaScript. Visual Studio inclui um modelo para criar aplicativos de página única usando o Knockout. js e API Web do ASP.NET. Além do modelo interno do SPA, os modelos criados pela comunidade do SPA também estão disponíveis para download.

[Saiba mais sobre o desenvolvimento de aplicativo de página única](single-page-application/index.md)

## <a name="webhooks"></a>WebHooks

WebHooks é um padrão HTTP leve, fornecendo um modelo simples de pub/sub para conectar os serviços de SaaS e APIs da Web. Quando ocorre um evento em um serviço, uma notificação é enviada na forma de uma solicitação HTTP POST para assinantes registrados. A solicitação POST contém informações sobre o evento que torna possível para o destinatário para agir de acordo.

WebHooks são expostos por um grande número de serviços, incluindo o Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello e muito mais. Por exemplo, um WebHook pode indicar que um arquivo foi alterado no Dropbox, ou uma alteração de código foi confirmada no GitHub, ou um pagamento foi iniciado no PayPal ou foi criado um cartão no Trello.

[Saiba mais sobre WebHooks](webhooks/index.md)





<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
