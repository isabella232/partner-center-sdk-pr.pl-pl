---
title: Pobieranie faktur — elementy linii zużycia komercyjnego
description: Za pomocą interfejsów API Centrum partnerskiego można uzyskać kolekcję nienaliczanych szczegółowych informacji o towarach związanych z sprzedażą komercyjną dla określonej faktury.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b6ca8d6ff7af53dd2a258ea20e6eaeb26421440
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274669"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="066fb-103">Pobieranie faktur — elementy linii zużycia komercyjnego</span><span class="sxs-lookup"><span data-stu-id="066fb-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="066fb-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="066fb-104">**Applies to:**</span></span>

- <span data-ttu-id="066fb-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="066fb-105">Partner Center</span></span>

<span data-ttu-id="066fb-106">Jak uzyskać kolekcję rozliczonych szczegółów dotyczących elementów linii zużycia komercyjnego.</span><span class="sxs-lookup"><span data-stu-id="066fb-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="066fb-107">Korzystając z poniższych metod, można użyć programu w celu uzyskania kolekcji szczegółów dotyczących nieobciążanych elementów linii zużycia komercyjnego (nazywanych również otwartymi elementami wiersza użycia).</span><span class="sxs-lookup"><span data-stu-id="066fb-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="066fb-108">Dzienne użycie zwykle trwa 24 godziny w centrum partnerskim lub dostęp do niego za pomocą interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="066fb-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="066fb-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="066fb-109">Prerequisites</span></span>

- <span data-ttu-id="066fb-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="066fb-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="066fb-111">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="066fb-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="066fb-112">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="066fb-112">An invoice identifier.</span></span> <span data-ttu-id="066fb-113">Identyfikuje fakturę, dla której mają zostać pobrane elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="066fb-114">C\#</span><span class="sxs-lookup"><span data-stu-id="066fb-114">C\#</span></span>

<span data-ttu-id="066fb-115">Aby pobrać elementy wiersza dla określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="066fb-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="066fb-116">Wywołaj metodę [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , aby uzyskać interfejs do fakturowania operacji dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="066fb-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="066fb-117">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="066fb-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="066fb-118">**Obiekt Invoice** zawiera wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="066fb-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="066fb-119">**Dostawca** identyfikuje źródło informacji o nieobciążanych szczegółach (na przykład **jednorazowej**).</span><span class="sxs-lookup"><span data-stu-id="066fb-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="066fb-120">**InvoiceLineItemType** określa typ (na przykład **UsageLineItem**).</span><span class="sxs-lookup"><span data-stu-id="066fb-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="066fb-121">Poniższy przykładowy kod używa pętli **foreach** do przetwarzania kolekcji **InvoiceLineItems** .</span><span class="sxs-lookup"><span data-stu-id="066fb-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="066fb-122">Dla każdego **InvoiceLineItemType** pobierana jest oddzielna Kolekcja elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="066fb-123">Aby uzyskać kolekcję elementów wierszy, które odpowiadają wystąpieniu **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="066fb-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="066fb-124">Przekaż **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="066fb-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="066fb-125">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="066fb-126">Utwórz moduł wyliczający, który przejdzie do kolekcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="066fb-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="066fb-127">Aby poznać podobny przykład, zobacz:</span><span class="sxs-lookup"><span data-stu-id="066fb-127">For a similar example, see:</span></span>

- <span data-ttu-id="066fb-128">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="066fb-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="066fb-129">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="066fb-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="066fb-130">Klasa: **GetUnBilledConsumptionReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="066fb-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="066fb-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="066fb-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="066fb-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="066fb-132">Request syntax</span></span>

<span data-ttu-id="066fb-133">W zależności od przypadku użycia można użyć następujących składni dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="066fb-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="066fb-134">Aby uzyskać więcej informacji, zobacz opisy poszczególnych składni.</span><span class="sxs-lookup"><span data-stu-id="066fb-134">For more information, see the descriptions for each syntax.</span></span>

