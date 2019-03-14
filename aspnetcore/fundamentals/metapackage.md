---
title: Metapacote Microsoft.AspNetCore.All para ASP.NET Core 2.0
author: Rick-Anderson
description: O metapacote Microsoft.AspNetCore.All não é recomendado para o ASP.NET Core 2.1 e posterior.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064853"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>Metapacote Microsoft.AspNetCore.All para ASP.NET Core 2.0

> [!NOTE]
> Recomendamos que os aplicativos direcionados ao ASP.NET Core 2.1 e posterior usem o [metapacote Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) em vez desse pacote. Veja [Migração do Microsoft.AspNetCore.All para Microsoft.AspNetCore.App](#migrate) neste artigo.

Este recurso exige o ASP.NET Core 2.x direcionado ao .NET Core 2.x.

O [Metapacote do Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) para ASP.NET Core inclui:

* Todos os pacotes com suporte da equipe do ASP.NET Core.
* Todos os pacotes com suporte pelo Entity Framework Core.
* Dependências internas e de terceiros usadas por ASP.NET Core e pelo Entity Framework Core.

Todos os recursos do ASP.NET Core 2.x e do Entity Framework Core 2.x são incluídos no pacote `Microsoft.AspNetCore.All`. Os modelos de projeto padrão direcionados para ASP.NET Core 2.0 usam este pacote.

O número de versão do metapacote `Microsoft.AspNetCore.All` representa a versão do ASP.NET Core e a versão do Entity Framework Core.

Aplicativos que usam o metapacote `Microsoft.AspNetCore.All` aproveitam automaticamente o novo [Repositório de Tempo de Execução do .NET Core](/dotnet/core/deploying/runtime-store). O Repositório de Tempo de Execução contém todos os ativos de tempo de execução necessários para executar aplicativos ASP.NET Core 2.x. Quando você usa o metapacote `Microsoft.AspNetCore.All`, **nenhum** ativo dos pacotes NuGet do ASP.NET Core referenciados é implantado com o aplicativo &mdash;, porque o Repositório de Tempo de Execução do .NET Core contém esse ativos. Os ativos no Repositório de Tempo de Execução são pré-compilados para melhorar o tempo de inicialização do aplicativo.

Use o processo de filtragem de pacote para remover os pacotes não utilizados. Pacotes filtrados são excluídos na saída do aplicativo publicado.

O seguinte arquivo *.csproj* referencia os metapacotes `Microsoft.AspNetCore.All` para o ASP.NET Core:

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a>Controle de versão implícita

No ASP.NET Core 2.1 ou posterior, você pode especificar a referência de pacote `Microsoft.AspNetCore.All` sem uma versão. Quando a versão não for especificada, uma versão implícita será especificada pelo SDK (`Microsoft.NET.Sdk.Web`). Recomendamos que você conte com a versão implícita especificada pelo SDK, e não defina explicitamente o número de versão na referência de pacote. Caso tenha dúvidas sobre essa abordagem, deixe um comentário no GitHub na [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430) (Discussão sobre a versão implícita do Microsoft.AspNetCore.App).

A versão implícita é definida como `major.minor.0` para aplicativos portátil. O mecanismo de roll forward da estrutura compartilhada executará o aplicativo na versão compatível mais recente entre as estruturas compartilhadas instaladas. Para garantir que a mesma versão seja usada no desenvolvimento, no teste e na produção, certifique-se de que a mesma versão da estrutura compartilhada seja instalada em todos os ambientes. Para aplicativos autossuficientes, o número de versão implícita é definido como o `major.minor.patch` da estrutura compartilhada agrupada no SDK instalado.

A especificação de um número de versão na referência de pacote `Microsoft.AspNetCore.All` **não** assegura que a versão da estrutura compartilhada será escolhida. Por exemplo, suponha que a versão "2.1.1" foi especificada, mas "2.1.3" está instalada. Nesse caso, o aplicativo usará "2.1.3". Embora não seja recomendado, você pode desabilitar o roll forward (patch e/ou secundária). Para obter mais informações sobre como efetuar roll forward do host dotnet e como configurar seu comportamento, veja [Efetuar roll forward do host dotnet](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).

O SDK do projeto precisa ser definido como `Microsoft.NET.Sdk.Web` no arquivo de projeto para usar a versão implícita do `Microsoft.AspNetCore.All`. Quando o SDK `Microsoft.NET.Sdk` for especificado (`<Project Sdk="Microsoft.NET.Sdk">` na parte superior do arquivo de projeto), o seguinte aviso será gerado:

*Aviso NU1604: Dependência de projeto Microsoft.AspNetCore.All não contém um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.*

Esse é um problema conhecido com o SDK do .NET Core 2.1 e será corrigido no SDK do .NET Core 2.2.

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a>Migração do Microsoft.AspNetCore.All para Microsoft.AspNetCore.App

Os pacotes a seguir estão incluídos no `Microsoft.AspNetCore.All`, mas não no pacote `Microsoft.AspNetCore.App`.

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

Para mover de `Microsoft.AspNetCore.All` para `Microsoft.AspNetCore.App`, se seu aplicativo usa APIs dos pacotes acima ou de pacotes trazidos por eles, adicione referências a eles em seu projeto.

Todas as dependências dos pacotes anteriores que, de outra forma, não são dependências de `Microsoft.AspNetCore.App` não são incluídas implicitamente. Por exemplo:

* `StackExchange.Redis` como uma dependência de `Microsoft.Extensions.Caching.Redis`
* `Microsoft.ApplicationInsights` como uma dependência de `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`

## <a name="update-aspnet-core-21"></a>Atualizar o ASP.NET Core 2.1

É recomendável migrar para o metapacote `Microsoft.AspNetCore.App` para a versão 2.1 e posteriores. Para continuar usando o metapacote `Microsoft.AspNetCore.All` e certificar-se de que a versão de patch mais recente foi implantada:

* Em computadores de desenvolvimento e servidores de compilação: Instale o versão mais recente [SDK do .NET Core](https://www.microsoft.com/net/download).
* Nos servidores de implantação: Instale o versão mais recente [tempo de execução do .NET Core](https://www.microsoft.com/net/download).
 Seu aplicativo efetuará roll forward para a versão instalada mais recente em uma reinicialização do aplicativo.
