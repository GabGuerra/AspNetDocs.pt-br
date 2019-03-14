---
title: Padrão de opções no ASP.NET Core
author: guardrex
description: Descubra como usar o padrão de opções para representar grupos de configurações relacionadas em aplicativos ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 02/26/2019
uid: fundamentals/configuration/options
ms.openlocfilehash: 9566ed75375bdfaa9d6d8bf898b9fb2054356017
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065213"
---
# <a name="options-pattern-in-aspnet-core"></a>Padrão de opções no ASP.NET Core

Por [Luke Latham](https://github.com/guardrex)

::: moniker range="<= aspnetcore-1.1"

Para obter a versão 1.1 deste tópico, baixe o [Padrão de opções no ASP.NET Core (versão 1.1, PDF)](https://webpifeed.blob.core.windows.net/webpifeed/Partners/Options_1.1.pdf).

::: moniker-end

O padrão de opções usa classes para representar grupos de configurações relacionadas. Quando as [definições de configuração](xref:fundamentals/configuration/index) são isoladas por cenário em classes separadas, o aplicativo segue dois princípios importantes de engenharia de software:

* O [ISP (Princípio de Segregação da Interface) ou Encapsulamento](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#encapsulation) &ndash; os cenários (classes) que dependem das definições de configuração dependem apenas das definições de configuração usadas por eles.
* [Separação de Interesses](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#separation-of-concerns) &ndash; As configurações para diferentes partes do aplicativo não são dependentes nem acopladas entre si.

As opções também fornecem um mecanismo para validar os dados da configuração. Para obter mais configurações, consulte a seção [Validação de opções](#options-validation).

[Exibir ou baixar código de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/options/samples) ([como baixar](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>Pré-requisitos

Referencie o [metapacote Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) ou adicione uma referência de pacote ao pacote [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/).

## <a name="options-interfaces"></a>Interfaces de opções

O <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> é usado para recuperar as opções e gerenciar notificações de opções para instâncias de `TOptions`. O <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> dá suporte aos seguintes cenários:

* Notificações de alteração
* [Opções nomeadas](#named-options-support-with-iconfigurenamedoptions)
* [Configuração recarregável](#reload-configuration-data-with-ioptionssnapshot)
* Invalidação seletiva de opções (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1>)

Os cenários de [Pós-configuração](#options-post-configuration) permitem que você defina ou altere as opções depois de todas as configurações do <xref:Microsoft.Extensions.Options.IConfigureOptions`1> serem feitas.

O <xref:Microsoft.Extensions.Options.IOptionsFactory`1> é responsável por criar novas instâncias de opções. Ele tem um único método <xref:Microsoft.Extensions.Options.IOptionsFactory`1.Create*>. A implementação padrão usa todos os <xref:Microsoft.Extensions.Options.IConfigureOptions`1> e <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1> registrados e executa todas as configurações primeiro, seguidas da pós-configuração. Ela faz distinção entre <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> e <xref:Microsoft.Extensions.Options.IConfigureOptions`1> e chama apenas a interface apropriada.

O <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> é usado pelo <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> para armazenar em cache as instâncias do `TOptions`. O <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1> invalida as instâncias de opções no monitor, de modo que o valor seja recalculado (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryRemove*>). Os valores podem ser manualmente inseridos com <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.TryAdd*>. O método <xref:Microsoft.Extensions.Options.IOptionsMonitorCache`1.Clear*> é usado quando todas as instâncias nomeadas devem ser recriadas sob demanda.

O <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> é útil em cenários em que as opções devam ser novamente computadas em cada solicitação. Para saber mais, consulte a seção [Recarregar dados de configuração com IOptionsSnapshot](#reload-configuration-data-with-ioptionssnapshot).

O <xref:Microsoft.Extensions.Options.IOptions`1> pode ser usado para dar suporte a opções. No entanto, o <xref:Microsoft.Extensions.Options.IOptions`1> não dá suporte a cenários anteriores do <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>. Você pode continuar a usar o <xref:Microsoft.Extensions.Options.IOptions`1> em estruturas e bibliotecas existentes que já usam a interface do <xref:Microsoft.Extensions.Options.IOptions`1> e não exigem os cenários fornecidos pelo <xref:Microsoft.Extensions.Options.IOptionsMonitor`1>.

## <a name="general-options-configuration"></a>Configuração de opções gerais

A configuração de opções gerais é demonstrada no Exemplo &num;1 no aplicativo de exemplo.

Uma classe de opções deve ser não abstrata e com um construtor público sem parâmetros. A classe a seguir, `MyOptions`, tem duas propriedades, `Option1` e `Option2`. A configuração de valores padrão é opcional, mas o construtor de classe no exemplo a seguir define o valor padrão de `Option1`. `Option2` tem um valor padrão definido com a inicialização da propriedade diretamente (*Models/MyOptions.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptions.cs?name=snippet1)]

A classe `MyOptions` é adicionada ao contêiner de serviço com <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure*> e associada à configuração:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example1)]

O seguinte modelo de página usa a [injeção de dependência de construtor](xref:mvc/controllers/dependency-injection) com <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> para acessar as configurações (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example1)]

O arquivo *appsettings.json* de exemplo especifica valores para `option1` e `option2`:

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=2-3)]

Quando o aplicativo é executado, o método `OnGet` do modelo de página retorna uma cadeia de caracteres que mostra os valores da classe de opção:

```html
option1 = value1_from_json, option2 = -1
```

> [!NOTE]
> Ao usar um <xref:System.Configuration.ConfigurationBuilder> personalizado para carregar opções de configuração de um arquivo de configurações, confirme se o caminho de base está corretamente configurado:
>
> ```csharp
> var configBuilder = new ConfigurationBuilder()
>    .SetBasePath(Directory.GetCurrentDirectory())
>    .AddJsonFile("appsettings.json", optional: true);
> var config = configBuilder.Build();
>
> services.Configure<MyOptions>(config);
> ```
>
> Não é necessário configurar o caminho de base explicitamente ao carregar opções de configuração do arquivo de configurações por meio do <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.

## <a name="configure-simple-options-with-a-delegate"></a>Configurar opções simples com um delegado

A configuração de opções simples com um delegado é demonstrada no Exemplo &num;2 no aplicativo de exemplo.

Use um delegado para definir valores de opções. O aplicativo de exemplo usa a classe `MyOptionsWithDelegateConfig` (*Models/MyOptionsWithDelegateConfig.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MyOptionsWithDelegateConfig.cs?name=snippet1)]

No código a seguir, um segundo serviço <xref:Microsoft.Extensions.Options.IConfigureOptions`1> é adicionado ao contêiner de serviço. Ele usa um delegado para configurar a associação com `MyOptionsWithDelegateConfig`:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example2)]

*Index.cshtml.cs*:

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3,9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example2)]

Adicione vários provedores de configuração. Os provedores de configuração estão disponíveis nos pacotes do NuGet e são aplicados na ordem em que são registrados. Para obter mais informações, consulte <xref:fundamentals/configuration/index>.

Cada chamada à <xref:Microsoft.Extensions.Options.IConfigureOptions`1.Configure*> adiciona um serviço <xref:Microsoft.Extensions.Options.IConfigureOptions`1> ao contêiner de serviço. No exemplo anterior, os valores `Option1` e `Option2` são especificados em *appsettings.json*, mas os valores `Option1` e `Option2` são substituídos pelo delegado configurado.

Quando mais de um serviço de configuração é habilitado, a última fonte de configuração especificada *vence* e define o valor de configuração. Quando o aplicativo é executado, o método `OnGet` do modelo de página retorna uma cadeia de caracteres que mostra os valores da classe de opção:

```html
delegate_option1 = value1_configured_by_delgate, delegate_option2 = 500
```

## <a name="suboptions-configuration"></a>Configuração de subopções

A configuração de subopções é demonstrada no Exemplo &num;3 no aplicativo de exemplo.

Os aplicativos devem criar classes de opções que pertencem a grupos de cenários específicos (classes) no aplicativo. Partes do aplicativo que exigem valores de configuração devem ter acesso apenas aos valores de configuração usados por elas.

Ao associar opções à configuração, cada propriedade no tipo de opções é associada a uma chave de configuração do formato `property[:sub-property:]`. Por exemplo, a propriedade `MyOptions.Option1` é associada à chave `Option1`, que é lida da propriedade `option1` em *appsettings.json*.

No código a seguir, um terceiro serviço <xref:Microsoft.Extensions.Options.IConfigureOptions`1> é adicionado ao contêiner de serviço. Ele associa `MySubOptions` à seção `subsection` do arquivo *appsettings.json*:

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example3)]

O método de extensão `GetSection` exige o pacote NuGet [Microsoft.Extensions.Options.ConfigurationExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Options.ConfigurationExtensions/). Se o aplicativo usa o [metapacote Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) (ASP.NET Core 2.1 ou posterior), o pacote é automaticamente incluído.

O arquivo *appsettings.json* de exemplo define um membro `subsection` com chaves para `suboption1` e `suboption2`:

[!code-json[](options/samples/2.x/OptionsSample/appsettings.json?highlight=4-7)]

A classe `MySubOptions` define as propriedades `SubOption1` e `SubOption2`, para armazenar os valores de opções (*Models/MySubOptions.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Models/MySubOptions.cs?name=snippet1)]

