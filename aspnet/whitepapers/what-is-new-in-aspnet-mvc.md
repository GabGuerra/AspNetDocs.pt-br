---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: O que há de novo no ASP.NET MVC 2 | Microsoft Docs
author: rick-anderson
description: Este documento descreve novos recursos e aprimoramentos introduzidos no ASP.NET MVC 2. Este documento também está disponível para download.
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: 7f846e807309f3123db52b3053b9aa8d6aca81e6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59394829"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>Novidades no ASP.NET MVC 2

> Este documento descreve novos recursos e aprimoramentos introduzidos no ASP.NET MVC 2. Este documento também está disponível para [baixar](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)


[Introdução](#_TOC1)   
[Atualizando um projeto do ASP.NET MVC 1.0 para o ASP.NET MVC 2](#_TOC2)   
[Novos recursos](#_TOC3)   
[Auxiliares com modelos](#_TOC3_1)   
[Áreas](#_TOC3_2)   
[Suporte para controladores assíncronos](#_TOC3_3)   
[Suporte para DefaultValueAttribute nos parâmetros do método de ação](#_TOC3_4)   
[Suporte para dados binários com associadores de modelo de associação](#_TOC3_5)   
[Classes de ModelMetadataProvider e ModelMetadata](#_TOC3_6)   
[Suporte para atributos de DataAnnotations](#_TOC3_7)   
[Provedores do validador de modelo](#_TOC3_8)   
[Validação do lado do cliente](#_TOC3_9)   
[Novos trechos de código para Visual Studio 2010](#_TOC3_10)   
[Novo filtro de ação RequireHttpsAttribute](#_TOC3_11)   
[Substituindo o método HTTP verbo](#_TOC3_12)   
[Nova classe HiddenInputAttribute para auxiliares com modelos](#_TOC3_13)   
[Método auxiliar Html.ValidationSummary pode exibir erros de nível de modelo](#_TOC3_14)   
[Modelos T4 no Visual Studio gerar código específico para a versão de destino do .NET Framework](#_TOC3_15)[melhorias na API](#_TOC4)  
[Alterações significativas](#_TOC5)  
[Aviso de isenção de responsabilidade](#_TOC6)  

## <a id="_TOC1"></a>  Introdução

ASP.NET MVC 2 se baseia no ASP.NET MVC 1.0 e apresenta um grande conjunto de aprimoramentos e recursos voltados para o aumento da produtividade. Esta versão é compatível com o ASP.NET MVC 1.0, para que todos os seus dados de Conhecimento, habilidades, código e extensões para o ASP.NET MVC 1.0 continuam a aplicar.

Para obter mais informações sobre o ASP.NET MVC, visite os seguintes recursos:

- [Documentação do ASP.NET MVC no MSDN](https://go.microsoft.com/fwlink/?LinkId=159758)
- [O site da Web do ASP.NET MVC](https://asp.net/mvc/)
- [Fóruns do ASP.NET MVC](https://forums.asp.net/1146.aspx)

## <a id="_TOC2"></a>  Atualizando um projeto do ASP.NET MVC 1.0 para o ASP.NET MVC 2

ASP.NET MVC 2 pode ser instalado lado a lado com o ASP.NET MVC 1.0 no mesmo servidor, que fornece a flexibilidade de desenvolvedores de aplicativo na escolha quando atualizar um aplicativo ASP.NET MVC 1.0 para o ASP.NET MVC 2. Para obter informações sobre como atualizar, consulte o documento [atualizando um aplicativo ASP.NET MVC 1.0 para o ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185459).

## <a id="_TOC3"></a>  Novos recursos

Esta seção descreve os recursos que foram introduzidos na versão 2 do MVC.

### <a id="_TOC3_1"></a>  Auxiliares com modelos

Auxiliares com modelos permitem que você associados automaticamente elementos HTML para edição e exibição com tipos de dados. Por exemplo, quando os dados do tipo System. DateTime são exibidos em uma exibição, um elemento de interface do usuário do seletor de data pode ser processado automaticamente. Isso é semelhante ao funcionam dos modelos de campo nos dados dinâmicos do ASP.NET. Para obter mais informações, consulte [usando auxiliares modelo para exibir dados](https://go.microsoft.com/fwlink/?LinkId=159062) no site do MSDN.

### <a id="_TOC3_2"></a>  Areas

Áreas permitem organizar um projeto grande em várias seções menores para gerenciar a complexidade de um aplicativo Web grande. Cada seção ("área") normalmente representa uma seção separada de um site grande e é usada para agrupar conjuntos relacionados de controladores e exibições. Para obter mais informações, confira [Passo a passo: Organizando um aplicativo ASP.NET MVC por áreas](https://go.microsoft.com/fwlink/?LinkId=158978) no site do MSDN.

Para criar uma nova área, no Gerenciador de soluções, clique com botão direito no projeto, clique em Adicionar e, em seguida, clique em área. Isso exibe uma caixa de diálogo que solicitará o nome da área. Depois de inserir o nome da área, o Visual Studio adiciona uma nova área ao projeto.

A figura a seguir mostra um exemplo de layout para um projeto com duas áreas, Blogs e administrador.

![](what-is-new-in-aspnet-mvc/_static/image1.png)

Quando você cria uma área, o Visual Studio adiciona uma classe que deriva de AreaRegistration para cada área. Essa classe é necessária para registrar a área e suas rotas, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

O modelo de projeto padrão do ASP.NET MVC 2 inclui uma chamada ao método RegisterAllAreas no código para o arquivo global asax. Esse método registra cada área no projeto, procurando por todos os tipos que derivam da classe AreaRegistration, criando uma instância do tipo e, em seguida, chamando o método RegisterArea na instância. O exemplo a seguir mostra como isso é feito.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

Se você não especificar o namespace no método RegisterArea chamando o contexto. Método Namespaces.Add, o namespace da classe de registro é usado por padrão.

### <a id="_TOC3_3"></a>  Suporte para controladores assíncronos

ASP.NET MVC 2 agora permite que os controladores processar solicitações de forma assíncrona. Isso pode levar a ganhos de desempenho, permitindo que os servidores que frequentemente chamar operações de bloqueio (como solicitações de rede) para chamar contrapartes sem bloqueio em vez disso. Para obter mais informações, consulte o [usando um controlador assíncrono no ASP.NET MVC](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) tópico no MSDN.

### <a id="_TOC3_4"></a>  Suporte para DefaultValueAttribute nos parâmetros do método de ação

A classe System.ComponentModel.DefaultValueAttribute permite que um valor padrão deve ser fornecido para o parâmetro de argumento para um método de ação. Por exemplo, suponha que a rota padrão a seguir é definida:

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.json)]

Suponha também que o seguinte método de controlador e ação é definido:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

Qualquer um dos seguinte solicitação URLs invocará o método de ação de exibição que é definido no exemplo anterior.

- Artigo/123/exibição
- Artigo/123/modo de exibição? página = 1 (efetivamente o mesmo que a solicitação anterior)
- /Article/View/123?page=2

Sem o atributo DefaultValueAttribute, a primeira URL da lista anterior não funcionaria, pois o argumento de página é um tipo de valor não anulável cujo valor não foi fornecido.

Se seu código é escrito em Visual Basic 2010 ou Visual c# 2010, você pode usar parâmetros opcionais em vez do atributo DefaultValueAttribute, conforme mostrado no exemplo a seguir:

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a id="_TOC3_5"></a>  Suporte para dados binários com associadores de modelo de associação

Há duas novas sobrecargas do auxiliar Html.Hidden que codificar valores binários como cadeias de caracteres codificada em base-64:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

Um uso típico é inserir um carimbo de hora para um objeto no modo de exibição. Por exemplo, seu aplicativo pode incluir o seguinte objeto de produto:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

Um formulário de edição pode processar a propriedade de carimbo de hora no formulário, conforme mostrado no exemplo a seguir:

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

Essa marcação renderiza um elemento de entrada oculto com o valor de carimbo de hora como uma cadeia de caracteres codificado em base 64 que se parece com o exemplo a seguir:

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

Este formulário pode ser lançado para um método de ação que tem um argumento do tipo de produto, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

No método de ação, a propriedade de carimbo de hora é preenchida corretamente porque a cadeia de caracteres postada codificado em base 64 é convertida em uma matriz de bytes.

### <a id="_TOC3_6"></a>  Classes de ModelMetadataProvider e ModelMetadata

A classe ModelMetadataProvider fornece uma abstração para obtenção de metadados para o modelo em um modo de exibição. MVC 2 inclui um provedor padrão que disponibiliza os metadados que é exposto pelos atributos no namespace DataAnnotations. É possível criar provedores de metadados que fornecem metadados de outros armazenamentos de dados, como bancos de dados ou arquivos XML.

A classe ViewDataDictionary expõe um objeto ModelMetadata que contém os metadados que é extraído do modelo pela classe ModelMetadataProvider. Isso permite que os auxiliares de modelo para consumir esses metadados e ajustar sua saída de acordo.

Para obter mais informações, consulte a documentação para o [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) e [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) classes.

### <a id="_TOC3_7"></a>  Suporte para atributos de DataAnnotations

ASP.NET MVC 2 dá suporte ao uso de atributos de validação RangeAttribute, RequiredAttribute, StringLengthAttribute e RegexAttribute (definidos no namespace DataAnnotations) quando você associa a um modelo para fornecer entrada validação.

Para obter mais informações, confira [Como: Validar dados de modelo usando atributos de DataAnnotations](https://go.microsoft.com/fwlink/?LinkId=159063) no site do MSDN. Um projeto de exemplo que ilustra o uso desses atributos está disponível para download em [ https://go.microsoft.com/fwlink/?LinkId=157753 ](https://go.microsoft.com/fwlink/?LinkId=157753).

### <a id="_TOC3_8"></a>  Provedores do validador de modelo

A classe de provedor de validação do modelo representa uma abstração que fornece lógica de validação para o modelo. O ASP.NET MVC inclui um provedor de padrão com base em atributos de validação que estão incluídos no namespace DataAnnotations. Você também pode criar seus próprios provedores de validação que definem as regras de validação personalizada e mapeamentos personalizados de regras de validação ao modelo. Para obter mais informações, consulte a documentação para o [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) classe.

### <a id="_TOC3_9"></a>  Validação do lado do cliente

A classe de provedor de validador de modelo expõe metadados de validação para o navegador na forma de dados serializados em JSON que podem ser consumidos por uma biblioteca de validação do lado do cliente. ASP.NET MVC 2 inclui uma biblioteca de validação de cliente e o adaptador que ofereça suporte os atributos de validação de namespace DataAnnotations observados anteriormente. A classe de provedor também permite que você usar outras bibliotecas de validação do cliente, escrevendo um adaptador que processa os dados JSON e chamadas para a biblioteca alternativa.

### <a id="_TOC3_10"></a>  Novos trechos de código para Visual Studio 2010

Um conjunto de trechos de código HTML para o ASP.NET MVC 2 é instalado com o Visual Studio 2010. Para exibir uma lista de trechos de código, no menu Ferramentas, selecione o Gerenciador de trechos de código. Para o idioma, selecione o HTML e para o local, selecione ASP.NET MVC 2. Para obter mais informações sobre como usar trechos de código, consulte a documentação do Visual Studio.

### <a id="_TOC3_11"></a>  Novo filtro de ação RequireHttpsAttribute

O ASP.NET MVC 2 inclui uma nova classe RequireHttpsAttribute que pode ser aplicada a controladores e métodos de ação. Por padrão, o filtro redireciona uma solicitação de HTTP não - SSL para o equivalente de habilitado para SSL (HTTPS).

### <a id="_TOC3_12"></a>  Substituindo o método HTTP verbo

Quando você cria um site da Web usando o estilo de arquitetura REST, verbos HTTP são usados para determinar qual ação executar para um recurso. O REST requer que suportam aplicativos a gama completa de verbos HTTP comuns, incluindo GET, PUT, POST e excluir.

O ASP.NET MVC 2 inclui novos atributos que você pode aplicar métodos de ação e essa sintaxe compacta do recurso. Esses atributos habilitam o ASP.NET MVC selecionar um método de ação com base no verbo HTTP. No exemplo a seguir, uma solicitação POST chamará o primeiro método de ação e uma solicitação PUT chamará o segundo método de ação.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

Em versões anteriores do ASP.NET MVC, esses métodos de ação necessária uma sintaxe mais detalhada, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

Como navegadores oferecem suporte a somente os verbos GET e HTTP POST, não é possível postar em uma ação que requer um verbo diferente. Portanto, não é possível com suporte nativo de todas as solicitações RESTful.

No entanto, para dar suporte a RESTful solicitações durante as operações POST, o ASP.NET MVC 2 introduz um novo método auxiliar HttpMethodOverride HTML. Este método renderiza um elemento de entrada oculta que faz com que o formulário emular efetivamente qualquer método HTTP. Por exemplo, usando o método auxiliar HttpMethodOverride HTML, você pode ter um envio de formulário aparecer uma solicitação PUT ou DELETE. O comportamento de HttpMethodOverride afeta os seguintes atributos:

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

O elemento de entrada oculto tem seu nome X-HTTP-Method-Override e seu valor definido para o verbo HTTP para emular. O valor de substituição também pode ser especificado em um cabeçalho HTTP ou em um valor de cadeia de caracteres de consulta como um par nome/valor.

A substituição só pode ser usada quando a solicitação real é uma solicitação POST. O valor de substituição será ignorado para solicitações que usam qualquer outro verbo HTTP.

### <a id="_TOC3_13"></a>  Nova classe HiddenInputAttribute para auxiliares com modelos

Você pode aplicar o novo atributo HiddenInputAttribute para uma propriedade de modelo para indicar se um elemento de entrada oculto deve ser renderizado ao exibir o modelo em um modelo do editor. (O atributo define um valor de UIHint implícito de HiddenInput). A propriedade do atributo DisplayValue permite especificar se o valor é exibido no editor e modos de exibição. Quando DisplayValue é definido como false, nada é exibido, nem mesmo a marcação HTML que normalmente envolve um campo. O valor padrão para DisplayValue é verdadeiro.

Você pode usar o atributo HiddenInputAttribute nos seguintes cenários:

- Quando um modo de exibição permite aos usuários editar a ID de um objeto e é necessário exibir o valor, bem como para fornecer um elemento de entrada oculto que contém a ID do antiga para que ele pode ser passado de volta para o controlador.
- Quando um modo de exibição permite que os usuários editar uma propriedade binária que nunca deve ser exibida, como uma propriedade de carimbo de hora. Nesse caso, o valor e uma marcação HTML ao redor (como o rótulo e valor) não são exibidos.

O exemplo a seguir mostra como usar a classe HiddenInputAttribute.

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

Quando o atributo é definido como true (ou nenhum parâmetro for especificado), ocorre o seguinte:

- Em modelos de exibição, um rótulo é renderizado e o valor é exibido ao usuário.
- No editor de modelos, um rótulo é renderizado e o valor é processado em um elemento de entrada oculto.

Quando o atributo é definido como false, ocorre o seguinte:

- Em modelos de exibição, nada será renderizado para esse campo.
- No editor de modelos, nenhum rótulo é renderizado e o valor é processado em um elemento de entrada oculto.

### <a id="_TOC3_14"></a>  Método auxiliar Html.ValidationSummary pode exibir erros de nível de modelo

Em vez de sempre exibir todos os erros de validação, o método auxiliar Html.ValidationSummary tem uma nova opção para exibir somente os erros de nível de modelo. Isso permite que os erros de nível de modelo a ser exibido no resumo de validação e erros específicos de campo a ser exibido ao lado de cada campo.

### <a id="_TOC3_15"></a>  Modelos T4 no Visual Studio gerar código específico para a versão de destino do .NET Framework

Uma nova propriedade está disponível para arquivos T4 do host do ASP.NET MVC T4 que especifica a versão do .NET Framework que é usado pelo aplicativo. Isso permite que os modelos T4 gerar o código e a marcação que é específica para uma versão do .NET Framework. No Visual Studio 2008, o valor é sempre .NET 3.5. No Visual Studio 2010, o valor é o .NET 3.5 ou 4 do .NET.

## <a id="_TOC4"></a>  Melhorias na API

Esta seção descreve as alterações a membros e tipos de ASP.NET MVC existentes.

- Adicionado um método CreateActionInvoker virtual protegido na classe do controlador. Esse método é invocado pela propriedade ActionInvoker do controlador e permite a instanciação lenta do invocador se nenhum chamador já está definido.
- Adicionado um método HandleUnauthorizedRequest virtual protegido na classe AuthorizeAttribute. Isso permite que os filtros que derivam de AuthorizeAttribute para controlar o comportamento quando ocorre falha na autorização.
- Adicionado um método Add (cadeia de caracteres chave, valor do objeto) na classe ValueProviderDictionary. Isso permite que você use a sintaxe do inicializador de dicionário para ValueProviderDictionary, como no exemplo a seguir:

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- Adicionado um get\_método na classe Sys.Mvc.AjaxContext do objeto. Esse é um método de JavaScript que é semelhante ao get\_método de dados, mas se o tipo de conteúdo da resposta é application/json, obter\_retorna o objeto JSON.
- Adicionada uma propriedade ActionDescriptor na classe AuthorizationContext.
- Adicionado um token de UrlParameter.Optional que pode ser usado para solucionar problemas ao associar a um modelo que contém uma propriedade de ID quando a propriedade estiver ausente em uma postagem de formulário. Para obter mais detalhes, consulte a entrada [parâmetros de URL opcional do ASP.NET MVC 2](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) no blog de Phil Haack.

## <a id="_TOC5"></a>  Alterações significativas

As seguintes alterações podem causar erros em aplicativos existentes do ASP.NET MVC 1.0.

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>Alteração no comportamento de validação de propriedade para classes que implementam IDataErrorInfo

Para objetos de modelo que usam IDataErrorInfo para executar a validação, cada propriedade é validada, independentemente se um novo valor foi definido. No ASP.NET MVC 1.0, apenas as propriedades que tinham novos valores definida foram validadas. No ASP.NET MVC 2, a propriedade Error de IDataErrorInfo é chamada apenas se todos os validadores de propriedade foram bem-sucedidas.

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>Script de mapeamento de script do IIS não está mais disponível no instalador

O script de mapeamento de script do IIS é um script de linha de comando que é usado para configurar mapeamentos de script para IIS 6 e IIS 7 no modo clássico. O script de mapeamento de script não será necessária se você usar o Visual Studio Development Server ou se você usar o IIS 7 no modo integrado. Os scripts estão disponíveis como um download separado sem suporte nas [WebStack ASP.NET](https://github.com/aspnet/AspNetWebStack).

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>O método auxiliar de Html.Substitute na versão futura do MVC não está mais disponível

Devido a alterações no comportamento de renderização de mecanismos de exibição do MVC, o método auxiliar Html.Substitute não funciona e foi removido.

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>A interface do IValueProvider substitui todos os usos de IDictionary

Cada argumento de método ou propriedade que aceita o IDictionary no MVC 1.0 agora aceita IValueProvider. Essa alteração afeta somente os aplicativos que incluem provedores de valor personalizados ou associadores de modelo personalizados. Exemplos de propriedades e métodos que são afetados por essa alteração incluem o seguinte:

- A propriedade ValueProvider das classes ControllerBase e ModelBindingContext.
- Os métodos de TryUpdateModel da classe do controlador.

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>Novas classes CSS foram adicionadas no arquivo site.

O arquivo CSS nos modelos de projeto do ASP.NET MVC foi atualizado para incluir novos estilos usados pela funcionalidade de validação e pelos auxiliares de modelo.

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Os auxiliares agora retornam um objeto MvcHtmlString

Para aproveitar a nova sintaxe de expressão de codificação HTML no ASP.NET 4, o tipo de retorno para os auxiliares HTML estará MvcHtmlString em vez de uma cadeia de caracteres. Se você usar o ASP.NET MVC 2 e os auxiliares de novo no ASP.NET 3.5, você não poderá aproveitar a sintaxe de codificação HTML; a nova sintaxe está disponível somente quando você executar o ASP.NET MVC 2 no ASP.NET 4.

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult agora responde apenas às solicitações HTTP POST

Para minimizar ataques que têm o potencial de divulgação de informações, por padrão, de sequestro de JSON a classe JsonResult agora responde apenas às solicitações HTTP POST. OBTER AJAX chamadas a métodos de ação que retornam um objeto JsonResult devem ser alteradas para usar POST em vez disso. Se necessário, você pode substituir esse comportamento, definindo a propriedade JsonRequestBehavior novo de JsonResult. Para obter mais informações sobre a exploração de possíveis, consulte o postagem no blog [sequestro de JSON](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) no blog de Phil Haack.

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>Modelo e os setters de propriedade ModelType em ModelBindingContext estão obsoletos

Uma nova propriedade ModelMetadata configurável adicionou à classe ModelBindingContext. A nova propriedade encapsula o modelo e as propriedades de ModelType. Embora as propriedades de modelo e ModelType são obsoletas, para compatibilidade com versões anteriores de getters de propriedade ainda funcionam; eles delegam para a propriedade ModelMetadata para recuperar o valor.

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>Alterações para a classe de DefaultControllerFactory interromper alocadores de controlador personalizado que derivam dela

A classe de DefaultControllerFactory foi corrigida, removendo a propriedade RequestContext. No lugar essa propriedade, a instância do contexto de solicitação é passada para os métodos GetControllerInstance e GetControllerType virtuais protegidos. Essa alteração afeta os alocadores de controlador personalizado que derivam de DefaultControllerFactory.

Alocadores de controlador personalizado geralmente são usados para fornecer aplicativos de injeção de dependência para o ASP.NET MVC. Para atualizar as fábricas de controlador personalizado para dar suporte a ASP.NET MVC 2, alterar a assinatura do método ou assinaturas para coincidir com as novas assinaturas e usar o parâmetro de contexto de solicitação em vez da propriedade.

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>"Área de" agora é uma uma chave do valor de rota reservado

A cadeia de caracteres "área de" em valores de rota agora tem um significado especial no ASP.NET MVC, da mesma maneira que fazem "controller" e "ação". Uma implicação é que se os auxiliares HTML são fornecidos com um dicionário de valores de rota que contém "área", os auxiliares não acrescentará "área de" na cadeia de caracteres de consulta.

Se você estiver usando o recurso de áreas, verifique se não usar {área} como parte de sua URL da rota.


## <a id="_TOC6"></a>  Isenção de responsabilidade

Este é um documento preliminar e pode ser alterado substancialmente antes da versão comercial final do software descrito aqui.

As informações contidas neste documento representam a visão atual da Microsoft Corporation sobre os problemas discutidos a partir da data da publicação. Como a Microsoft deve responder às condições do mercado em constante mudança, este documento não deve ser interpretado como um compromisso por parte da Microsoft, e a Microsoft não pode garantir a exatidão de nenhuma informação apresentada após a data da publicação.

Este whitepaper é apenas para fins informativos. A MICROSOFT NÃO OFERECE GARANTIA, EXPRESSA, IMPLÍCITA OU ESTATUTÁRIA, DAS INFORMAÇÕES CONTIDAS NESTE DOCUMENTO.

Estar em conformidade com todas as leis de direitos autorais aplicáveis é responsabilidade do usuário. Sem limitar os direitos autorais, nenhuma parte deste documento pode ser reproduzida, armazenada ou inserida em um sistema de recuperação, ou transmitida de qualquer forma, por qualquer meio (eletrônico, mecânico, fotocópia, gravação ou outro) ou para qualquer fim, sem a permissão expressa, por escrito, da Microsoft Corporation.

A Microsoft pode ter patentes, solicitações de patente, marcas comerciais, direitos autorais ou outros direitos de propriedade intelectual que abrangem o conteúdo deste documento. A não ser que especificado expressamente em um contrato de licença da Microsoft, o fornecimento deste documento não confere a você nenhum direito sobre as supracitadas patentes, marcas comerciais, direitos autorais ou outra propriedade intelectual.

A menos que indicado o contrário, os exemplos de empresas que as organizações, produtos, nomes de domínio, endereços de email, logotipos, pessoas, lugares e eventos aqui representados são fictícios e nenhuma associação com qualquer empresa, organização, produto, nome de domínio, email endereço, logotipo, pessoa, lugar ou evento é intencional ou deve ser inferido.

© 2010 Microsoft Corporation. Todos os direitos reservados.

Microsoft e Windows são marcas registradas ou comerciais da Microsoft Corporation nos Estados Unidos e/ou em outros países.

Os nomes de empresas reais e produtos mencionados aqui podem ser marcas comerciais de seus respectivos proprietários.
