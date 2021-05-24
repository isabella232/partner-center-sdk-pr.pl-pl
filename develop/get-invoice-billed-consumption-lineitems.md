---
title: Uzyskiwanie pozycji użycia komercyjnego rozliczanych na podstawie faktury
description: Możesz uzyskać kolekcję szczegółów pozycji faktury za użycie komercyjne (zamkniętego dziennego użycia) dla określonej faktury przy użyciu interfejsów API Partner Center.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1406938b16e5a363a73c36ef0338eb5fc4305279
ms.sourcegitcommit: 89aefbff6dbe740b6f27a888492ffc2e5f98b1e9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2021
ms.locfileid: "110325449"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="79c63-103">Uzyskiwanie pozycji użycia komercyjnego rozliczanych na podstawie faktury</span><span class="sxs-lookup"><span data-stu-id="79c63-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="79c63-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="79c63-104">**Applies to:**</span></span>

- <span data-ttu-id="79c63-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="79c63-105">Partner Center</span></span>

<span data-ttu-id="79c63-106">Aby uzyskać kolekcję szczegółów dla pozycji faktur za użycie komercyjne (zwane również zamkniętymi pozycjami do dziennego użycia) dla określonej faktury, można użyć następujących metod.</span><span class="sxs-lookup"><span data-stu-id="79c63-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="79c63-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79c63-107">Prerequisites</span></span>

- <span data-ttu-id="79c63-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="79c63-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79c63-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79c63-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="79c63-110">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="79c63-110">An invoice identifier.</span></span> <span data-ttu-id="79c63-111">Identyfikuje fakturę, dla której mają zostać pobrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="79c63-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="79c63-112">C\#</span><span class="sxs-lookup"><span data-stu-id="79c63-112">C\#</span></span>

