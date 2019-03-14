---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059633"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="a593e-101">Demonstração de model binding personalizado</span><span class="sxs-lookup"><span data-stu-id="a593e-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="a593e-102">Teste o `ByteArrayModelBinder` executando o aplicativo e postando uma cadeia de caracteres codificada em Base64 no ponto de extremidade `ImageController` (`/api/image/`).</span><span class="sxs-lookup"><span data-stu-id="a593e-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="a593e-103">Especifique as propriedades de arquivo e de nome de arquivo no corpo da solicitação como dados de formulário (usando o [Postman](https://www.getpostman.com/) ou uma ferramenta semelhante).</span><span class="sxs-lookup"><span data-stu-id="a593e-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="a593e-104">Use [esta cadeia de caracteres de exemplo](Base64String.txt).</span><span class="sxs-lookup"><span data-stu-id="a593e-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="a593e-105">O resultado é salvo na pasta *wwwroot/images/upload* com o nome do arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="a593e-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="a593e-106">Para testar o exemplo de associação personalizada, experimente os seguintes pontos de extremidade:</span><span class="sxs-lookup"><span data-stu-id="a593e-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="a593e-107">/api/authors/1</span><span class="sxs-lookup"><span data-stu-id="a593e-107">/api/authors/1</span></span>
* <span data-ttu-id="a593e-108">/api/authors/2 (NOT FOUND)</span><span class="sxs-lookup"><span data-stu-id="a593e-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="a593e-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="a593e-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="a593e-110">/api/boundauthors/2 (NOT FOUND)</span><span class="sxs-lookup"><span data-stu-id="a593e-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="a593e-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="a593e-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="a593e-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; Essa ação não verifica se há nulos e retorna um *404 Não Encontrado*.</span><span class="sxs-lookup"><span data-stu-id="a593e-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
