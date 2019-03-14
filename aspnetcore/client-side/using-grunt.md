---
title: Usar o Grunt no ASP.NET Core
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2016
uid: client-side/using-grunt
ms.openlocfilehash: 21fa565c930563bbc819c2a02ea71655193513d0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049793"
---
# <a name="use-grunt-in-aspnet-core"></a><span data-ttu-id="7b6cd-102">Usar o Grunt no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7b6cd-102">Use Grunt in ASP.NET Core</span></span>

<span data-ttu-id="7b6cd-103">Por [Noel arroz](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)</span><span class="sxs-lookup"><span data-stu-id="7b6cd-103">By [Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/)</span></span>

<span data-ttu-id="7b6cd-104">Grunt é um executor de tarefas JavaScript que automatiza a minimização de script, compilação TypeScript, ferramentas de "lint" qualidade do código, processadores de pré-lançamento do CSS e praticamente qualquer tarefa repetitiva que precisa fazer para dar suporte ao desenvolvimento de cliente.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-104">Grunt is a JavaScript task runner that automates script minification, TypeScript compilation, code quality "lint" tools, CSS pre-processors, and just about any repetitive chore that needs doing to support client development.</span></span> <span data-ttu-id="7b6cd-105">Grunt é totalmente suportado no Visual Studio, embora os modelos de projeto do ASP.NET usam o Gulp por padrão (consulte [usar o Gulp](using-gulp.md)).</span><span class="sxs-lookup"><span data-stu-id="7b6cd-105">Grunt is fully supported in Visual Studio, though the ASP.NET project templates use Gulp by default (see [Use Gulp](using-gulp.md)).</span></span>

<span data-ttu-id="7b6cd-106">Este exemplo usa um projeto vazio do ASP.NET Core como ponto de partida, para mostrar como automatizar o processo de compilação do cliente do zero.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-106">This example uses an empty ASP.NET Core project as its starting point, to show how to automate the client build process from scratch.</span></span>

<span data-ttu-id="7b6cd-107">O exemplo concluído limpa o diretório de implantação de destino, combina arquivos JavaScript, verificações de qualidade do código, condensa o conteúdo do arquivo JavaScript e implanta na raiz do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-107">The finished example cleans the target deployment directory, combines JavaScript files, checks code quality, condenses JavaScript file content and deploys to the root of your web application.</span></span> <span data-ttu-id="7b6cd-108">Usaremos os seguintes pacotes:</span><span class="sxs-lookup"><span data-stu-id="7b6cd-108">We will use the following packages:</span></span>

* <span data-ttu-id="7b6cd-109">**grunt**: O pacote de executor de tarefa do Grunt.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-109">**grunt**: The Grunt task runner package.</span></span>

* <span data-ttu-id="7b6cd-110">**grunt-contrib-clean**: Um plug-in que remove os arquivos ou diretórios.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-110">**grunt-contrib-clean**: A plugin that removes files or directories.</span></span>

* <span data-ttu-id="7b6cd-111">**grunt-contrib-jshint**: Um plug-in que analisa a qualidade do código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-111">**grunt-contrib-jshint**: A plugin that reviews JavaScript code quality.</span></span>

* <span data-ttu-id="7b6cd-112">**grunt-contrib-concat**: Um plug-in que une os arquivos em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-112">**grunt-contrib-concat**: A plugin that joins files into a single file.</span></span>

* <span data-ttu-id="7b6cd-113">**grunt-contrib-uglify**: Um plug-in que minimiza o JavaScript para reduzir o tamanho.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-113">**grunt-contrib-uglify**: A plugin that minifies JavaScript to reduce size.</span></span>

* <span data-ttu-id="7b6cd-114">**grunt-contrib-watch**: Um plug-in que observa a atividade de arquivos.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-114">**grunt-contrib-watch**: A plugin that watches file activity.</span></span>

## <a name="preparing-the-application"></a><span data-ttu-id="7b6cd-115">Preparando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="7b6cd-115">Preparing the application</span></span>