<span data-ttu-id="79c63-113">Aby uzyskać komercyjne pozycje dla określonej faktury, musisz pobrać obiekt faktury:</span><span class="sxs-lookup"><span data-stu-id="79c63-113">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="79c63-114">Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="79c63-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="79c63-115">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="79c63-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="79c63-116">Obiekt faktury zawiera wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="79c63-116">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="79c63-117">Dostawca **identyfikuje** źródło informacji szczegółowych rozliczanych (na przykład **onetime**).</span><span class="sxs-lookup"><span data-stu-id="79c63-117">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="79c63-118">**InvoiceLineItemType** określa typ (na przykład **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="79c63-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="79c63-119">Poniższy przykładowy kod używa **pętli foreach** do przetwarzania kolekcji elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="79c63-119">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="79c63-120">Dla każdego typu **InvoiceLineItemType** pobierana jest oddzielna kolekcja elementów wierszy.</span><span class="sxs-lookup"><span data-stu-id="79c63-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="79c63-121">Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="79c63-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="79c63-122">Przekaż wartości **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="79c63-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="79c63-123">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="79c63-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="79c63-124">Utwórz moduł wyliczający, aby przejść przez kolekcję, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="79c63-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="79c63-125">Podobny przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="79c63-125">For a similar example, see the following:</span></span>

- <span data-ttu-id="79c63-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="79c63-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="79c63-127">Projekt: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="79c63-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="79c63-128">Klasa: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="79c63-128">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="79c63-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="79c63-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79c63-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="79c63-130">Request syntax</span></span>

<span data-ttu-id="79c63-131">Użyj pierwszej składni, aby zwrócić pełną listę wszystkich pozycji dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="79c63-131">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="79c63-132">W przypadku dużych faktur użyj drugiej składni z określonym rozmiarem i przesunięciem 0, aby zwrócić stronicowane listy elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="79c63-132">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="79c63-133">Użyj trzeciej składni, aby uzyskać następną stronę ponownego wiersza elementów przy użyciu polecenia `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="79c63-133">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="79c63-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="79c63-134">Method</span></span>  | <span data-ttu-id="79c63-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="79c63-135">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="79c63-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="79c63-136">**GET**</span></span> | <span data-ttu-id="79c63-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="79c63-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="79c63-138">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="79c63-138">**GET**</span></span> | <span data-ttu-id="79c63-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="79c63-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="79c63-140">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="79c63-140">**GET**</span></span> | <span data-ttu-id="79c63-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="79c63-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="79c63-142">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="79c63-142">URI parameters</span></span>

<span data-ttu-id="79c63-143">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="79c63-143">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="79c63-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="79c63-144">Name</span></span>                   | <span data-ttu-id="79c63-145">Typ</span><span class="sxs-lookup"><span data-stu-id="79c63-145">Type</span></span>   | <span data-ttu-id="79c63-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="79c63-146">Required</span></span> | <span data-ttu-id="79c63-147">Opis</span><span class="sxs-lookup"><span data-stu-id="79c63-147">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="79c63-148">invoice-id</span><span class="sxs-lookup"><span data-stu-id="79c63-148">invoice-id</span></span>             | <span data-ttu-id="79c63-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-149">string</span></span> | <span data-ttu-id="79c63-150">Tak</span><span class="sxs-lookup"><span data-stu-id="79c63-150">Yes</span></span>      | <span data-ttu-id="79c63-151">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="79c63-151">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="79c63-152">Dostawca</span><span class="sxs-lookup"><span data-stu-id="79c63-152">provider</span></span>               | <span data-ttu-id="79c63-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-153">string</span></span> | <span data-ttu-id="79c63-154">Tak</span><span class="sxs-lookup"><span data-stu-id="79c63-154">Yes</span></span>      | <span data-ttu-id="79c63-155">Dostawca: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="79c63-155">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="79c63-156">typ elementu wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="79c63-156">invoice-line-item-type</span></span> | <span data-ttu-id="79c63-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-157">string</span></span> | <span data-ttu-id="79c63-158">Tak</span><span class="sxs-lookup"><span data-stu-id="79c63-158">Yes</span></span>      | <span data-ttu-id="79c63-159">Typ szczegółów faktury: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="79c63-159">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="79c63-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="79c63-160">currencyCode</span></span>           | <span data-ttu-id="79c63-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-161">string</span></span> | <span data-ttu-id="79c63-162">Tak</span><span class="sxs-lookup"><span data-stu-id="79c63-162">Yes</span></span>      | <span data-ttu-id="79c63-163">Kod waluty dla rozliowanych pozycji.</span><span class="sxs-lookup"><span data-stu-id="79c63-163">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="79c63-164">period</span><span class="sxs-lookup"><span data-stu-id="79c63-164">period</span></span>                 | <span data-ttu-id="79c63-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-165">string</span></span> | <span data-ttu-id="79c63-166">Tak</span><span class="sxs-lookup"><span data-stu-id="79c63-166">Yes</span></span>      | <span data-ttu-id="79c63-167">Okres dla rozliowanych rekonesencji.</span><span class="sxs-lookup"><span data-stu-id="79c63-167">The period for billed recon.</span></span> <span data-ttu-id="79c63-168">przykład: current, previous.</span><span class="sxs-lookup"><span data-stu-id="79c63-168">example: current, previous.</span></span>        |
| <span data-ttu-id="79c63-169">size</span><span class="sxs-lookup"><span data-stu-id="79c63-169">size</span></span>                   | <span data-ttu-id="79c63-170">liczba</span><span class="sxs-lookup"><span data-stu-id="79c63-170">number</span></span> | <span data-ttu-id="79c63-171">Nie</span><span class="sxs-lookup"><span data-stu-id="79c63-171">No</span></span>       | <span data-ttu-id="79c63-172">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="79c63-172">The maximum number of items to return.</span></span> <span data-ttu-id="79c63-173">Domyślny rozmiar to 2000</span><span class="sxs-lookup"><span data-stu-id="79c63-173">Default size is 2000</span></span>       |
| <span data-ttu-id="79c63-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="79c63-174">seekOperation</span></span>          | <span data-ttu-id="79c63-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="79c63-175">string</span></span> | <span data-ttu-id="79c63-176">Nie</span><span class="sxs-lookup"><span data-stu-id="79c63-176">No</span></span>       | <span data-ttu-id="79c63-177">Ustaw wartość seekOperation=Next, aby uzyskać następną stronę elementów ponownego wiersza.</span><span class="sxs-lookup"><span data-stu-id="79c63-177">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="79c63-178">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="79c63-178">Request headers</span></span>

<span data-ttu-id="79c63-179">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="79c63-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79c63-180">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="79c63-180">Request body</span></span>

<span data-ttu-id="79c63-181">Brak.</span><span class="sxs-lookup"><span data-stu-id="79c63-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="79c63-182">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="79c63-182">REST response</span></span>

<span data-ttu-id="79c63-183">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="79c63-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="79c63-184">W przypadku elementu wiersza **ChargeType** wartość **Zakup** jest mapowana na **nowy**.</span><span class="sxs-lookup"><span data-stu-id="79c63-184">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="79c63-185">Wartość Zwrot **jest** mapowana na **anuluj**.</span><span class="sxs-lookup"><span data-stu-id="79c63-185">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79c63-186">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="79c63-186">Response success and error codes</span></span>

<span data-ttu-id="79c63-187">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="79c63-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79c63-188">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="79c63-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79c63-189">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="79c63-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="79c63-190">Przykłady rest</span><span class="sxs-lookup"><span data-stu-id="79c63-190">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="79c63-191">Przykład żądania i odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="79c63-191">Request-response example 1</span></span>

<span data-ttu-id="79c63-192">Szczegóły tego przykładowego żądania REST i odpowiedzi są następujące:</span><span class="sxs-lookup"><span data-stu-id="79c63-192">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="79c63-193">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="79c63-193">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="79c63-194">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="79c63-194">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="79c63-195">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="79c63-195">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="79c63-196">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="79c63-196">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="79c63-197">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="79c63-197">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="79c63-198">Przykład żądania i odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="79c63-198">Request-response example 2</span></span>

<span data-ttu-id="79c63-199">Szczegóły tego przykładowego żądania REST i odpowiedzi są następujące:</span><span class="sxs-lookup"><span data-stu-id="79c63-199">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="79c63-200">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="79c63-200">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="79c63-201">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="79c63-201">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="79c63-202">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="79c63-202">**Period**: **Previous**</span></span>
- <span data-ttu-id="79c63-203">**SeekOperation:** **Dalej**</span><span class="sxs-lookup"><span data-stu-id="79c63-203">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="79c63-204">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="79c63-204">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="79c63-205">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="79c63-205">Response example 2</span></span>

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
