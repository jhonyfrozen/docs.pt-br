---
title: Use o ML.NET em um cenário de detecção de anomalias de vendas
description: Descubra como usar o ML.NET em um cenário de detecção de anomalias de vendas de produto para compreender como analisar os dados de anomalias de ponto de alteração e picos para tomar as devidas providências.
ms.date: 05/06/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 39e812facccfa75d1643704f8960a387a70c94bc
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65641141"
---
# <a name="tutorial-use-mlnet-for-product-sales-anomaly-detection"></a><span data-ttu-id="62157-103">Tutorial: Use o ML.NET para detecção de anomalias de vendas do produto</span><span class="sxs-lookup"><span data-stu-id="62157-103">Tutorial: Use ML.NET for product sales anomaly detection</span></span> 

<span data-ttu-id="62157-104">Este tutorial de exemplo ilustra o uso do ML.NET para detectar anomalias nos dados de vendas de produto para executar a ação apropriada por meio de um aplicativo de console do .NET Core usando C# no Visual Studio de 2019.</span><span class="sxs-lookup"><span data-stu-id="62157-104">This sample tutorial illustrates using ML.NET to detect anomalies in product sales data to take the appropriate action via a .NET Core console application using C# in Visual Studio 2019.</span></span> 

<span data-ttu-id="62157-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="62157-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="62157-106">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="62157-106">Load the data</span></span>
> * <span data-ttu-id="62157-107">Treinar o modelo para detecção de anomalias de pico</span><span class="sxs-lookup"><span data-stu-id="62157-107">Train the model for spike anomaly detection</span></span>
> * <span data-ttu-id="62157-108">Detectar anomalias de pico com o modelo treinado</span><span class="sxs-lookup"><span data-stu-id="62157-108">Detect spike anomalies with the trained model</span></span>
> * <span data-ttu-id="62157-109">Treinar o modelo para detecção de anomalias de ponto de alteração</span><span class="sxs-lookup"><span data-stu-id="62157-109">Train the model for change point anomaly detection</span></span>
> * <span data-ttu-id="62157-110">Detectar anomalias de ponto de alteração com o modelo treinado</span><span class="sxs-lookup"><span data-stu-id="62157-110">Detect change point anomalies with the trained model</span></span>

<span data-ttu-id="62157-111">Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection).</span><span class="sxs-lookup"><span data-stu-id="62157-111">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) repository.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62157-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="62157-112">Prerequisites</span></span>

* <span data-ttu-id="62157-113">[Visual Studio 2017 15.6 ou posterior](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) com a carga de trabalho "Desenvolvimento de plataforma cruzada do .NET Core" instalada.</span><span class="sxs-lookup"><span data-stu-id="62157-113">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) with the ".NET Core cross-platform development" workload installed.</span></span>

* [<span data-ttu-id="62157-114">O conjunto de dados product-sales.csv</span><span class="sxs-lookup"><span data-stu-id="62157-114">The product-sales.csv dataset</span></span>](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)

>[!NOTE]
> <span data-ttu-id="62157-115">Os dados de formato em `product-sales.csv` baseiam-se no conjunto de dados "Vendas de xampu no período de três anos" originalmente adquiridos do DataMarket e fornecidos pela TSDL (Biblioteca de Dados de Série Temporal), criado por Rob Hyndman.</span><span class="sxs-lookup"><span data-stu-id="62157-115">The data format in `product-sales.csv` is based on the dataset “Shampoo Sales Over a Three Year Period” originally sourced from DataMarket and provided by Time Series Data Library (TSDL), created by Rob Hyndman.</span></span> <span data-ttu-id="62157-116">Conjunto de dados de "Vendas de xampu no período de três anos" licenciado sob a Licença Aberta Padrão do DataMarket.</span><span class="sxs-lookup"><span data-stu-id="62157-116">“Shampoo Sales Over a Three Year Period” Dataset Licensed Under the DataMarket Default Open License.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="62157-117">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="62157-117">Create a console application</span></span>

1. <span data-ttu-id="62157-118">Crie um **Aplicativo de Console do .NET Core** chamado "ProductSalesAnomalyDetection".</span><span class="sxs-lookup"><span data-stu-id="62157-118">Create a **.NET Core Console Application** called "ProductSalesAnomalyDetection".</span></span>

2. <span data-ttu-id="62157-119">Crie um diretório chamado *Data* no seu projeto para salvar os arquivos do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="62157-119">Create a directory named *Data* in your project to save your data set files.</span></span>

3. <span data-ttu-id="62157-120">Instalar o **Pacote NuGet Microsoft.ML**:</span><span class="sxs-lookup"><span data-stu-id="62157-120">Install the **Microsoft.ML NuGet Package**:</span></span>

    <span data-ttu-id="62157-121">No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="62157-121">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="62157-122">Escolha "nuget.org" como a origem do pacote, selecione a guia Procurar, pesquise **Microsoft.ML**, selecione o pacote **v1.0.0** na lista e selecione o botão **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="62157-122">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**, select the **v1.0.0** package in the list, and select the **Install** button.</span></span> <span data-ttu-id="62157-123">Selecione o botão **OK** na caixa de diálogo **Visualizar Alterações** e selecione o botão **Aceito** na caixa de diálogo **Aceitação da Licença**, se concordar com o termos de licença para os pacotes listados.</span><span class="sxs-lookup"><span data-stu-id="62157-123">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span> <span data-ttu-id="62157-124">Repita essas etapas para **Microsoft.ML.TimeSeries v0.12.0**.</span><span class="sxs-lookup"><span data-stu-id="62157-124">Repeat these steps for **Microsoft.ML.TimeSeries v0.12.0**.</span></span>

