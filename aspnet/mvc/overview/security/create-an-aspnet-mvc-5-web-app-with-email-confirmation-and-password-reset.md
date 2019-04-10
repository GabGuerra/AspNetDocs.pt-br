---
uid: mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
title: Criar um aplicativo de web do ASP.NET MVC 5 seguro com logon, o email de confirmação e redefinição de senha (c#) | Microsoft Docs
author: Rick-Anderson
description: Este tutorial mostra como criar um aplicativo de web do ASP.NET MVC 5 com confirmação por email e redefinição de senha usando o sistema de associação do ASP.NET Identity. Ca...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: d4911cb3-1afb-4805-b860-10818c4b1280
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 165343fd20b92becee1956c7a19870219323e073
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409389"
---
# <a name="create-a-secure-aspnet-mvc-5-web-app-with-log-in-email-confirmation-and-password-reset-c"></a><span data-ttu-id="8f78b-104">Criar um aplicativo Web seguro do ASP.NET MVC 5 com logon, confirmação por email e redefinição de senha (C#)</span><span class="sxs-lookup"><span data-stu-id="8f78b-104">Create a secure ASP.NET MVC 5 web app with log in, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="8f78b-105">por [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="8f78b-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="8f78b-106">Este tutorial mostra como criar um aplicativo de web do ASP.NET MVC 5 com confirmação por email e redefinição de senha usando o sistema de associação do ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="8f78b-106">This tutorial shows you how to build an ASP.NET MVC 5 web app with email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="8f78b-107">Você pode baixar o aplicativo concluído [aqui](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="8f78b-107">You can download the completed application [here](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="8f78b-108">O download contém os auxiliares de depuração que permitem que você teste confirmação por email e SMS sem configurar um email ou um provedor de SMS.</span><span class="sxs-lookup"><span data-stu-id="8f78b-108">The download contains debugging helpers that let you test email confirmation and SMS without setting up an email or SMS provider.</span></span>
> 
> <span data-ttu-id="8f78b-109">Este tutorial foi escrito por [Rick Anderson](https://blogs.msdn.com/rickAndy) (Twitter: [ @RickAndMSFT ](https://twitter.com/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="8f78b-109">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>


<a id="createMvc"></a>
## <a name="create-an-aspnet-mvc-app"></a><span data-ttu-id="8f78b-110">Criar um aplicativo ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8f78b-110">Create an ASP.NET MVC app</span></span>

<span data-ttu-id="8f78b-111">Comece instalando e executando [Visual Studio Express 2013 para Web](https://go.microsoft.com/fwlink/?LinkId=299058) ou [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span><span class="sxs-lookup"><span data-stu-id="8f78b-111">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="8f78b-112">Instale [Visual Studio 2013 atualização 3](https://go.microsoft.com/fwlink/?LinkId=390465) ou superior.</span><span class="sxs-lookup"><span data-stu-id="8f78b-112">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="8f78b-113">Aviso: Você deve instalar [Visual Studio 2013 atualização 3](https://go.microsoft.com/fwlink/?LinkId=390465) ou superior para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8f78b-113">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="8f78b-114">Crie um novo projeto da Web do ASP.NET e selecione o modelo MVC.</span><span class="sxs-lookup"><span data-stu-id="8f78b-114">Create a new ASP.NET Web project and select the MVC template.</span></span> <span data-ttu-id="8f78b-115">Web Forms também oferece suporte a identidade do ASP.NET, você pode seguir etapas semelhantes em um aplicativo de formulários da web.</span><span class="sxs-lookup"><span data-stu-id="8f78b-115">Web Forms also supports ASP.NET Identity, so you could follow similar steps in a web forms app.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image1.png)
2. <span data-ttu-id="8f78b-116">Deixe a autenticação padrão como **contas de usuário individuais**.</span><span class="sxs-lookup"><span data-stu-id="8f78b-116">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="8f78b-117">Se você quiser hospedar o aplicativo no Azure, deixe a caixa de seleção marcada.</span><span class="sxs-lookup"><span data-stu-id="8f78b-117">If you'd like to host the app in Azure, leave the check box checked.</span></span> <span data-ttu-id="8f78b-118">Posteriormente no tutorial, implantaremos para o Azure.</span><span class="sxs-lookup"><span data-stu-id="8f78b-118">Later in the tutorial we will deploy to Azure.</span></span> <span data-ttu-id="8f78b-119">Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8f78b-119">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
3. <span data-ttu-id="8f78b-120">Defina as [projeto para usar SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8f78b-120">Set the [project to use SSL](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
4. <span data-ttu-id="8f78b-121">Execute o aplicativo, clique no **registrar** vincular e registrar um usuário.</span><span class="sxs-lookup"><span data-stu-id="8f78b-121">Run the app, click the **Register** link and register a user.</span></span> <span data-ttu-id="8f78b-122">Neste ponto, a validação apenas no email é com o [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) atributo.</span><span class="sxs-lookup"><span data-stu-id="8f78b-122">At this point, the only validation on the email is with the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute.</span></span>
5. <span data-ttu-id="8f78b-123">No Server Explorer, navegue até **dados Connections\DefaultConnection\Tables\AspNetUsers**, clique com o botão direito e selecione **abrir definição de tabela**.</span><span class="sxs-lookup"><span data-stu-id="8f78b-123">In Server Explorer, navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span>

    <span data-ttu-id="8f78b-124">A imagem a seguir mostra o `AspNetUsers` esquema:</span><span class="sxs-lookup"><span data-stu-id="8f78b-124">The following image shows the `AspNetUsers` schema:</span></span>

    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="8f78b-125">Clique com botão direito do **AspNetUsers** de tabela e selecione **Mostrar dados da tabela**.</span><span class="sxs-lookup"><span data-stu-id="8f78b-125">Right click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
    ![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="8f78b-126">Neste ponto o email não foi confirmado.</span><span class="sxs-lookup"><span data-stu-id="8f78b-126">At this point the email has not been confirmed.</span></span>
7. <span data-ttu-id="8f78b-127">Clique na linha e selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="8f78b-127">Click on the row and select delete.</span></span> <span data-ttu-id="8f78b-128">Você adicionará este email novamente na próxima etapa e enviar um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="8f78b-128">You'll add this email again in the next step, and send a confirmation email.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="8f78b-129">Email de confirmação</span><span class="sxs-lookup"><span data-stu-id="8f78b-129">Email confirmation</span></span>

<span data-ttu-id="8f78b-130">Ele é uma prática recomendada para confirmar o email de um novo registro de usuário para verificar se eles não são representando a outra pessoa (ou seja, eles ainda não registrados com o email de outra pessoa).</span><span class="sxs-lookup"><span data-stu-id="8f78b-130">It's a best practice to confirm the email of a new user registration to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="8f78b-131">Suponha que você tivesse um fórum de discussão, convém evitar `"bob@example.com"` de registrar como `"joe@contoso.com"`.</span><span class="sxs-lookup"><span data-stu-id="8f78b-131">Suppose you had a discussion forum, you would want to prevent `"bob@example.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="8f78b-132">Sem email de confirmação, `"joe@contoso.com"` poderia obter email indesejado do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f78b-132">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="8f78b-133">Suponha que Bob acidentalmente registrado como `"bib@example.com"` e ainda não tenha notado, ele não seria capaz de usar a senha de recuperação porque o aplicativo não tiver seu email correto.</span><span class="sxs-lookup"><span data-stu-id="8f78b-133">Suppose Bob accidentally registered as `"bib@example.com"` and hadn't noticed it, he wouldn't be able to use password recover because the app doesn't have his correct email.</span></span> <span data-ttu-id="8f78b-134">Email de confirmação fornece apenas proteção limitada de bots e não fornece proteção de determinado remetentes de spam, eles têm muitos aliases de email de trabalho, que eles podem usar para se registrar.</span><span class="sxs-lookup"><span data-stu-id="8f78b-134">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers, they have many working email aliases they can use to register.</span></span>

<span data-ttu-id="8f78b-135">Você geralmente deseja impedir que usuários novos lançamentos de todos os dados para seu site da web antes de confirmar por email, uma mensagem de texto SMS ou outro mecanismo.</span><span class="sxs-lookup"><span data-stu-id="8f78b-135">You generally want to prevent new users from posting any data to your web site before they have been confirmed by email, a SMS text message or another mechanism.</span></span> <a id="build"></a><span data-ttu-id="8f78b-136">Nas seções a seguir, podemos habilitará o email de confirmação e modificar o código para impedir que usuários recém-registrados entrar até que o email foi confirmado.</span><span class="sxs-lookup"><span data-stu-id="8f78b-136">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="8f78b-137">Enganchar SendGrid</span><span class="sxs-lookup"><span data-stu-id="8f78b-137">Hook up SendGrid</span></span>

<span data-ttu-id="8f78b-138">As instruções nesta seção não são atuais.</span><span class="sxs-lookup"><span data-stu-id="8f78b-138">The instructions in this section are not current.</span></span> <span data-ttu-id="8f78b-139">Ver [provedor de email SendGrid configurar](/aspnet/core/security/authentication/accconfirm#configure-email-provider) para instruções de atualização.</span><span class="sxs-lookup"><span data-stu-id="8f78b-139">See [Configure SendGrid email provider](/aspnet/core/security/authentication/accconfirm#configure-email-provider) for updated instructions.</span></span>

<span data-ttu-id="8f78b-140">Embora este tutorial apenas mostra como adicionar notificação por email por meio [SendGrid](http://sendgrid.com/), você pode enviar emails usando SMTP e outros mecanismos (consulte [recursos adicionais](#addRes)).</span><span class="sxs-lookup"><span data-stu-id="8f78b-140">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="8f78b-141">No Console do Gerenciador de pacotes, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8f78b-141">In the Package Manager Console, enter the following command:</span></span> 

    [!code-console[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample1.cmd)]
2. <span data-ttu-id="8f78b-142">Vá para o [página de inscrição do Azure SendGrid](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) e registre-se para uma conta gratuita do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="8f78b-142">Go to the [Azure SendGrid sign up page](https://go.microsoft.com/fwlink/?linkid=271033&clcid=0x409) and register for a free SendGrid account.</span></span> <span data-ttu-id="8f78b-143">Configure o SendGrid, adicionando código semelhante ao seguinte no *App_Start/IdentityConfig.cs*:</span><span class="sxs-lookup"><span data-stu-id="8f78b-143">Configure SendGrid by adding code similar to the following in *App_Start/IdentityConfig.cs*:</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample2.cs?highlight=3,5)]

<span data-ttu-id="8f78b-144">Você precisará adicionar o que inclui o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8f78b-144">You'll need to add the following includes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample3.cs)]

<span data-ttu-id="8f78b-145">Para simplificar este exemplo, vamos armazenar as configurações do aplicativo na *Web. config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="8f78b-145">To keep this sample simple, we'll store the app settings in the *web.config* file:</span></span>

[!code-xml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample4.xml)]

> [!WARNING]
> <span data-ttu-id="8f78b-146">Security - nunca armazenar os dados confidenciais em seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="8f78b-146">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="8f78b-147">A conta e as credenciais são armazenadas na appSetting.</span><span class="sxs-lookup"><span data-stu-id="8f78b-147">The account and credentials are stored in the appSetting.</span></span> <span data-ttu-id="8f78b-148">No Azure, você pode armazenar com segurança esses valores sobre o **[configurar](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** guia no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f78b-148">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="8f78b-149">Ver [práticas recomendadas para implantar senhas e outros dados confidenciais no ASP.NET e o Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8f78b-149">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>


### <a name="enable-email-confirmation-in-the-account-controller"></a><span data-ttu-id="8f78b-150">Habilitar o email de confirmação no controlador da conta</span><span class="sxs-lookup"><span data-stu-id="8f78b-150">Enable email confirmation in the Account controller</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample5.cs?highlight=16-21)]

<span data-ttu-id="8f78b-151">Verifique se o *Views\Account\ConfirmEmail.cshtml* arquivo tem a sintaxe do razor correto.</span><span class="sxs-lookup"><span data-stu-id="8f78b-151">Verify the *Views\Account\ConfirmEmail.cshtml* file has correct razor syntax.</span></span> <span data-ttu-id="8f78b-152">(O caractere no primeiro @ linha pode estar ausente.</span><span class="sxs-lookup"><span data-stu-id="8f78b-152">( The @ character in the first line might be missing.</span></span> <span data-ttu-id="8f78b-153">)</span><span class="sxs-lookup"><span data-stu-id="8f78b-153">)</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="8f78b-154">Execute o aplicativo e clique no link de registro.</span><span class="sxs-lookup"><span data-stu-id="8f78b-154">Run the app and click the Register link.</span></span> <span data-ttu-id="8f78b-155">Depois de enviar o formulário de registro, você está conectado.</span><span class="sxs-lookup"><span data-stu-id="8f78b-155">Once you submit the registration form, you are logged in.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image4.png)

<span data-ttu-id="8f78b-156">Verifique sua conta de email e clique no link para confirmar seu email.</span><span class="sxs-lookup"><span data-stu-id="8f78b-156">Check your email account and click on the link to confirm your email.</span></span>

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="8f78b-157">Exigir email de confirmação antes de entrar</span><span class="sxs-lookup"><span data-stu-id="8f78b-157">Require email confirmation before log in</span></span>

<span data-ttu-id="8f78b-158">No momento, depois que o usuário concluir o formulário de registro, elas são registradas no.</span><span class="sxs-lookup"><span data-stu-id="8f78b-158">Currently once a user completes the registration form, they are logged in.</span></span> <span data-ttu-id="8f78b-159">Você geralmente deseja confirmar seu email antes do registro em log.</span><span class="sxs-lookup"><span data-stu-id="8f78b-159">You generally want to confirm their email before logging them in.</span></span> <span data-ttu-id="8f78b-160">A seção a seguir, modificaremos o código para exigir que novos usuários ter um email confirmado antes que eles estejam conectados (autenticado).</span><span class="sxs-lookup"><span data-stu-id="8f78b-160">In the section below, we will modify the code to require new users to have a confirmed email before they are logged in (authenticated).</span></span> <span data-ttu-id="8f78b-161">Atualização de `HttpPost Register` método com as seguintes alterações realçadas:</span><span class="sxs-lookup"><span data-stu-id="8f78b-161">Update the `HttpPost Register` method with the following highlighted changes:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample7.cs?highlight=14-15,23-30)]

<span data-ttu-id="8f78b-162">Comentando o `SignInAsync` método, o usuário não será conectado pelo registro.</span><span class="sxs-lookup"><span data-stu-id="8f78b-162">By commenting out the `SignInAsync` method, the user will not be signed in by the registration.</span></span> <span data-ttu-id="8f78b-163">O `TempData["ViewBagLink"] = callbackUrl;` linha pode ser usada para [depurar o aplicativo](#dbg) e testar o registro sem enviar email.</span><span class="sxs-lookup"><span data-stu-id="8f78b-163">The `TempData["ViewBagLink"] = callbackUrl;` line can be used to [debug the app](#dbg) and test registration without sending email.</span></span> `ViewBag.Message` <span data-ttu-id="8f78b-164">é usado para exibir as instruções de confirmar.</span><span class="sxs-lookup"><span data-stu-id="8f78b-164">is used to display the confirm instructions.</span></span> <span data-ttu-id="8f78b-165">O [baixar exemplo](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contém código para testar o email de confirmação sem configurar o email e também pode ser usado para depurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f78b-165">The [download sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952) contains code to test email confirmation without setting up email, and can also be used to debug the application.</span></span>

<span data-ttu-id="8f78b-166">Criar um `Views\Shared\Info.cshtml` arquivo e adicione a seguinte marcação razor:</span><span class="sxs-lookup"><span data-stu-id="8f78b-166">Create a `Views\Shared\Info.cshtml` file and add the following razor markup:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample8.cshtml)]

<span data-ttu-id="8f78b-167">Adicione a [atributo Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) para o `Contact` método de ação do controlador Home.</span><span class="sxs-lookup"><span data-stu-id="8f78b-167">Add the [Authorize attribute](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.118).aspx) to the `Contact` action method of the Home controller.</span></span> <span data-ttu-id="8f78b-168">Você pode clicar na **entre em contato com** link para verificar se os usuários anônimos não têm acesso e os usuários autenticados têm acesso.</span><span class="sxs-lookup"><span data-stu-id="8f78b-168">You can click on the **Contact** link to verify anonymous users don't have access and authenticated users do have access.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample9.cs?highlight=1)]

<span data-ttu-id="8f78b-169">Você também deve atualizar o `HttpPost Login` método de ação:</span><span class="sxs-lookup"><span data-stu-id="8f78b-169">You must also update the `HttpPost Login` action method:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample10.cs?highlight=13-22)]

<span data-ttu-id="8f78b-170">Atualizar o *Views\Shared\Error.cshtml* exibição para exibir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="8f78b-170">Update the *Views\Shared\Error.cshtml* view to display the error message:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample11.cshtml?highlight=8-17)]

