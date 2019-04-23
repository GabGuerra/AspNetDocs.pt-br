---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: Como faço Criar um auxiliar HTML personalizado para um aplicativo MVC? | Microsoft Docs
author: rick-anderson
description: Neste vídeo, Chris Pels mostra como criar um HtmlHelper personalizado que não está disponível no conjunto de padrão em um aplicativo MVC. Primeiro, um aplicativo MVC de exemplo...
ms.author: riande
ms.date: 12/11/2009
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 60953243d3038667e4f729b1394e68f0c9d7c178
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59415044"
---
# <a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="46337-105">Como faço Criar um auxiliar HTML personalizado para um aplicativo MVC?</span><span class="sxs-lookup"><span data-stu-id="46337-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>

<span data-ttu-id="46337-106">por [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="46337-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="46337-107">Neste vídeo, Chris Pels mostra como criar um HtmlHelper personalizado que não está disponível no conjunto de padrão em um aplicativo MVC.</span><span class="sxs-lookup"><span data-stu-id="46337-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="46337-108">Primeiro, um aplicativo MVC de exemplo é criado com um controlador de demonstração e uma exibição para testar o HtmlHelper personalizado.</span><span class="sxs-lookup"><span data-stu-id="46337-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="46337-109">Em seguida, um módulo é criado com uma função pública que é um método de extensão que representa a implementação de HtmlHelper o personalizado.</span><span class="sxs-lookup"><span data-stu-id="46337-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="46337-110">O auxiliar personalizado é para a criação de `<img>` marcas em uma página e recebe vários parâmetros de entrada, incluindo a id, a url e o texto alternativo para a marca de imagem.</span><span class="sxs-lookup"><span data-stu-id="46337-110">The custom helper is for creating `<img>` tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="46337-111">A lógica é adicionada à função para retornar o concluído `<img>` marca com as informações especificadas.</span><span class="sxs-lookup"><span data-stu-id="46337-111">The logic is then added to the function for returning the completed `<img>` tag with the specified information.</span></span> <span data-ttu-id="46337-112">Em seguida, o HtmlHelper personalizado é usado na página de demonstração para exibir uma imagem.</span><span class="sxs-lookup"><span data-stu-id="46337-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="46337-113">Por fim, o HtmlHelper personalizado é expandido para incluir várias substituições de construtor que fornecem flexibilidade para mais facilmente criando diferentes `<img>` marcas.</span><span class="sxs-lookup"><span data-stu-id="46337-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different `<img>` tags.</span></span>

[<span data-ttu-id="46337-114">&#9654;Assista ao vídeo (18 minutos)</span><span class="sxs-lookup"><span data-stu-id="46337-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

> [!div class="step-by-step"]
> <span data-ttu-id="46337-115">[Anterior](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
> [Próximo](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="46337-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>
