---
uid: web-pages/readme/overview
title: WebMatrix Readme | Microsoft Docs
author: rick-anderson
description: O WebMatrix e o Leiame do ASP.NET Web Pages (Razor) versão 1.0
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133189"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="235f3-103">Leiame do WebMatrix</span><span class="sxs-lookup"><span data-stu-id="235f3-103">WebMatrix Readme</span></span>

<span data-ttu-id="235f3-104">13 de janeiro de 2011</span><span class="sxs-lookup"><span data-stu-id="235f3-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="235f3-105">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="235f3-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="235f3-106">Este arquivo Leiame aplica-se a 1.0 versão do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="235f3-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="235f3-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="235f3-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="235f3-108">Instalação</span><span class="sxs-lookup"><span data-stu-id="235f3-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="235f3-109">Como publicar aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="235f3-110">As alterações e questões</span><span class="sxs-lookup"><span data-stu-id="235f3-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="235f3-111">Instalação do WebMatrix 1.0</span><span class="sxs-lookup"><span data-stu-id="235f3-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="235f3-112">Páginas da Web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="235f3-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="235f3-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="235f3-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="235f3-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="235f3-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="235f3-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="235f3-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="235f3-116">Instalação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="235f3-117">Publicação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="235f3-118">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="235f3-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="235f3-119">Visão geral</span><span class="sxs-lookup"><span data-stu-id="235f3-119">Overview</span></span>

> <span data-ttu-id="235f3-120">Microsoft WebMatrix 1.0 é uma pilha de desenvolvimento da web gratuito que instala em minutos.</span><span class="sxs-lookup"><span data-stu-id="235f3-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="235f3-121">Ele integra um servidor web com o banco de dados e estruturas para criar uma experiência única e integrada de programação.</span><span class="sxs-lookup"><span data-stu-id="235f3-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="235f3-122">Você pode usar o WebMatrix para simplificar a maneira de código, testar e publicar seu próprio site ASP.NET ou PHP, ou você pode usar o WebMatrix para iniciar um novo site usando aplicativos de software livre populares, como o Joomla, Umbraco, WordPress ou DotNetNuke.</span><span class="sxs-lookup"><span data-stu-id="235f3-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="235f3-123">O WebMatrix usa o mesmo servidor da web avançados, o mecanismo de banco de dados e o ambiente de estruturas que executará o seu site na internet, o que faz a transição do desenvolvimento para produção simples e direta.</span><span class="sxs-lookup"><span data-stu-id="235f3-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="235f3-124">Instalação</span><span class="sxs-lookup"><span data-stu-id="235f3-124">Installation</span></span>