| <span data-ttu-id="066fb-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="066fb-135">Method</span></span>  | <span data-ttu-id="066fb-136">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="066fb-136">Request URI</span></span>                                                                                                                                                                                              | <span data-ttu-id="066fb-137">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="066fb-137">Description of syntax use case</span></span>                                                                                                     |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="066fb-138">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="066fb-138">**GET**</span></span> | <span data-ttu-id="066fb-139">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/unbilled/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &okres = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="066fb-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                       | <span data-ttu-id="066fb-140">Użyj tej składni, aby zwrócić pełną listę każdego elementu wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="066fb-140">Use this syntax to return a full list of every line item for the given invoice.</span></span>                                                    |
| <span data-ttu-id="066fb-141">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="066fb-141">**GET**</span></span> | <span data-ttu-id="066fb-142">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/unbilled/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="066fb-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>           | <span data-ttu-id="066fb-143">Ta składnia jest używana w przypadku dużych faktur.</span><span class="sxs-lookup"><span data-stu-id="066fb-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="066fb-144">Użyj tej składni z określonym rozmiarem i przesunięciu na 0, aby zwrócić stronicowaną listę elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="066fb-145">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="066fb-145">**GET**</span></span> | <span data-ttu-id="066fb-146">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/unbilled/LineItems? Provider = jednorazowej&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="066fb-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span> | <span data-ttu-id="066fb-147">Użyj tej składni, aby uzyskać następną stronę elementów wiersza uzgodnienia przy użyciu `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="066fb-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span>                                  |

#### <a name="uri-parameters"></a><span data-ttu-id="066fb-148">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="066fb-148">URI parameters</span></span>

<span data-ttu-id="066fb-149">Podczas tworzenia żądania Użyj następujących parametrów URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="066fb-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="066fb-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="066fb-150">Name</span></span>                   | <span data-ttu-id="066fb-151">Typ</span><span class="sxs-lookup"><span data-stu-id="066fb-151">Type</span></span>   | <span data-ttu-id="066fb-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="066fb-152">Required</span></span> | <span data-ttu-id="066fb-153">Opis</span><span class="sxs-lookup"><span data-stu-id="066fb-153">Description</span></span>                                                                                                                                                                                                                                |
|------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="066fb-154">dostawcy</span><span class="sxs-lookup"><span data-stu-id="066fb-154">provider</span></span>               | <span data-ttu-id="066fb-155">ciąg</span><span class="sxs-lookup"><span data-stu-id="066fb-155">string</span></span> | <span data-ttu-id="066fb-156">Tak</span><span class="sxs-lookup"><span data-stu-id="066fb-156">Yes</span></span>      | <span data-ttu-id="066fb-157">Dostawca: "**jednorazowej**".</span><span class="sxs-lookup"><span data-stu-id="066fb-157">The provider: "**OneTime**".</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="066fb-158">Typ faktury-wiersz-element</span><span class="sxs-lookup"><span data-stu-id="066fb-158">invoice-line-item-type</span></span> | <span data-ttu-id="066fb-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="066fb-159">string</span></span> | <span data-ttu-id="066fb-160">Tak</span><span class="sxs-lookup"><span data-stu-id="066fb-160">Yes</span></span>      | <span data-ttu-id="066fb-161">Typ faktury szczegóły: "**UsageLineItems**", "**UsageLineItems**".</span><span class="sxs-lookup"><span data-stu-id="066fb-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>                                                                                                                                                                    |
| <span data-ttu-id="066fb-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="066fb-162">currencyCode</span></span>           | <span data-ttu-id="066fb-163">ciąg</span><span class="sxs-lookup"><span data-stu-id="066fb-163">string</span></span> | <span data-ttu-id="066fb-164">Tak</span><span class="sxs-lookup"><span data-stu-id="066fb-164">Yes</span></span>      | <span data-ttu-id="066fb-165">Kod waluty dla nieobciążanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-165">The currency code for the unbilled line items.</span></span>                                                                                                                                                                                             |
| <span data-ttu-id="066fb-166">period</span><span class="sxs-lookup"><span data-stu-id="066fb-166">period</span></span>                 | <span data-ttu-id="066fb-167">ciąg</span><span class="sxs-lookup"><span data-stu-id="066fb-167">string</span></span> | <span data-ttu-id="066fb-168">Tak</span><span class="sxs-lookup"><span data-stu-id="066fb-168">Yes</span></span>      | <span data-ttu-id="066fb-169">Okres nienaliczanych Rekonesans (na przykład: **Current**, **Previous**).</span><span class="sxs-lookup"><span data-stu-id="066fb-169">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="066fb-170">Załóżmy, że musisz wykonać zapytanie dotyczące nienaliczanych danych użycia cyklu rozliczeniowego (01/01/2020 – 01/31/2020) w styczniu, wybierz okres jako **"Current", "** else **".**</span><span class="sxs-lookup"><span data-stu-id="066fb-170">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **"Current,"** else **"Previous."**</span></span> |
| <span data-ttu-id="066fb-171">size</span><span class="sxs-lookup"><span data-stu-id="066fb-171">size</span></span>                   | <span data-ttu-id="066fb-172">liczba</span><span class="sxs-lookup"><span data-stu-id="066fb-172">number</span></span> | <span data-ttu-id="066fb-173">Nie</span><span class="sxs-lookup"><span data-stu-id="066fb-173">No</span></span>       | <span data-ttu-id="066fb-174">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="066fb-174">The maximum number of items to return.</span></span> <span data-ttu-id="066fb-175">Domyślny rozmiar to 2000.</span><span class="sxs-lookup"><span data-stu-id="066fb-175">The default size is 2000.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="066fb-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="066fb-176">seekOperation</span></span>          | <span data-ttu-id="066fb-177">ciąg</span><span class="sxs-lookup"><span data-stu-id="066fb-177">string</span></span> | <span data-ttu-id="066fb-178">Nie</span><span class="sxs-lookup"><span data-stu-id="066fb-178">No</span></span>       | <span data-ttu-id="066fb-179">Ustaw `seekOperation=Next` , aby uzyskać następną stronę elementów linii uzgadniania.</span><span class="sxs-lookup"><span data-stu-id="066fb-179">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                                                                                                                                                                |

