---
title: 'Autenticação de Facebook, Google e de provedor externo no ASP.NET Core'
author: rick-anderson
description: Este tutorial demonstra como criar um aplicativo do ASP.NET Core 2.x usando o OAuth 2.0 com provedores de autenticação externa.
ms.author: riande
ms.custom: mvc
ms.date: 1/19/2019
uid: security/authentication/social/index
---
# <a name="facebook-google-and-external-provider-authentication-in-aspnet-core"></a><span data-ttu-id="ee33f-103">Autenticação de Facebook, Google e de provedor externo no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ee33f-103">Facebook, Google, and external provider authentication in ASP.NET Core</span></span>

<span data-ttu-id="ee33f-104">Por [Valeriy Novytskyy](https://github.com/01binary) e [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ee33f-104">By [Valeriy Novytskyy](https://github.com/01binary) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ee33f-105">Este tutorial demonstra como criar um aplicativo ASP.NET Core 2.2, que permite aos usuários fazer logon usando o OAuth 2.0 com as credenciais de provedores de autenticação externa.</span><span class="sxs-lookup"><span data-stu-id="ee33f-105">This tutorial demonstrates how to build an ASP.NET Core 2.2 app that enables users to log in using OAuth 2.0 with credentials from external authentication providers.</span></span>

<span data-ttu-id="ee33f-106">Os provedores [Facebook](xref:security/authentication/facebook-logins), [Twitter](xref:security/authentication/twitter-logins), [Google](xref:security/authentication/google-logins) e [Microsoft](xref:security/authentication/microsoft-logins) são abordados nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee33f-106">[Facebook](xref:security/authentication/facebook-logins), [Twitter](xref:security/authentication/twitter-logins), [Google](xref:security/authentication/google-logins), and [Microsoft](xref:security/authentication/microsoft-logins) providers are covered in the following sections.</span></span> <span data-ttu-id="ee33f-107">Outros provedores estão disponíveis em pacotes de terceiros, como [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) e [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers).</span><span class="sxs-lookup"><span data-stu-id="ee33f-107">Other providers are available in third-party packages such as [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) and [AspNet.Security.OpenId.Providers](https://github.com/aspnet-contrib/AspNet.Security.OpenId.Providers).</span></span>

![Ícones de mídia social do Facebook, Twitter, Google+ e Windows](index/_static/social.png)

<span data-ttu-id="ee33f-109">Permitir que os usuários entrem com suas credenciais existentes é conveniente para os usuários e transfere muitas das complexidades de gerenciar o processo de entrada para um terceiro.</span><span class="sxs-lookup"><span data-stu-id="ee33f-109">Enabling users to sign in with their existing credentials is convenient for the users and shifts many of the complexities of managing the sign-in process onto a third party.</span></span> <span data-ttu-id="ee33f-110">Para obter exemplos de como os logons sociais podem impulsionar o tráfego e as conversões de clientes, consulte os estudos de caso do [Facebook](https://www.facebook.com/unsupportedbrowser) e do [Twitter](https://dev.twitter.com/resources/case-studies).</span><span class="sxs-lookup"><span data-stu-id="ee33f-110">For examples of how social logins can drive traffic and customer conversions, see case studies by [Facebook](https://www.facebook.com/unsupportedbrowser) and [Twitter](https://dev.twitter.com/resources/case-studies).</span></span>

## <a name="create-a-new-aspnet-core-project"></a><span data-ttu-id="ee33f-111">Criar um novo projeto ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ee33f-111">Create a New ASP.NET Core Project</span></span>

* <span data-ttu-id="ee33f-112">No Visual Studio 2017, crie um projeto na Página Inicial ou por meio de **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="ee33f-112">In Visual Studio 2017, create a new project from the Start Page, or via **File** > **New** > **Project**.</span></span>

* <span data-ttu-id="ee33f-113">Selecione o modelo **Aplicativo Web ASP.NET Core**, disponível na categoria **Visual C#** > **.NET Core**:</span><span class="sxs-lookup"><span data-stu-id="ee33f-113">Select the **ASP.NET Core Web Application** template available in the **Visual C#** > **.NET Core** category:</span></span>
* <span data-ttu-id="ee33f-114">Selecione **Alterar Autenticação** e defina a autenticação para **Contas de Usuário Individuais**.</span><span class="sxs-lookup"><span data-stu-id="ee33f-114">Select **Change Authentication** and set authentication to **Individual User Accounts**.</span></span>

## <a name="apply-migrations"></a><span data-ttu-id="ee33f-115">Aplicar migrações</span><span class="sxs-lookup"><span data-stu-id="ee33f-115">Apply migrations</span></span>

* <span data-ttu-id="ee33f-116">Execute o aplicativo e selecione o link **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="ee33f-116">Run the app and select the **Register** link.</span></span>
* <span data-ttu-id="ee33f-117">Insira o email e a senha para a nova conta e, em seguida, selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="ee33f-117">Enter the email and password for the new account, and then select **Register**.</span></span>
* <span data-ttu-id="ee33f-118">Siga as instruções para aplicar as migrações.</span><span class="sxs-lookup"><span data-stu-id="ee33f-118">Follow the instructions to apply migrations.</span></span>

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]

## <a name="use-secretmanager-to-store-tokens-assigned-by-login-providers"></a><span data-ttu-id="ee33f-119">Usar o SecretManager para armazenar os tokens atribuídos por provedores de logon</span><span class="sxs-lookup"><span data-stu-id="ee33f-119">Use SecretManager to store tokens assigned by login providers</span></span>

<span data-ttu-id="ee33f-120">Os provedores de logon social atribuem tokens de **ID do Aplicativo** e **Segredo do Aplicativo** durante o processo de registro.</span><span class="sxs-lookup"><span data-stu-id="ee33f-120">Social login providers assign **Application Id** and **Application Secret** tokens during the registration process.</span></span> <span data-ttu-id="ee33f-121">Os nomes de token exatos variam de acordo com o provedor.</span><span class="sxs-lookup"><span data-stu-id="ee33f-121">The exact token names vary by provider.</span></span> <span data-ttu-id="ee33f-122">Esses tokens representam as credenciais que seu aplicativo usa para acessar a API.</span><span class="sxs-lookup"><span data-stu-id="ee33f-122">These tokens represent the credentials your app uses to access their API.</span></span> <span data-ttu-id="ee33f-123">Os tokens constituem os "segredos" que podem ser vinculados à configuração de aplicativo com a ajuda do [Secret Manager](xref:security/app-secrets#secret-manager).</span><span class="sxs-lookup"><span data-stu-id="ee33f-123">The tokens constitute the "secrets" that can be linked to your app configuration with the help of [Secret Manager](xref:security/app-secrets#secret-manager).</span></span> <span data-ttu-id="ee33f-124">O Secret Manager é uma alternativa mais segura para armazenar os tokens em um arquivo de configuração, como *appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="ee33f-124">Secret Manager is a more secure alternative to storing the tokens in a configuration file, such as *appsettings.json*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee33f-125">O Secret Manager destina-se apenas para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ee33f-125">Secret Manager is for development purposes only.</span></span> <span data-ttu-id="ee33f-126">Você pode armazenar e proteger os segredos de teste e produção do Azure com o [provedor de configuração do Azure Key Vault](xref:security/key-vault-configuration).</span><span class="sxs-lookup"><span data-stu-id="ee33f-126">You can store and protect Azure test and production secrets with the [Azure Key Vault configuration provider](xref:security/key-vault-configuration).</span></span>

<span data-ttu-id="ee33f-127">Siga as etapas no tópico [Armazenamento seguro dos segredos do aplicativo em desenvolvimento no ASP.NET Core](xref:security/app-secrets) para armazenar os tokens atribuídos por cada provedor de logon abaixo.</span><span class="sxs-lookup"><span data-stu-id="ee33f-127">Follow the steps in [Safe storage of app secrets in development in ASP.NET Core](xref:security/app-secrets) topic to store tokens assigned by each login provider below.</span></span>

## <a name="setup-login-providers-required-by-your-application"></a><span data-ttu-id="ee33f-128">Configurar os provedores de logon necessários para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee33f-128">Setup login providers required by your application</span></span>

<span data-ttu-id="ee33f-129">Use os seguintes tópicos para configurar seu aplicativo para usar os respectivos provedores:</span><span class="sxs-lookup"><span data-stu-id="ee33f-129">Use the following topics to configure your application to use the respective providers:</span></span>

* <span data-ttu-id="ee33f-130">Instruções do [Facebook](xref:security/authentication/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="ee33f-130">[Facebook](xref:security/authentication/facebook-logins) instructions</span></span>
* <span data-ttu-id="ee33f-131">Instruções do [Twitter](xref:security/authentication/twitter-logins)</span><span class="sxs-lookup"><span data-stu-id="ee33f-131">[Twitter](xref:security/authentication/twitter-logins) instructions</span></span>
* <span data-ttu-id="ee33f-132">Instruções do [Google](xref:security/authentication/google-logins)</span><span class="sxs-lookup"><span data-stu-id="ee33f-132">[Google](xref:security/authentication/google-logins) instructions</span></span>
* <span data-ttu-id="ee33f-133">Instruções da [Microsoft](xref:security/authentication/microsoft-logins)</span><span class="sxs-lookup"><span data-stu-id="ee33f-133">[Microsoft](xref:security/authentication/microsoft-logins) instructions</span></span>
* <span data-ttu-id="ee33f-134">[Outras](xref:security/authentication/otherlogins) instruções do provedor</span><span class="sxs-lookup"><span data-stu-id="ee33f-134">[Other provider](xref:security/authentication/otherlogins) instructions</span></span>

[!INCLUDE[](includes/chain-auth-providers.md)]

## <a name="optionally-set-password"></a><span data-ttu-id="ee33f-135">Definir a senha opcionalmente</span><span class="sxs-lookup"><span data-stu-id="ee33f-135">Optionally set password</span></span>

<span data-ttu-id="ee33f-136">Ao registrar um provedor de logon externo, você não precisa ter uma senha registrada no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee33f-136">When you register with an external login provider, you don't have a password registered with the app.</span></span> <span data-ttu-id="ee33f-137">Isso o alivia da tarefa de criar e lembrar de uma senha para o site, mas também o torna dependente do provedor de logon externo.</span><span class="sxs-lookup"><span data-stu-id="ee33f-137">This alleviates you from creating and remembering a password for the site, but it also makes you dependent on the external login provider.</span></span> <span data-ttu-id="ee33f-138">Se o provedor de logon externo não estiver disponível, você não poderá fazer logon no site.</span><span class="sxs-lookup"><span data-stu-id="ee33f-138">If the external login provider is unavailable, you won't be able to log in to the web site.</span></span>

<span data-ttu-id="ee33f-139">Para criar uma senha e entrar usando seu email definido durante o processo de entrada com provedores externos:</span><span class="sxs-lookup"><span data-stu-id="ee33f-139">To create a password and sign in using your email that you set during the sign in process with external providers:</span></span>

* <span data-ttu-id="ee33f-140">Selecione o link **Olá,&lt; &gt;alias de email** na parte superior direita para navegar até a exibição **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ee33f-140">Select the **Hello &lt;email alias&gt;** link at the top right corner to navigate to the **Manage** view.</span></span>

![Exibição Gerenciar do Aplicativo Web](index/_static/pass1a.png)

* <span data-ttu-id="ee33f-142">Selecione **Criar**</span><span class="sxs-lookup"><span data-stu-id="ee33f-142">Select **Create**</span></span>

![Definir a página de senha](index/_static/pass2a.png)

* <span data-ttu-id="ee33f-144">Defina uma senha válida e use-a para entrar com seu email.</span><span class="sxs-lookup"><span data-stu-id="ee33f-144">Set a valid password and you can use this to sign in with your email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee33f-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee33f-145">Next steps</span></span>

* <span data-ttu-id="ee33f-146">Este artigo apresentou a autenticação externa e explicou os pré-requisitos necessários para adicionar logons externos ao aplicativo ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ee33f-146">This article introduced external authentication and explained the prerequisites required to add external logins to your ASP.NET Core app.</span></span>

* <span data-ttu-id="ee33f-147">Páginas de referência específicas ao provedor para configurar logons para os provedores necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee33f-147">Reference provider-specific pages to configure logins for the providers required by your app.</span></span>

* <span data-ttu-id="ee33f-148">Você talvez queira manter os dados adicionais sobre o usuário e seus tokens de atualização e acesso.</span><span class="sxs-lookup"><span data-stu-id="ee33f-148">You may want to persist additional data about the user and their access and refresh tokens.</span></span> <span data-ttu-id="ee33f-149">Para obter mais informações, consulte <xref:security/authentication/social/additional-claims>.</span><span class="sxs-lookup"><span data-stu-id="ee33f-149">For more information, see <xref:security/authentication/social/additional-claims>.</span></span>
