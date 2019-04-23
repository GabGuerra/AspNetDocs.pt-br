---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: Validação com os validadores de anotação de dados (VB) | Microsoft Docs
author: microsoft
description: Aproveite o associador de modelo de anotação de dados para executar a validação dentro de um aplicativo ASP.NET MVC. Saiba como usar os diferentes tipos de validador...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 6893d1f2445452b1d802b89027b09d8294bdc5b7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59422831"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="18079-104">Validação com os validadores de anotação de dados (VB)</span><span class="sxs-lookup"><span data-stu-id="18079-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="18079-105">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="18079-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="18079-106">Aproveite o associador de modelo de anotação de dados para executar a validação dentro de um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="18079-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="18079-107">Saiba como usar os diferentes tipos de atributos de validador e trabalhar com eles no Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="18079-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>


<span data-ttu-id="18079-108">Neste tutorial, você aprenderá como usar os validadores de anotação de dados para executar a validação em um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="18079-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="18079-109">A vantagem de usar os validadores de anotação de dados é que eles permitem que você executar a validação simplesmente adicionando um ou mais atributos – como exigida ou o atributo StringLength – para uma propriedade de classe.</span><span class="sxs-lookup"><span data-stu-id="18079-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="18079-110">Antes de usar os validadores de anotação de dados, você deve baixar o associador de modelo de anotações de dados.</span><span class="sxs-lookup"><span data-stu-id="18079-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="18079-111">Você pode baixar a amostra de associador de modelo de anotações de dados do site do CodePlex clicando [aqui](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span><span class="sxs-lookup"><span data-stu-id="18079-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>


<span data-ttu-id="18079-112">É importante entender que o associador de modelo de anotações de dados não é uma parte oficial da Microsoft ASP.NET MVC framework.</span><span class="sxs-lookup"><span data-stu-id="18079-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="18079-113">Embora o associador de modelo de anotações de dados foi criado pela equipe do Microsoft ASP.NET MVC, a Microsoft não oferece suporte oficial do produto para o associador de modelo de anotações de dados descrito e usado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="18079-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>


## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="18079-114">Usando o associador de modelo de anotação de dados</span><span class="sxs-lookup"><span data-stu-id="18079-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="18079-115">Para usar o associador de modelo de anotações de dados em um aplicativo ASP.NET MVC, primeiro você precisa adicionar uma referência ao assembly Microsoft.Web.Mvc.DataAnnotations.dll e o assembly de unirem às.</span><span class="sxs-lookup"><span data-stu-id="18079-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="18079-116">Selecione a opção de menu **projeto, adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="18079-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="18079-117">Em seguida clique o **navegue** guia e navegue até o local onde você baixou (e descompactado) a amostra de associador de modelo de anotações de dados (consulte **Figura 1**).</span><span class="sxs-lookup"><span data-stu-id="18079-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="18079-118">**Figura 1**: Adicionando uma referência ao associador de modelo de anotações de dados ([clique para exibir a imagem em tamanho normal](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="18079-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="18079-119">Selecione o assembly Microsoft.Web.Mvc.DataAnnotations.dll e o assembly de unirem às e clique o **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="18079-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>


<span data-ttu-id="18079-120">Você não pode usar o assembly de unirem às incluído com o .NET Framework Service Pack 1 com o associador de modelo de anotações de dados.</span><span class="sxs-lookup"><span data-stu-id="18079-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="18079-121">Você deve usar a versão do assembly unirem às incluído no download de amostra de associador de modelo de anotações de dados.</span><span class="sxs-lookup"><span data-stu-id="18079-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>


<span data-ttu-id="18079-122">Por fim, você precisa registrar o associador de modelo de DataAnnotations no arquivo global. asax.</span><span class="sxs-lookup"><span data-stu-id="18079-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="18079-123">Adicione a seguinte linha de código para o aplicativo\_manipulador de eventos Start () para que o aplicativo\_método Start () tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="18079-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="18079-124">Esta linha de código registra o DataAnnotationsModelBinder como o associador de modelo padrão para todo o aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="18079-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="18079-125">Usando os atributos de validador de anotação de dados</span><span class="sxs-lookup"><span data-stu-id="18079-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="18079-126">Quando você usa o associador de modelo de anotações de dados, você use atributos de validador para executar a validação.</span><span class="sxs-lookup"><span data-stu-id="18079-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="18079-127">O namespace DataAnnotations inclui os seguintes atributos de validador:</span><span class="sxs-lookup"><span data-stu-id="18079-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="18079-128">Intervalo de – permite que você valide se o valor de uma propriedade fica entre um intervalo de valores especificado.</span><span class="sxs-lookup"><span data-stu-id="18079-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="18079-129">RegularExpression – permite que você valide se o valor de uma propriedade corresponde a um padrão de expressão regular especificada.</span><span class="sxs-lookup"><span data-stu-id="18079-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="18079-130">Obrigatório – permite marcar uma propriedade conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="18079-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="18079-131">StringLength – permite que você especificar um comprimento máximo para uma propriedade de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="18079-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="18079-132">Validação – a classe base para todos os atributos de validador.</span><span class="sxs-lookup"><span data-stu-id="18079-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18079-133">Se suas necessidades de validação não são atendidas por qualquer um dos validadores padrão, em seguida, você sempre terá a opção de criação de um atributo de validador personalizado herdando de um novo atributo de validador de atributo de validação de base.</span><span class="sxs-lookup"><span data-stu-id="18079-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>


