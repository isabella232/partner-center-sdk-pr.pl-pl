---
title: Pobierz pozycje dotyczące nienadmierowego użycia komercyjnego na fakturze
description: Możesz uzyskać kolekcję nienalicznych szczegółów elementu wiersza użycia komercyjnego dla określonej faktury przy użyciu interfejsów API Partner Center.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7c74bedfd6412fc5954ed2ddc1388936e418fa3
ms.sourcegitcommit: 722992eea6f8ea366dc088e5dd1ee63c17d56f61
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/15/2021
ms.locfileid: "114224772"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="1de40-103">Pobierz pozycje dotyczące nienadmierowego użycia komercyjnego na fakturze</span><span class="sxs-lookup"><span data-stu-id="1de40-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="1de40-104">Jak uzyskać kolekcję nienaliowanych szczegółów elementu wiersza użycia komercyjnego.</span><span class="sxs-lookup"><span data-stu-id="1de40-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="1de40-105">Za pomocą poniższych metod można programowo pobrać kolekcję szczegółów nienadmiernie rozlicznych pozycji zużycia komercyjnego (nazywanych również otwartymi elementami wiersza użycia).</span><span class="sxs-lookup"><span data-stu-id="1de40-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="1de40-106">Dzienne użycie oceniane zwykle trwa 24 godziny, aby pojawiać się w Partner Center lub uzyskać do niego dostęp za pośrednictwem interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1de40-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1de40-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1de40-107">Prerequisites</span></span>

- <span data-ttu-id="1de40-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1de40-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1de40-109">Ten scenariusz obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1de40-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1de40-110">C\#</span><span class="sxs-lookup"><span data-stu-id="1de40-110">C\#</span></span>

