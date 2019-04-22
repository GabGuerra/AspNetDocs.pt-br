---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Teste da força de uma senha (c#) | Microsoft Docs
author: wenz
description: As senhas são necessárias em praticamente qualquer lugar, para que os usuários lentos tendem a escolher senhas simples, que são fáceis de interromper. O controle PasswordStrength do ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: d8ac50874d0325ed9583a16e1b4e19b3becabb99
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59391507"
---
# <a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="43654-104">Teste da força de uma senha (C#)</span><span class="sxs-lookup"><span data-stu-id="43654-104">Testing the Strength of a Password (C#)</span></span>

<span data-ttu-id="43654-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="43654-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="43654-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="43654-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="43654-107">As senhas são necessárias em praticamente qualquer lugar, para que os usuários lentos tendem a escolher senhas simples, que são fáceis de interromper.</span><span class="sxs-lookup"><span data-stu-id="43654-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="43654-108">O controle PasswordStrength no ASP.NET AJAX Control Toolkit pode verificar o quão bom é de uma senha.</span><span class="sxs-lookup"><span data-stu-id="43654-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="43654-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="43654-109">Overview</span></span>

<span data-ttu-id="43654-110">As senhas são necessárias em praticamente qualquer lugar, para que os usuários lentos tendem a escolher senhas simples, que são fáceis de interromper.</span><span class="sxs-lookup"><span data-stu-id="43654-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="43654-111">O `PasswordStrength` controle no ASP.NET AJAX Control Toolkit pode verificar o quão bom é de uma senha.</span><span class="sxs-lookup"><span data-stu-id="43654-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="43654-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="43654-112">Steps</span></span>

<span data-ttu-id="43654-113">O `PasswordStrength` controle estende uma caixa de texto e verifica se a senha nele é bom o suficiente.</span><span class="sxs-lookup"><span data-stu-id="43654-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="43654-114">Ele oferece uma infinidade de opções por meio de atributos. Aqui estão apenas alguns deles:</span><span class="sxs-lookup"><span data-stu-id="43654-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="43654-115">`MinimumNumericCharacters` número mínimo de caracteres necessários na senha</span><span class="sxs-lookup"><span data-stu-id="43654-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="43654-116">`MinimumSymbolCharacters` número mínimo de caracteres de símbolo (não letras e dígitos) necessário na senha</span><span class="sxs-lookup"><span data-stu-id="43654-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="43654-117">`PreferredPasswordLength` comprimento mínimo da senha</span><span class="sxs-lookup"><span data-stu-id="43654-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="43654-118">`RequiresUpperAndLowerCaseCharacters` Se a senha precisa usar caracteres maiusculos e minúsculos</span><span class="sxs-lookup"><span data-stu-id="43654-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="43654-119">O `StrengthIndicatorType` fornece as informações de como apresentar a força da senha, como texto (valor `"Text"`) ou como um tipo de barra de progresso (valor `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="43654-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="43654-120">No `DisplayPosition` atributo, configure onde as informações são exibidas.</span><span class="sxs-lookup"><span data-stu-id="43654-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="43654-121">Aqui está um exemplo completo, incluindo o ASP.NET AJAX `ScriptManager` controle, o `PasswordStrength` controle e certamente uma caixa de texto em que o usuário pode inserir uma senha.</span><span class="sxs-lookup"><span data-stu-id="43654-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="43654-122">Para fins de demonstração, o campo de segunda forma é um campo de texto normal e não é um campo de senha para que você pode ver durante o desenvolvimento, o que está digitando.</span><span class="sxs-lookup"><span data-stu-id="43654-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="43654-123">Execute a página e digite imediatamente: Somente depois que você inseriu letras minúsculas, letras maiusculas, dígitos e símbolos, a senha é considerada como inviolável.</span><span class="sxs-lookup"><span data-stu-id="43654-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="43654-124">[![Agora, a senha é bom (muito)](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="43654-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="43654-125">Agora, a senha é bom (muito) ([clique para exibir a imagem em tamanho normal](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="43654-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="43654-126">Avançar</span><span class="sxs-lookup"><span data-stu-id="43654-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