4. <span data-ttu-id="62157-125">Adicione as seguintes instruções `using` à parte superior do arquivo *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="62157-125">Add the following `using` statements at the top of your *Program.cs* file:</span></span>

    [!code-csharp[AddUsings](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a><span data-ttu-id="62157-126">Baixar os dados</span><span class="sxs-lookup"><span data-stu-id="62157-126">Download your data</span></span>

1. <span data-ttu-id="62157-127">Baixe o conjunto de dados e salve-o na pasta *Data* criada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="62157-127">Download the dataset and save it to the *Data* folder you previously created:</span></span>

   * <span data-ttu-id="62157-128">Clique com o botão direito do mouse em [*product-sales.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv) e selecione "Salvar Link (ou destino) como…"</span><span class="sxs-lookup"><span data-stu-id="62157-128">Right click on [*product-sales.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv) and select "Save Link (or Target) As..."</span></span>

     <span data-ttu-id="62157-129">Salve o arquivo \*.csv na pasta *Data* ou, depois de salvá-lo em outro lugar, mova o arquivo \*.csv para a pasta *Data*.</span><span class="sxs-lookup"><span data-stu-id="62157-129">Make sure you either save the \*.csv file to the *Data* folder, or after you save it elsewhere, move the \*.csv file to the *Data* folder.</span></span>

2. <span data-ttu-id="62157-130">No Gerenciador de Soluções, clique com o botão direito do mouse no arquivo \*.csv e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="62157-130">In Solution Explorer, right-click the \*.csv file and select **Properties**.</span></span> <span data-ttu-id="62157-131">Em **Avançado**, altere o valor de **Copiar para Diretório de Saída** para **Copiar se for mais novo**.</span><span class="sxs-lookup"><span data-stu-id="62157-131">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="62157-132">A tabela a seguir é uma visualização de dados do seu arquivo \*.csv:</span><span class="sxs-lookup"><span data-stu-id="62157-132">The following table is a data preview from your \*.csv file:</span></span>

|<span data-ttu-id="62157-133">Mês</span><span class="sxs-lookup"><span data-stu-id="62157-133">Month</span></span>  |<span data-ttu-id="62157-134">ProductSales</span><span class="sxs-lookup"><span data-stu-id="62157-134">ProductSales</span></span> |
|-------|-------------|
|<span data-ttu-id="62157-135">1-Jan</span><span class="sxs-lookup"><span data-stu-id="62157-135">1-Jan</span></span>  |    <span data-ttu-id="62157-136">271</span><span class="sxs-lookup"><span data-stu-id="62157-136">271</span></span>      |
|<span data-ttu-id="62157-137">2-Jan</span><span class="sxs-lookup"><span data-stu-id="62157-137">2-Jan</span></span>  |    <span data-ttu-id="62157-138">150.9</span><span class="sxs-lookup"><span data-stu-id="62157-138">150.9</span></span>    |
|<span data-ttu-id="62157-139">.....</span><span class="sxs-lookup"><span data-stu-id="62157-139">.....</span></span>  |    <span data-ttu-id="62157-140">.....</span><span class="sxs-lookup"><span data-stu-id="62157-140">.....</span></span>    |
|<span data-ttu-id="62157-141">1-Feb</span><span class="sxs-lookup"><span data-stu-id="62157-141">1-Feb</span></span>  |    <span data-ttu-id="62157-142">199.3</span><span class="sxs-lookup"><span data-stu-id="62157-142">199.3</span></span>    |
|<span data-ttu-id="62157-143">.....</span><span class="sxs-lookup"><span data-stu-id="62157-143">.....</span></span>  |    <span data-ttu-id="62157-144">.....</span><span class="sxs-lookup"><span data-stu-id="62157-144">.....</span></span>    |

### <a name="create-classes-and-define-paths"></a><span data-ttu-id="62157-145">Criar classes e definir demarcadores</span><span class="sxs-lookup"><span data-stu-id="62157-145">Create classes and define paths</span></span>

<span data-ttu-id="62157-146">Em seguida, defina a estrutura de dados de classe de entrada.</span><span class="sxs-lookup"><span data-stu-id="62157-146">Next, define your input class data structure.</span></span>

<span data-ttu-id="62157-147">Adicione uma nova classe ao seu projeto:</span><span class="sxs-lookup"><span data-stu-id="62157-147">Add a new class to your project:</span></span>

1. <span data-ttu-id="62157-148">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e, em seguida, selecione **Adicionar > Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="62157-148">In **Solution Explorer**, right-click the project, and then select **Add > New Item**.</span></span>

2. <span data-ttu-id="62157-149">Na caixa de diálogo **Adicionar Novo Item**, selecione **Classe** e altere o campo **Nome** para *ProductSalesData.cs*.</span><span class="sxs-lookup"><span data-stu-id="62157-149">In the **Add New Item dialog box**, select **Class** and change the **Name** field to *ProductSalesData.cs*.</span></span> <span data-ttu-id="62157-150">Em seguida, selecione o botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="62157-150">Then, select the **Add** button.</span></span>

<span data-ttu-id="62157-151">O arquivo *ProductSalesData.cs* é aberto no editor de códigos.</span><span class="sxs-lookup"><span data-stu-id="62157-151">The *ProductSalesData.cs* file opens in the code editor.</span></span> <span data-ttu-id="62157-152">Adicione a seguinte instrução `using` à parte superior do *ProductSalesData.cs*:</span><span class="sxs-lookup"><span data-stu-id="62157-152">Add the following `using` statement to the top of *ProductSalesData.cs*:</span></span>

```csharp
using Microsoft.ML.Data;
```

<span data-ttu-id="62157-153">Remova a definição de classe existente e adicione o seguinte código, que tem duas classes, `ProductSalesData` e `ProductSalesPrediction`, ao arquivo *ProductSalesData.cs*:</span><span class="sxs-lookup"><span data-stu-id="62157-153">Remove the existing class definition and add the following code, which has two classes `ProductSalesData` and `ProductSalesPrediction`, to the *ProductSalesData.cs* file:</span></span>

[!code-csharp[DeclareTypes](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/ProductSalesData.cs#DeclareTypes "Declare data record types")]

<span data-ttu-id="62157-154">`ProductSalesData` especifica uma classe de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="62157-154">`ProductSalesData` specifies an input data class.</span></span> <span data-ttu-id="62157-155">O atributo [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) especifica quais colunas (por índice de coluna) no conjunto de dados devem ser carregadas.</span><span class="sxs-lookup"><span data-stu-id="62157-155">The [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) attribute specifies which columns (by column index) in the dataset should be loaded.</span></span> 

<span data-ttu-id="62157-156">Adicione as seguintes instruções `using` adicionais ao início do arquivo *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="62157-156">Add the following additional `using` statements to the top of the *Program.cs* file:</span></span>

[!code-csharp[AddUsings](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddUsings "Add necessary usings")]

<span data-ttu-id="62157-157">Você precisa criar dois campos globais para armazenar o caminho do arquivo de conjunto de dados baixado recentemente e o caminho do arquivo de modelo salvo:</span><span class="sxs-lookup"><span data-stu-id="62157-157">You need to create two global fields to hold the recently downloaded dataset file path and the saved model file path:</span></span>

* <span data-ttu-id="62157-158">`_dataPath` tem o demarcador para o conjunto de dados usado para treinar o modelo.</span><span class="sxs-lookup"><span data-stu-id="62157-158">`_dataPath` has the path to the dataset used to train the model.</span></span>
* <span data-ttu-id="62157-159">O `_docsize` tem o número de registros no arquivo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="62157-159">`_docsize` has the number of records in dataset file.</span></span> <span data-ttu-id="62157-160">Você usará isso para calcular `pvalueHistoryLength`.</span><span class="sxs-lookup"><span data-stu-id="62157-160">You'll use this to calculate `pvalueHistoryLength`.</span></span>

<span data-ttu-id="62157-161">Adicione o seguinte código à linha logo acima do método `Main` para especificar estes caminhos:</span><span class="sxs-lookup"><span data-stu-id="62157-161">Add the following code to the line right above the `Main` method to specify those paths:</span></span>

[!code-csharp[Declare global variables](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DeclareGlobalVariables "Declare global variables")]

<span data-ttu-id="62157-162">A [classe MLContext](xref:Microsoft.ML.MLContext) é um ponto de partida para todas as operações do ML.NET e a inicialização do `mlContext` cria um ambiente do ML.NET que pode ser compartilhado entre os objetos de fluxo de trabalho da criação de modelo.</span><span class="sxs-lookup"><span data-stu-id="62157-162">The [MLContext class](xref:Microsoft.ML.MLContext) is a starting point for all ML.NET operations, and initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="62157-163">Ele é semelhante, conceitualmente, a `DBContext` no Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="62157-163">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

### <a name="initialize-variables-in-main"></a><span data-ttu-id="62157-164">Inicializar variáveis em Main</span><span class="sxs-lookup"><span data-stu-id="62157-164">Initialize variables in Main</span></span>

<span data-ttu-id="62157-165">Substitua a linha `Console.WriteLine("Hello World!")` no método `Main` pelo seguinte código para declarar e inicializar a variável `mlContext`:</span><span class="sxs-lookup"><span data-stu-id="62157-165">Replace the `Console.WriteLine("Hello World!")` line in the `Main` method with the following code to declare and initialize the `mlContext` variable:</span></span>

[!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateMLContext "Create the ML Context")]

### <a name="load-the-data"></a><span data-ttu-id="62157-166">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="62157-166">Load the data</span></span>

<span data-ttu-id="62157-167">Os dados do ML.NET são representados como uma [classe IDataView](xref:Microsoft.ML.IDataView).</span><span class="sxs-lookup"><span data-stu-id="62157-167">Data in ML.NET is represented as an [IDataView class](xref:Microsoft.ML.IDataView).</span></span> <span data-ttu-id="62157-168">`IDataView` é uma maneira flexível e eficiente de descrever dados tabulares (numéricos e texto).</span><span class="sxs-lookup"><span data-stu-id="62157-168">`IDataView` is a flexible, efficient way of describing tabular data (numeric and text).</span></span> <span data-ttu-id="62157-169">Os dados podem ser carregados de um arquivo de texto ou em tempo real (por exemplo, banco de dados SQL ou arquivos de log) para um objeto `IDataView`.</span><span class="sxs-lookup"><span data-stu-id="62157-169">Data can be loaded from a text file or in real time (for example, SQL database or log files) to an `IDataView` object.</span></span> <span data-ttu-id="62157-170">Adicione o seguinte código como a próxima linha do método `Main()`:</span><span class="sxs-lookup"><span data-stu-id="62157-170">Add the following code as the next line of the `Main()` method:</span></span>

[!code-csharp[LoadData](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#LoadData "loading dataset")]

<span data-ttu-id="62157-171">O [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) define o esquema de dados e lê o arquivo.</span><span class="sxs-lookup"><span data-stu-id="62157-171">The [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) defines the data schema and reads in the file.</span></span> <span data-ttu-id="62157-172">Ele usa as variáveis de caminho de dados e retorna uma `IDataView`.</span><span class="sxs-lookup"><span data-stu-id="62157-172">It takes in the data path variables and returns an `IDataView`.</span></span>

## <a name="ml-task---time-series-anomaly-detection"></a><span data-ttu-id="62157-173">Tarefa de ML – detecção de anomalias de série temporal</span><span class="sxs-lookup"><span data-stu-id="62157-173">ML task - time series anomaly detection</span></span> 

<span data-ttu-id="62157-174">Detecção de anomalias sinaliza comportamentos ou eventos incomuns ou inesperados.</span><span class="sxs-lookup"><span data-stu-id="62157-174">Anomaly detection flags unexpected or unusual events or behaviors.</span></span> <span data-ttu-id="62157-175">Ela dá dicas de em que local procurar problemas e ajuda a responder à pergunta "Isso é estranho?".</span><span class="sxs-lookup"><span data-stu-id="62157-175">It gives clues where to look for problems and helps you answer the question "Is this weird?".</span></span>

![Isso é estranho](./media/sales-anomaly-detection/anomalydetection.png)

<span data-ttu-id="62157-177">A detecção de anomalias é o processo de detectar exceções de dados de série temporal; pontos em uma série temporal de entrada em que o comportamento não é o esperado ou "estranho".</span><span class="sxs-lookup"><span data-stu-id="62157-177">Anomaly detection is the process of detecting time-series data outliers; points on a given input time-series where the behavior isn't what was expected, or "weird".</span></span>

<span data-ttu-id="62157-178">Isso pode ser útil de várias formas.</span><span class="sxs-lookup"><span data-stu-id="62157-178">This can be useful in lots of ways.</span></span> <span data-ttu-id="62157-179">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="62157-179">For instance:</span></span>

<span data-ttu-id="62157-180">Se você tiver um carro, talvez queira saber: Essa leitura do medidor de gasolina está normal ou tenho um vazamento?</span><span class="sxs-lookup"><span data-stu-id="62157-180">If you have a car, you might want to know: Is this oil gauge reading normal, or do I have a leak?</span></span>
<span data-ttu-id="62157-181">Se você estiver monitorando o consumo de energia, vai querer saber: Há uma interrupção?</span><span class="sxs-lookup"><span data-stu-id="62157-181">If you're monitoring power consumption, you’d want to know: Is there an outage?</span></span>

<span data-ttu-id="62157-182">Há dois tipos de anomalias de série temporal que podem ser detectados:</span><span class="sxs-lookup"><span data-stu-id="62157-182">There are two types of time series anomalies that can be detected:</span></span> 

* <span data-ttu-id="62157-183">**Picos** indicam intermitências temporárias de comportamentos anormais no sistema.</span><span class="sxs-lookup"><span data-stu-id="62157-183">**Spikes** indicate temporary bursts of anomalous behavior in the system.</span></span> 

* <span data-ttu-id="62157-184">**Pontos de alteração** indicam o início de alterações persistentes ao longo do tempo no sistema.</span><span class="sxs-lookup"><span data-stu-id="62157-184">**Change points** indicate the beginning of persistent changes over time in the system.</span></span> 

<span data-ttu-id="62157-185">No ML.NET, os algoritmos de Detecção de Pico IID ou Detecção de Ponto de Alteração IID são adequados para [conjuntos de dados independentes e distribuídos de forma idêntica](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables).</span><span class="sxs-lookup"><span data-stu-id="62157-185">In ML.NET, The IID Spike Detection or IID Change point Detection algorithms are suited for [independent and identically distributed datasets](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables).</span></span> 

<span data-ttu-id="62157-186">Você vai analisar os mesmos dados de vendas do produto para detectar picos e pontos de alteração.</span><span class="sxs-lookup"><span data-stu-id="62157-186">You'll analyze the same product sales data to detect spikes and change points.</span></span> <span data-ttu-id="62157-187">O processo de criar e treinar o modelo é o mesmo para detecção de pico e detecção de ponto de alteração; a principal diferença é o algoritmo de detecção específico usado.</span><span class="sxs-lookup"><span data-stu-id="62157-187">The building and training model process is the same for spike detection and change point detection; the main difference is the specific detection algorithm used.</span></span>

## <a name="spike-detection"></a><span data-ttu-id="62157-188">Detecção de pico</span><span class="sxs-lookup"><span data-stu-id="62157-188">Spike detection</span></span> 

<span data-ttu-id="62157-189">A meta da detecção de pico é identificar picos repentinos, mas temporários, que diferem significativamente da maioria dos valores de dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="62157-189">The goal of spike detection is to identify sudden yet temporary bursts that significantly differ from the majority of the time series data values.</span></span> <span data-ttu-id="62157-190">É importante detectar esses itens raros, eventos ou observações suspeitos de maneira oportuna para que sejam minimizados.</span><span class="sxs-lookup"><span data-stu-id="62157-190">It's important to detect these suspicious rare items, events or observations in a timely manner to be minimized.</span></span> <span data-ttu-id="62157-191">A abordagem a seguir pode ser usada para detectar uma variedade de anomalias, como: interrupções, ataques cibernéticos ou conteúdo da Web viral.</span><span class="sxs-lookup"><span data-stu-id="62157-191">The following approach can be used to detect a variety of anomalies such as: outages, cyber-attacks, or viral web content.</span></span> <span data-ttu-id="62157-192">A imagem a seguir é um exemplo de picos em um conjunto de dados de série temporal:</span><span class="sxs-lookup"><span data-stu-id="62157-192">The following image is an example of spikes in a time series dataset:</span></span>

![SpikeDetection](./media/sales-anomaly-detection/SpikeDetection.png)

### <a name="create-the-detectspike-method"></a><span data-ttu-id="62157-194">Crie o método DetectSpike()</span><span class="sxs-lookup"><span data-stu-id="62157-194">Create the DetectSpike() method</span></span>

<span data-ttu-id="62157-195">Adicione a seguinte chamada ao método `DetectSpike()` como a próxima linha de código no método `Main()`:</span><span class="sxs-lookup"><span data-stu-id="62157-195">Add the following call to the `DetectSpike()`method as the next line of code in the `Main()` method:</span></span>

[!code-csharp[CallDetectSpike](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectSpike)]

<span data-ttu-id="62157-196">O método `DetectSpike()` executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="62157-196">The `DetectSpike()` method executes the following tasks:</span></span>

* <span data-ttu-id="62157-197">Treina o modelo.</span><span class="sxs-lookup"><span data-stu-id="62157-197">Trains the model.</span></span>
* <span data-ttu-id="62157-198">Detecta picos com base em dados históricos de vendas.</span><span class="sxs-lookup"><span data-stu-id="62157-198">Detects spikes based on on historical sales data.</span></span>
* <span data-ttu-id="62157-199">Exibe os resultados.</span><span class="sxs-lookup"><span data-stu-id="62157-199">Displays the results.</span></span>

<span data-ttu-id="62157-200">Crie o método `DetectSpike()`, logo após o método `Main()`, usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="62157-200">Create the `DetectSpike()` method, just after the `Main()` method, using the following code:</span></span>

```csharp
static void DetectSpike(MLContext mlContext, int docSize, IDataView productSales)
{

}
```

<span data-ttu-id="62157-201">Use [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator) para treinar o modelo para a detecção de pico.</span><span class="sxs-lookup"><span data-stu-id="62157-201">Use the [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator) to train the model for spike detection.</span></span> <span data-ttu-id="62157-202">Adicione-o ao método `DetectChangepoint()` com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="62157-202">Add it to the `DetectChangepoint()` method with the following code:</span></span>

[!code-csharp[AddSpikeTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddSpikeTrainer)]

<span data-ttu-id="62157-203">Ajuste o modelo aos dados `productSales` e retorne o modelo treinado adicionando o seguinte como a próxima linha de código no método `DetectSpike()`:</span><span class="sxs-lookup"><span data-stu-id="62157-203">Fit the model to the `productSales` data and return the trained model by adding the following as the next line of code in the `DetectSpike()` method:</span></span>

[!code-csharp[TrainModel1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel1)]

<span data-ttu-id="62157-204">O método [Fit()](xref:Microsoft.ML.Data.TrivialEstimator%601.Fit%2A) treina o modelo transformando o conjunto de dados e aplicando o treinamento.</span><span class="sxs-lookup"><span data-stu-id="62157-204">The [Fit()](xref:Microsoft.ML.Data.TrivialEstimator%601.Fit%2A) method trains your model by transforming the dataset and applying the training.</span></span>

<span data-ttu-id="62157-205">Adicione a seguinte linha de código para transformar os dados `productSales` como a próxima linha no método `DetectSpike()`:</span><span class="sxs-lookup"><span data-stu-id="62157-205">Add the following line of code to transform the `productSales` data as the next line in the `DetectSpike()` method:</span></span>

[!code-csharp[TransformData1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData1)]

<span data-ttu-id="62157-206">O código anterior usa o método [Transform](xref:Microsoft.ML.ITransformer.Transform%2A) para fazer previsões para várias linhas de entrada fornecidas por um conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="62157-206">The previous code uses the [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) method to make predictions for multiple provided input rows of a test dataset.</span></span>

<span data-ttu-id="62157-207">Converta seu `transformedData` em um `IEnumerable` fortemente tipado para exibição mais fácil usando o método [CreateEnumerable()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="62157-207">Convert your `transformedData` into a strongly-typed `IEnumerable` for easier display using the [CreateEnumerable()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) method with the following code:</span></span>

[!code-csharp[CreateEnumerable1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable1)]

<span data-ttu-id="62157-208">Crie uma linha de cabeçalho de exibição usando o seguinte código <xref:System.Console.WriteLine?displayProperty=nameWithType>:</span><span class="sxs-lookup"><span data-stu-id="62157-208">Create a display header line using the following <xref:System.Console.WriteLine?displayProperty=nameWithType> code:</span></span>

[!code-csharp[DisplayHeader1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader1)]

<span data-ttu-id="62157-209">Você exibirá as informações a seguir nos resultados da detecção de pico:</span><span class="sxs-lookup"><span data-stu-id="62157-209">You'll display the following information in your spike detection results:</span></span>

* <span data-ttu-id="62157-210">`Alert` indica um alerta de pico para um ponto de dados específico.</span><span class="sxs-lookup"><span data-stu-id="62157-210">`Alert` indicates a spike alert for a given data point.</span></span>

* <span data-ttu-id="62157-211">`Score` é o valor `ProductSales` para um dado ponto de dados no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="62157-211">`Score` is the `ProductSales` value for a given data point in the dataset.</span></span>

* <span data-ttu-id="62157-212">`P-Value` O "P" significa probabilidade.</span><span class="sxs-lookup"><span data-stu-id="62157-212">`P-Value` The "P" stands for probability.</span></span> <span data-ttu-id="62157-213">Isso indica a probabilidade de esse ponto de dados ser uma anomalia.</span><span class="sxs-lookup"><span data-stu-id="62157-213">This indicates how likely this data point is an anomaly.</span></span> 

<span data-ttu-id="62157-214">Use o seguinte código para iterar por `predictions` `IEnumerable` e exibir os resultados:</span><span class="sxs-lookup"><span data-stu-id="62157-214">Use the following code to iterate through the `predictions` `IEnumerable` and display the results:</span></span>

[!code-csharp[DisplayResults1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults1)]

## <a name="spike-detection-results"></a><span data-ttu-id="62157-215">Resultados da detecção de pico</span><span class="sxs-lookup"><span data-stu-id="62157-215">Spike detection results</span></span>

<span data-ttu-id="62157-216">Seus resultados devem ser semelhantes aos seguintes.</span><span class="sxs-lookup"><span data-stu-id="62157-216">Your results should be similar to the following.</span></span> <span data-ttu-id="62157-217">Durante o processamento, as mensagens são exibidas.</span><span class="sxs-lookup"><span data-stu-id="62157-217">During processing, messages are displayed.</span></span> <span data-ttu-id="62157-218">Você pode ver avisos ou mensagens de processamento.</span><span class="sxs-lookup"><span data-stu-id="62157-218">You may see warnings, or processing messages.</span></span> <span data-ttu-id="62157-219">Eles foram removidos dos seguintes resultados para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="62157-219">These have been removed from the following results for clarity.</span></span>

```console
Detect temporary changes in pattern
=============== Training the model ===============
=============== End of training process ===============
Alert   Score   P-Value
0       271.00  0.50
0       150.90  0.00
0       188.10  0.41
0       124.30  0.13
0       185.30  0.47
0       173.50  0.47
0       236.80  0.19
0       229.50  0.27
0       197.80  0.48
0       127.90  0.13
1       341.50  0.00 <-- Spike detected
0       190.90  0.48
0       199.30  0.48
0       154.50  0.24
0       215.10  0.42
0       278.30  0.19
0       196.40  0.43
0       292.00  0.17
0       231.00  0.45
0       308.60  0.18
0       294.90  0.19
1       426.60  0.00 <-- Spike detected
0       269.50  0.47
0       347.30  0.21
0       344.70  0.27
0       445.40  0.06
0       320.90  0.49
0       444.30  0.12
0       406.30  0.29
0       442.40  0.21
1       580.50  0.00 <-- Spike detected
0       412.60  0.45
1       687.00  0.01 <-- Spike detected
0       480.30  0.40
0       586.30  0.20
0       651.90  0.14
```

## <a name="change-point-detection"></a><span data-ttu-id="62157-220">Detecção de ponto de alteração</span><span class="sxs-lookup"><span data-stu-id="62157-220">Change point detection</span></span>

<span data-ttu-id="62157-221">`Change points` são alterações persistentes em uma distribuição de valores de fluxo de evento de série temporal, como alterações de nível e tendências.</span><span class="sxs-lookup"><span data-stu-id="62157-221">`Change points` are persistent changes in a time series event stream distribution of values, like level changes and trends.</span></span> <span data-ttu-id="62157-222">Essas alterações persistentes duram muito mais que `spikes` e podem indicar eventos catastróficos.</span><span class="sxs-lookup"><span data-stu-id="62157-222">These persistent changes last much longer than `spikes` and could indicate catastrophic event(s).</span></span> <span data-ttu-id="62157-223">`Change points` normalmente não estão visíveis a olho nu, mas podem ser detectados em seus dados usando abordagens como o método a seguir.</span><span class="sxs-lookup"><span data-stu-id="62157-223">`Change points` are not usually visible to the naked eye, but can be detected in your data using approaches such as in the following method.</span></span>  <span data-ttu-id="62157-224">A imagem a seguir é um exemplo de uma detecção de ponto de alteração:</span><span class="sxs-lookup"><span data-stu-id="62157-224">The following image is an example of a change point detection:</span></span>

![ChangePointDetection](./media/sales-anomaly-detection/ChangePointDetection.png)

### <a name="create-the-detectchangepoint-method"></a><span data-ttu-id="62157-226">Crie o método DetectChangepoint()</span><span class="sxs-lookup"><span data-stu-id="62157-226">Create the DetectChangepoint() method</span></span>

<span data-ttu-id="62157-227">Adicione a seguinte chamada ao método `DetectChangepoint()` como a próxima linha de código no método `Main()`:</span><span class="sxs-lookup"><span data-stu-id="62157-227">Add the following call to the `DetectChangepoint()`method as the next line of code in the `Main()` method:</span></span>

[!code-csharp[CallDetectChangepoint](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectChangepoint)]

<span data-ttu-id="62157-228">O método `DetectChangepoint()` executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="62157-228">The `DetectChangepoint()` method executes the following tasks:</span></span>

* <span data-ttu-id="62157-229">Treina o modelo.</span><span class="sxs-lookup"><span data-stu-id="62157-229">Trains the model.</span></span>
* <span data-ttu-id="62157-230">Detecta pontos de alteração com base em dados históricos de vendas.</span><span class="sxs-lookup"><span data-stu-id="62157-230">Detects change points based on historical sales data.</span></span>
* <span data-ttu-id="62157-231">Exibe os resultados.</span><span class="sxs-lookup"><span data-stu-id="62157-231">Displays the results.</span></span>

<span data-ttu-id="62157-232">Crie o método `DetectChangepoint()`, logo após o método `Main()`, usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="62157-232">Create the `DetectChangepoint()` method, just after the `Main()` method, using the following code:</span></span>

```csharp
static void DetectChangepoint(MLContext mlContext, int docSize, IDataView productSales)
{

}
```

<span data-ttu-id="62157-233">O [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator) é usado para treinar o modelo para a detecção de ponto de alteração.</span><span class="sxs-lookup"><span data-stu-id="62157-233">The [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator) is used to train the model for change point detection.</span></span> <span data-ttu-id="62157-234">Adicione-o ao método `DetectChangepoint()` com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="62157-234">Add it to the `DetectChangepoint()` method with the following code:</span></span>

[!code-csharp[AddChangepointTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddChangepointTrainer)]

<span data-ttu-id="62157-235">Como você fez antes, ajuste o modelo aos dados `productSales` e retorne o modelo treinado adicionando o seguinte como a próxima linha de código no método `DetectChangePoint()`:</span><span class="sxs-lookup"><span data-stu-id="62157-235">As you did previously, fit the model to the `productSales` data and return the trained model by adding the following as the next line of code in the `DetectChangePoint()` method:</span></span>

[!code-csharp[TrainModel2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel2)]

<span data-ttu-id="62157-236">Use o método `Transform()` para transformar os dados `Training` adicionando o seguinte código a `DetectChangePoint()`:</span><span class="sxs-lookup"><span data-stu-id="62157-236">Use the `Transform()` method to transform the `Training` data by adding the following code to `DetectChangePoint()`:</span></span>

[!code-csharp[TransformData2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData2)]

<span data-ttu-id="62157-237">Como você fez antes, converta seu `transformedData` em um `IEnumerable` fortemente tipado para exibição mais fácil usando o método `CreateEnumerable()` com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="62157-237">As you did previously, convert your `transformedData` into a strongly-typed `IEnumerable` for easier display using the `CreateEnumerable()`method with the following code:</span></span>

[!code-csharp[CreateEnumerable2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable2)]

<span data-ttu-id="62157-238">Crie um cabeçalho de exibição com o código a seguir como a próxima linha no método `DetectChangePoint()`:</span><span class="sxs-lookup"><span data-stu-id="62157-238">Create a display header with the following code as the next line in the `DetectChangePoint()` method:</span></span>

[!code-csharp[DisplayHeader2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader2)]

<span data-ttu-id="62157-239">Você exibirá as informações a seguir nos resultados da detecção de ponto de alteração:</span><span class="sxs-lookup"><span data-stu-id="62157-239">You'll display the following information in your change point detection results:</span></span>

* <span data-ttu-id="62157-240">`Alert` indica um alerta de ponto de alteração para um ponto de dados específico.</span><span class="sxs-lookup"><span data-stu-id="62157-240">`Alert` indicates a change point alert for a given data point.</span></span>
* <span data-ttu-id="62157-241">`Score` é o valor `ProductSales` para um dado ponto de dados no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="62157-241">`Score` is the `ProductSales` value for a given data point in the dataset.</span></span>
* <span data-ttu-id="62157-242">`P-Value` O "P" significa probabilidade.</span><span class="sxs-lookup"><span data-stu-id="62157-242">`P-Value` The "P" stands for probability.</span></span> <span data-ttu-id="62157-243">Isso indica a probabilidade de esse ponto de dados ser uma anomalia.</span><span class="sxs-lookup"><span data-stu-id="62157-243">This indicates how likely this data point is an anomaly.</span></span> 
* <span data-ttu-id="62157-244">`Martingale value` é usado para identificar o quão "estranho" um ponto de dados é com base na sequência de valores de P.</span><span class="sxs-lookup"><span data-stu-id="62157-244">`Martingale value` is used to identify how "weird" a data point is, based on the sequence of P-values.</span></span>  

<span data-ttu-id="62157-245">Itere por `predictions` `IEnumerable` e exiba os resultados com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="62157-245">Iterate through the `predictions` `IEnumerable` and display the results with the following code:</span></span>

[!code-csharp[DisplayResults2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults2)]

## <a name="change-point-detection-results"></a><span data-ttu-id="62157-246">Resultados da detecção de ponto de alteração</span><span class="sxs-lookup"><span data-stu-id="62157-246">Change point detection results</span></span>

<span data-ttu-id="62157-247">Seus resultados devem ser semelhantes aos seguintes.</span><span class="sxs-lookup"><span data-stu-id="62157-247">Your results should be similar to the following.</span></span> <span data-ttu-id="62157-248">Durante o processamento, as mensagens são exibidas.</span><span class="sxs-lookup"><span data-stu-id="62157-248">During processing, messages are displayed.</span></span> <span data-ttu-id="62157-249">Você pode ver avisos ou mensagens de processamento.</span><span class="sxs-lookup"><span data-stu-id="62157-249">You may see warnings, or processing messages.</span></span> <span data-ttu-id="62157-250">Eles foram removidos dos seguintes resultados para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="62157-250">These have been removed from the following results for clarity.</span></span>

```console
Detect Persistent changes in pattern
=============== Training the model Using Change Point Detection Algorithm===============
=============== End of training process ===============
Alert   Score   P-Value Martingale value
0       271.00  0.50    0.00
0       150.90  0.00    2.33
0       188.10  0.41    2.80
0       124.30  0.13    9.16
0       185.30  0.47    9.77
0       173.50  0.47    10.41
0       236.80  0.19    24.46
0       229.50  0.27    42.38
1       197.80  0.48    44.23 <-- alert is on, predicted changepoint
0       127.90  0.13    145.25
0       341.50  0.00    0.01
0       190.90  0.48    0.01
0       199.30  0.48    0.00
0       154.50  0.24    0.00
0       215.10  0.42    0.00
0       278.30  0.19    0.00
0       196.40  0.43    0.00
0       292.00  0.17    0.01
0       231.00  0.45    0.00
0       308.60  0.18    0.00
0       294.90  0.19    0.00
0       426.60  0.00    0.00
0       269.50  0.47    0.00
0       347.30  0.21    0.00
0       344.70  0.27    0.00
0       445.40  0.06    0.02
0       320.90  0.49    0.01
0       444.30  0.12    0.02
0       406.30  0.29    0.01
0       442.40  0.21    0.01
0       580.50  0.00    0.01
0       412.60  0.45    0.01
0       687.00  0.01    0.12
0       480.30  0.40    0.08
0       586.30  0.20    0.03
0       651.90  0.14    0.09
```

<span data-ttu-id="62157-251">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="62157-251">Congratulations!</span></span> <span data-ttu-id="62157-252">Você agora criou com êxito os modelos de machine learning para detectar anomalias de pontos de alteração e picos nos dados de vendas.</span><span class="sxs-lookup"><span data-stu-id="62157-252">You've now successfully built machine learning models for detecting spikes and change point anomalies in sales data.</span></span>

<span data-ttu-id="62157-253">Você pode encontrar o código-fonte para este tutorial no repositório [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection).</span><span class="sxs-lookup"><span data-stu-id="62157-253">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) repository.</span></span>

<span data-ttu-id="62157-254">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="62157-254">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="62157-255">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="62157-255">Load the data</span></span>
> * <span data-ttu-id="62157-256">Treinar o modelo para detecção de anomalias de pico</span><span class="sxs-lookup"><span data-stu-id="62157-256">Train the model for spike anomaly detection</span></span>
> * <span data-ttu-id="62157-257">Detectar anomalias de pico com o modelo treinado</span><span class="sxs-lookup"><span data-stu-id="62157-257">Detect spike anomalies with the trained model</span></span>
> * <span data-ttu-id="62157-258">Treinar o modelo para detecção de anomalias de ponto de alteração</span><span class="sxs-lookup"><span data-stu-id="62157-258">Train the model for change point anomaly detection</span></span>
> * <span data-ttu-id="62157-259">Detectar anomalias de ponto de alteração com o modo treinado</span><span class="sxs-lookup"><span data-stu-id="62157-259">Detect change point anomalies with the trained mode</span></span>

## <a name="next-steps"></a><span data-ttu-id="62157-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="62157-260">Next steps</span></span>

<span data-ttu-id="62157-261">Confira o repositório do GitHub de exemplos de Machine Learning para explorar um exemplo de Detecção de Anomalias de Consumo de Energia.</span><span class="sxs-lookup"><span data-stu-id="62157-261">Check out the Machine Learning samples GitHub repository to explore a Power Consumption Anomaly Detection sample.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="62157-262">dotnet/machinelearning-samples GitHub repository</span><span class="sxs-lookup"><span data-stu-id="62157-262">dotnet/machinelearning-samples GitHub repository</span></span>](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/TimeSeries_PowerAnomalyDetection)