<span data-ttu-id="8f78b-171">Excluir qualquer conta na **AspNetUsers** tabela que contém o alias de email que você deseja testar com.</span><span class="sxs-lookup"><span data-stu-id="8f78b-171">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test with.</span></span> <span data-ttu-id="8f78b-172">Execute o aplicativo e verifique se que você não pode fazer logon até que você confirmar seu endereço de email.</span><span class="sxs-lookup"><span data-stu-id="8f78b-172">Run the app and verify you can't log in until you have confirmed your email address.</span></span> <span data-ttu-id="8f78b-173">Depois de confirmar seu endereço de email, clique no **entre em contato com** link.</span><span class="sxs-lookup"><span data-stu-id="8f78b-173">Once you confirm your email address, click the **Contact** link.</span></span>

<a id="reset"></a>
## <a name="password-recoveryreset"></a><span data-ttu-id="8f78b-174">Recuperação/redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="8f78b-174">Password recovery/reset</span></span>

<span data-ttu-id="8f78b-175">Remova os caracteres de comentário do `HttpPost ForgotPassword` método de ação no controlador da conta:</span><span class="sxs-lookup"><span data-stu-id="8f78b-175">Remove the comment characters from the `HttpPost ForgotPassword` action method in the account controller:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample12.cs?highlight=17-20)]