O método `OnGet` do modelo da página retorna uma cadeia de caracteres com os valores de opções (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=4,10)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example3)]

Quando o aplicativo é executado, o método `OnGet` retorna uma cadeia de caracteres que mostra os valores da classe de subopção:

```html
subOption1 = subvalue1_from_json, subOption2 = 200
```

## <a name="options-provided-by-a-view-model-or-with-direct-view-injection"></a>Opções fornecidas por um modelo de exibição ou com a injeção de exibição direta

As opções fornecidas por um modelo de exibição ou com a injeção de exibição direta são demonstradas no Exemplo &num;4 no aplicativo de exemplo.

As opções podem ser fornecidas em um modelo de exibição ou pela injeção de <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> diretamente em uma exibição (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=9)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=2,8)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example4)]

O aplicativo de exemplo mostra como injetar `IOptionsMonitor<MyOptions>` com uma diretiva `@inject`:

[!code-cshtml[](options/samples/2.x/OptionsSample/Pages/Index.cshtml?range=1-10&highlight=4)]

Quando o aplicativo é executado, os valores de opções são mostrados na página renderizada:

![Os valores de opções Option1: value1_from_json e Option2: -1 são carregados do modelo e pela injeção na exibição.](options/_static/view.png)

## <a name="reload-configuration-data-with-ioptionssnapshot"></a>Recarregar dados de configuração com IOptionsSnapshot

