### <a name="deflatestream-uses-native-apis-for-decompression"></a><span data-ttu-id="46360-101">O DeflateStream usa APIs nativas para descompactação</span><span class="sxs-lookup"><span data-stu-id="46360-101">DeflateStream uses native APIs for decompression</span></span>

|   |   |
|---|---|
|<span data-ttu-id="46360-102">Detalhes</span><span class="sxs-lookup"><span data-stu-id="46360-102">Details</span></span>|<span data-ttu-id="46360-103">Começando com o .NET Framework 4.7.2, a implementação da descompactação na classe <code>T:System.IO.Compression.DeflateStream</code> foi alterada para usar APIs nativas do Windows por padrão.</span><span class="sxs-lookup"><span data-stu-id="46360-103">Starting with the .NET Framework 4.7.2, the implementation of decompression in the <code>T:System.IO.Compression.DeflateStream</code> class has changed to use native Windows APIs by default.</span></span> <span data-ttu-id="46360-104">Normalmente, isso resulta em uma melhoria significativa de desempenho.</span><span class="sxs-lookup"><span data-stu-id="46360-104">Typically, this results in a substantial performance improvement.</span></span> <span data-ttu-id="46360-105">Todos os aplicativos .NET direcionados ao .NET Framework versão 4.7.2 ou superior usam a implementação nativo. Essa alteração pode resultar em algumas diferenças no comportamento, que incluem:</span><span class="sxs-lookup"><span data-stu-id="46360-105">All .NET applications targeting the .NET Framework version 4.7.2 or higher use the native implementation.This change might result in some differences in behavior, which include:</span></span><ul><li><span data-ttu-id="46360-106">As mensagens de exceção podem ser diferentes.</span><span class="sxs-lookup"><span data-stu-id="46360-106">Exception messages may be different.</span></span> <span data-ttu-id="46360-107">No entanto, o tipo de exceção gerada permanece o mesmo.</span><span class="sxs-lookup"><span data-stu-id="46360-107">However, the type of exception thrown remains the same.</span></span></li><li><span data-ttu-id="46360-108">Algumas situações especiais, como não ter memória suficiente para concluir uma operação, podem ser tratadas de maneira diferente.</span><span class="sxs-lookup"><span data-stu-id="46360-108">Some special situations, such as not having enough memory to complete an operation, may be handled differently.</span></span></li><li><span data-ttu-id="46360-109">Existem diferenças conhecidas para analisar o cabeçalho gzip (observação: somente o <code>GZipStream</code> definido para descompactação é afetado):</span><span class="sxs-lookup"><span data-stu-id="46360-109">There are known differences for parsing gzip header (note: only <code>GZipStream</code> set for decompression is affected):</span></span></li><li><span data-ttu-id="46360-110">As exceções durante a análise de cabeçalhos inválidos podem ser geradas em momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="46360-110">Exceptions when parsing invalid headers may be thrown at different times.</span></span></li><li><span data-ttu-id="46360-111">A implementação nativa impõe que os valores de alguns sinalizadores reservados dentro do cabeçalho gzip (ou seja, [FLG](http://www.zlib.org/rfc-gzip.html#header-trailer)) são definidos de acordo com a especificação, o que pode causar a geração de uma exceção em casos em que, anteriormente, valores inválidos eram ignorados.</span><span class="sxs-lookup"><span data-stu-id="46360-111">The native implementation enforces that values for some reserved flags inside the gzip header (i.e. [FLG](http://www.zlib.org/rfc-gzip.html#header-trailer)) are set according to the specification, which may cause it to throw an exception where previously invalid values were ignored.</span></span></li></ul>|
|<span data-ttu-id="46360-112">Sugestão</span><span class="sxs-lookup"><span data-stu-id="46360-112">Suggestion</span></span>|<span data-ttu-id="46360-113">Se a descompactação com as APIs nativas tiver prejudicado o comportamento do aplicativo, você poderá recusar esse recurso adicionando a opção <code>Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression</code> à seção <code>runtime</code> do arquivo app.config e configurando-a como <code>true</code>:</span><span class="sxs-lookup"><span data-stu-id="46360-113">If decompression with native APIs has adversely affected the behavior of your app, you can opt out of this feature by adding the <code>Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression</code> switch to the <code>runtime</code> section of your app.config file and setting it to <code>true</code>:</span></span><pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot; ?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides&#13;&#10;value=&quot;Switch.System.IO.Compression.DoNotUseNativeZipLibraryForDecompression=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="46360-114">Escopo</span><span class="sxs-lookup"><span data-stu-id="46360-114">Scope</span></span>|<span data-ttu-id="46360-115">Secundário</span><span class="sxs-lookup"><span data-stu-id="46360-115">Minor</span></span>|
|<span data-ttu-id="46360-116">Versão</span><span class="sxs-lookup"><span data-stu-id="46360-116">Version</span></span>|<span data-ttu-id="46360-117">4.7.2</span><span class="sxs-lookup"><span data-stu-id="46360-117">4.7.2</span></span>|
|<span data-ttu-id="46360-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="46360-118">Type</span></span>|<span data-ttu-id="46360-119">Redirecionando</span><span class="sxs-lookup"><span data-stu-id="46360-119">Retargeting</span></span>|
|<span data-ttu-id="46360-120">APIs afetadas</span><span class="sxs-lookup"><span data-stu-id="46360-120">Affected APIs</span></span>|<ul><li><xref:System.IO.Compression.DeflateStream?displayProperty=nameWithType></li><li><xref:System.IO.Compression.GZipStream?displayProperty=nameWithType></li></ul>|
