---
title: Pobierz fakturowanie elementów linii rozliczeniowej
description: Możesz uzyskać informacje o liczbie elementów wiersza faktury użycia komercyjnego (zamknięty dzienny) dla określonej faktury przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1e19792da6a7510bf02dd11b3e77f40a8365be2b
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730199"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="1aca2-103">Pobierz fakturowanie elementów linii rozliczeniowej</span><span class="sxs-lookup"><span data-stu-id="1aca2-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="1aca2-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="1aca2-104">**Applies to:**</span></span>

- <span data-ttu-id="1aca2-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1aca2-105">Partner Center</span></span>

<span data-ttu-id="1aca2-106">Korzystając z poniższych metod, można uzyskać kolekcję szczegółów dla handlowych elementów wiersza faktury (nazywanych również zamkniętymi codziennymi elementami wiersza użycia) dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>

<span data-ttu-id="1aca2-107">Ten interfejs API obsługuje również typy dostawców **platformy Azure** dla subskrypcji Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="1aca2-107">This API also supports **azure** provider types for Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span> <span data-ttu-id="1aca2-108">Oznacza to, że ten interfejs API jest funkcją zgodną z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="1aca2-108">This means this API is a backward-compatible feature.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1aca2-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1aca2-109">Prerequisites</span></span>

- <span data-ttu-id="1aca2-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1aca2-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1aca2-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1aca2-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1aca2-112">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-112">An invoice identifier.</span></span> <span data-ttu-id="1aca2-113">Identyfikuje fakturę, dla której mają zostać pobrane elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="1aca2-114">C\#</span><span class="sxs-lookup"><span data-stu-id="1aca2-114">C\#</span></span>