O recarregamento de dados de configuração com <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> é demonstrado no Exemplo &num;5 no aplicativo de exemplo.

O <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> dá suporte a opções de recarregamento com sobrecarga mínima de processamento.

As opções são calculadas uma vez por solicitação, quando acessadas e armazenadas em cache durante o tempo de vida da solicitação.

O exemplo a seguir demonstra como um novo <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1> é criado após a alteração de *appsettings.json* (*Pages/Index.cshtml.cs*). Várias solicitações ao servidor retornam valores de constante fornecidos pelo arquivo *appsettings.json*, até que o arquivo seja alterado e a configuração seja recarregada.

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=12)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=5,11)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example5)]

A seguinte imagem mostra is valores `option1` e `option2` iniciais carregados do arquivo *appsettings.json*:

```html
snapshot option1 = value1_from_json, snapshot option2 = -1
```

Altere os valores no arquivo *appsettings.json* para `value1_from_json UPDATED` e `200`. Salve o arquivo *appsettings.json*. Atualize o navegador para ver se os valores de opções foram atualizados:

```html
snapshot option1 = value1_from_json UPDATED, snapshot option2 = 200
```

## <a name="named-options-support-with-iconfigurenamedoptions"></a>Suporte de opções nomeadas com IConfigureNamedOptions

O suporte de opções nomeadas com <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> é demonstrado como no Exemplo &num;6 no aplicativo de exemplo.

O suporte de *opções nomeadas* permite que o aplicativo faça a distinção entre as configurações de opções nomeadas. No aplicativo de exemplo, as opções nomeadas são declaradas com [OptionsServiceCollectionExtensions.Configure](xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure*) que chama o método de extensão [ConfigureNamedOptions\<TOptions>.Configure](xref:Microsoft.Extensions.Options.ConfigureNamedOptions`1.Configure*):

[!code-csharp[](options/samples/2.x/OptionsSample/Startup.cs?name=snippet_Example6)]

O aplicativo de exemplo acessa as opções nomeadas com <xref:Microsoft.Extensions.Options.IOptionsSnapshot`1.Get*> (*Pages/Index.cshtml.cs*):

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?range=13-14)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet2&highlight=6,12-13)]

[!code-csharp[](options/samples/2.x/OptionsSample/Pages/Index.cshtml.cs?name=snippet_Example6)]

Executando o aplicativo de exemplo, as opções nomeadas são retornadas:

```html
named_options_1: option1 = value1_from_json, option2 = -1
named_options_2: option1 = named_options_2_value1_from_action, option2 = 5
```