<span data-ttu-id="1de40-111">Aby uzyskać pozycje dla określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="1de40-111">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="1de40-112">Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1de40-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="1de40-113">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="1de40-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="1de40-114">Obiekt **faktury zawiera** wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1de40-114">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="1de40-115">Dostawca **identyfikuje** źródło nienaliczonych szczegółowych informacji (na przykład **OneTime).**</span><span class="sxs-lookup"><span data-stu-id="1de40-115">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="1de40-116">Typ **invoiceLineItemType** określa typ (na przykład **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="1de40-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="1de40-117">Poniższy przykładowy kod używa pętli **foreach** do przetwarzania **kolekcji InvoiceLineItems.**</span><span class="sxs-lookup"><span data-stu-id="1de40-117">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="1de40-118">Dla każdego typu **InvoiceLineItemType** pobierana jest oddzielna kolekcja elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1de40-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="1de40-119">Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="1de40-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="1de40-120">Przekaż wartości **BillingProvider i** **InvoiceLineItemType** wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="1de40-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="1de40-121">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="1de40-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="1de40-122">Utwórz moduł wyliczający, aby przejść przez kolekcję, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1de40-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="1de40-123">Aby uzyskać podobny przykład, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1de40-123">For a similar example, see:</span></span>

- <span data-ttu-id="1de40-124">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1de40-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1de40-125">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="1de40-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1de40-126">Klasa: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="1de40-126">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1de40-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1de40-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1de40-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1de40-128">Request syntax</span></span>

<span data-ttu-id="1de40-129">W zależności od przypadku użycia możesz użyć następujących składni dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="1de40-129">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="1de40-130">Aby uzyskać więcej informacji, zobacz opisy każdej składni.</span><span class="sxs-lookup"><span data-stu-id="1de40-130">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="1de40-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="1de40-131">Method</span></span>  | <span data-ttu-id="1de40-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1de40-132">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="1de40-133">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="1de40-133">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1de40-134">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1de40-134">**GET**</span></span> | <span data-ttu-id="1de40-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1de40-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="1de40-136">Użyj tej składni, aby zwrócić pełną listę wszystkich pozycji dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="1de40-136">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="1de40-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1de40-137">**GET**</span></span> | <span data-ttu-id="1de40-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1de40-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="1de40-139">Użyj tej składni w przypadku dużych faktur.</span><span class="sxs-lookup"><span data-stu-id="1de40-139">Use this syntax for large invoices.</span></span> <span data-ttu-id="1de40-140">Użyj tej składni z określonym rozmiarem i przesunięciem 0, aby zwrócić stronicowane listy elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1de40-140">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="1de40-141">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1de40-141">**GET**</span></span> | <span data-ttu-id="1de40-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="1de40-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="1de40-143">Użyj tej składni, aby uzyskać następną stronę elementów wiersza uzgodnień przy użyciu polecenia `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="1de40-143">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="1de40-144">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="1de40-144">URI parameters</span></span>

<span data-ttu-id="1de40-145">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="1de40-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="1de40-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1de40-146">Name</span></span>                   | <span data-ttu-id="1de40-147">Typ</span><span class="sxs-lookup"><span data-stu-id="1de40-147">Type</span></span>   | <span data-ttu-id="1de40-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1de40-148">Required</span></span> | <span data-ttu-id="1de40-149">Opis</span><span class="sxs-lookup"><span data-stu-id="1de40-149">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1de40-150">Dostawca</span><span class="sxs-lookup"><span data-stu-id="1de40-150">provider</span></span>               | <span data-ttu-id="1de40-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="1de40-151">string</span></span> | <span data-ttu-id="1de40-152">Tak</span><span class="sxs-lookup"><span data-stu-id="1de40-152">Yes</span></span>      | <span data-ttu-id="1de40-153">Dostawca: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="1de40-153">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="1de40-154">typ-elementu-wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="1de40-154">invoice-line-item-type</span></span> | <span data-ttu-id="1de40-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="1de40-155">string</span></span> | <span data-ttu-id="1de40-156">Tak</span><span class="sxs-lookup"><span data-stu-id="1de40-156">Yes</span></span>      | <span data-ttu-id="1de40-157">Typ szczegółów faktury: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="1de40-157">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="1de40-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1de40-158">currencyCode</span></span>           | <span data-ttu-id="1de40-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="1de40-159">string</span></span> | <span data-ttu-id="1de40-160">Tak</span><span class="sxs-lookup"><span data-stu-id="1de40-160">Yes</span></span>      | <span data-ttu-id="1de40-161">Kod waluty dla nienaliowanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1de40-161">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="1de40-162">period</span><span class="sxs-lookup"><span data-stu-id="1de40-162">period</span></span>                 | <span data-ttu-id="1de40-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="1de40-163">string</span></span> | <span data-ttu-id="1de40-164">Tak</span><span class="sxs-lookup"><span data-stu-id="1de40-164">Yes</span></span>      | <span data-ttu-id="1de40-165">Okres dla rozeznania nienadmiernego (na przykład: **bieżący**, **poprzedni**).</span><span class="sxs-lookup"><span data-stu-id="1de40-165">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="1de40-166">Załóżmy, że musisz odpytać dane o nienaliczonym użyciu dla cyklu rozliczeniowego (01.01.2020 – 31.01.2020) w styczniu, wybierz okres **"Bieżący",** a w innym przypadku **"Poprzedni".**</span><span class="sxs-lookup"><span data-stu-id="1de40-166">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="1de40-167">size</span><span class="sxs-lookup"><span data-stu-id="1de40-167">size</span></span>                   | <span data-ttu-id="1de40-168">liczba</span><span class="sxs-lookup"><span data-stu-id="1de40-168">number</span></span> | <span data-ttu-id="1de40-169">Nie</span><span class="sxs-lookup"><span data-stu-id="1de40-169">No</span></span>       | <span data-ttu-id="1de40-170">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="1de40-170">The maximum number of items to return.</span></span> <span data-ttu-id="1de40-171">Domyślny rozmiar to 2000.</span><span class="sxs-lookup"><span data-stu-id="1de40-171">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="1de40-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="1de40-172">seekOperation</span></span>          | <span data-ttu-id="1de40-173">ciąg</span><span class="sxs-lookup"><span data-stu-id="1de40-173">string</span></span> | <span data-ttu-id="1de40-174">Nie</span><span class="sxs-lookup"><span data-stu-id="1de40-174">No</span></span>       | <span data-ttu-id="1de40-175">Ustaw `seekOperation=Next` wartość , aby uzyskać następną stronę elementów wiersza uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="1de40-175">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="1de40-176">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1de40-176">Request headers</span></span>

<span data-ttu-id="1de40-177">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1de40-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1de40-178">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1de40-178">Request body</span></span>

<span data-ttu-id="1de40-179">Brak.</span><span class="sxs-lookup"><span data-stu-id="1de40-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="1de40-180">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1de40-180">REST response</span></span>

<span data-ttu-id="1de40-181">Jeśli to się powiedzie, odpowiedź będzie zawierała kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="1de40-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="1de40-182">*W przypadku elementu wiersza **ChargeType** wartość **Zakup** jest mapowana na wartość **Nowy,** a wartość **Zwrot** jest mapowana na **wartość Anuluj.***</span><span class="sxs-lookup"><span data-stu-id="1de40-182">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1de40-183">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1de40-183">Response success and error codes</span></span>

<span data-ttu-id="1de40-184">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1de40-184">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1de40-185">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1de40-185">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1de40-186">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1de40-186">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="1de40-187">Przykłady żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1de40-187">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="1de40-188">Przykład żądania i odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="1de40-188">Request-response example 1</span></span>

<span data-ttu-id="1de40-189">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="1de40-189">The following details apply to this example:</span></span>

- <span data-ttu-id="1de40-190">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="1de40-190">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="1de40-191">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="1de40-191">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="1de40-192">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1de40-192">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="1de40-193">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="1de40-193">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a><span data-ttu-id="1de40-194">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="1de40-194">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 0,
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemTypce": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="1de40-195">Przykład żądania i odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="1de40-195">Request-response example 2</span></span>

<span data-ttu-id="1de40-196">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="1de40-196">The following details apply to this example:</span></span>

- <span data-ttu-id="1de40-197">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="1de40-197">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="1de40-198">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="1de40-198">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="1de40-199">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1de40-199">**Period**: **Previous**</span></span>
- <span data-ttu-id="1de40-200">**SeekOperation:** **Dalej**</span><span class="sxs-lookup"><span data-stu-id="1de40-200">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="1de40-201">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="1de40-201">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="1de40-202">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="1de40-202">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
