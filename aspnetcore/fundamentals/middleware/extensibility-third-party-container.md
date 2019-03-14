---
title: Ativação de middleware com um contêiner de terceiros no ASP.NET Core
author: guardrex
description: Saiba como usar o middleware fortemente tipado com a ativação baseada em alocador e um contêiner de terceiros no ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 02/02/2018
uid: fundamentals/middleware/extensibility-third-party-container
ms.openlocfilehash: 6af775c66a1de7f1a4f06a4a639ade20c6493b2a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026293"
---
# <a name="middleware-activation-with-a-third-party-container-in-aspnet-core"></a>Ativação de middleware com um contêiner de terceiros no ASP.NET Core

Por [Luke Latham](https://github.com/guardrex)

Este artigo demonstra como usar o [IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) e o [IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) como um ponto de extensibilidade para a ativação do [middleware](xref:fundamentals/middleware/index) com um contêiner de terceiros. Para obter informações introdutórias sobre o `IMiddlewareFactory` e o `IMiddleware`, confira o tópico [Ativação de middleware baseada em alocador no ASP.NET Core](xref:fundamentals/middleware/extensibility).

[Exibir ou baixar código de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/middleware/extensibility-third-party-container/sample) ([como baixar](xref:index#how-to-download-a-sample))

O aplicativo de exemplo demonstra a ativação do middleware por uma implementação de `IMiddlewareFactory`, `SimpleInjectorMiddlewareFactory`. O exemplo usa o contêiner de DI (injeção de dependência) [Simple Injector](https://simpleinjector.org).

A implementação do middleware do exemplo registra o valor fornecido por um parâmetro de cadeia de consulta (`key`). O middleware usa um contexto de banco de dados injetado (um serviço com escopo) para registrar o valor da cadeia de consulta em um banco de dados em memória.

> [!NOTE]
> O aplicativo de exemplo usa o [Simple Injector](https://github.com/simpleinjector/SimpleInjector) simplesmente para fins de demonstração. O uso do Simple Injector não é um endosso. As abordagens de ativação do middleware descritas na documentação do Simple Injector e nos problemas do GitHub são recomendadas pelos mantenedores do Simple Injector. Para obter mais informações, confira a [Documentação do Simple Injector](https://simpleinjector.readthedocs.io/en/latest/index.html) e o [repositório do GitHub do Simple Injector](https://github.com/simpleinjector/SimpleInjector).

## <a name="imiddlewarefactory"></a>IMiddlewareFactory

[IMiddlewareFactory](/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory) fornece métodos para a criação do middleware.

No aplicativo de amostra, um alocador de middleware é implementado para criar uma instância de `SimpleInjectorActivatedMiddleware`. O alocador de middleware usa o contêiner do Simple Injector para resolver o middleware:

[!code-csharp[](extensibility-third-party-container/sample/Middleware/SimpleInjectorMiddlewareFactory.cs?name=snippet1&highlight=5-8,12)]

## <a name="imiddleware"></a>IMiddleware

[IMiddleware](/dotnet/api/microsoft.aspnetcore.http.imiddleware) define o middleware para o pipeline de solicitação do aplicativo.

Middleware ativado por uma implementação de `IMiddlewareFactory` (*Middleware/SimpleInjectorActivatedMiddleware.cs*):

[!code-csharp[](extensibility-third-party-container/sample/Middleware/SimpleInjectorActivatedMiddleware.cs?name=snippet1)]

Uma extensão é criada para o middleware (*Middleware/MiddlewareExtensions.cs*):

[!code-csharp[](extensibility-third-party-container/sample/Middleware/MiddlewareExtensions.cs?name=snippet1)]

O `Startup.ConfigureServices` precisa executar várias tarefas:

* Configure o contêiner do Simple Injector.
* Registre o alocador e o middleware.
* Disponibilize o contexto do banco de dados do aplicativo por meio do contêiner do Simple Injector para uma página Razor.

[!code-csharp[](extensibility-third-party-container/sample/Startup.cs?name=snippet1)]

O middleware é registrado no pipeline de processamento da solicitação em `Startup.Configure`:

[!code-csharp[](extensibility-third-party-container/sample/Startup.cs?name=snippet2&highlight=13)]

## <a name="additional-resources"></a>Recursos adicionais

* [Middleware](xref:fundamentals/middleware/index)
* [Ativação de middleware de fábrica](xref:fundamentals/middleware/extensibility)
* [Repositório do GitHub do Simple Injector](https://github.com/simpleinjector/SimpleInjector)
* [Documentação do Simple Injector](https://simpleinjector.readthedocs.io/en/latest/index.html)