Os valores `named_options_1` são fornecidos pela configuração, que são carregados do arquivo *appsettings.json*. Os valores `named_options_2` são fornecidos pelo:

* Delegado `named_options_2` em `ConfigureServices` para `Option1`.
* Valor padrão para `Option2` fornecido pela classe `MyOptions`.

## <a name="configure-all-options-with-the-configureall-method"></a>Configurar todas as opções com o método ConfigureAll

Configure todas as instâncias de opções com o método <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*>. O código a seguir configura `Option1` para todas as instâncias de configuração com um valor comum. Adicione o seguinte código manualmente ao método `Startup.ConfigureServices`:

```csharp
services.ConfigureAll<MyOptions>(myOptions => 
{
    myOptions.Option1 = "ConfigureAll replacement value";
});
```

A execução do aplicativo de exemplo após a adição do código produz o seguinte resultado:

```html
named_options_1: option1 = ConfigureAll replacement value, option2 = -1
named_options_2: option1 = ConfigureAll replacement value, option2 = 5
```

> [!NOTE]
> Todas as opções são instâncias nomeadas. As instâncias <xref:Microsoft.Extensions.Options.IConfigureOptions`1> existentes são tratadas como sendo direcionadas à instância `Options.DefaultName`, que é `string.Empty`. <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> também implementa <xref:Microsoft.Extensions.Options.IConfigureOptions`1>. A implementação padrão de <xref:Microsoft.Extensions.Options.IOptionsFactory`1> tem lógica para usar cada um de forma adequada. A opção nomeada `null` é usada para direcionar todas as instâncias nomeadas, em vez de uma instância nomeada específica (<xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll*> e <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*> usam essa convenção).

## <a name="optionsbuilder-api"></a>API OptionsBuilder

<xref:Microsoft.Extensions.Options.OptionsBuilder`1> é usada para configurar instâncias `TOptions`. `OptionsBuilder` simplifica a criação de opções nomeadas, pois é apenas um único parâmetro para a chamada `AddOptions<TOptions>(string optionsName)` inicial, em vez de aparecer em todas as chamadas subsequentes. A validação de opções e as sobrecargas `ConfigureOptions` que aceitam dependências de serviço só estão disponíveis por meio de `OptionsBuilder`.

```csharp
// Options.DefaultName = "" is used.
services.AddOptions<MyOptions>().Configure(o => o.Property = "default");

services.AddOptions<MyOptions>("optionalName")
    .Configure(o => o.Property = "named");
```

## <a name="use-di-services-to-configure-options"></a>Usar os serviços de injeção de dependência para configurar as opções

Você pode acessar outros serviços de injeção de dependência ao configurar as opções de duas maneiras:

* Passar um delegado de configuração para [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) em [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1). [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder`1) fornece sobrecargas de [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) que permitem que você use até cinco serviços para configurar as opções:

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<Service1, Service2, Service3, Service4, Service5>(
          (o, s, s2, s3, s4, s5) => 
              o.Property = DoSomethingWith(s, s2, s3, s4, s5));
  ```

* Criar seu próprio tipo que implementa <xref:Microsoft.Extensions.Options.IConfigureOptions`1> ou <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1> e registrar o tipo como um serviço.

É recomendável transmitir um delegado de configuração para [Configurar](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*), já que a criação de um serviço é algo mais complexo. Criar seu próprio tipo é equivalente ao que a estrutura faz para você quando você usa [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*). Chamar [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder`1.Configure*) registra um genérico transitório <xref:Microsoft.Extensions.Options.IConfigureNamedOptions`1>, que tem um construtor que aceita os tipos de serviço genérico especificados. 

::: moniker range=">= aspnetcore-2.2"

## <a name="options-validation"></a>Validação de opções

A validação de opções permite validar as opções depois de configurá-las. Chame `Validate` com um método de validação que retorna `true` quando as opções são válidas, e `false` quando não são:

```csharp
// Registration
services.AddOptions<MyOptions>("optionalOptionsName")
    .Configure(o => { }) // Configure the options
    .Validate(o => YourValidationShouldReturnTrueIfValid(o), 
        "custom error");

// Consumption
var monitor = services.BuildServiceProvider()
    .GetService<IOptionsMonitor<MyOptions>>();
  