### <a name="request-headers"></a><span data-ttu-id="066fb-180">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="066fb-180">Request headers</span></span>

<span data-ttu-id="066fb-181">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="066fb-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="066fb-182">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="066fb-182">Request body</span></span>

<span data-ttu-id="066fb-183">Brak.</span><span class="sxs-lookup"><span data-stu-id="066fb-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="066fb-184">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="066fb-184">REST response</span></span>

<span data-ttu-id="066fb-185">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="066fb-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="066fb-186">*Dla pozycji **line ItemType** wartość **Purchase** jest mapowana na **nową** , a **zwrot** wartości jest mapowany na **przycisk Anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="066fb-186">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="066fb-187">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="066fb-187">Response success and error codes</span></span>

<span data-ttu-id="066fb-188">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="066fb-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="066fb-189">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="066fb-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="066fb-190">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="066fb-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="066fb-191">Przykłady żądania-odpowiedź</span><span class="sxs-lookup"><span data-stu-id="066fb-191">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="066fb-192">Przykład żądania — odpowiedź 1</span><span class="sxs-lookup"><span data-stu-id="066fb-192">Request-response example 1</span></span>

<span data-ttu-id="066fb-193">Następujące szczegóły dotyczą tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="066fb-193">The following details apply to this example:</span></span>

- <span data-ttu-id="066fb-194">**Dostawca**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="066fb-194">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="066fb-195">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="066fb-195">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="066fb-196">**Okres**: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="066fb-196">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="066fb-197">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="066fb-197">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="066fb-198">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="066fb-198">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="066fb-199">Przykład żądania — odpowiedź 2</span><span class="sxs-lookup"><span data-stu-id="066fb-199">Request-response example 2</span></span>

<span data-ttu-id="066fb-200">Następujące szczegóły dotyczą tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="066fb-200">The following details apply to this example:</span></span>

- <span data-ttu-id="066fb-201">**Dostawca**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="066fb-201">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="066fb-202">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="066fb-202">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="066fb-203">**Okres**: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="066fb-203">**Period**: **Previous**</span></span>
- <span data-ttu-id="066fb-204">**SeekOperation**: **dalej**</span><span class="sxs-lookup"><span data-stu-id="066fb-204">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="066fb-205">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="066fb-205">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="066fb-206">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="066fb-206">Response example 2</span></span>

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