<span data-ttu-id="1aca2-115">Aby uzyskać elementy linii komercyjnej dla określonej faktury, należy pobrać obiekt Invoice:</span><span class="sxs-lookup"><span data-stu-id="1aca2-115">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="1aca2-116">Wywołaj metodę [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , aby uzyskać interfejs do fakturowania operacji dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="1aca2-117">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="1aca2-118">Obiekt Invoice zawiera wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-118">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="1aca2-119">**Dostawca** identyfikuje źródło informacji o rozliczanych szczegółach (na przykład **jednorazowej**).</span><span class="sxs-lookup"><span data-stu-id="1aca2-119">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="1aca2-120">**InvoiceLineItemType** określa typ (na przykład **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="1aca2-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="1aca2-121">Poniższy przykładowy kod używa pętli **foreach** do przetworzenia kolekcji elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-121">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="1aca2-122">Dla każdego **InvoiceLineItemType** pobierana jest oddzielna Kolekcja elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="1aca2-123">Aby uzyskać kolekcję elementów wierszy, które odpowiadają wystąpieniu **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="1aca2-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="1aca2-124">Przekaż **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="1aca2-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="1aca2-125">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="1aca2-126">Utwórz moduł wyliczający, który przejdzie do kolekcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1aca2-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="1aca2-127">Podobny przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="1aca2-127">For a similar example, see the following:</span></span>

- <span data-ttu-id="1aca2-128">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1aca2-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1aca2-129">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="1aca2-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1aca2-130">Klasa: **GetBilledConsumptionReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="1aca2-130">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1aca2-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1aca2-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1aca2-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1aca2-132">Request syntax</span></span>

<span data-ttu-id="1aca2-133">Użyj pierwszej składni, aby zwrócić pełną listę każdego elementu wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="1aca2-133">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="1aca2-134">W przypadku dużych faktur należy użyć drugiej składni z określonym rozmiarem i przesunięciu na 0, aby zwrócić stronicowaną listę elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-134">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="1aca2-135">Użyj trzeciej składni, aby uzyskać następną stronę elementów Rekonesans line przy użyciu `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="1aca2-135">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="1aca2-136">Metoda</span><span class="sxs-lookup"><span data-stu-id="1aca2-136">Method</span></span>  | <span data-ttu-id="1aca2-137">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1aca2-137">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1aca2-138">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1aca2-138">**GET**</span></span> | <span data-ttu-id="1aca2-139">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="1aca2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="1aca2-140">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1aca2-140">**GET**</span></span> | <span data-ttu-id="1aca2-141">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="1aca2-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="1aca2-142">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1aca2-142">**GET**</span></span> | <span data-ttu-id="1aca2-143">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &size = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="1aca2-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="1aca2-144">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="1aca2-144">URI parameters</span></span>

<span data-ttu-id="1aca2-145">Podczas tworzenia żądania Użyj następujących parametrów URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="1aca2-145">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="1aca2-146">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1aca2-146">Name</span></span>                   | <span data-ttu-id="1aca2-147">Typ</span><span class="sxs-lookup"><span data-stu-id="1aca2-147">Type</span></span>   | <span data-ttu-id="1aca2-148">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1aca2-148">Required</span></span> | <span data-ttu-id="1aca2-149">Opis</span><span class="sxs-lookup"><span data-stu-id="1aca2-149">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="1aca2-150">Identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="1aca2-150">invoice-id</span></span>             | <span data-ttu-id="1aca2-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-151">string</span></span> | <span data-ttu-id="1aca2-152">Tak</span><span class="sxs-lookup"><span data-stu-id="1aca2-152">Yes</span></span>      | <span data-ttu-id="1aca2-153">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="1aca2-153">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="1aca2-154">dostawcy</span><span class="sxs-lookup"><span data-stu-id="1aca2-154">provider</span></span>               | <span data-ttu-id="1aca2-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-155">string</span></span> | <span data-ttu-id="1aca2-156">Tak</span><span class="sxs-lookup"><span data-stu-id="1aca2-156">Yes</span></span>      | <span data-ttu-id="1aca2-157">Dostawca: "jednorazowej".</span><span class="sxs-lookup"><span data-stu-id="1aca2-157">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="1aca2-158">Typ faktury-wiersz-element</span><span class="sxs-lookup"><span data-stu-id="1aca2-158">invoice-line-item-type</span></span> | <span data-ttu-id="1aca2-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-159">string</span></span> | <span data-ttu-id="1aca2-160">Tak</span><span class="sxs-lookup"><span data-stu-id="1aca2-160">Yes</span></span>      | <span data-ttu-id="1aca2-161">Typ szczegółów faktury: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="1aca2-161">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="1aca2-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1aca2-162">currencyCode</span></span>           | <span data-ttu-id="1aca2-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-163">string</span></span> | <span data-ttu-id="1aca2-164">Tak</span><span class="sxs-lookup"><span data-stu-id="1aca2-164">Yes</span></span>      | <span data-ttu-id="1aca2-165">Kod waluty dla elementów rozliczanej linii.</span><span class="sxs-lookup"><span data-stu-id="1aca2-165">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="1aca2-166">period</span><span class="sxs-lookup"><span data-stu-id="1aca2-166">period</span></span>                 | <span data-ttu-id="1aca2-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-167">string</span></span> | <span data-ttu-id="1aca2-168">Tak</span><span class="sxs-lookup"><span data-stu-id="1aca2-168">Yes</span></span>      | <span data-ttu-id="1aca2-169">Okres dla rozliczeń rekonesans.</span><span class="sxs-lookup"><span data-stu-id="1aca2-169">The period for billed recon.</span></span> <span data-ttu-id="1aca2-170">przykład: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="1aca2-170">example: current, previous.</span></span>        |
| <span data-ttu-id="1aca2-171">size</span><span class="sxs-lookup"><span data-stu-id="1aca2-171">size</span></span>                   | <span data-ttu-id="1aca2-172">liczba</span><span class="sxs-lookup"><span data-stu-id="1aca2-172">number</span></span> | <span data-ttu-id="1aca2-173">Nie</span><span class="sxs-lookup"><span data-stu-id="1aca2-173">No</span></span>       | <span data-ttu-id="1aca2-174">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="1aca2-174">The maximum number of items to return.</span></span> <span data-ttu-id="1aca2-175">Rozmiar domyślny to 2000</span><span class="sxs-lookup"><span data-stu-id="1aca2-175">Default size is 2000</span></span>       |
| <span data-ttu-id="1aca2-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="1aca2-176">seekOperation</span></span>          | <span data-ttu-id="1aca2-177">ciąg</span><span class="sxs-lookup"><span data-stu-id="1aca2-177">string</span></span> | <span data-ttu-id="1aca2-178">Nie</span><span class="sxs-lookup"><span data-stu-id="1aca2-178">No</span></span>       | <span data-ttu-id="1aca2-179">Ustaw seekOperation = dalej, aby uzyskać następną stronę elementów wiersza rekonesans.</span><span class="sxs-lookup"><span data-stu-id="1aca2-179">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1aca2-180">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1aca2-180">Request headers</span></span>

<span data-ttu-id="1aca2-181">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1aca2-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1aca2-182">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1aca2-182">Request body</span></span>

<span data-ttu-id="1aca2-183">Brak.</span><span class="sxs-lookup"><span data-stu-id="1aca2-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="1aca2-184">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1aca2-184">REST response</span></span>

<span data-ttu-id="1aca2-185">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="1aca2-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="1aca2-186">Dla pozycji **line ItemType** wartość **Purchase** jest mapowana na **nową**.</span><span class="sxs-lookup"><span data-stu-id="1aca2-186">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="1aca2-187">**Zwrot** wartości jest mapowany na **Anuluj**.</span><span class="sxs-lookup"><span data-stu-id="1aca2-187">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1aca2-188">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1aca2-188">Response success and error codes</span></span>

<span data-ttu-id="1aca2-189">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1aca2-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1aca2-190">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1aca2-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1aca2-191">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1aca2-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="1aca2-192">Przykłady REST</span><span class="sxs-lookup"><span data-stu-id="1aca2-192">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="1aca2-193">Przykład żądania — odpowiedź 1</span><span class="sxs-lookup"><span data-stu-id="1aca2-193">Request-response example 1</span></span>

<span data-ttu-id="1aca2-194">Szczegóły dotyczące tego przykładowego żądania REST i odpowiedzi są następujące:</span><span class="sxs-lookup"><span data-stu-id="1aca2-194">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="1aca2-195">**Dostawca**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="1aca2-195">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="1aca2-196">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="1aca2-196">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="1aca2-197">**Okres**: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1aca2-197">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="1aca2-198">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="1aca2-198">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="1aca2-199">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="1aca2-199">Response example 1</span></span>

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
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="1aca2-200">Przykład żądania — odpowiedź 2</span><span class="sxs-lookup"><span data-stu-id="1aca2-200">Request-response example 2</span></span>

<span data-ttu-id="1aca2-201">Szczegóły dotyczące tego przykładowego żądania REST i odpowiedzi są następujące:</span><span class="sxs-lookup"><span data-stu-id="1aca2-201">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="1aca2-202">**Dostawca**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="1aca2-202">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="1aca2-203">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="1aca2-203">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="1aca2-204">**Okres**: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1aca2-204">**Period**: **Previous**</span></span>
- <span data-ttu-id="1aca2-205">**SeekOperation**: **dalej**</span><span class="sxs-lookup"><span data-stu-id="1aca2-205">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="1aca2-206">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="1aca2-206">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a><span data-ttu-id="1aca2-207">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="1aca2-207">Response example 2</span></span>

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
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
