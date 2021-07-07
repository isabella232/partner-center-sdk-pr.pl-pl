---
title: Uzyskiwanie nienaliowanych pozycji użycia komercyjnego na fakturze
description: Możesz uzyskać kolekcję nienalicznych szczegółów pozycji użycia komercyjnego dla określonej faktury przy użyciu Partner Center API.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1b7dba3333aaec8df73f0e8147b0bbbc78b9b184
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446150"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="cc492-103">Uzyskiwanie nienaliowanych pozycji użycia komercyjnego na fakturze</span><span class="sxs-lookup"><span data-stu-id="cc492-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="cc492-104">How to get a collection of unbilled commercial consumption line item details (Jak uzyskać kolekcję nienadmiernych szczegółów elementu wiersza użycia komercyjnego).</span><span class="sxs-lookup"><span data-stu-id="cc492-104">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="cc492-105">Za pomocą poniższych metod można programowo pobrać kolekcję szczegółowych informacji o nienadmiernych pozycjach użycia komercyjnego (nazywanych również otwartymi elementami wiersza użycia).</span><span class="sxs-lookup"><span data-stu-id="cc492-105">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="cc492-106">Dzienne użycie oceniane zwykle trwa 24 godziny, aby pojawiać się w Partner Center lub uzyskać do niego dostęp za pośrednictwem interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="cc492-106">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc492-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc492-107">Prerequisites</span></span>

- <span data-ttu-id="cc492-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cc492-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc492-109">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc492-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cc492-110">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="cc492-110">An invoice identifier.</span></span> <span data-ttu-id="cc492-111">Identyfikuje fakturę, dla której mają zostać pobrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="cc492-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="cc492-112">C\#</span><span class="sxs-lookup"><span data-stu-id="cc492-112">C\#</span></span>

