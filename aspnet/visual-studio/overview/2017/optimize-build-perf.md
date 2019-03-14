---
uid: visual-studio/overview/2017/optimize-build-perf
title: Otimizar o desempenho de build para a solução
author: AngelosP
description: Otimizar o desempenho de build para a solução
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050503"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="6f1ca-103">Otimizar o desempenho de build para a solução</span><span class="sxs-lookup"><span data-stu-id="6f1ca-103">Optimize build performance for solution</span></span>

<span data-ttu-id="6f1ca-104">15,8 de 2017 do Visual Studio ou posterior inclui um item de menu: **Crie** > **compilação ASP.NET** > **otimizar o desempenho de compilação para a solução**.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![captura de tela do novo item de menu](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="6f1ca-106">O ASP.NET compila seus modos de exibição em tempo de execução, o que significa que um projeto ASP.NET carrega uma cópia do compilador.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="6f1ca-107">No entanto em um computador de desenvolvedor quando a cópia do compilador não corresponde a cópia do Visual Studio, o desempenho de compilação é afetado na ordem de 1 a 3 segundos por compilação incremental.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="6f1ca-108">Esse recurso atualiza a cópia do seu projeto do compilador para coincidir com o Visual Studio, que geralmente acelera a compilações incrementais.</span><span class="sxs-lookup"><span data-stu-id="6f1ca-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="6f1ca-109">**Isso é aplicável ao ASP.NET Framework 4.7.1 ou posterior somente a projetos, não se aplica ao ASP.NET Core.**</span><span class="sxs-lookup"><span data-stu-id="6f1ca-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