<span data-ttu-id="7b6cd-116">Para começar, configure um novo aplicativo web vazio e adicionar arquivos de exemplo do TypeScript.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-116">To begin, set up a new empty web application and add TypeScript example files.</span></span> <span data-ttu-id="7b6cd-117">Arquivos TypeScript são automaticamente compilados em JavaScript usando as configurações do Visual Studio padrão e serão nosso matéria-prima para processar usando o Grunt.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-117">TypeScript files are automatically compiled into JavaScript using default Visual Studio settings and will be our raw material to process using Grunt.</span></span>

1.  <span data-ttu-id="7b6cd-118">No Visual Studio, crie um novo `ASP.NET Web Application`.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-118">In Visual Studio, create a new `ASP.NET Web Application`.</span></span>

2.  <span data-ttu-id="7b6cd-119">No **novo projeto ASP.NET** caixa de diálogo, selecione o ASP.NET Core **vazia** modelo e clique no botão Okey.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-119">In the **New ASP.NET Project** dialog, select the ASP.NET Core **Empty** template and click the OK button.</span></span>

3.  <span data-ttu-id="7b6cd-120">No Gerenciador de soluções, examine a estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-120">In the Solution Explorer, review the project structure.</span></span> <span data-ttu-id="7b6cd-121">O `\src` pasta inclui vazia `wwwroot` e `Dependencies` nós.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-121">The `\src` folder includes empty `wwwroot` and `Dependencies` nodes.</span></span>

    ![solução de web vazio](using-grunt/_static/grunt-solution-explorer.png)

4.  <span data-ttu-id="7b6cd-123">Adicionar uma nova pasta chamada `TypeScript` no diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-123">Add a new folder named `TypeScript` to your project directory.</span></span>

5.  <span data-ttu-id="7b6cd-124">Antes de adicionar todos os arquivos, certifique-se de que o Visual Studio tem a opção ' Compilar ao salvar ' para arquivos TypeScript check.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-124">Before adding any files, make sure that Visual Studio has the option 'compile on save' for TypeScript files checked.</span></span> <span data-ttu-id="7b6cd-125">Navegue até **ferramentas** > **opções** > **Editor de texto** > **Typescript**  >  **Projeto**:</span><span class="sxs-lookup"><span data-stu-id="7b6cd-125">Navigate to **Tools** > **Options** > **Text Editor** > **Typescript** > **Project**:</span></span>

    ![Opções de configuração compliation automática de arquivos TypeScript](using-grunt/_static/typescript-options.png)

6.  <span data-ttu-id="7b6cd-127">Clique com botão direito do `TypeScript` diretório e selecione **Adicionar > Novo Item** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-127">Right-click the `TypeScript` directory and select **Add > New Item** from the context menu.</span></span> <span data-ttu-id="7b6cd-128">Selecione o **arquivo JavaScript** de item e nomeie o arquivo *Tastes.ts* (Observe o \*extensão. TS).</span><span class="sxs-lookup"><span data-stu-id="7b6cd-128">Select the **JavaScript file** item and name the file *Tastes.ts* (note the \*.ts extension).</span></span> <span data-ttu-id="7b6cd-129">Copie a linha de código do TypeScript abaixo para o arquivo (quando você salva, um novo *Tastes.js* arquivo aparecerá com a fonte do JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7b6cd-129">Copy the line of TypeScript code below into the file (when you save, a new *Tastes.js* file will appear with the JavaScript source).</span></span>
    
    ```typescript
    enum Tastes { Sweet, Sour, Salty, Bitter }
    ```

7.  <span data-ttu-id="7b6cd-130">Adicionar um segundo arquivo para o **TypeScript** diretório e nomeie-o `Food.ts`.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-130">Add a second file to the **TypeScript** directory and name it `Food.ts`.</span></span> <span data-ttu-id="7b6cd-131">Copie o código a seguir para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-131">Copy the code below into the file.</span></span>

    ```typescript
    class Food {
      constructor(name: string, calories: number) {
        this._name = name;
        this._calories = calories;
      }
    
      private _name: string;
      get Name() {
        return this._name;
      }
    
      private _calories: number;
      get Calories() {
        return this._calories;
      }
    
      private _taste: Tastes;
      get Taste(): Tastes { return this._taste }
      set Taste(value: Tastes) {
        this._taste = value;
      }
    }
    ```

