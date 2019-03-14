---
title: Compilar seu primeiro aplicativo com Razor Components
author: guardrex
description: Compile passo a passo um aplicativo com Razor Components e aprenda os conceitos básicos do Razor Components.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040773"
---
# <a name="build-your-first-razor-components-app"></a>Compilar seu primeiro aplicativo com Razor Components

Por [Daniel Roth](https://github.com/danroth27) e [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Este tutorial mostra como compilar um aplicativo com Razor Components e demonstra os conceitos básicos do Razor Components. Aproveite melhor esse tutorial usando um projeto com base em Razor Components (com suporte no .NET Core 3.0 ou posterior) ou usando um projeto com base em Blazor (com suporte em uma versão futura do .NET Core).

Para ter uma experiência de uso do Razor Components no ASP.NET Core (*recomendado*):

* Siga as orientações em <xref:razor-components/get-started> para criar um projeto com base no Razor Components.
* Nomeie o projeto `RazorComponents`.
* Uma solução com vários projetos é criada do modelo Razor Components. O projeto em Razor Components é gerado como *RazorComponents.App*.

Para ter uma experiência de uso do Blazor:

* Siga as orientações em <xref:spa/blazor/get-started> para criar um projeto com base no Blazor.
* Nomeie o projeto `Blazor`.
* Uma solução de projeto único é criada do modelo de Blazor.

[Exibir ou baixar um código de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([como baixar](xref:index#how-to-download-a-sample)). Conheça os pré-requisitos nos tópicos a seguir:

## <a name="build-components"></a>Componentes do build

1. Navegue para cada uma das três páginas do aplicativo: Início, Contador e Buscar dados. Essas páginas são implementadas por arquivos Razor na pasta *Páginas*: *Index.cshtml*, *Counter.cshtml* e *FetchData.cshtml*.

1. Na página Contador, selecione o botão **Clique aqui** para incrementar o contador sem uma atualização de página. A incrementação de um contador em uma página da Web normalmente exige JavaScript, mas o Razor Components fornece uma abordagem melhor usando C#.

1. Examine a implementação do componente Counter no arquivo *Counter.cshtml*.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   A interface do usuário do componente Counter é definida usando HTML. A lógica de renderização dinâmica (por exemplo, loops, condicionais, expressões) é adicionada usando uma sintaxe de C# inserida chamada [Razor](xref:mvc/views/razor). A marcação HTML e a lógica de renderização de C# são convertidas em uma classe de componente no momento da compilação. O nome da classe .NET gerada corresponde ao nome do arquivo.

   Os membros da classe de componente são definidos em um bloco `@functions`. No bloco `@functions`, o estado do componente (propriedades, campos) e os métodos são especificados para manipulação de eventos ou para definição de outra lógica de componente. Assim, esses membros são usados como parte da lógica de renderização do componente e para manipulação de eventos.

   Quando o botão **Clique aqui** botão é selecionado:

   * O manipulador `onclick` registrado do componente Counter é chamado (o método `IncrementCount`).
   * O componente Counter regenera sua árvore de renderização.
   * A nova árvore de renderização é comparada à anterior.
   * Apenas as modificações ao DOM (Modelo de Objeto do Documento) são aplicadas. A contagem exibida é atualizada.

1. Modifique a lógica de C# do componente Counter para que o incremento da contagem seja por dois em vez de um.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. Recompile e execute o aplicativo para ver as alterações. Selecione o botão **Clique aqui**, e o contador é incrementado em dois.

## <a name="use-components"></a>Usar componentes

Inclua um componente em outro componente usando uma sintaxe semelhante a HTML.

1. Adicione o componente Counter ao componente Index (página inicial) do aplicativo adicionando um elemento `<Counter />` ao componente Index.

   Se você estiver usando Blazor para essa experiência, um componente Survey Prompt (elemento `<SurveyPrompt>`) estará no componente Index. Substitua o elemento `<SurveyPrompt>` pelo elemento `<Counter>`.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. Recompile e execute o aplicativo. A home page tem seu próprio contador.

## <a name="component-parameters"></a>Parâmetros do componente

Componentes também podem ter parâmetros. Os parâmetros do componente são definidos usando propriedades não públicas na classe de componente decorada com `[Parameter]`. Use atributos para especificar argumentos para um componente na marcação.

1. Atualizar o código C# do componente `@functions`:

   * Adicione uma propriedade `IncrementAmount` decorada com o atributo `[Parameter]`.
   * Altere o método `IncrementCount` para usar o `IncrementAmount` ao aumentar o valor de `currentCount`.

   *Pages/Counter.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. Especifique um parâmetro `IncrementAmount` no elemento `<Counter>` do componente Home usando um atributo. Defina o valor para incrementar o contador em 10.

   *Pages/Index.cshtml*:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. Recarregue a página. O contador de página inicial é incrementado em 10 sempre que o botão **Clique aqui** é selecionado. O contador na página *Contador* aumenta em um.

## <a name="route-to-components"></a>Rotear para componentes

A diretiva `@page` no início do arquivo *Counter.cshtml* especifica que esse componente é um ponto de extremidade de roteamento. O componente Counter manipula solicitações enviadas para `/Counter`. Sem a diretiva `@page`, o componente não trata as solicitações roteadas, mas o componente ainda pode ser usado por outros componentes.

## <a name="dependency-injection"></a>Injeção de dependência

Os serviços registrados no contêiner do serviço de aplicativo estão disponíveis para componentes por meio da [DI (injeção de dependência)](xref:fundamentals/dependency-injection). Injete os serviços em um componente usando a diretiva `@inject`.

Examine as diretivas do componente FetchData (*Pages/FetchData.cshtml*). A diretiva `@inject` é usada para injetar a instância do serviço `WeatherForecastService` no componente:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

O serviço `WeatherForecastService` é registrado como um [singleton](xref:fundamentals/dependency-injection#service-lifetimes), portanto, uma instância do serviço está disponível em todo o aplicativo.

O componente FetchData usa o serviço injetado, como `ForecastService`, para recuperar uma matriz de objetos `WeatherForecast`:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

Um loop [@foreach](/dotnet/csharp/language-reference/keywords/foreach-in) é usado para renderizar cada instância de previsão como uma linha na tabela de dados meteorológicos:

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a>Criar uma lista de tarefas pendentes

Adicione uma nova página ao aplicativo que implemente uma lista de tarefas pendentes simples.

1. Adicione um arquivo vazio à pasta *Páginas* denominado *Todo.cshtml*.

1. Forneça a marcação inicial à página:

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. Adicione a página Tarefas Pendentes à barra de navegação.

   O componente NavMenu (*Shared/NavMenu.csthml*) é usado no layout do aplicativo. Layouts são componentes que permitem que você evite a duplicação de conteúdo no aplicativo. Para obter mais informações, consulte <xref:razor-components/layouts>.

   Adicione um `<NavLink>` à página de Tarefas Pendentes, incluindo a marcação de item de lista a seguir, abaixo dos itens de lista existentes no arquivo *Shared/NavMenu.csthml*:

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. Recompile e execute o aplicativo. Visite a nova página de Tarefas Pendentes para confirmar se o link para a página está funcionando.

1. Adicione um arquivo *TodoItem.cs* à raiz do projeto para manter uma classe que representará um item de tarefa pendente. Use o seguinte código C# para a classe `TodoItem`:

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. Retorne ao componente Todo (*Todo.cshtml*):

   * Adicione um campo para as tarefas pendentes em um bloco `@functions`. O componente Todo usa esse campo para manter o estado da lista de tarefas pendentes.
   * Adicione marcação da lista não ordenada e um loop `foreach` para renderizar cada item de tarefa pendente como um item de lista.

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. O aplicativo requer os elementos de interface do usuário para adicionar tarefas pendentes à lista. Adicione uma entrada de texto e um botão abaixo da lista:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. Recompile e execute o aplicativo. Nada acontece quando o botão **Adicionar tarefas pendentes** é selecionado porque nenhum manipulador de eventos está conectado ao botão.

1. Adicione um método `AddTodo` ao componente Todo e registre-o para cliques de botão usando o atributo `onclick`:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   O método `AddTodo` em C# é chamado quando o botão é selecionado.

1. Para obter o título do novo item de tarefas pendentes, adicione um campo de cadeia de caracteres `newTodo` e associe-o ao valor da próxima entrada de texto usando o atributo `bind`:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. Atualize o método `AddTodo` para adicionar o `TodoItem` com o título especificado à lista. Limpe o valor da entrada de texto configurando `newTodo` para uma cadeia de caracteres vazia:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. Recompile e execute o aplicativo. Adicione algumas tarefas à lista de tarefas para testar o novo código.

1. O texto do título de cada item de tarefa pode ser editável, e uma caixa de seleção pode ajudar o usuário a manter o controle dos itens concluídos. Adicione uma entrada de caixa de seleção para cada item de tarefa pendente e associe seu valor à propriedade `IsDone`. Altere `@todo.Title` para um elemento `<input>` associado a `@todo.Title`:

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. Para verificar se esses valores estão associados, atualize o cabeçalho `<h1>` para mostrar uma contagem do número de itens de tarefa pendente que não estão concluídos (`IsDone` é `false`).

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. O componente Todo concluído (*Todo.cshtml*):

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. Recompile e execute o aplicativo. Adicione itens de tarefa pendente para testar o novo código.

## <a name="publish-and-deploy-the-app"></a>Publicar e implantar o aplicativo

Para publicar o aplicativo, confira <xref:host-and-deploy/razor-components/index#publish-the-app>.
