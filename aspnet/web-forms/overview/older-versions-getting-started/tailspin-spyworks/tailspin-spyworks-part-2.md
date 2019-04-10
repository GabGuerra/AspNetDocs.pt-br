---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Parte 2: Camada de acesso a dados | Microsoft Docs'
author: JoeStagner
description: Esta série de tutoriais fornece detalhes sobre todas as etapas realizadas para compilar o aplicativo de exemplo Tailspin Spyworks. Parte 2 mostra a adição de camada de acesso a dados.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378378"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="0921e-104">Parte 2: Camada de acesso a dados</span><span class="sxs-lookup"><span data-stu-id="0921e-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="0921e-105">por [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="0921e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="0921e-106">Tailspin Spyworks demonstra como incrivelmente simples é criar aplicativos avançados e escalonáveis para a plataforma .NET.</span><span class="sxs-lookup"><span data-stu-id="0921e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="0921e-107">Ele mostra como usar os novos recursos no ASP.NET 4 para criar uma loja online, incluindo as compras, check-out e administração.</span><span class="sxs-lookup"><span data-stu-id="0921e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="0921e-108">Esta série de tutoriais fornece detalhes sobre todas as etapas realizadas para compilar o aplicativo de exemplo Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="0921e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="0921e-109">Parte 2 mostra a adição de camada de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="0921e-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="0921e-110">Adicionar a camada de acesso de dados</span><span class="sxs-lookup"><span data-stu-id="0921e-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="0921e-111">Nosso aplicativo de comércio eletrônico dependerá de dois bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="0921e-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="0921e-112">Para obter informações do cliente, usaremos o banco de dados de associação do ASP.NET padrão.</span><span class="sxs-lookup"><span data-stu-id="0921e-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="0921e-113">Para nosso catálogo de produto e de carrinho de compras, implementaremos um banco de dados do SQL Express da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="0921e-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="0921e-114">Depois de criar o banco de dados (Commerce.mdf) no aplicativo do aplicativo\_pasta de dados pode prosseguir para criar nossa camada de acesso de dados usando o Entity Framework do .NET.</span><span class="sxs-lookup"><span data-stu-id="0921e-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="0921e-115">Vamos criar uma pasta denominada "dados\_acesso" e eles clique com o botão direito na pasta e selecione "Adicionar Novo Item".</span><span class="sxs-lookup"><span data-stu-id="0921e-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="0921e-116">Em "Installed Templates" item e, em seguida, selecione "dados de modelo de entidade ADO.NET" Insira EDM\_Commerce.edmx como o nome e clique no botão "Adicionar".</span><span class="sxs-lookup"><span data-stu-id="0921e-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="0921e-117">Escolha "Gerar do banco de dados".</span><span class="sxs-lookup"><span data-stu-id="0921e-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="0921e-118">Salve e compile.</span><span class="sxs-lookup"><span data-stu-id="0921e-118">Save and build.</span></span>

<span data-ttu-id="0921e-119">Agora estamos prontos para adicionar nosso primeiro recurso – um menu de categoria de produto.</span><span class="sxs-lookup"><span data-stu-id="0921e-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0921e-120">[Anterior](tailspin-spyworks-part-1.md)
> [Próximo](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="0921e-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