<span data-ttu-id="8f78b-176">Remova os caracteres de comentário do `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) no *Views\Account\Login.cshtml* arquivo de exibição do razor:</span><span class="sxs-lookup"><span data-stu-id="8f78b-176">Remove the comment characters from the `ForgotPassword` [ActionLink](https://msdn.microsoft.com/library/system.web.mvc.html.linkextensions.actionlink(v=vs.118).aspx) in the *Views\Account\Login.cshtml* razor view file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample13.cshtml?highlight=47-50)]

<span data-ttu-id="8f78b-177">A página de logon agora mostrará um link para redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="8f78b-177">The Log in page will now show a link to reset the password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="8f78b-178">Reenviar link de confirmação de email</span><span class="sxs-lookup"><span data-stu-id="8f78b-178">Resend email confirmation link</span></span>

<span data-ttu-id="8f78b-179">Depois que um usuário cria uma nova conta local, eles são enviados por email um link de confirmação que são obrigados a usar antes que eles podem fazer logon.</span><span class="sxs-lookup"><span data-stu-id="8f78b-179">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="8f78b-180">Se o usuário exclui acidentalmente o email de confirmação, ou o email chega nunca, será necessário o link de confirmação enviado novamente.</span><span class="sxs-lookup"><span data-stu-id="8f78b-180">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="8f78b-181">As alterações de código a seguir mostram como habilitar isso.</span><span class="sxs-lookup"><span data-stu-id="8f78b-181">The following code changes show how to enable this.</span></span>

<span data-ttu-id="8f78b-182">Adicione o seguinte método auxiliar na parte inferior do *Controllers\AccountController.cs* arquivo:</span><span class="sxs-lookup"><span data-stu-id="8f78b-182">Add the following helper method to the bottom of the *Controllers\AccountController.cs* file:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample14.cs)]

<span data-ttu-id="8f78b-183">O método Register para usar o novo auxiliar de atualização:</span><span class="sxs-lookup"><span data-stu-id="8f78b-183">Update the Register method to use the new helper:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample15.cs?highlight=17)]

<span data-ttu-id="8f78b-184">Atualize o método de logon para reenviar a senha se a conta de usuário não foi confirmada:</span><span class="sxs-lookup"><span data-stu-id="8f78b-184">Update the Login method to resend the password if the user account has not been confirmed:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/samples/sample16.cs?highlight=20)]

<a id="combine"></a>
## <a name="combine-social-and-local-login-accounts"></a><span data-ttu-id="8f78b-185">Combine as contas de logon social e local</span><span class="sxs-lookup"><span data-stu-id="8f78b-185">Combine social and local login accounts</span></span>

<span data-ttu-id="8f78b-186">Você pode combinar as contas locais e sociais clicando no link seu email.</span><span class="sxs-lookup"><span data-stu-id="8f78b-186">You can combine local and social accounts by clicking on your email link.</span></span> <span data-ttu-id="8f78b-187">Na sequência a seguir **RickAndMSFT@gmail.com** é criado como um logon local, mas você pode criar a conta como um logon social no primeiro e adicionar um logon local.</span><span class="sxs-lookup"><span data-stu-id="8f78b-187">In the following sequence **RickAndMSFT@gmail.com** is first created as a local login, but you can create the account as a social log in first, then add a local login.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image5.png)

<span data-ttu-id="8f78b-188">Clique no **gerenciar** link.</span><span class="sxs-lookup"><span data-stu-id="8f78b-188">Click on the **Manage** link.</span></span> <span data-ttu-id="8f78b-189">Observação o **logons externos: 0** associada com esta conta.</span><span class="sxs-lookup"><span data-stu-id="8f78b-189">Note the **External Logins: 0** associated with this account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image6.png)

<span data-ttu-id="8f78b-190">Clique no link para outro log no serviço e aceitar as solicitações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f78b-190">Click the link to another log in service and accept the app requests.</span></span> <span data-ttu-id="8f78b-191">As duas contas foram combinadas, você poderá fazer logon com qualquer uma das contas.</span><span class="sxs-lookup"><span data-stu-id="8f78b-191">The two accounts have been combined, you will be able to log on with either account.</span></span> <span data-ttu-id="8f78b-192">Convém que os usuários adicionem contas locais no caso de seu logon social no serviço de autenticação está inoperante ou, mais provavelmente eles tem perdido o acesso à sua conta social.</span><span class="sxs-lookup"><span data-stu-id="8f78b-192">You might want your users to add local accounts in case their social log in authentication service is down, or more likely they have lost access to their social account.</span></span>

<span data-ttu-id="8f78b-193">Na imagem a seguir, Tom é um logon social (que você pode ver o **logons externos: 1** mostradas na página).</span><span class="sxs-lookup"><span data-stu-id="8f78b-193">In the following image, Tom is a social log in (which you can see from the **External Logins: 1** shown on the page).</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image7.png)

<span data-ttu-id="8f78b-194">Clicar em **escolha uma senha** permite que você adicione um log local em associado com a mesma conta.</span><span class="sxs-lookup"><span data-stu-id="8f78b-194">Clicking on **Pick a password** allows you to add a local log on associated with the same account.</span></span>

![](create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset/_static/image8.png)

## <a name="email-confirmation-in-more-depth"></a><span data-ttu-id="8f78b-195">Email de confirmação com mais profundidade</span><span class="sxs-lookup"><span data-stu-id="8f78b-195">Email confirmation in more depth</span></span>

<span data-ttu-id="8f78b-196">Tutorial de minha [confirmação de conta e recuperação de senha com o ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) entra neste tópico com mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="8f78b-196">My tutorial [Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) goes into this topic with more details.</span></span>

<a id="dbg"></a>
## <a name="debugging-the-app"></a><span data-ttu-id="8f78b-197">Depuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f78b-197">Debugging the app</span></span>

<span data-ttu-id="8f78b-198">Se você não receber um email contendo o link:</span><span class="sxs-lookup"><span data-stu-id="8f78b-198">If you don't get an email containing the link:</span></span>

- <span data-ttu-id="8f78b-199">Verifique a pasta Lixo eletrônico ou spam.</span><span class="sxs-lookup"><span data-stu-id="8f78b-199">Check your junk or spam folder.</span></span>
- <span data-ttu-id="8f78b-200">Faça logon em sua conta do SendGrid e clique no [link da atividade de Email](https://sendgrid.com/logs/index).</span><span class="sxs-lookup"><span data-stu-id="8f78b-200">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>

<span data-ttu-id="8f78b-201">Para testar o link de verificação sem email, baixe o [amostra concluída](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span><span class="sxs-lookup"><span data-stu-id="8f78b-201">To test the verification link without email, download the [completed sample](https://code.msdn.microsoft.com/MVC-5-with-2FA-email-8f26d952).</span></span> <span data-ttu-id="8f78b-202">O link de confirmação e códigos de confirmação serão exibidos na página.</span><span class="sxs-lookup"><span data-stu-id="8f78b-202">The confirmation link and confirmation codes will be displayed on the page.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="8f78b-203">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8f78b-203">Additional Resources</span></span>

- [<span data-ttu-id="8f78b-204">Recursos recomendados de links para a identidade do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8f78b-204">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- <span data-ttu-id="8f78b-205">[Confirmação de conta e recuperação de senha com o ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) apresenta mais detalhes na confirmação de conta e recuperação de senha.</span><span class="sxs-lookup"><span data-stu-id="8f78b-205">[Account Confirmation and Password Recovery with ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md) Goes into more detail on password recovery and account confirmation.</span></span>
- <span data-ttu-id="8f78b-206">[Aplicativo do MVC 5 com o Facebook, Twitter, LinkedIn e Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) este tutorial mostra como escrever um aplicativo ASP.NET MVC 5 com o Facebook e Google OAuth 2 autorização.</span><span class="sxs-lookup"><span data-stu-id="8f78b-206">[MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) This tutorial shows you how to write an ASP.NET MVC 5 app with Facebook and Google OAuth 2 authorization.</span></span> <span data-ttu-id="8f78b-207">Ele também mostra como adicionar dados adicionais para o banco de dados de identidade.</span><span class="sxs-lookup"><span data-stu-id="8f78b-207">It also shows how to add additional data to the Identity database.</span></span>
- <span data-ttu-id="8f78b-208">[Implantar um aplicativo ASP.NET MVC seguro com associação, OAuth e banco de dados SQL no Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="8f78b-208">[Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="8f78b-209">Este tutorial adiciona a implantação do Azure, como proteger seu aplicativo com as funções, como usar a API de associação para adicionar usuários e funções e recursos de segurança adicionais.</span><span class="sxs-lookup"><span data-stu-id="8f78b-209">This tutorial adds Azure deployment, how to secure your app with roles, how to use the membership API to add users and roles, and additional security features.</span></span>
- [<span data-ttu-id="8f78b-210">Criando um aplicativo do Google para o OAuth 2 e conectar o aplicativo ao projeto</span><span class="sxs-lookup"><span data-stu-id="8f78b-210">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#goog)
- [<span data-ttu-id="8f78b-211">Criando o aplicativo no Facebook e conectar o aplicativo ao projeto</span><span class="sxs-lookup"><span data-stu-id="8f78b-211">Creating the app in Facebook and connecting the app to the project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#fb)
- [<span data-ttu-id="8f78b-212">Configurar o SSL no projeto</span><span class="sxs-lookup"><span data-stu-id="8f78b-212">Setting up SSL in the Project</span></span>](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md#ssl)
