---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Criando uma cadeia de Conexão e trabalhando com LocalDB do SQL Server | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: e29fe14d2c7fafe2edb9c02029b678090ea83cc5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59403812"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="8dced-102">Criar uma cadeia de conexão e trabalhando com LocalDB do SQL Server</span><span class="sxs-lookup"><span data-stu-id="8dced-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8dced-103">por [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="8dced-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="8dced-104">Criar uma cadeia de conexão e trabalhando com LocalDB do SQL Server</span><span class="sxs-lookup"><span data-stu-id="8dced-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="8dced-105">O `MovieDBContext` classe criada por você lida com a tarefa de conectar-se ao banco de dados e mapeamento `Movie` objetos para os registros de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8dced-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="8dced-106">Uma pergunta que você pode fazer, no entanto, é como especificar qual banco de dados que ele se conectará.</span><span class="sxs-lookup"><span data-stu-id="8dced-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="8dced-107">Você realmente não precisa especificar qual banco de dados usar, Entity Framework usará como padrão [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="8dced-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="8dced-108">Nesta seção vamos explicitamente adicionar uma cadeia de caracteres de conexão na *Web. config* arquivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8dced-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="8dced-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="8dced-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="8dced-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) é uma versão leve do SQL Server Express Database Engine que é iniciado sob demanda e executado no modo de usuário.</span><span class="sxs-lookup"><span data-stu-id="8dced-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="8dced-111">LocalDB é executado em um modo de execução especial do SQL Server Express que permite que você trabalhe com bancos de dados como *mdf* arquivos.</span><span class="sxs-lookup"><span data-stu-id="8dced-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="8dced-112">Normalmente, os arquivos de banco de dados LocalDB são mantidos na *App\_dados* pasta de um projeto web.</span><span class="sxs-lookup"><span data-stu-id="8dced-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="8dced-113">SQL Server Express não é recomendado para uso em aplicativos da web de produção.</span><span class="sxs-lookup"><span data-stu-id="8dced-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="8dced-114">LocalDB em particular não deve ser usado para produção com um aplicativo web porque ela não foi projetada para trabalhar com o IIS.</span><span class="sxs-lookup"><span data-stu-id="8dced-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="8dced-115">No entanto, um banco de dados LocalDB pode ser migrado facilmente para SQL Server ou SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8dced-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="8dced-116">No Visual Studio 2017, o LocalDB é instalado por padrão com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8dced-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="8dced-117">Por padrão, o Entity Framework procura uma cadeia de caracteres de conexão que o mesmo nomeada que a classe de contexto de objeto (`MovieDBContext` para este projeto).</span><span class="sxs-lookup"><span data-stu-id="8dced-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="8dced-118">Para obter mais informações, consulte [cadeias de Conexão do SQL Server para aplicativos Web ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="8dced-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="8dced-119">Abra a raiz do aplicativo *Web. config* arquivo mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8dced-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="8dced-120">(Não o *Web. config* arquivo na *modos de exibição* pasta.)</span><span class="sxs-lookup"><span data-stu-id="8dced-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="8dced-121">Encontre o `<connectionStrings>` elemento:</span><span class="sxs-lookup"><span data-stu-id="8dced-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="8dced-122">Adicione a seguinte cadeia de conexão para o `<connectionStrings>` elemento na *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8dced-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="8dced-123">O exemplo a seguir mostra uma parte do *Web. config* arquivo com a cadeia de caracteres de conexão nova adicionada:</span><span class="sxs-lookup"><span data-stu-id="8dced-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="8dced-124">As cadeias de caracteres de duas conexão são muito semelhantes.</span><span class="sxs-lookup"><span data-stu-id="8dced-124">The two connection strings are very similar.</span></span> <span data-ttu-id="8dced-125">A primeira cadeia de caracteres de conexão é denominada `DefaultConnection` e é usado para o banco de dados de associação para controlar quem pode acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8dced-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="8dced-126">A cadeia de caracteres de conexão que você adicionou Especifica um banco de dados LocalDB denominado *Movie.mdf* localizado na *App\_dados* pasta.</span><span class="sxs-lookup"><span data-stu-id="8dced-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="8dced-127">Usamos não o banco de dados de associação neste tutorial, para obter mais informações sobre associação, autenticação e segurança, consulte o tutorial [criar um aplicativo ASP.NET MVC com autenticação e o banco de dados SQL e implantar no serviço de aplicativo do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="8dced-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="8dced-128">O nome da cadeia de caracteres de conexão deve corresponder ao nome da [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="8dced-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="8dced-129">Na verdade, não precisa adicionar o `MovieDBContext` cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="8dced-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="8dced-130">Se você não especificar uma cadeia de caracteres de conexão, o Entity Framework criará um banco de dados LocalDB no diretório de usuários com o nome totalmente qualificado do [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) classe (nesse caso, `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="8dced-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="8dced-131">Você pode nomear o banco de dados que desejar, desde que ela tenha o *. Arquivos MDF* sufixo.</span><span class="sxs-lookup"><span data-stu-id="8dced-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="8dced-132">Por exemplo, podemos pode nomear o banco de dados *MyFilms.mdf*.</span><span class="sxs-lookup"><span data-stu-id="8dced-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="8dced-133">Em seguida, você criará um novo `MoviesController` classe que você pode usar para exibir os dados de filme e permitir que usuários criem novas listagens de filme.</span><span class="sxs-lookup"><span data-stu-id="8dced-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8dced-134">[Anterior](adding-a-model.md)
> [Próximo](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="8dced-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
