---
ms.openlocfilehash: 96cd8c78178b02ad3eb4a471540950b4581af583
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033373"
---
# <a name="gdpr-sample"></a><span data-ttu-id="0645c-101">Exemplo GDPR</span><span class="sxs-lookup"><span data-stu-id="0645c-101">GDPR Sample</span></span>

* <span data-ttu-id="0645c-102">Na *appSettings. JSON*, defina `CheckNotConsentNeeded` para `false` exigir consentimento; caso contrário, definida como true ou omitir.</span><span class="sxs-lookup"><span data-stu-id="0645c-102">In *appsettings.json*, set `CheckNotConsentNeeded` to `false` to require consent; otherwise set to true or omit.</span></span> <span data-ttu-id="0645c-103">Testar o aplicativo com `CheckNotConsentNeeded` definido como `false` e defina como `true`.</span><span class="sxs-lookup"><span data-stu-id="0645c-103">Test the app with `CheckNotConsentNeeded` set to `false` and set to `true`.</span></span>
* <span data-ttu-id="0645c-104">Criar cookies essenciais e não essenciais com cada variação de `CheckConsentNeeded` e consentimento concedido.</span><span class="sxs-lookup"><span data-stu-id="0645c-104">Create essential and non-essential cookies with each variation of `CheckConsentNeeded` and consent granted.</span></span>
* <span data-ttu-id="0645c-105">Registre-se um usuário.</span><span class="sxs-lookup"><span data-stu-id="0645c-105">Register a user.</span></span>
* <span data-ttu-id="0645c-106">Exclua cookies.</span><span class="sxs-lookup"><span data-stu-id="0645c-106">Delete cookies.</span></span>