<span data-ttu-id="18079-134">A classe de produto na **listagem 1** ilustra como usar esses atributos de validador.</span><span class="sxs-lookup"><span data-stu-id="18079-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="18079-135">As propriedades de nome, descrição e UnitPrice são marcadas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="18079-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="18079-136">A propriedade de nome deve ter um comprimento de cadeia de caracteres que é menor que 10 caracteres.</span><span class="sxs-lookup"><span data-stu-id="18079-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="18079-137">Por fim, a propriedade UnitPrice deve corresponder a um padrão de expressão regular que representa um valor de moeda.</span><span class="sxs-lookup"><span data-stu-id="18079-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="18079-138">**Listagem 1**: Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="18079-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="18079-139">A classe Product ilustra como usar um atributo adicional: o atributo DisplayName.</span><span class="sxs-lookup"><span data-stu-id="18079-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="18079-140">O atributo DisplayName permite que você modifique o nome da propriedade quando a propriedade é exibida em uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="18079-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="18079-141">Em vez de exibir a mensagem de erro "o campo UnitPrice é necessário" é possível exibir a mensagem de erro "o campo de preço é necessário".</span><span class="sxs-lookup"><span data-stu-id="18079-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18079-142">Se você quiser personalizar completamente a mensagem de erro exibida por um validador pode atribuir uma mensagem de erro personalizado à propriedade de ErrorMessage do validador como este: `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="18079-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>


<span data-ttu-id="18079-143">Você pode usar a classe de produto na **listagem 1** com a ação de controlador de Create () em **listagem 2**.</span><span class="sxs-lookup"><span data-stu-id="18079-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="18079-144">Esta ação do controlador exibe novamente a exibição criar quando o estado do modelo contém erros.</span><span class="sxs-lookup"><span data-stu-id="18079-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="18079-145">**Listagem 2**: Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="18079-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="18079-146">Por fim, você pode criar o modo de exibição **listagem 3** clicando duas vezes a ação Create () e selecionando a opção de menu **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="18079-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="18079-147">Crie uma exibição fortemente tipada com a classe Product como a classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="18079-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="18079-148">Selecione **Create** na lista suspensa de conteúdo view (consulte **Figura 2**).</span><span class="sxs-lookup"><span data-stu-id="18079-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="18079-149">**Figura 2**: Adicionar modo de exibição criar</span><span class="sxs-lookup"><span data-stu-id="18079-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="18079-150">**Listagem 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="18079-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18079-151">Remover o campo de Id do formulário Criar gerado pelo **adicionar exibição** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="18079-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="18079-152">Como o campo de Id corresponde a uma coluna de identidade, você não deseja permitir que os usuários a inserir um valor para esse campo.</span><span class="sxs-lookup"><span data-stu-id="18079-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>