## <a name="configuring-npm"></a><span data-ttu-id="7b6cd-132">Configuração do NPM</span><span class="sxs-lookup"><span data-stu-id="7b6cd-132">Configuring NPM</span></span>

<span data-ttu-id="7b6cd-133">Em seguida, configure o NPM para baixar o grunt e tarefas do grunt.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-133">Next, configure NPM to download grunt and grunt-tasks.</span></span>

1. <span data-ttu-id="7b6cd-134">No Gerenciador de soluções, clique com botão direito no projeto e selecione **Adicionar > Novo Item** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-134">In the Solution Explorer, right-click the project and select **Add > New Item** from the context menu.</span></span> <span data-ttu-id="7b6cd-135">Selecione o **arquivo de configuração do NPM** item, deixe o nome padrão, *Package. JSON*e clique no **Add** botão.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-135">Select the **NPM configuration file** item, leave the default name, *package.json*, and click the **Add** button.</span></span>

2. <span data-ttu-id="7b6cd-136">No *Package. JSON* do arquivo, dentro de `devDependencies` chaves de objeto, digite "grunt".</span><span class="sxs-lookup"><span data-stu-id="7b6cd-136">In the *package.json* file, inside the `devDependencies` object braces, enter "grunt".</span></span> <span data-ttu-id="7b6cd-137">Selecione `grunt` do Intellisense lista e pressione a tecla Enter.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-137">Select `grunt` from the Intellisense list and press the Enter key.</span></span> <span data-ttu-id="7b6cd-138">Visual Studio será colocada entre aspas no nome do pacote grunt e adicione dois-pontos.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-138">Visual Studio will quote the grunt package name, and add a colon.</span></span> <span data-ttu-id="7b6cd-139">À direita dos dois pontos, selecione a versão estável mais recente do pacote na parte superior da lista do Intellisense (pressione `Ctrl-Space` se o Intellisense não aparece).</span><span class="sxs-lookup"><span data-stu-id="7b6cd-139">To the right of the colon, select the latest stable version of the package from the top of the Intellisense list (press `Ctrl-Space` if Intellisense doesn't appear).</span></span>

    ![grun Intellisense](using-grunt/_static/devdependencies-grunt.png)
    
    > [!NOTE]
    > <span data-ttu-id="7b6cd-141">Usa NPM [controle de versão semântico](http://semver.org/) para organizar as dependências.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-141">NPM uses [semantic versioning](http://semver.org/) to organize dependencies.</span></span> <span data-ttu-id="7b6cd-142">Controle de versão semântico, também conhecido como SemVer, identifica os pacotes com o esquema de numeração <major>.<minor>. <patch>. IntelliSense simplifica o controle de versão semântico, mostrando apenas algumas opções comuns.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-142">Semantic versioning, also known as SemVer, identifies packages with the numbering scheme <major>.<minor>.<patch>. Intellisense simplifies semantic versioning by showing only a few common choices.</span></span> <span data-ttu-id="7b6cd-143">O item superior na lista do Intellisense (0.4.5 no exemplo acima) é considerado a versão estável mais recente do pacote.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-143">The top item in the Intellisense list (0.4.5 in the example above) is considered the latest stable version of the package.</span></span> <span data-ttu-id="7b6cd-144">O símbolo de acento circunflexo (^) corresponde à versão principal mais recente e o til (~) corresponde a versão secundária mais recente.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-144">The caret (^) symbol matches the most recent major version and the tilde (~) matches the most recent minor version.</span></span> <span data-ttu-id="7b6cd-145">Consulte a [referência do analisador de versão do NPM semver](https://www.npmjs.com/package/semver) como um guia para a expressividade completa que fornece SemVer.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-145">See the [NPM semver version parser reference](https://www.npmjs.com/package/semver) as a guide to the full expressivity that SemVer provides.</span></span>

3. <span data-ttu-id="7b6cd-146">Adicionar mais dependências ao carregar o grunt-contrib -\* pacotes de *limpa*, *jshint*, *concat*, *tarefa uglify*e *inspeção* conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-146">Add more dependencies to load grunt-contrib-\* packages for *clean*, *jshint*, *concat*, *uglify*, and *watch* as shown in the example below.</span></span> <span data-ttu-id="7b6cd-147">As versões não precisam coincidir com o exemplo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-147">The versions don't need to match the example.</span></span>

    ```json
    "devDependencies": {
      "grunt": "0.4.5",
      "grunt-contrib-clean": "0.6.0",
      "grunt-contrib-jshint": "0.11.0",
      "grunt-contrib-concat": "0.5.1",
      "grunt-contrib-uglify": "0.8.0",
      "grunt-contrib-watch": "0.6.1"
    }
    ```

4. <span data-ttu-id="7b6cd-148">Salvar a *Package. JSON* arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-148">Save the *package.json* file.</span></span>

<span data-ttu-id="7b6cd-149">Baixarão os pacotes para cada item devDependencies, juntamente com todos os arquivos que requer que cada pacote.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-149">The packages for each devDependencies item will download, along with any files that each package requires.</span></span> <span data-ttu-id="7b6cd-150">Você pode encontrar os arquivos de pacote a `node_modules` diretório, permitindo a **Show All Files** botão no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-150">You can find the package files in the `node_modules` directory by enabling the **Show All Files** button in the Solution Explorer.</span></span>

![grunt node_modules](using-grunt/_static/node-modules.png)

> [!NOTE]
> <span data-ttu-id="7b6cd-152">Se necessário, você pode restaurar manualmente as dependências no Gerenciador de soluções clicando em `Dependencies\NPM` e selecionando os **restaurar pacotes** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-152">If you need to, you can manually restore dependencies in Solution Explorer by right-clicking on `Dependencies\NPM` and selecting the **Restore Packages** menu option.</span></span>

![Restaurar pacotes](using-grunt/_static/restore-packages.png)

## <a name="configuring-grunt"></a><span data-ttu-id="7b6cd-154">Configurando o Grunt</span><span class="sxs-lookup"><span data-stu-id="7b6cd-154">Configuring Grunt</span></span>

<span data-ttu-id="7b6cd-155">Grunt é configurado usando um manifesto chamado *gruntfile* que define, carrega e registra as tarefas que podem ser executadas manualmente ou configuradas para ser executado automaticamente com base em eventos no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-155">Grunt is configured using a manifest named *Gruntfile.js* that defines, loads and registers tasks that can be run manually or configured to run automatically based on events in Visual Studio.</span></span>

1. <span data-ttu-id="7b6cd-156">Clique com botão direito no projeto e selecione **Adicionar > Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-156">Right-click the project and select **Add > New Item**.</span></span> <span data-ttu-id="7b6cd-157">Selecione o **arquivo de configuração do Grunt** opção, deixe o nome padrão, *gruntfile*e clique no **Add** botão.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-157">Select the **Grunt Configuration file** option, leave the default name, *Gruntfile.js*, and click the **Add** button.</span></span>

   <span data-ttu-id="7b6cd-158">O código inicial inclui uma definição de módulo e o `grunt.initConfig()` método.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-158">The initial code includes a module definition and the `grunt.initConfig()` method.</span></span> <span data-ttu-id="7b6cd-159">O `initConfig()` é usado para definir opções para cada pacote, e o restante do módulo carregará e registrar tarefas.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-159">The `initConfig()` is used to set options for each package, and the remainder of the module will load and register tasks.</span></span>
    
   ```javascript
   module.exports = function (grunt) {
     grunt.initConfig({
     });
   };
   ```

2. <span data-ttu-id="7b6cd-160">Dentro de `initConfig()` método, adicionar opções para o `clean` conforme mostrado no exemplo de tarefa *gruntfile* abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-160">Inside the `initConfig()` method, add options for the `clean` task as shown in the example *Gruntfile.js* below.</span></span> <span data-ttu-id="7b6cd-161">A tarefa limpar aceita uma matriz de cadeias de caracteres de diretório.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-161">The clean task accepts an array of directory strings.</span></span> <span data-ttu-id="7b6cd-162">Essa tarefa remove os arquivos do wwwroot/lib e remove o diretório temp/inteiro.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-162">This task removes files from wwwroot/lib and removes the entire /temp directory.</span></span>

    ```javascript
    module.exports = function (grunt) {
      grunt.initConfig({
        clean: ["wwwroot/lib/*", "temp/"],
      });
    };
    ```

3. <span data-ttu-id="7b6cd-163">Abaixo do método initConfig(), adicione uma chamada para `grunt.loadNpmTasks()`.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-163">Below the initConfig() method, add a call to `grunt.loadNpmTasks()`.</span></span> <span data-ttu-id="7b6cd-164">Isso tornará a tarefa executável do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-164">This will make the task runnable from Visual Studio.</span></span>

    ```javascript
    grunt.loadNpmTasks("grunt-contrib-clean");
    ```

4. <span data-ttu-id="7b6cd-165">Salve *gruntfile*.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-165">Save *Gruntfile.js*.</span></span> <span data-ttu-id="7b6cd-166">O arquivo deve ser semelhante a captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-166">The file should look something like the screenshot below.</span></span>

    ![gruntfile inicial](using-grunt/_static/gruntfile-js-initial.png)

5. <span data-ttu-id="7b6cd-168">Clique com botão direito *gruntfile* e selecione **Task Runner Explorer** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-168">Right-click *Gruntfile.js* and select **Task Runner Explorer** from the context menu.</span></span> <span data-ttu-id="7b6cd-169">A janela do Task Runner Explorer será aberta.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-169">The Task Runner Explorer window will open.</span></span>

    ![menu do Gerenciador de executor de tarefas](using-grunt/_static/task-runner-explorer-menu.png)

6. <span data-ttu-id="7b6cd-171">Verifique `clean` mostra sob **tarefas** no Gerenciador de executor de tarefas.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-171">Verify that `clean` shows under **Tasks** in the Task Runner Explorer.</span></span>

    ![lista de tarefas do Gerenciador de executor de tarefas](using-grunt/_static/task-runner-explorer-tasks.png)

7. <span data-ttu-id="7b6cd-173">A tarefa limpar com o botão direito e selecione **executar** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-173">Right-click the clean task and select **Run** from the context menu.</span></span> <span data-ttu-id="7b6cd-174">Uma janela de comando exibe o progresso da tarefa.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-174">A command window displays progress of the task.</span></span>

    ![tarefa de limpeza runner explorer executar tarefa](using-grunt/_static/task-runner-explorer-run-clean.png)
    
    > [!NOTE]
    > <span data-ttu-id="7b6cd-176">Não há nenhum arquivo ou diretório para limpar ainda.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-176">There are no files or directories to clean yet.</span></span> <span data-ttu-id="7b6cd-177">Se desejar, você pode criá-las manualmente no Gerenciador de soluções e, em seguida, executar a tarefa de limpeza como um teste.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-177">If you like, you can manually create them in the Solution Explorer and then run the clean task as a test.</span></span>
    
8. <span data-ttu-id="7b6cd-178">No método initConfig(), adicione uma entrada para `concat` usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-178">In the initConfig() method, add an entry for `concat` using the code below.</span></span>

    <span data-ttu-id="7b6cd-179">O `src` matriz de propriedade lista arquivos combinar, na ordem em que eles devem ser combinados.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-179">The `src` property array lists files to combine, in the order that they should be combined.</span></span> <span data-ttu-id="7b6cd-180">O `dest` propriedade atribui o caminho para o arquivo combinado que é produzido.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-180">The `dest` property assigns the path to the combined file that's produced.</span></span>

    ```javascript
    concat: {
      all: {
        src: ['TypeScript/Tastes.js', 'TypeScript/Food.js'],
        dest: 'temp/combined.js'
      }
    },
    ```
    
    > [!NOTE]
    > <span data-ttu-id="7b6cd-181">O `all` propriedade no código acima é o nome de um destino.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-181">The `all` property in the code above is the name of a target.</span></span> <span data-ttu-id="7b6cd-182">Destinos são usados em algumas tarefas do Grunt para permitir que vários ambientes de compilação.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-182">Targets are used in some Grunt tasks to allow multiple build environments.</span></span> <span data-ttu-id="7b6cd-183">Você pode exibir os destinos internos usando o Intellisense ou atribuir seu próprio.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-183">You can view the built-in targets using Intellisense or assign your own.</span></span>
    
9. <span data-ttu-id="7b6cd-184">Adicionar o `jshint` de tarefas usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-184">Add the `jshint` task using the code below.</span></span>

    <span data-ttu-id="7b6cd-185">O utilitário de qualidade do código jshint é executado em todos os arquivos JavaScript encontrado no diretório temporário.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-185">The jshint code-quality utility is run against every JavaScript file found in the temp directory.</span></span>
    
    ```javascript
    jshint: {
      files: ['temp/*.js'],
      options: {
        '-W069': false,
      }
    },
    ```

    > [!NOTE]
    > <span data-ttu-id="7b6cd-186">A opção "-W069" é um erro gerado pela jshint quando o JavaScript usa a sintaxe para atribuir uma propriedade em vez de notação de ponto, ou seja, de colchete `Tastes["Sweet"]` em vez de `Tastes.Sweet`.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-186">The option "-W069" is an error produced by jshint when JavaScript uses bracket syntax to assign a property instead of dot notation, i.e. `Tastes["Sweet"]` instead of `Tastes.Sweet`.</span></span> <span data-ttu-id="7b6cd-187">A opção desliga o aviso para permitir que o restante do processo para continuar.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-187">The option turns off the warning to allow the rest of the process to continue.</span></span>

10. <span data-ttu-id="7b6cd-188">Adicionar o `uglify` de tarefas usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-188">Add the `uglify` task using the code below.</span></span>

    <span data-ttu-id="7b6cd-189">A tarefa minimiza a *combined.js* arquivo encontrado no diretório temp e cria o arquivo de resultado no seguindo a convenção de nomenclatura padrão wwwroot/lib  *\<nome do arquivo\>. Min*.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-189">The task minifies the *combined.js* file found in the temp directory and creates the result file in wwwroot/lib following the standard naming convention *\<file name\>.min.js*.</span></span>
    
    ```javascript
    uglify: {
     all: {
       src: ['temp/combined.js'],
       dest: 'wwwroot/lib/combined.min.js'
     }
    },
    ```

11. <span data-ttu-id="7b6cd-190">Em grunt.loadNpmTasks() a chamada que carrega o grunt-contrib-clean, inclua a mesma chamada para jshint, concat e tarefa uglify usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-190">Under the call grunt.loadNpmTasks() that loads grunt-contrib-clean, include the same call for jshint, concat and uglify using the code below.</span></span>
    
    ```javascript
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-concat');
    grunt.loadNpmTasks('grunt-contrib-uglify');
    ```

12. <span data-ttu-id="7b6cd-191">Salve *gruntfile*.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-191">Save *Gruntfile.js*.</span></span> <span data-ttu-id="7b6cd-192">O arquivo deve ser algo parecido com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-192">The file should look something like the example below.</span></span>

    ![exemplo de arquivo completo do grunt](using-grunt/_static/gruntfile-js-complete.png)

13. <span data-ttu-id="7b6cd-194">Observe que a lista de tarefas do Gerenciador de executor de tarefas inclui `clean`, `concat`, `jshint` e `uglify` tarefas.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-194">Notice that the Task Runner Explorer Tasks list includes `clean`, `concat`, `jshint` and `uglify` tasks.</span></span> <span data-ttu-id="7b6cd-195">Executar cada tarefa na ordem e observar os resultados no Gerenciador de soluções.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-195">Run each task in order and observe the results in Solution Explorer.</span></span> <span data-ttu-id="7b6cd-196">Cada tarefa deve ser executado sem erros.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-196">Each task should run without errors.</span></span>
    
    ![Gerenciador de executor executar cada tarefa](using-grunt/_static/task-runner-explorer-run-each-task.png)
    
    <span data-ttu-id="7b6cd-198">A tarefa concat cria um novo *combined.js* de arquivo e o coloca no diretório temporário.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-198">The concat task creates a new *combined.js* file and places it into the temp directory.</span></span> <span data-ttu-id="7b6cd-199">A tarefa jshint simplesmente é executado e não produz a saída.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-199">The jshint task simply runs and doesn't produce output.</span></span> <span data-ttu-id="7b6cd-200">A tarefa uglify cria um novo *combined.min.js* de arquivo e o coloca na wwwroot/lib.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-200">The uglify task creates a new *combined.min.js* file and places it into wwwroot/lib.</span></span> <span data-ttu-id="7b6cd-201">Após a conclusão, a solução deve ser algo parecido com a captura de tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="7b6cd-201">On completion, the solution should look something like the screenshot below:</span></span>
    
    ![Depois que todas as tarefas de Gerenciador de soluções](using-grunt/_static/solution-explorer-after-all-tasks.png)
    
    > [!NOTE]
    > <span data-ttu-id="7b6cd-203">Para obter mais informações sobre as opções para cada pacote, visite [ https://www.npmjs.com/ ](https://www.npmjs.com/) e pesquisa o nome do pacote na caixa de pesquisa na página principal.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-203">For more information on the options for each package, visit [https://www.npmjs.com/](https://www.npmjs.com/) and lookup the package name in the search box on the main page.</span></span> <span data-ttu-id="7b6cd-204">Por exemplo, você pode procurar o pacote grunt-contrib-clean para obter um link de documentação que explica todos os seus parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-204">For example, you can look up the grunt-contrib-clean package to get a documentation link that explains all of its parameters.</span></span>

### <a name="all-together-now"></a><span data-ttu-id="7b6cd-205">Todos juntos agora</span><span class="sxs-lookup"><span data-stu-id="7b6cd-205">All together now</span></span>

<span data-ttu-id="7b6cd-206">Usar o Grunt `registerTask()` método para executar uma série de tarefas em uma sequência específica.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-206">Use the Grunt `registerTask()` method to run a series of tasks in a particular sequence.</span></span> <span data-ttu-id="7b6cd-207">Por exemplo, para executar o exemplo etapas acima na ordem limpa -> concat -> jshint -> tarefa uglify, adicione o código a seguir para o módulo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-207">For example, to run the example steps above in the order clean -> concat -> jshint -> uglify, add the code below to the module.</span></span> <span data-ttu-id="7b6cd-208">O código deve ser adicionado ao mesmo nível que as chamadas loadNpmTasks(), fora initConfig.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-208">The code should be added to the same level as the loadNpmTasks() calls, outside initConfig.</span></span>

```javascript
grunt.registerTask("all", ['clean', 'concat', 'jshint', 'uglify']);
```

<span data-ttu-id="7b6cd-209">A nova tarefa aparece no Gerenciador do executor de tarefas em tarefas de Alias.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-209">The new task shows up in Task Runner Explorer under Alias Tasks.</span></span> <span data-ttu-id="7b6cd-210">Pode-se com o botão direito e executá-lo exatamente como faria com outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-210">You can right-click and run it just as you would other tasks.</span></span> <span data-ttu-id="7b6cd-211">O `all` tarefa será executada `clean`, `concat`, `jshint` e `uglify`, na ordem.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-211">The `all` task will run `clean`, `concat`, `jshint` and `uglify`, in order.</span></span>

![tarefas do grunt de alias](using-grunt/_static/alias-tasks.png)

## <a name="watching-for-changes"></a><span data-ttu-id="7b6cd-213">Monitorando alterações</span><span class="sxs-lookup"><span data-stu-id="7b6cd-213">Watching for changes</span></span>

<span data-ttu-id="7b6cd-214">Um `watch` tarefa fica de olho em arquivos e diretórios.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-214">A `watch` task keeps an eye on files and directories.</span></span> <span data-ttu-id="7b6cd-215">A inspeção dispara tarefas automaticamente se detectar alterações.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-215">The watch triggers tasks automatically if it detects changes.</span></span> <span data-ttu-id="7b6cd-216">Adicione o código abaixo ao initConfig observar alterações para \*arquivos. js no diretório do TypeScript.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-216">Add the code below to initConfig to watch for changes to \*.js files in the TypeScript directory.</span></span> <span data-ttu-id="7b6cd-217">Se um arquivo JavaScript for alterado, `watch` executará o `all` tarefa.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-217">If a JavaScript file is changed, `watch` will run the `all` task.</span></span>

```javascript
watch: {
  files: ["TypeScript/*.js"],
  tasks: ["all"]
}
```

<span data-ttu-id="7b6cd-218">Adicione uma chamada para `loadNpmTasks()` para mostrar o `watch` tarefa em Task Runner Explorer.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-218">Add a call to `loadNpmTasks()` to show the `watch` task in Task Runner Explorer.</span></span>

```javascript
grunt.loadNpmTasks('grunt-contrib-watch');
```

<span data-ttu-id="7b6cd-219">A tarefa de inspeção do Task Runner Explorer com o botão direito e selecione Executar no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-219">Right-click the watch task in Task Runner Explorer and select Run from the context menu.</span></span> <span data-ttu-id="7b6cd-220">A janela de comando que mostra a tarefa de inspeção em execução exibirá um "Aguardando..." Mensagem.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-220">The command window that shows the watch task running will display a "Waiting…" message.</span></span> <span data-ttu-id="7b6cd-221">Abra um dos arquivos TypeScript, adicione um espaço e, em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-221">Open one of the TypeScript files, add a space, and then save the file.</span></span> <span data-ttu-id="7b6cd-222">Isso disparar a tarefa de inspeção e disparar as outras tarefas executadas em ordem.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-222">This will trigger the watch task and trigger the other tasks to run in order.</span></span> <span data-ttu-id="7b6cd-223">Captura de tela abaixo mostra uma exemplo de execução.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-223">The screenshot below shows a sample run.</span></span>

![executar tarefas de saída](using-grunt/_static/watch-running.png)

## <a name="binding-to-visual-studio-events"></a><span data-ttu-id="7b6cd-225">Associação a eventos do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b6cd-225">Binding to Visual Studio events</span></span>

<span data-ttu-id="7b6cd-226">A menos que você deseja iniciar manualmente suas tarefas toda vez que você trabalha no Visual Studio, você pode vincular tarefas a serem **antes da compilação**, **depois de compilar**, **Clean**, e  **Projeto aberto** eventos.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-226">Unless you want to manually start your tasks every time you work in Visual Studio, you can bind tasks to **Before Build**, **After Build**, **Clean**, and **Project Open** events.</span></span>

<span data-ttu-id="7b6cd-227">Vamos associar `watch` para que ele seja executado sempre que o Visual Studio abre.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-227">Let’s bind `watch` so that it runs every time Visual Studio opens.</span></span> <span data-ttu-id="7b6cd-228">No Gerenciador de executor, a tarefa de inspeção com o botão direito e selecione **associações > Abrir projeto** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-228">In Task Runner Explorer, right-click the watch task and select **Bindings > Project Open** from the context menu.</span></span>

![associar uma tarefa para a abertura de projeto](using-grunt/_static/bindings-project-open.png)

<span data-ttu-id="7b6cd-230">Descarregue e recarregue o projeto.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-230">Unload and reload the project.</span></span> <span data-ttu-id="7b6cd-231">Quando o projeto for carregado novamente, a tarefa de inspeção iniciará a execução automática.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-231">When the project loads again, the watch task will start running automatically.</span></span>

## <a name="summary"></a><span data-ttu-id="7b6cd-232">Resumo</span><span class="sxs-lookup"><span data-stu-id="7b6cd-232">Summary</span></span>

<span data-ttu-id="7b6cd-233">Grunt é um executor de tarefas poderosa que pode ser usado para automatizar a maioria das tarefas de build do cliente.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-233">Grunt is a powerful task runner that can be used to automate most client-build tasks.</span></span> <span data-ttu-id="7b6cd-234">Grunt aproveita o NPM para fornecer seus pacotes, recursos e ferramentas de integração com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-234">Grunt leverages NPM to deliver its packages, and features tooling integration with Visual Studio.</span></span> <span data-ttu-id="7b6cd-235">Gerenciador de executor de tarefas do Visual Studio detecta alterações nos arquivos de configuração e fornece uma interface conveniente para executar tarefas, exibir tarefas em execução e vincular tarefas a eventos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b6cd-235">Visual Studio's Task Runner Explorer detects changes to configuration files and provides a convenient interface to run tasks, view running tasks, and bind tasks to Visual Studio events.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b6cd-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7b6cd-236">Additional resources</span></span>

   * [<span data-ttu-id="7b6cd-237">Usar o Gulp</span><span class="sxs-lookup"><span data-stu-id="7b6cd-237">Use Gulp</span></span>](using-gulp.md)