> <span data-ttu-id="235f3-125">Para instalar o WebMatrix 1.0, você deve primeiro instalar o [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="235f3-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="235f3-126">Depois de instalar o Web Platform Installer, você pode usá-lo para instalar o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="235f3-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="235f3-127">Se você tiver problemas durante a instalação, consulte [Solucionando problemas com o Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span><span class="sxs-lookup"><span data-stu-id="235f3-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="235f3-128">Como publicar aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-128">How to Publish Applications</span></span>

> <span data-ttu-id="235f3-129">Consulte [instruções passo a passo para a publicação de aplicativos](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="235f3-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="235f3-130">As alterações e questões</span><span class="sxs-lookup"><span data-stu-id="235f3-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="235f3-131">Problemas de instalação 1.0 do WebMatrix</span><span class="sxs-lookup"><span data-stu-id="235f3-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="235f3-132">Problema: O WebMatrix 1.0 está disponível somente nas plataformas que dão suporte ao Microsoft .NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="235f3-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="235f3-133">O .NET Framework versão 4 é necessário para o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="235f3-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="235f3-134">Em alguns casos, o instalador do WebMatrix 1.0 será permitem que você tente instalar em uma plataforma que não faz parte do conjunto de configurações com suporte.</span><span class="sxs-lookup"><span data-stu-id="235f3-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="235f3-135">Em particular, Windows Vista sem a atualização do SP1 lhe permitirá começar a instalação do WebMatrix, mas o componente do .NET Framework 4 falhará e bloquear a instalação.</span><span class="sxs-lookup"><span data-stu-id="235f3-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="235f3-136">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-136">**Workaround**</span></span>  
> <span data-ttu-id="235f3-137">Instale em uma plataforma com suporte, que inclui:</span><span class="sxs-lookup"><span data-stu-id="235f3-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="235f3-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="235f3-138">Windows 7</span></span>
> - <span data-ttu-id="235f3-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="235f3-139">Windows Server 2008</span></span>
> - <span data-ttu-id="235f3-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="235f3-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="235f3-141">Windows Vista SP1 ou posterior</span><span class="sxs-lookup"><span data-stu-id="235f3-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="235f3-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="235f3-142">Windows XP SP3</span></span>
> - <span data-ttu-id="235f3-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="235f3-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="235f3-144">Problema: Não é possível instalar o WebMatrix 1.0, se o Microsoft Visual Studio 2008 é instalado sem o Microsoft Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="235f3-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="235f3-145">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-145">**Workaround**</span></span>  
> <span data-ttu-id="235f3-146">Instale [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) do Centro de Download da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="235f3-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="235f3-147">Problema: Alguns assemblies para o SQL Server Compact 4.0 não estão instalados no GAC</span><span class="sxs-lookup"><span data-stu-id="235f3-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="235f3-148">Os assemblies gerenciados para o SQL Server Compact 4.0 não são colocados no cache de assembly global (GAC), quando você instala o SQL Server Compact 4.0 em um computador de 64 bits e o computador tem apenas o .NET Framework 3.5 SP1 Client Profile instalado.</span><span class="sxs-lookup"><span data-stu-id="235f3-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="235f3-149">São os assemblies gerenciados que não estão instalados no GAC:</span><span class="sxs-lookup"><span data-stu-id="235f3-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="235f3-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span><span class="sxs-lookup"><span data-stu-id="235f3-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="235f3-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span><span class="sxs-lookup"><span data-stu-id="235f3-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="235f3-152">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-152">**Workaround**</span></span>  
> <span data-ttu-id="235f3-153">Desinstalar o SQL Server Compact 4.0.</span><span class="sxs-lookup"><span data-stu-id="235f3-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="235f3-154">Baixe e instale a versão completa do .NET Framework 3.5 SP1 no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="235f3-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="235f3-155">Microsoft .NET Framework 3.5 Service pack 1 (pacote completo)</span><span class="sxs-lookup"><span data-stu-id="235f3-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="235f3-156">Em seguida, reinstale o SQL Server Compact 4.0.</span><span class="sxs-lookup"><span data-stu-id="235f3-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="235f3-157">Problema: Não é possível desinstalar o SQL Server Compact usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="235f3-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="235f3-158">Desinstalação do SQL Server Compact usando as opções de linha de comando não funciona nesta versão.</span><span class="sxs-lookup"><span data-stu-id="235f3-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="235f3-159">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-159">**Workaround**</span></span>  
> <span data-ttu-id="235f3-160">Use *programas e recursos* no painel de controle do Windows para desinstalar o Microsoft SQL Server Compact 4.0.</span><span class="sxs-lookup"><span data-stu-id="235f3-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="235f3-161">Páginas da Web do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="235f3-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="235f3-162">Esta seção do documento descreve novos recursos, alterações e problemas conhecidos com a 1.0 versão do ASP.NET Web Pages com sintaxe do Razor.</span><span class="sxs-lookup"><span data-stu-id="235f3-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="235f3-163">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="235f3-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="235f3-164">Alterações</span><span class="sxs-lookup"><span data-stu-id="235f3-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="235f3-165">Problemas</span><span class="sxs-lookup"><span data-stu-id="235f3-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a>  <span data-ttu-id="235f3-166">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="235f3-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="235f3-167">Novo: Definição de configuração adicionada para desabilitar o Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="235f3-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="235f3-168">Uma nova `asp:AdminManagerEnabled` chave está disponível para o `<appSettings>` elemento o *Web. config* arquivo, que permite que você desabilite completamente o Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="235f3-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="235f3-169">O valor padrão para esse elemento for true, o que significa que, se ele não está incluído na *Web. config* arquivo, o Gerenciador de pacotes está habilitado.</span><span class="sxs-lookup"><span data-stu-id="235f3-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="235f3-170">Para desabilitar o Gerenciador de pacotes, adicione o seguinte elemento para o *Web. config* arquivo na raiz do site:</span><span class="sxs-lookup"><span data-stu-id="235f3-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>  <span data-ttu-id="235f3-171">Alterações</span><span class="sxs-lookup"><span data-stu-id="235f3-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="235f3-172">Alterar: chave de "webPages:AdminFolderVirtualPath" renomeado para "asp: AdminFolderVirtualPath"</span><span class="sxs-lookup"><span data-stu-id="235f3-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="235f3-173">O `webPages:AdminFolderVirtualPath` chave que pode ser adicionado ao *Web. config* arquivo para especificar o local do Gerenciador de pacotes foi renomeado para usar os `asp:` namespace em vez do `webPages` namespace.</span><span class="sxs-lookup"><span data-stu-id="235f3-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="235f3-174">Se você tiver usado esse elemento, você deverá renomeá-la no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="235f3-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a>  <span data-ttu-id="235f3-175">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="235f3-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="235f3-176">Problema: Senhas de usuários de associação não reconhecidos</span><span class="sxs-lookup"><span data-stu-id="235f3-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="235f3-177">O algoritmo para criar e armazenar as senhas de participação (logon) foi alterado para ser mais seguro.</span><span class="sxs-lookup"><span data-stu-id="235f3-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="235f3-178">Como resultado, as senhas armazenadas para membros (usuários) criados em versões Beta do ASP.NET Razor não serão reconhecidas.</span><span class="sxs-lookup"><span data-stu-id="235f3-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="235f3-179">**Solução alternativa** se o site ainda não foi colocado em produção, remova os registros de usuário do banco de dados de associação.</span><span class="sxs-lookup"><span data-stu-id="235f3-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="235f3-180">Se o banco de dados em tempo real, por meio de programação regenere as senhas existentes no banco de dados de associação.</span><span class="sxs-lookup"><span data-stu-id="235f3-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="235f3-181">Problema: Comportamento inesperado ao usar uma tabela de usuário personalizada para a associação</span><span class="sxs-lookup"><span data-stu-id="235f3-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="235f3-182">Para inicializar o provedor de associação para um site do ASP.NET Razor, você deve chamar o `WebSecurity.InitializeDatabaseConnection` método.</span><span class="sxs-lookup"><span data-stu-id="235f3-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="235f3-183">(No WebMatrix, o modelo Site inicial inclui uma chamada para esse método na  *\_AppStart.cshtml* arquivo.) Se o `autoCreateTables` parâmetro desse método é definido como true (por padrão, ele é definido como true no modelo de Site inicial), e se um nome de tabela não reconhecido é passado para o método (o segundo parâmetro), o método não lança um erro.</span><span class="sxs-lookup"><span data-stu-id="235f3-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="235f3-184">Em vez disso, ele automaticamente cria a tabela.</span><span class="sxs-lookup"><span data-stu-id="235f3-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="235f3-185">Isso pode ser um problema se você pretende usar uma tabela de usuário personalizada para a associação, mas passe o nome da tabela incorreta para o `WebSecurity.InitializeDatabaseConnection` método.</span><span class="sxs-lookup"><span data-stu-id="235f3-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="235f3-186">Como o método por padrão gerará um erro se a tabela que você especificar não existir, e em vez disso, ele cria uma nova tabela, o aplicativo pode parecer estar funcionando.</span><span class="sxs-lookup"><span data-stu-id="235f3-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="235f3-187">No entanto, o código do aplicativo que se baseia em sua tabela de usuário personalizada (e em campos nele), eventualmente, pode falhar com erros inesperados.</span><span class="sxs-lookup"><span data-stu-id="235f3-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="235f3-188">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-188">**Workaround**</span></span>  
> <span data-ttu-id="235f3-189">Certifique-se de que o nome passado a `InitializeDatabaseConnection` correspondências de método, o perfil do usuário no banco de dados de associação de tabela, ou certifique-se de que o `autoCreateTables` parâmetro é definido como false.</span><span class="sxs-lookup"><span data-stu-id="235f3-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a><span data-ttu-id="235f3-190">Problema: Mensagem de erro "o módulo de administração requer acesso ao ~/App\_dados"</span><span class="sxs-lookup"><span data-stu-id="235f3-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="235f3-191">Em algumas circunstâncias, tentando criar usuários ou trabalhar com o sistema de associação do ASP.NET pode fazer com que a página para exibir o erro *o módulo de administração requer acesso ao ~/App\_dados*.</span><span class="sxs-lookup"><span data-stu-id="235f3-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="235f3-192">Isso ocorre se a conta que o IIS ou IIS Express é executado em não tem permissões para criar e gravar o *App\_dados* pasta sob a raiz do site.</span><span class="sxs-lookup"><span data-stu-id="235f3-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="235f3-193">**Solução alternativa** criar manualmente uma *App\_dados* pasta para o site.</span><span class="sxs-lookup"><span data-stu-id="235f3-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="235f3-194">Em seguida, certifique-se de que a conta do Windows que o aplicativo é executado (normalmente o serviço de rede) tem permissões de leitura/gravação para pastas raiz do aplicativo em subpastas, como aplicativo\_dados.</span><span class="sxs-lookup"><span data-stu-id="235f3-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="235f3-195">Informações mais detalhadas estão disponíveis no artigo da Base de Conhecimento [problemas com a instância de usuário do SQL Server Express e o ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="235f3-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="235f3-196">Problema: Erro "Falha ao gerar uma instância de usuário do SQL Server"</span><span class="sxs-lookup"><span data-stu-id="235f3-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="235f3-197">Se um aplicativo Web do WebMatrix usa o SQL Server Express e está executando o IIS 7.5 no Windows 7 ou Windows Server 2008 R2, você poderá ver um erro que indica que o SQL Server não pode recuperar caminho do aplicativo local do usuário em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="235f3-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="235f3-198">**Solução alternativa** Certifique-se de que a conta do Windows que o aplicativo é executado (normalmente o serviço de rede) tem permissões de leitura/gravação para pastas raiz do aplicativo em subpastas, como *aplicativo\_dados*.</span><span class="sxs-lookup"><span data-stu-id="235f3-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="235f3-199">Informações mais detalhadas estão disponíveis no artigo da Base de Conhecimento [problemas com a instância de usuário do SQL Server Express e o ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span><span class="sxs-lookup"><span data-stu-id="235f3-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="235f3-200">Problema: Arquivos que contém recursos do Gerenciador de pacotes ou as senhas do Gerenciador de pacote são fornecíveis no IIS 6.0 e versões anteriores</span><span class="sxs-lookup"><span data-stu-id="235f3-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="235f3-201">Se você implantar um aplicativo ASP.NET Web Pages (Razor) que foi criado usando a versão RC2, e se o aplicativo contém um *Password* ou *packagesources.txt* arquivo sob */App\_ Administrador dedados/*, IIS 6.0 servirá o arquivo se solicitado, potencialmente expor as senhas para sua instância do Gerenciador de pacote.</span><span class="sxs-lookup"><span data-stu-id="235f3-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="235f3-202">**Solução alternativa** renomear os *Password* ou *packagesources.txt* arquivo *password.config* ou *packagesources.config*. Por padrão, o IIS 6.0 não servirá os arquivos que têm o *. config* extensão.</span><span class="sxs-lookup"><span data-stu-id="235f3-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="235f3-203">(No IIS 7, nenhum arquivo o *App\_dados* pasta são atendidos, portanto você não precisa renomear os arquivos.)</span><span class="sxs-lookup"><span data-stu-id="235f3-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="235f3-204">Problema: Os pacotes instalados usando a versão Beta 3 de desinstalação não remove completamente os componentes de pacote</span><span class="sxs-lookup"><span data-stu-id="235f3-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="235f3-205">Se você instalou um pacote usando o Gerenciador de pacotes na versão Beta 3 e, em seguida, tente desinstalá-lo usando a versão atual, o pacote não foi completamente desinstalado.</span><span class="sxs-lookup"><span data-stu-id="235f3-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="235f3-206">Usando o Gerenciador de pacotes **Uninstall** botão remove alguns componentes, mas deixa o código da biblioteca do pacote e não atualiza o *Package* arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="235f3-207">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-207">**Workaround** </span></span>  
> <span data-ttu-id="235f3-208">Execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="235f3-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="235f3-209">Excluir o *App\_Data\packages* pasta.</span><span class="sxs-lookup"><span data-stu-id="235f3-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="235f3-210">Isso remove todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="235f3-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="235f3-211">Excluir o *Packages. config* arquivo na raiz do site.</span><span class="sxs-lookup"><span data-stu-id="235f3-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="235f3-212">Problema: No Visual Studio, invocar o Gerenciador de pacotes baseado na web leva para o aplicativo offline</span><span class="sxs-lookup"><span data-stu-id="235f3-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="235f3-213">Se você estiver trabalhando no Visual Studio (não o WebMatrix) e usar o  *\_admin* funcionalidade para iniciar o Gerenciador de pacotes, o Visual Studio coloca o aplicativo offline e posta os *aplicativo\_ offline.htm* para a raiz do site, que interrompe a capacidade de usar o Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="235f3-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="235f3-214">Embora você geralmente veria esse comportamento ao usar a interface do Gerenciador de pacotes baseado na web, o mesmo comportamento ocorre se você adiciona, remove ou modificar em todos os arquivos a *App\_dados* pasta.</span><span class="sxs-lookup"><span data-stu-id="235f3-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="235f3-215">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-215">**Workaround** </span></span>  
> <span data-ttu-id="235f3-216">Para trabalhar com pacotes no Visual Studio, use a extensão do NuGet em vez do Gerenciador de pacotes baseado na web.</span><span class="sxs-lookup"><span data-stu-id="235f3-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="235f3-217">Para obter informações, consulte o [documentação do NuGet](https://docs.microsoft.com/nuget/).</span><span class="sxs-lookup"><span data-stu-id="235f3-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="235f3-218">Se você estiver trabalhando com outros arquivos na *App\_dados* pasta, considere manter os arquivos em outro lugar para evitar esse problema.</span><span class="sxs-lookup"><span data-stu-id="235f3-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="235f3-219">Se não for prático, exclua o *app\_offline.htm* arquivo manualmente ou esperar até que o site fica online automaticamente (por padrão, após 30 segundos).</span><span class="sxs-lookup"><span data-stu-id="235f3-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="235f3-220">Problema: Studio IntelliSense e o projeto de modelos do Visual disponíveis apenas no ASP.NET MVC versão 3</span><span class="sxs-lookup"><span data-stu-id="235f3-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="235f3-221">Instalar páginas da Web ASP.NET não também instalará as ferramentas para Visual Studio como IntelliSense e modelos de projeto para aplicativos de páginas da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="235f3-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="235f3-222">**Solução alternativa** para usar o IntelliSense e modelos de projeto para aplicativos de páginas da Web ASP.NET no Visual Studio, instalar o ASP.NET MVC 3 RC por meio do Web Platform Installer ou o [instalador autônomo](https://go.microsoft.com/fwlink/?LinkID=191797).</span><span class="sxs-lookup"><span data-stu-id="235f3-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="235f3-223">Problema: Feeds de leitura ou outros dados externos por meio de um servidor proxy</span><span class="sxs-lookup"><span data-stu-id="235f3-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="235f3-224">Se o servidor que executa o site estiver atrás de um servidor proxy, você talvez precise configurar informações de proxy nas *Web. config* arquivo para que seja possível ler informações provenientes de fora do site.</span><span class="sxs-lookup"><span data-stu-id="235f3-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="235f3-225">Por exemplo, se você usar o `ReCaptcha` auxiliar, o auxiliar se comunica com o serviço reCAPTCHA, mas podem ser bloqueado pelo seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="235f3-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="235f3-226">Da mesma forma, os feeds que são usados no ASP.NET Web Pages, como o feed usado pelo Gerenciador de pacote, podem exigir configuração de proxy.</span><span class="sxs-lookup"><span data-stu-id="235f3-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="235f3-227">Se você tiver problemas em trabalhar com um serviço externo ou trabalhar com o feed de pacote, coloque os seguintes elementos raiz do seu aplicativo *Web. config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="235f3-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="235f3-228">Para obter mais informações sobre como configurar um servidor proxy, consulte [ &lt;proxy&gt; (configurações de rede)](https://msdn.microsoft.com/library/sa91de1e.aspx) no site do MSDN.</span><span class="sxs-lookup"><span data-stu-id="235f3-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="235f3-229">Problema: Desinstalando o .NET Framework versão 4 desabilita a ASP.NET Web Pages com sintaxe do Razor</span><span class="sxs-lookup"><span data-stu-id="235f3-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="235f3-230">Se você desinstalar o .NET Framework versão 4 e, em seguida, reinstalá-lo, ASP.NET Web Pages com sintaxe do Razor estão desabilitados.</span><span class="sxs-lookup"><span data-stu-id="235f3-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="235f3-231">As páginas com as *. cshtml* extensão não são executados corretamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="235f3-232">Páginas da Web ASP.NET registra um assembly na raiz da máquina *Web. config* arquivo e remover o .NET Framework remove esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="235f3-233">Reinstalar o .NET Framework instala uma nova versão do arquivo de configuração, mas não adiciona a referência para o assembly de páginas da Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="235f3-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="235f3-234">**Solução alternativa** após reinstalar o .NET Framework, reinstale o ASP.NET Web Pages com sintaxe do Razor.</span><span class="sxs-lookup"><span data-stu-id="235f3-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="235f3-235">Isso adiciona o elemento a seguir para o *Web. config* arquivo na raiz do computador, que normalmente é no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="235f3-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="235f3-236">Problema: URLs sem extensão não encontrar arquivos.cshtml/.vbhtml no IIS 7 ou IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="235f3-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="235f3-237">No IIS 7 ou IIS 7.5, solicitações com uma URL semelhante à seguinte não serão possível localizar as páginas que têm o *. cshtml* ou *. vbhtml* extensão:</span><span class="sxs-lookup"><span data-stu-id="235f3-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="235f3-238">O problema surge porque a regravação de URL não está habilitado por padrão para o IIS 7 ou IIS 7.5.</span><span class="sxs-lookup"><span data-stu-id="235f3-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="235f3-239">O cenário mais provável é que você não vir o problema ao testar localmente usando o IIS Express, mas a experiência quando você implanta seu site em um site de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="235f3-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="235f3-240">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="235f3-241">Se você tiver controle sobre o computador do servidor, no computador do servidor instale a atualização descrita no [uma atualização está disponível que permite que certos manipuladores do IIS 7.0 ou IIS 7.5 para manipular as solicitações cujas URLs não terminam com um período](https://support.microsoft.com/kb/980368).</span><span class="sxs-lookup"><span data-stu-id="235f3-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="235f3-242">Se você não tem controle sobre o computador do servidor (por exemplo, você estiver implantando em um site de hospedagem), adicione o seguinte para o site *Web. config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="235f3-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="235f3-243">Problema: Implantando um aplicativo em um computador que não tenha o SQL Server Compact instalado</span><span class="sxs-lookup"><span data-stu-id="235f3-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="235f3-244">Aplicativos que incluem bancos de dados do SQL Server Compact podem ser executados em um computador em que o SQL Server Compact não está instalado.</span><span class="sxs-lookup"><span data-stu-id="235f3-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="235f3-245">Microsoft WebMatrix 1.0 copia esses binários para você automaticamente e executa apropriado *Web. config* transformações de arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="235f3-246">**Solução alternativa** se você precisar copiar esses arquivos e fazer a *Web. config* alterações de arquivo manualmente, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="235f3-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="235f3-247">Copie os assemblies do mecanismo de banco de dados para o *Bin* pasta (e as subpastas) do aplicativo no computador de destino:</span><span class="sxs-lookup"><span data-stu-id="235f3-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="235f3-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="235f3-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="235f3-249">**to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="235f3-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="235f3-250">Cópia *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*  **para** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="235f3-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="235f3-251">Cópia *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **para** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="235f3-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="235f3-252">Na pasta raiz do site, crie ou abra uma *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="235f3-253">(No WebMatrix 1.0, esse tipo de arquivo está disponível se você clicar **todos os** na **escolher um tipo de arquivo** caixa de diálogo.)</span><span class="sxs-lookup"><span data-stu-id="235f3-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="235f3-254">Adicione o seguinte elemento como um filho de `<configuration>` elemento (não dentro a `<system.web>` elemento):</span><span class="sxs-lookup"><span data-stu-id="235f3-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="235f3-255">Problema: "Banco de dados" e "WebGrid" auxiliares não funcionam no nível de confiança média no Visual Basic</span><span class="sxs-lookup"><span data-stu-id="235f3-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="235f3-256">Se você estiver usando o Visual Basic (criando *. vbhtml* arquivos), o `Database` e `WebGrid` auxiliares não funcionará se o aplicativo está configurado para usar confiança média.</span><span class="sxs-lookup"><span data-stu-id="235f3-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="235f3-257">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-257">**Workaround**</span></span>  
> <span data-ttu-id="235f3-258">Se você usar o Visual Studio 2010, você pode resolver esse problema ao instalar a versão de Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="235f3-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="235f3-259">Até que a versão final da versão do SP1 está disponível, você pode baixar a versão Beta do SP1 a partir de [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) página no Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="235f3-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="235f3-260">Se isso não é prático, ou se você não usar o Visual Studio 2010, você pode temporariamente, defina o aplicativo para usar a confiança total.</span><span class="sxs-lookup"><span data-stu-id="235f3-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="235f3-261">Problema: Recursos de "ApplicationPart" sejam acessíveis externamente</span><span class="sxs-lookup"><span data-stu-id="235f3-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="235f3-262">Se um assembly contém objetos que deriva de `ApplicationPart` classe, que os recursos do assembly são expostos pelo `ResourceRouteHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="235f3-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="235f3-263">Por exemplo, considere a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="235f3-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="235f3-264">Essa solicitação baixa todas as cadeias de caracteres de recurso nas *System.Web.WebPages.Administration.dll* assembly.</span><span class="sxs-lookup"><span data-stu-id="235f3-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="235f3-265">Todos os recursos incorporados (mesmo aqueles que não se destina a ser atendido como conteúdo estático) são baixados.</span><span class="sxs-lookup"><span data-stu-id="235f3-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="235f3-266">Se os recursos incorporados contiverem informações confidenciais, isso pode representar um risco à segurança.</span><span class="sxs-lookup"><span data-stu-id="235f3-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="235f3-267">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-267">**Workaround** </span></span>  
> <span data-ttu-id="235f3-268">Se você criar uma **ApplicationPart** do objeto, certifique-se de que os recursos incorporados associados a esse **ApplicationPart** assembly do objeto não contêm informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="235f3-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="235f3-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="235f3-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="235f3-270">Para obter informações sobre problemas de instalação para o WebMatrix, consulte [problemas de instalação do WebMatrix](#Known_Issues_Installation) anteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="235f3-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="235f3-271">Esta seção do documento descreve problemas conhecidos para o ambiente de desenvolvimento do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="235f3-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="235f3-272">Problema: Alterações no nome de usuário ou senha de uma cadeia de caracteres de conexão de banco de dados em um arquivo Web. config não são refletidas no espaço de trabalho de bancos de dados</span><span class="sxs-lookup"><span data-stu-id="235f3-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="235f3-273">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="235f3-274">No *Web. config* file, altere o nome do banco de dados na cadeia de conexão (por exemplo, adicione "1" a ele).</span><span class="sxs-lookup"><span data-stu-id="235f3-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="235f3-275">Salvar a *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="235f3-276">Clique em **bancos de dados** e atualizar.</span><span class="sxs-lookup"><span data-stu-id="235f3-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="235f3-277">Altere o nome do banco de dados na cadeia de conexão a *Web. config* arquivo de volta para o nome do banco de dados original.</span><span class="sxs-lookup"><span data-stu-id="235f3-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="235f3-278">Salvar a *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="235f3-279">Clique em **bancos de dados** e atualizar.</span><span class="sxs-lookup"><span data-stu-id="235f3-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="235f3-280">Problema: Não não possível excluir pastas criadas pelo WebMatrix</span><span class="sxs-lookup"><span data-stu-id="235f3-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="235f3-281">Se o WebMatrix está em execução usando permissões elevadas (ou seja, você iniciou o WebMatrix usando o **executar como administrador** opção no Windows), as pastas criadas pelo WebMatrix não podem ser excluídas usando o Windows Explorer.</span><span class="sxs-lookup"><span data-stu-id="235f3-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="235f3-282">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-282">**Workaround**</span></span>  
> <span data-ttu-id="235f3-283">Execute o Explorer do Windows usando permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="235f3-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="235f3-284">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="235f3-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="235f3-285">No Windows, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="235f3-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="235f3-286">Insira "Windows Explorer" e a entrada para o botão direito do mouse **Windows Explorer**.</span><span class="sxs-lookup"><span data-stu-id="235f3-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="235f3-287">Clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="235f3-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="235f3-288">Em seguida, você pode excluir as pastas.</span><span class="sxs-lookup"><span data-stu-id="235f3-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="235f3-289">Problema: O WebMatrix 1.0 não consegue realizar certas tarefas que exigem elevação</span><span class="sxs-lookup"><span data-stu-id="235f3-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="235f3-290">O WebMatrix 1.0 não consegue realizar certas tarefas que exigem elevação de privilégio, como a instalação de componentes adicionais nas seguintes situações:</span><span class="sxs-lookup"><span data-stu-id="235f3-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="235f3-291">No Windows Vista ou Windows 7, você está conectado com uma conta que não tem privilégios administrativos e controle de conta de usuário (UAC) está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="235f3-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="235f3-292">Você está usando o Microsoft Windows XP ou Microsoft Windows Server 2003.</span><span class="sxs-lookup"><span data-stu-id="235f3-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="235f3-293">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-293">**Workaround**</span></span>  
> <span data-ttu-id="235f3-294">A maioria das tarefas no WebMatrix 1.0 não exigem permissão administrativa.</span><span class="sxs-lookup"><span data-stu-id="235f3-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="235f3-295">Para aqueles que fazer, você pode executar a operação como um administrador ou siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="235f3-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="235f3-296">No Windows Vista ou Windows 7, habilite o UAC.</span><span class="sxs-lookup"><span data-stu-id="235f3-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="235f3-297">No Windows XP, adicione o usuário ao grupo de segurança Administradores.</span><span class="sxs-lookup"><span data-stu-id="235f3-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="235f3-298">Problema: "Site da Galeria de Web" está desabilitado</span><span class="sxs-lookup"><span data-stu-id="235f3-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="235f3-299">O **Site da Galeria de Web** opção será desabilitada se o Web Platform Installer 3.0 não está instalado.</span><span class="sxs-lookup"><span data-stu-id="235f3-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="235f3-300">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-300">**Workaround**</span></span>  
> <span data-ttu-id="235f3-301">Instalar o [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span><span class="sxs-lookup"><span data-stu-id="235f3-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="235f3-302">Problema: Google Chrome não está disponível como uma opção de execução</span><span class="sxs-lookup"><span data-stu-id="235f3-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="235f3-303">Google Chrome não é exibido na lista de navegadores em **executados** sobre o **Home** guia.</span><span class="sxs-lookup"><span data-stu-id="235f3-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="235f3-304">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-304">**Workaround**</span></span>  
> <span data-ttu-id="235f3-305">Algumas versões do Google Chrome não se registram corretamente com o recurso de programas padrão no Windows.</span><span class="sxs-lookup"><span data-stu-id="235f3-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="235f3-306">Como alternativa, inicie o Google Chrome, clique o *personalizar e controle Google Chrome* menu, clique em *opções*e, em seguida, clique em *Make Google Chrome meu navegador padrão*.</span><span class="sxs-lookup"><span data-stu-id="235f3-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="235f3-307">Problema: A caixa de diálogo "Foreign Key" não permite a inserção de uma chave primária</span><span class="sxs-lookup"><span data-stu-id="235f3-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="235f3-308">O **Foreign Key** caixa de diálogo não permite que você insira o nome da chave primário da tabela de chave primária.</span><span class="sxs-lookup"><span data-stu-id="235f3-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="235f3-309">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-309">**Workaround**</span></span>  
> <span data-ttu-id="235f3-310">Isso é intencional.</span><span class="sxs-lookup"><span data-stu-id="235f3-310">This is intentional.</span></span> <span data-ttu-id="235f3-311">Você não precisará inserir o nome da chave primária da tabela de chave primária.</span><span class="sxs-lookup"><span data-stu-id="235f3-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="235f3-312">Problema: IntelliSense não está disponível no WebMatrix para sintaxe do Razor, C#, ou o Visual Basic</span><span class="sxs-lookup"><span data-stu-id="235f3-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="235f3-313">Há suporte para o IntelliSense para HTML e CSS no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="235f3-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="235f3-314">No entanto, ele não está disponível para outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="235f3-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="235f3-315">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-315">**Workaround** </span></span>  
> <span data-ttu-id="235f3-316">nenhuma.</span><span class="sxs-lookup"><span data-stu-id="235f3-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="235f3-317">Problema: IntelliSense para HTML e CSS sugere elementos que não são contextualmente apropriados</span><span class="sxs-lookup"><span data-stu-id="235f3-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="235f3-318">IntelliSense para marcação no WebMatrix dá suporte a HTML usando o [esquema XHTML 1.0 Transitional](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) e CSS usando o [esquema CSS 2.1](http://www.w3.org/TR/CSS2/).</span><span class="sxs-lookup"><span data-stu-id="235f3-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="235f3-319">Como o IntelliSense se baseia nesses esquemas específicos, determinadas marcas, atributos ou propriedades talvez sugeridas que não são apropriados para a definição de estilo ou de página atual.</span><span class="sxs-lookup"><span data-stu-id="235f3-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="235f3-320">Para HTML, ele também pode levar a sugestões inesperados no conteúdo que pode ser interpretada como XHTML malformada (por exemplo, quando as marcas não estão fechadas).</span><span class="sxs-lookup"><span data-stu-id="235f3-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="235f3-321">Esse problema pode ser mais perceptível se o ponto de inserção está dentro de uma marca incompleta; Nesse caso, IntelliSense pode sugerir novos marcas de abertura ou oferecer outras sugestões incorretos.</span><span class="sxs-lookup"><span data-stu-id="235f3-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="235f3-322">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-322">**Workaround** </span></span>  
> <span data-ttu-id="235f3-323">Para HTML, certifique-se de que você está trabalhando em uma página XHTML bem formada e completa.</span><span class="sxs-lookup"><span data-stu-id="235f3-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="235f3-324">Para o CSS, não há nenhuma solução alternativa.</span><span class="sxs-lookup"><span data-stu-id="235f3-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="235f3-325">Problema: IntelliSense não é chamado enquanto você digita</span><span class="sxs-lookup"><span data-stu-id="235f3-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="235f3-326">Às vezes, IntelliSense não pode ser invocado como HTML ou CSS está sendo inserido no editor.</span><span class="sxs-lookup"><span data-stu-id="235f3-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="235f3-327">Em particular, isso pode acontecer quando o ponto de inserção está diretamente ao lado do outro elemento ou no final de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="235f3-328">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-328">**Workaround** </span></span>  
> <span data-ttu-id="235f3-329">Certifique-se de que há espaço em branco em torno do ponto de inserção e o ponto de inserção não está no final de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="235f3-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="235f3-330">Você também pode invocar IntelliSense manualmente, pressionando Ctrl + espaço.</span><span class="sxs-lookup"><span data-stu-id="235f3-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="235f3-331">Problema: Nenhuma interface do usuário está disponível para desabilitar o IntelliSense</span><span class="sxs-lookup"><span data-stu-id="235f3-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="235f3-332">O WebMatrix 1.0 não fornece nenhuma interface do usuário ou gesto para desativar o IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="235f3-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="235f3-333">**Solução alternativa** </span><span class="sxs-lookup"><span data-stu-id="235f3-333">**Workaround** </span></span>  
> <span data-ttu-id="235f3-334">Inicie o WebMatrix usando o comando a seguir, que inclui uma opção que desativa o IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="235f3-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="235f3-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="235f3-335">IIS Express</span></span>

<span data-ttu-id="235f3-336">O IIS Express tem seu próprio arquivo Leiame, que está disponível na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="235f3-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="235f3-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="235f3-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="235f3-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="235f3-338">SQL Server Compact</span></span>

<span data-ttu-id="235f3-339">O SQL Server Compact tem seu próprio arquivo Leiame, que está disponível na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="235f3-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="235f3-340">Para obter informações sobre problemas que envolvem a instalação do SQL Server Compact como parte do WebMatrix, consulte [problemas de instalação do WebMatrix](#Known_Issues_Installation) anteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="235f3-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a>  <span data-ttu-id="235f3-341">Instalação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="235f3-342">Problema: Instalação de um aplicativo pode levar muito tempo se a pasta Meus documentos do usuário é redirecionada para um compartilhamento de rede</span><span class="sxs-lookup"><span data-stu-id="235f3-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="235f3-343">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-343">**Workaround**</span></span>  
> <span data-ttu-id="235f3-344">nenhuma.</span><span class="sxs-lookup"><span data-stu-id="235f3-344">None.</span></span> <span data-ttu-id="235f3-345">O aplicativo pode levar algum tempo para ser instalado, mas será instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a>  <span data-ttu-id="235f3-346">Publicação de aplicativos</span><span class="sxs-lookup"><span data-stu-id="235f3-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="235f3-347">Problema: Erro de "Exige as permissões não podem ser adquiridas" ao publicar um banco de dados do SQL Compact</span><span class="sxs-lookup"><span data-stu-id="235f3-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="235f3-348">O WebMatrix não suporta totalmente implantar binários do suporte para SQL Server Compact em um servidor que executa o .NET Framework versão 3.5 com uma configuração de confiança média.</span><span class="sxs-lookup"><span data-stu-id="235f3-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="235f3-349">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-349">**Workaround**</span></span>  
> <span data-ttu-id="235f3-350">É a solução preferencial instalar o .NET Framework 4 no servidor.</span><span class="sxs-lookup"><span data-stu-id="235f3-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="235f3-351">Como alternativa, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="235f3-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="235f3-352">Adicione os seguintes elementos para o `SecurityClasses` seção *Web\_MediumTrust.config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="235f3-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="235f3-353">Criar um novo conjunto de permissões na *Web\_MediumTrust.config* arquivo com as permissões necessárias a seguir:</span><span class="sxs-lookup"><span data-stu-id="235f3-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="235f3-354">Aplicar o conjunto de permissões para o SQL Server Compact, colocando os seguintes elementos *Web\_MediumTrust.config* arquivo:</span><span class="sxs-lookup"><span data-stu-id="235f3-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="235f3-355">Problema: Aplicativos da web da galeria e PhpBB exibem um erro "O serviço não está disponível" após a publicação</span><span class="sxs-lookup"><span data-stu-id="235f3-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="235f3-356">Em algumas circunstâncias, a publicação de um aplicativo faz com que um erro "serviço indisponível".</span><span class="sxs-lookup"><span data-stu-id="235f3-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="235f3-357">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-357">**Workaround**</span></span>  
> <span data-ttu-id="235f3-358">No WebMatrix, adicionar uma barra invertida (\) ao final do nome do servidor do **configurações de publicação** janela e, em seguida, publicar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="235f3-359">Problema: Layout de site do Moodle e links são desfeitos após a publicação</span><span class="sxs-lookup"><span data-stu-id="235f3-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="235f3-360">Depois de publicar um aplicativo Moodle, o aplicativo não funciona corretamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="235f3-361">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-361">**Workaround**</span></span>  
> <span data-ttu-id="235f3-362">No WebMatrix, adicione uma barra (/) ao final do **nome do Site** campo o **configurações de publicação** janela e, em seguida, publicar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="235f3-363">Problema: O nopCommerce publicação falhará com um erro de banco de dados</span><span class="sxs-lookup"><span data-stu-id="235f3-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="235f3-364">Publicação nopCommerce falhar e relata um erro de banco de dados, como "inserir o nop\_tabela de log falhou."</span><span class="sxs-lookup"><span data-stu-id="235f3-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="235f3-365">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="235f3-366">No WebMatrix, clique em **executar** para iniciar o nopCommerce localmente.</span><span class="sxs-lookup"><span data-stu-id="235f3-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="235f3-367">Faça logon na página de administração.</span><span class="sxs-lookup"><span data-stu-id="235f3-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="235f3-368">Clique o **sistema** menu.</span><span class="sxs-lookup"><span data-stu-id="235f3-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="235f3-369">Clique o **Log** opção.</span><span class="sxs-lookup"><span data-stu-id="235f3-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="235f3-370">Clique o **Limpar Log** botão.</span><span class="sxs-lookup"><span data-stu-id="235f3-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="235f3-371">Publique o nopCommerce novamente.</span><span class="sxs-lookup"><span data-stu-id="235f3-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="235f3-372">Problema: O Silverstripe CMS exibe um "Erro HTTP 500 PHP FCGI" quando você baixa um site publicado</span><span class="sxs-lookup"><span data-stu-id="235f3-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="235f3-373">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-373">**Workaround**</span></span>  
> <span data-ttu-id="235f3-374">Depois de clicar em **site publicado do Download**, ignore `silverstripe-cache/manifest_main` na **Publicar visualização**.</span><span class="sxs-lookup"><span data-stu-id="235f3-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="235f3-375">Esse arquivo é usado para fins de cache e é específico para cada computador.</span><span class="sxs-lookup"><span data-stu-id="235f3-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="235f3-376">Problema: Subtexto exibe "Erro de servidor no aplicativo '/'" quando você baixa um site publicado</span><span class="sxs-lookup"><span data-stu-id="235f3-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="235f3-377">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-377">**Workaround**</span></span>  
> <span data-ttu-id="235f3-378">Abra o site *Web. config* de arquivo e substitua a ID de usuário e senha na cadeia de conexão de banco de dados com as credenciais de administrador do SQL Server (as credenciais de "sa").</span><span class="sxs-lookup"><span data-stu-id="235f3-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="235f3-379">Como alternativa, siga estas etapas para conceder a conta de usuário que você efetuou logon com `db_owner` permissões:</span><span class="sxs-lookup"><span data-stu-id="235f3-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="235f3-380">Instale o SQL Server Management Studio usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="235f3-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="235f3-381">Conectar-se à instância local do SQL Server Express (por padrão, `.\SQLEXPRESS`).</span><span class="sxs-lookup"><span data-stu-id="235f3-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="235f3-382">Clique em **bancos de dados** &gt; *[localSubtextDatabase]* &gt; **segurança** &gt; **usuários** &gt; *[localSubtextUser*] (o padrão é `subtextuser`], mouse e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="235f3-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="235f3-383">Selecione **db\_proprietário** na seção de associação de função.</span><span class="sxs-lookup"><span data-stu-id="235f3-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="235f3-384">Problema: Site pode não funcionar após a publicação se o campo "URL de destino" não é prefixado com http:// ou https://</span><span class="sxs-lookup"><span data-stu-id="235f3-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="235f3-385">No **configurações de publicação** caixa de diálogo, se a URL de destino não começa com `http://` ou `https://`, o site pode não funcionar após a implantação.</span><span class="sxs-lookup"><span data-stu-id="235f3-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="235f3-386">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-386">**Workaround**</span></span>  
> <span data-ttu-id="235f3-387">Certifique-se de que antes de publicar um site, a URL de destino na **configurações de publicação** caixa de diálogo começa com `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="235f3-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="235f3-388">Problema: Um banco de dados MySQL de publicação falha com o erro "Falha ao publicar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="235f3-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="235f3-389">Isso pode acontecer se o banco de dados remoto não é possível executar o script."</span><span class="sxs-lookup"><span data-stu-id="235f3-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="235f3-390">O erro pode ocorrer por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="235f3-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="235f3-391">Um motivo que você pode ver esse erro é se o script de banco de dados contém um caractere de aspas simples (') e o conjunto de caracteres de padrão de destino MySQL do banco de dados não está em UTF-8.</span><span class="sxs-lookup"><span data-stu-id="235f3-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="235f3-392">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-392">**Workaround**</span></span>  
> <span data-ttu-id="235f3-393">Defina o caractere padrão definido para o banco de dados remoto do MySQL como UTF-8.</span><span class="sxs-lookup"><span data-stu-id="235f3-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="235f3-394">Problema: Alguns links não são visíveis no DotNetNuke depois de publicar ou baixando o site</span><span class="sxs-lookup"><span data-stu-id="235f3-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="235f3-395">Se você publica ou baixar um site DotNetNuke, você talvez precise limpar o cache para obter novos links sejam exibidos no site.</span><span class="sxs-lookup"><span data-stu-id="235f3-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="235f3-396">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="235f3-397">Faça logon como "Host".</span><span class="sxs-lookup"><span data-stu-id="235f3-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="235f3-398">Vá para o menu de host e selecione **configurações de Host**.</span><span class="sxs-lookup"><span data-stu-id="235f3-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="235f3-399">Role para baixo e, sob **configurações avançadas**, expanda **configurações de desempenho**.</span><span class="sxs-lookup"><span data-stu-id="235f3-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="235f3-400">Clique o **Limpar Cache** link para as páginas.</span><span class="sxs-lookup"><span data-stu-id="235f3-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="235f3-401">Vá até a parte inferior da página e reiniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="235f3-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="235f3-402">Problema: O AtomSite alguns links foram interrompidos após o download de um site publicado</span><span class="sxs-lookup"><span data-stu-id="235f3-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="235f3-403">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-403">**Workaround**</span></span>  
> <span data-ttu-id="235f3-404">No *service.config* arquivo, *users.config* arquivo e todos os *. XML* arquivos, substitua a cadeia de caracteres de URL (por exemplo, `http://myhost.com/atomsite`) com um local (por exemplo, `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="235f3-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="235f3-405">Problema: Aplicativos com base em MySQL, como o WordPress não conseguem publicar e relatar um erro de banco de dados</span><span class="sxs-lookup"><span data-stu-id="235f3-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="235f3-406">Por padrão, o WebMatrix instala MySQL com o conjunto de caracteres UTF-8.</span><span class="sxs-lookup"><span data-stu-id="235f3-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="235f3-407">Se você instalar o MySQL por conta própria, e o conjunto de caracteres não é UTF-8 (por exemplo, é Latin1), o processo de publicação para bancos de dados poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="235f3-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="235f3-408">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="235f3-409">Altere o conjunto de caracteres para MySQL para UTF-8.</span><span class="sxs-lookup"><span data-stu-id="235f3-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="235f3-410">(Para obter detalhes, consulte [servidor do conjunto de caracteres e agrupamento](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) no site do MySQL.)</span><span class="sxs-lookup"><span data-stu-id="235f3-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="235f3-411">Reinstale o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="235f3-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="235f3-412">Republique o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="235f3-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="235f3-413">Problema: "Baixar site publicado" Falha para aplicativos que têm a instalação baseada em navegador</span><span class="sxs-lookup"><span data-stu-id="235f3-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="235f3-414">Alguns aplicativos (por exemplo, o Kentico CMS) exigem que você iniciá-los no navegador para executar a instalação após a instalação, como a criação de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="235f3-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="235f3-415">Se você publicar um aplicativo como este, sem concluir a instalação baseada em navegador, a tentativa de baixar o mesmo site de um servidor remoto falhará.</span><span class="sxs-lookup"><span data-stu-id="235f3-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="235f3-416">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-416">**Workaround**</span></span>  
> <span data-ttu-id="235f3-417">Conclua a instalação baseada em navegador antes de publicar o site.</span><span class="sxs-lookup"><span data-stu-id="235f3-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="235f3-418">Problema: "Baixar site publicado" falhará com um erro de banco de dados para o DotNetNuke e Kooboo CMS</span><span class="sxs-lookup"><span data-stu-id="235f3-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="235f3-419">Se você tentar baixar um aplicativo de um servidor e ter credenciais de administrador na cadeia de conexão de banco de dados na **configurações de publicação** caixa de diálogo, você poderá ver o seguinte erro no log de publicação:</span><span class="sxs-lookup"><span data-stu-id="235f3-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="235f3-420">**Solução alternativa**</span><span class="sxs-lookup"><span data-stu-id="235f3-420">**Workaround**</span></span>  
> <span data-ttu-id="235f3-421">Se for prático, republique o site (ou publicá-lo) usando as credenciais de não administrador para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="235f3-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="235f3-422">Para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="235f3-422">For More Information</span></span>

<span data-ttu-id="235f3-423">Para obter mais informações sobre o WebMatrix 1.0, consulte os seguintes sites:</span><span class="sxs-lookup"><span data-stu-id="235f3-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="235f3-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="235f3-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="235f3-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="235f3-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="235f3-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="235f3-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="235f3-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="235f3-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="235f3-428">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="235f3-428">All Rights Reserved.</span></span> <span data-ttu-id="235f3-429">[Termos de uso](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="235f3-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