try
{
    var options = monitor.Get("optionalOptionsName");
}
catch (OptionsValidationException e) 
{
   // e.OptionsName returns "optionalOptionsName"
   // e.OptionsType returns typeof(MyOptions)
   // e.Failures returns a list of errors, which would contain 
   //     "custom error"
}
```

O exemplo anterior define a instância de opções nomeadas como `optionalOptionsName`. A instância de opções padrão é `Options.DefaultName`.

A validação é executada após a criação da instância de opções. A instância de opções tem garantia de passar pela validação, na primeira vez em que for acessada.

> [!IMPORTANT]
> A validação não protege contra modificações de opções, depois que as opções são inicialmente configuradas e validadas.

O método `Validate` aceita um `Func<TOptions, bool>`. Para personalizar totalmente a validação, implemente `IValidateOptions<TOptions>`, que permite:

* A validação de vários tipos de opções: `class ValidateTwo : IValidateOptions<Option1>, IValidationOptions<Option2>`
* A validação que depende de outro tipo de opção: `public DependsOnAnotherOptionValidator(IOptionsMonitor<AnotherOption> options)`

`IValidateOptions` valida:

* Uma instância específica de opções nomeadas.
* Todas as opções quando `name` for `null`.

Retornar um `ValidateOptionsResult` da implementação da interface:

```csharp
public interface IValidateOptions<TOptions> where TOptions : class
{
    ValidateOptionsResult Validate(string name, TOptions options);
}
```

A validação de anotação de dados está disponível no pacote [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) por meio da chamada do método `ValidateDataAnnotations` em `OptionsBuilder<TOptions>`. O `Microsoft.Extensions.Options.DataAnnotations` está incluído no [metapacote Microsoft.AspNetCore.App](xref:fundamentals/metapackage-app) (ASP.NET Core 2.2 ou posterior).

```csharp
private class AnnotatedOptions
{
    [Required]
    public string Required { get; set; }

    [StringLength(5, ErrorMessage = "Too long.")]
    public string StringLength { get; set; }

    [Range(-5, 5, ErrorMessage = "Out of range.")]
    public int IntRange { get; set; }
}

[Fact]
public void CanValidateDataAnnotations()
{
    var services = new ServiceCollection();
    services.AddOptions<AnnotatedOptions>()
        .Configure(o =>
        {
            o.StringLength = "111111";
            o.IntRange = 10;
            o.Custom = "nowhere";
        })
        .ValidateDataAnnotations();

    var sp = services.BuildServiceProvider();

    var error = Assert.Throws<OptionsValidationException>(() => 
        sp.GetRequiredService<IOptionsMonitor<AnnotatedOptions>>().Value);
    ValidateFailure<AnnotatedOptions>(error, Options.DefaultName, 1,
        "DataAnnotation validation failed for members Required " +
            "with the error 'The Required field is required.'.",
        "DataAnnotation validation failed for members StringLength " +
            "with the error 'Too long.'.",
        "DataAnnotation validation failed for members IntRange " +
            "with the error 'Out of range.'.");
}
```

A validação adiantada (fail fast na inicialização) está sendo considerada para uma versão futura.

::: moniker-end

## <a name="options-post-configuration"></a>Pós-configuração de opções

Defina a pós-configuração com <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1>. A pós-configuração é executada depois que toda o configuração de <xref:Microsoft.Extensions.Options.IConfigureOptions`1> é feita:

```csharp
services.PostConfigure<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

O <xref:Microsoft.Extensions.Options.IPostConfigureOptions`1.PostConfigure*> está disponível para pós-configurar opções nomeadas:

```csharp
services.PostConfigure<MyOptions>("named_options_1", myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

Use <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll*> para pós-configurar todas as instâncias de configuração:

```csharp
services.PostConfigureAll<MyOptions>(myOptions =>
{
    myOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="accessing-options-during-startup"></a>Acessando opções durante a inicialização

<xref:Microsoft.Extensions.Options.IOptions`1> e <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> podem ser usados em `Startup.Configure`, pois os serviços são criados antes da execução do método `Configure`.

```csharp
public void Configure(IApplicationBuilder app, IOptionsMonitor<MyOptions> optionsAccessor)
{
    var option1 = optionsAccessor.CurrentValue.Option1;
}
```

Não use <xref:Microsoft.Extensions.Options.IOptions`1> ou <xref:Microsoft.Extensions.Options.IOptionsMonitor`1> em `Startup.ConfigureServices`. Pode haver um estado inconsistente de opções devido à ordenação dos registros de serviço.

## <a name="additional-resources"></a>Recursos adicionais

* <xref:fundamentals/configuration/index>