<span data-ttu-id="18079-153">Se você envia o formulário para a criação de um produto e você não inserir valores para os campos obrigatórios, então as mensagens de erro de validação no **Figura 3** são exibidos.</span><span class="sxs-lookup"><span data-stu-id="18079-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="18079-154">**Figura 3**: Campos obrigatórios ausentes</span><span class="sxs-lookup"><span data-stu-id="18079-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="18079-155">Se você inserir um valor inválido para moeda, em seguida, a mensagem de erro no **Figura 4** é exibida.</span><span class="sxs-lookup"><span data-stu-id="18079-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="18079-156">**Figura 4**: Valor inválido de moeda</span><span class="sxs-lookup"><span data-stu-id="18079-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="18079-157">Usando os validadores de anotação com o Entity Framework</span><span class="sxs-lookup"><span data-stu-id="18079-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="18079-158">Se você estiver usando o Microsoft Entity Framework para gerar classes de modelo de dados, em seguida, é possível aplicar os atributos de validador diretamente às suas classes.</span><span class="sxs-lookup"><span data-stu-id="18079-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="18079-159">Como o Entity Framework Designer gera as classes de modelo, as alterações feitas para as classes de modelo serão substituídas na próxima vez que você fizer alterações no Designer.</span><span class="sxs-lookup"><span data-stu-id="18079-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="18079-160">Se você quiser usar os validadores com as classes geradas pelo Entity Framework, em seguida, você precisa criar classes de dados de metadados.</span><span class="sxs-lookup"><span data-stu-id="18079-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="18079-161">Você pode aplicar os validadores para a classe de dados de metadados em vez de aplicar os validadores à classe real.</span><span class="sxs-lookup"><span data-stu-id="18079-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="18079-162">Por exemplo, imagine que você tenha criado uma classe de filme usando o Entity Framework (consulte **Figura 5**).</span><span class="sxs-lookup"><span data-stu-id="18079-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="18079-163">Além disso, imagine que você deseja tornar o título do filme e diretor de propriedades propriedades necessárias.</span><span class="sxs-lookup"><span data-stu-id="18079-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="18079-164">Nesse caso, você pode criar a classe parcial e a classe de dados de meta no **listagem 4**.</span><span class="sxs-lookup"><span data-stu-id="18079-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="18079-165">**Figura 5**: Classe Movie gerada pelo Entity Framework</span><span class="sxs-lookup"><span data-stu-id="18079-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="18079-166">**Listagem 4**: Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="18079-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="18079-167">O arquivo no **listagem 4** contém duas classes chamadas de filmes e MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="18079-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="18079-168">A classe de filme é uma classe parcial.</span><span class="sxs-lookup"><span data-stu-id="18079-168">The Movie class is a partial class.</span></span> <span data-ttu-id="18079-169">Ele corresponde à classe parcial gerada pelo Entity Framework que está contido no arquivo DataModel.Designer.vb.</span><span class="sxs-lookup"><span data-stu-id="18079-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="18079-170">Atualmente, o .NET framework não dá suporte a propriedades parciais.</span><span class="sxs-lookup"><span data-stu-id="18079-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="18079-171">Portanto, não há nenhuma maneira de aplicar os atributos de validador para as propriedades da classe Movie definido no arquivo DataModel.Designer.vb aplicando os atributos de validador para as propriedades da classe Movie definida no arquivo no **listagem 4**.</span><span class="sxs-lookup"><span data-stu-id="18079-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="18079-172">Observe que a classe parcial de filme é decorada com um atributo MetadataType que aponta para a classe MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="18079-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="18079-173">A classe MovieMetaData contém propriedades de proxy para as propriedades da classe filme.</span><span class="sxs-lookup"><span data-stu-id="18079-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="18079-174">Os atributos de validação são aplicados às propriedades da classe MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="18079-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="18079-175">As propriedades do título, diretor e DateReleased todos estiverem marcadas como propriedades necessárias.</span><span class="sxs-lookup"><span data-stu-id="18079-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="18079-176">A propriedade diretor deve ser atribuída a uma cadeia de caracteres que contém menos de 5 caracteres.</span><span class="sxs-lookup"><span data-stu-id="18079-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="18079-177">Por fim, o atributo DisplayName é aplicado à propriedade DateReleased para exibir uma mensagem de erro como "o campo de data de lançamento é obrigatório."</span><span class="sxs-lookup"><span data-stu-id="18079-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="18079-178">em vez do erro "o campo DateReleased é necessário."</span><span class="sxs-lookup"><span data-stu-id="18079-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="18079-179">Observe que as propriedades de proxy na classe MovieMetaData não precisam representar os mesmos tipos de propriedades correspondentes na classe de filme.</span><span class="sxs-lookup"><span data-stu-id="18079-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="18079-180">Por exemplo, a propriedade de diretor é uma propriedade de cadeia de caracteres na classe de filme e uma propriedade de objeto na classe MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="18079-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>


<span data-ttu-id="18079-181">A página no **Figura 6** ilustra as mensagens de erro retornadas quando você insere valores inválidos para as propriedades do filme.</span><span class="sxs-lookup"><span data-stu-id="18079-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="18079-182">**Figura 6**: Usando validadores com o Entity Framework ([clique para exibir a imagem em tamanho normal](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="18079-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="18079-183">Resumo</span><span class="sxs-lookup"><span data-stu-id="18079-183">Summary</span></span>

<span data-ttu-id="18079-184">Neste tutorial, você aprendeu como aproveitar o associador de modelo de anotação de dados para executar a validação dentro de um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="18079-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="18079-185">Você aprendeu a usar os diferentes tipos de atributos de validador, como o necessário e StringLength.</span><span class="sxs-lookup"><span data-stu-id="18079-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="18079-186">Você também aprendeu a usar esses atributos ao trabalhar com o Entity Framework da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="18079-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="18079-187">Anterior</span><span class="sxs-lookup"><span data-stu-id="18079-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