<span data-ttu-id="cc492-113">Aby uzyskać pozycje dla określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="cc492-113">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="cc492-114">Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="cc492-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="cc492-115">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="cc492-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="cc492-116">Obiekt **faktury zawiera** wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="cc492-116">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="cc492-117">Dostawca **identyfikuje** źródło nienaliczonych informacji szczegółowych (na przykład **OneTime).**</span><span class="sxs-lookup"><span data-stu-id="cc492-117">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="cc492-118">**InvoiceLineItemType** określa typ (na przykład **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="cc492-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="cc492-119">Poniższy przykładowy kod używa **pętli foreach** do przetwarzania kolekcji **InvoiceLineItems.**</span><span class="sxs-lookup"><span data-stu-id="cc492-119">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="cc492-120">Dla każdego typu **InvoiceLineItemType** pobierana jest oddzielna kolekcja elementów wierszy.</span><span class="sxs-lookup"><span data-stu-id="cc492-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="cc492-121">Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="cc492-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="cc492-122">Przekaż wartości **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="cc492-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="cc492-123">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc492-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="cc492-124">Utwórz moduł wyliczający w celu przechodzenia przez kolekcję, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cc492-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="cc492-125">Aby uzyskać podobny przykład, zobacz:</span><span class="sxs-lookup"><span data-stu-id="cc492-125">For a similar example, see:</span></span>

- <span data-ttu-id="cc492-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="cc492-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="cc492-127">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="cc492-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="cc492-128">Klasa: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="cc492-128">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="cc492-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cc492-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc492-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cc492-130">Request syntax</span></span>

<span data-ttu-id="cc492-131">W zależności od przypadku użycia możesz użyć następujących składni dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="cc492-131">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="cc492-132">Aby uzyskać więcej informacji, zobacz opisy poszczególnych składni.</span><span class="sxs-lookup"><span data-stu-id="cc492-132">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="cc492-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="cc492-133">Method</span></span>  | <span data-ttu-id="cc492-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cc492-134">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="cc492-135">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="cc492-135">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc492-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cc492-136">**GET**</span></span> | <span data-ttu-id="cc492-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cc492-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="cc492-138">Użyj tej składni, aby zwrócić pełną listę wszystkich elementów wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="cc492-138">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="cc492-139">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cc492-139">**GET**</span></span> | <span data-ttu-id="cc492-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cc492-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="cc492-141">Użyj tej składni w przypadku dużych faktur.</span><span class="sxs-lookup"><span data-stu-id="cc492-141">Use this syntax for large invoices.</span></span> <span data-ttu-id="cc492-142">Użyj tej składni z określonym rozmiarem i przesunięciem opartym na wartości 0, aby zwrócić stronicowane listy elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc492-142">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="cc492-143">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cc492-143">**GET**</span></span> | <span data-ttu-id="cc492-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="cc492-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="cc492-145">Użyj tej składni, aby uzyskać następną stronę elementów wiersza uzgodnień przy użyciu polecenia `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="cc492-145">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="cc492-146">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="cc492-146">URI parameters</span></span>

<span data-ttu-id="cc492-147">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="cc492-147">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="cc492-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cc492-148">Name</span></span>                   | <span data-ttu-id="cc492-149">Typ</span><span class="sxs-lookup"><span data-stu-id="cc492-149">Type</span></span>   | <span data-ttu-id="cc492-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cc492-150">Required</span></span> | <span data-ttu-id="cc492-151">Opis</span><span class="sxs-lookup"><span data-stu-id="cc492-151">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc492-152">Dostawca</span><span class="sxs-lookup"><span data-stu-id="cc492-152">provider</span></span>               | <span data-ttu-id="cc492-153">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc492-153">string</span></span> | <span data-ttu-id="cc492-154">Tak</span><span class="sxs-lookup"><span data-stu-id="cc492-154">Yes</span></span>      | <span data-ttu-id="cc492-155">Dostawca: "**OneTime**".</span><span class="sxs-lookup"><span data-stu-id="cc492-155">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="cc492-156">typ elementu wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="cc492-156">invoice-line-item-type</span></span> | <span data-ttu-id="cc492-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc492-157">string</span></span> | <span data-ttu-id="cc492-158">Tak</span><span class="sxs-lookup"><span data-stu-id="cc492-158">Yes</span></span>      | <span data-ttu-id="cc492-159">Typ szczegółów faktury: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="cc492-159">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="cc492-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="cc492-160">currencyCode</span></span>           | <span data-ttu-id="cc492-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc492-161">string</span></span> | <span data-ttu-id="cc492-162">Tak</span><span class="sxs-lookup"><span data-stu-id="cc492-162">Yes</span></span>      | <span data-ttu-id="cc492-163">Kod waluty dla nienaliowanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc492-163">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="cc492-164">period</span><span class="sxs-lookup"><span data-stu-id="cc492-164">period</span></span>                 | <span data-ttu-id="cc492-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc492-165">string</span></span> | <span data-ttu-id="cc492-166">Tak</span><span class="sxs-lookup"><span data-stu-id="cc492-166">Yes</span></span>      | <span data-ttu-id="cc492-167">Okres dla nienadmiernego rekonesencji (na przykład: **bieżący**, **poprzedni**).</span><span class="sxs-lookup"><span data-stu-id="cc492-167">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="cc492-168">Załóżmy, że musisz odpytać dane o nienaliczonym użyciu dla cyklu rozliczeniowego (01.01.2020 – 01.31.2020) w styczniu, wybrać okres **jako "Bieżący",** a jeszcze **"Poprzedni".**</span><span class="sxs-lookup"><span data-stu-id="cc492-168">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="cc492-169">size</span><span class="sxs-lookup"><span data-stu-id="cc492-169">size</span></span>                   | <span data-ttu-id="cc492-170">liczba</span><span class="sxs-lookup"><span data-stu-id="cc492-170">number</span></span> | <span data-ttu-id="cc492-171">Nie</span><span class="sxs-lookup"><span data-stu-id="cc492-171">No</span></span>       | <span data-ttu-id="cc492-172">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="cc492-172">The maximum number of items to return.</span></span> <span data-ttu-id="cc492-173">Domyślny rozmiar to 2000.</span><span class="sxs-lookup"><span data-stu-id="cc492-173">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="cc492-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="cc492-174">seekOperation</span></span>          | <span data-ttu-id="cc492-175">ciąg</span><span class="sxs-lookup"><span data-stu-id="cc492-175">string</span></span> | <span data-ttu-id="cc492-176">Nie</span><span class="sxs-lookup"><span data-stu-id="cc492-176">No</span></span>       | <span data-ttu-id="cc492-177">Ustaw `seekOperation=Next` , aby pobrać następną stronę elementów wiersza uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="cc492-177">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="cc492-178">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cc492-178">Request headers</span></span>

<span data-ttu-id="cc492-179">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cc492-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc492-180">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cc492-180">Request body</span></span>

<span data-ttu-id="cc492-181">Brak.</span><span class="sxs-lookup"><span data-stu-id="cc492-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="cc492-182">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cc492-182">REST response</span></span>

<span data-ttu-id="cc492-183">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc492-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="cc492-184">*W przypadku elementu wiersza **ChargeType** wartość **Zakup** jest mapowana na nowy, a wartość **Zwrot** jest mapowana na **anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="cc492-184">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc492-185">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cc492-185">Response success and error codes</span></span>

<span data-ttu-id="cc492-186">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="cc492-186">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc492-187">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cc492-187">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc492-188">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cc492-188">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="cc492-189">Przykłady żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cc492-189">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="cc492-190">Przykład żądania i odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="cc492-190">Request-response example 1</span></span>

<span data-ttu-id="cc492-191">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="cc492-191">The following details apply to this example:</span></span>

- <span data-ttu-id="cc492-192">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="cc492-192">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="cc492-193">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="cc492-193">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="cc492-194">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="cc492-194">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="cc492-195">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="cc492-195">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="cc492-196">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="cc492-196">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="cc492-197">Przykład żądania i odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="cc492-197">Request-response example 2</span></span>

<span data-ttu-id="cc492-198">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="cc492-198">The following details apply to this example:</span></span>

- <span data-ttu-id="cc492-199">**Dostawca:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="cc492-199">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="cc492-200">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="cc492-200">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="cc492-201">**Okres:** **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="cc492-201">**Period**: **Previous**</span></span>
- <span data-ttu-id="cc492-202">**SeekOperation:** **Dalej**</span><span class="sxs-lookup"><span data-stu-id="cc492-202">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="cc492-203">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="cc492-203">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="cc492-204">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="cc492-204">Response example 2</span></span>

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
