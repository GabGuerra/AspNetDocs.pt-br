---
title: Desenvolver aplicativos ASP.NET Core usando um observador de arquivo
author: rick-anderson
description: Este tutorial demonstra como instalar e usar a ferramenta observador de arquivo (observação de dotnet) da CLI do .NET Core em um aplicativo do ASP.NET Core.
ms.author: riande
ms.date: 05/31/2018
uid: tutorials/dotnet-watch
ms.openlocfilehash: f1e0d91b27df4af7cbfb6f2547c94c0370c65d0d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029583"
---
# <a name="develop-aspnet-core-apps-using-a-file-watcher"></a>Desenvolver aplicativos ASP.NET Core usando um observador de arquivo

Por [Rick Anderson](https://twitter.com/RickAndMSFT) e [Victor Hurdugaci](https://twitter.com/victorhurdugaci)

`dotnet watch` é uma ferramenta que executa um comando do [CLI do .NET Core](/dotnet/core/tools) quando os arquivos de origem são alterados. Por exemplo, uma alteração de arquivo pode disparar uma compilação, execução de teste ou uma implantação.

Este tutorial usa um aplicativo de API Web existente com dois pontos de extremidade: um que retorna uma soma e outro que retorna um produto. O método de produto tem um bug, que é corrigido neste tutorial.

Baixe o [aplicativo de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/dotnet-watch/sample). Ele é composto por dois projetos: *WebApp* (uma API Web do ASP.NET Core) e *WebAppTests* (testes de unidade para a API Web).

Em um shell de comando, navegue até a pasta *WebApp*. Execute o seguinte comando:

```console
dotnet run
```

O resultado do console mostra mensagens semelhantes à seguinte (indicando que o aplicativo está em execução e aguarda solicitações):

```console
$ dotnet run
Hosting environment: Development
Content root path: C:/Docs/aspnetcore/tutorials/dotnet-watch/sample/WebApp
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Em um navegador da Web, navegue até `http://localhost:<port number>/api/math/sum?a=4&b=5`. Você deve ver o resultado de `9`.

Navegue para o API do produto (`http://localhost:<port number>/api/math/product?a=4&b=5`). Ele retorna `9`, não `20`, conforme o esperado. Esse problema é corrigido mais adiante no tutorial.

::: moniker range="<= aspnetcore-2.0"

## <a name="add-dotnet-watch-to-a-project"></a>Adicionar `dotnet watch` a um projeto

A ferramenta de observador de arquivo `dotnet watch` está incluída com a versão 2.1.300 do SDK do .NET Core. As etapas a seguir são necessárias ao usar uma versão anterior do SDK do .NET Core.

1. Adicionar uma referência ao pacote de `Microsoft.DotNet.Watcher.Tools` para o arquivo *.csproj*:

    ```xml
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>
    ```

1. Instale o pacote `Microsoft.DotNet.Watcher.Tools` executando o seguinte comando:

    ```console
    dotnet restore
    ```

::: moniker-end

## <a name="run-net-core-cli-commands-using-dotnet-watch"></a>Executar os comandos da CLI do .NET Core usando `dotnet watch`

Qualquer [comando da CLI do .NET Core](/dotnet/core/tools#cli-commands) pode ser executado com `dotnet watch`. Por exemplo:

| Comando | Comando com inspeção |
| ---- | ----- |
| dotnet run | dotnet watch run |
| dotnet run -f netcoreapp2.0 | dotnet watch run -f netcoreapp2.0 |
| dotnet run -f netcoreapp2.0 -- --arg1 | dotnet watch run -f netcoreapp2.0 -- --arg1 |
| dotnet test | dotnet watch test |

Executar `dotnet watch run` na pasta *WebApp*. O resultado do console indica que `watch` foi iniciado.

## <a name="make-changes-with-dotnet-watch"></a>Fazer alterações com `dotnet watch`

Verifique se `dotnet watch` está em execução.

Corrija o bug no método `Product` do *MathController.cs* para que ele retorne o produto e não a soma:

```csharp
public static int Product(int a, int b)
{
  return a * b;
}
```

Salve o arquivo. O resultado do console indica que o `dotnet watch` detectou uma alteração de arquivo e reiniciou o aplicativo.

Verifique se `http://localhost:<port number>/api/math/product?a=4&b=5` retorna o resultado correto.

## <a name="run-tests-using-dotnet-watch"></a>Executar testes usando o `dotnet watch`

1. Altere o método `Product` de *MathController.cs* de volta para retornar a soma. Salve o arquivo.
1. Em um shell de comando, navegue até a pasta *WebAppTests*.
1. Execute [dotnet restore](/dotnet/core/tools/dotnet-restore).
1. Execute `dotnet watch test`. Seu resultado indica que um teste falhou e que o observador está aguardando as alterações de arquivo:

     ```console
     Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
     Test Run Failed.
     ```

1. Corrija o código do método `Product` para que ele retorne o produto. Salve o arquivo.

`dotnet watch` detecta a alteração de arquivo e executa os testes novamente. O resultado do console indica a aprovação nos testes.

## <a name="customize-files-list-to-watch"></a>Personalizar lista de arquivos a observar

Por padrão, o `dotnet-watch` controla todos os arquivos que correspondem aos seguintes padrões glob:

* `**/*.cs`
* `*.csproj`
* `**/*.resx`

Mais itens podem ser adicionados à lista de inspeção editando o arquivo *.csproj*. Os itens podem ser especificados individualmente ou usando padrões glob.

```xml
<ItemGroup>
    <!-- extends watching group to include *.js files -->
    <Watch Include="**\*.js" Exclude="node_modules\**\*;**\*.js.map;obj\**\*;bin\**\*" />
</ItemGroup>
```

## <a name="opt-out-of-files-to-be-watched"></a>Recusa de arquivos a serem observados

`dotnet-watch` pode ser configurado para ignorar as configurações padrão. Para ignorar arquivos específicos, adicione o atributo `Watch="false"` à definição de um item no arquivo *.csproj*:

```xml
<ItemGroup>
    <!-- exclude Generated.cs from dotnet-watch -->
    <Compile Include="Generated.cs" Watch="false" />

    <!-- exclude Strings.resx from dotnet-watch -->
    <EmbeddedResource Include="Strings.resx" Watch="false" />

    <!-- exclude changes in this referenced project -->
    <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj" Watch="false" />
</ItemGroup>
```

## <a name="custom-watch-projects"></a>Projetos de inspeção personalizados

`dotnet-watch` não é restrito a projetos C#. Projetos de inspeção personalizados podem ser criados para lidar com cenários diferentes. Considere o layout de projeto a seguir:

* **test/**
  * *UnitTests/UnitTests.csproj*
  * *IntegrationTests/IntegrationTests.csproj*

Se a meta é observar ambos os projetos, crie um arquivo de projeto personalizados configurado para observar os dois projetos:

```xml
<Project>
    <ItemGroup>
        <TestProjects Include="**\*.csproj" />
        <Watch Include="**\*.cs" />
    </ItemGroup>

    <Target Name="Test">
        <MSBuild Targets="VSTest" Projects="@(TestProjects)" />
    </Target>

    <Import Project="$(MSBuildExtensionsPath)\Microsoft.Common.targets" />
</Project>
```

Para iniciar a observação de arquivo em ambos os projetos, mude para a pasta de *teste*. Execute o seguinte comando:

```console
dotnet watch msbuild /t:Test
```

O VSTest é executado quando há qualquer mudança de arquivo no projeto de teste.

## <a name="dotnet-watch-in-github"></a>`dotnet-watch` no GitHub

`dotnet-watch` faz parte do [repositório aspnet/AspNetCore](https://github.com/aspnet/AspNetCore/tree/master/src/Tools/dotnet-watch) do GitHub.
