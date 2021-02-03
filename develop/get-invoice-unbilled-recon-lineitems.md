---
title: Pobieranie nierozliczanych elementów wierszy uzgadniania faktur
description: Za pomocą interfejsów API Centrum partnerskiego można uzyskać informacje o nienaliczanych szczegółach elementu wiersza uzgodnienia w określonym okresie.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768442"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="d40f0-103">Pobieranie nierozliczanych elementów wierszy uzgadniania faktur</span><span class="sxs-lookup"><span data-stu-id="d40f0-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="d40f0-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="d40f0-104">**Applies to:**</span></span>

- <span data-ttu-id="d40f0-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="d40f0-105">Partner Center</span></span>
- <span data-ttu-id="d40f0-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d40f0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d40f0-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="d40f0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d40f0-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d40f0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d40f0-109">Korzystając z poniższych metod, można uzyskać zbiór szczegółów dotyczących nienaliczanych elementów wierszy faktury (nazywanych również otwartymi wierszami rozliczeń).</span><span class="sxs-lookup"><span data-stu-id="d40f0-109">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d40f0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d40f0-110">Prerequisites</span></span>

- <span data-ttu-id="d40f0-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d40f0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d40f0-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d40f0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d40f0-113">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="d40f0-113">An invoice identifier.</span></span> <span data-ttu-id="d40f0-114">Identyfikuje fakturę, dla której mają zostać pobrane elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="d40f0-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d40f0-115">C\#</span></span>

<span data-ttu-id="d40f0-116">Aby uzyskać elementy wiersza dla określonej faktury, Pobierz obiekt Invoice:</span><span class="sxs-lookup"><span data-stu-id="d40f0-116">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="d40f0-117">Wywołaj metodę [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , aby uzyskać interfejs do fakturowania operacji dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="d40f0-117">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="d40f0-118">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="d40f0-118">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="d40f0-119">Obiekt Invoice zawiera wszystkie informacje dotyczące określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="d40f0-119">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="d40f0-120">**Dostawca** identyfikuje źródło informacji o nieobciążanych szczegółach (na przykład **jednorazowej**).</span><span class="sxs-lookup"><span data-stu-id="d40f0-120">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="d40f0-121">**InvoiceLineItemType** określa typ (na przykład **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="d40f0-121">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="d40f0-122">Aby uzyskać kolekcję elementów wierszy, które odpowiadają wystąpieniu **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="d40f0-122">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="d40f0-123">Przekaż BillingProvider i InvoiceLineItemType wystąpienia do metody [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="d40f0-123">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="d40f0-124">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="d40f0-125">Utwórz moduł wyliczający, który przejdzie do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d40f0-125">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="d40f0-126">Aby zapoznać się z przykładem, zobacz następujący przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="d40f0-126">For an example, see the following sample code.</span></span>

<span data-ttu-id="d40f0-127">Następujący przykładowy kod używa pętli **foreach** do przetwarzania kolekcji **InvoiceLineItems** .</span><span class="sxs-lookup"><span data-stu-id="d40f0-127">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="d40f0-128">Dla każdego **InvoiceLineItemType** pobierana jest oddzielna Kolekcja elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-128">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="d40f0-129">Aby poznać podobny przykład, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d40f0-129">For a similar example, see:</span></span>

- <span data-ttu-id="d40f0-130">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d40f0-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d40f0-131">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="d40f0-131">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="d40f0-132">Klasa: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="d40f0-132">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d40f0-133">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d40f0-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d40f0-134">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d40f0-134">Request syntax</span></span>

<span data-ttu-id="d40f0-135">W zależności od przypadku użycia można użyć następujących składni dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="d40f0-135">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="d40f0-136">Aby uzyskać więcej informacji, zobacz opisy poszczególnych składni.</span><span class="sxs-lookup"><span data-stu-id="d40f0-136">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="d40f0-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="d40f0-137">Method</span></span>  | <span data-ttu-id="d40f0-138">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d40f0-138">Request URI</span></span>            | <span data-ttu-id="d40f0-139">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="d40f0-139">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d40f0-140">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d40f0-140">**GET**</span></span> | <span data-ttu-id="d40f0-141">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &okres = {period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d40f0-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="d40f0-142">Użyj tej składni, aby zwrócić pełną listę każdego elementu wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="d40f0-142">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="d40f0-143">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d40f0-143">**GET**</span></span> | <span data-ttu-id="d40f0-144">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d40f0-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="d40f0-145">W przypadku dużych faktur należy użyć tej składni z określonym rozmiarem i przesunięciu na 0, aby zwrócić stronicowaną listę elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-145">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="d40f0-146">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d40f0-146">**GET**</span></span> | <span data-ttu-id="d40f0-147">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = billinglineitems&CurrencyCode = {currencycode} &period = {period} &size = {size} &SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="d40f0-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="d40f0-148">Użyj tej składni, aby uzyskać następną stronę elementów wiersza uzgodnienia przy użyciu `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="d40f0-148">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d40f0-149">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="d40f0-149">URI parameters</span></span>

<span data-ttu-id="d40f0-150">Podczas tworzenia żądania Użyj następujących parametrów URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="d40f0-150">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="d40f0-151">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d40f0-151">Name</span></span>                   | <span data-ttu-id="d40f0-152">Typ</span><span class="sxs-lookup"><span data-stu-id="d40f0-152">Type</span></span>   | <span data-ttu-id="d40f0-153">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d40f0-153">Required</span></span> | <span data-ttu-id="d40f0-154">Opis</span><span class="sxs-lookup"><span data-stu-id="d40f0-154">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="d40f0-155">Identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="d40f0-155">invoice-id</span></span>             | <span data-ttu-id="d40f0-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-156">string</span></span> | <span data-ttu-id="d40f0-157">Tak</span><span class="sxs-lookup"><span data-stu-id="d40f0-157">Yes</span></span>      | <span data-ttu-id="d40f0-158">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="d40f0-158">A string that identifies the invoice.</span></span> <span data-ttu-id="d40f0-159">Użyj "unbilld", aby uzyskać rozliczane oszacowania.</span><span class="sxs-lookup"><span data-stu-id="d40f0-159">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="d40f0-160">dostawcy</span><span class="sxs-lookup"><span data-stu-id="d40f0-160">provider</span></span>               | <span data-ttu-id="d40f0-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-161">string</span></span> | <span data-ttu-id="d40f0-162">Tak</span><span class="sxs-lookup"><span data-stu-id="d40f0-162">Yes</span></span>      | <span data-ttu-id="d40f0-163">Dostawca: "jednorazowej".</span><span class="sxs-lookup"><span data-stu-id="d40f0-163">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="d40f0-164">Typ faktury-wiersz-element</span><span class="sxs-lookup"><span data-stu-id="d40f0-164">invoice-line-item-type</span></span> | <span data-ttu-id="d40f0-165">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-165">string</span></span> | <span data-ttu-id="d40f0-166">Tak</span><span class="sxs-lookup"><span data-stu-id="d40f0-166">Yes</span></span>      | <span data-ttu-id="d40f0-167">Typ szczegółów faktury: "BillingLineItems".</span><span class="sxs-lookup"><span data-stu-id="d40f0-167">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="d40f0-168">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="d40f0-168">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="d40f0-169">bool</span><span class="sxs-lookup"><span data-stu-id="d40f0-169">bool</span></span>   | <span data-ttu-id="d40f0-170">Nie</span><span class="sxs-lookup"><span data-stu-id="d40f0-170">No</span></span>       | <span data-ttu-id="d40f0-171">Wartość wskazująca, czy zwrócić elementy wiersza z zastosowaniem środków uzyskanych przez partnera.</span><span class="sxs-lookup"><span data-stu-id="d40f0-171">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="d40f0-172">Uwaga: ten parametr zostanie zastosowany tylko wtedy, gdy typ dostawcy to jednorazowej, a InvoiceLineItemType to UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="d40f0-172">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="d40f0-173">currencyCode</span><span class="sxs-lookup"><span data-stu-id="d40f0-173">currencyCode</span></span>           | <span data-ttu-id="d40f0-174">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-174">string</span></span> | <span data-ttu-id="d40f0-175">Tak</span><span class="sxs-lookup"><span data-stu-id="d40f0-175">Yes</span></span>      | <span data-ttu-id="d40f0-176">Kod waluty dla nieobciążanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-176">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="d40f0-177">period</span><span class="sxs-lookup"><span data-stu-id="d40f0-177">period</span></span>                 | <span data-ttu-id="d40f0-178">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-178">string</span></span> | <span data-ttu-id="d40f0-179">Tak</span><span class="sxs-lookup"><span data-stu-id="d40f0-179">Yes</span></span>      | <span data-ttu-id="d40f0-180">Okres nienaliczanych rekonesans.</span><span class="sxs-lookup"><span data-stu-id="d40f0-180">The period for unbilled recon.</span></span> <span data-ttu-id="d40f0-181">przykład: Current, Previous.</span><span class="sxs-lookup"><span data-stu-id="d40f0-181">example: current, previous.</span></span>                      |
| <span data-ttu-id="d40f0-182">size</span><span class="sxs-lookup"><span data-stu-id="d40f0-182">size</span></span>                   | <span data-ttu-id="d40f0-183">liczba</span><span class="sxs-lookup"><span data-stu-id="d40f0-183">number</span></span> | <span data-ttu-id="d40f0-184">Nie</span><span class="sxs-lookup"><span data-stu-id="d40f0-184">No</span></span>       | <span data-ttu-id="d40f0-185">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="d40f0-185">The maximum number of items to return.</span></span> <span data-ttu-id="d40f0-186">Rozmiar domyślny to 2000</span><span class="sxs-lookup"><span data-stu-id="d40f0-186">Default size is 2000</span></span>                     |
| <span data-ttu-id="d40f0-187">seekOperation</span><span class="sxs-lookup"><span data-stu-id="d40f0-187">seekOperation</span></span>          | <span data-ttu-id="d40f0-188">ciąg</span><span class="sxs-lookup"><span data-stu-id="d40f0-188">string</span></span> | <span data-ttu-id="d40f0-189">Nie</span><span class="sxs-lookup"><span data-stu-id="d40f0-189">No</span></span>       | <span data-ttu-id="d40f0-190">Ustaw seekOperation = dalej, aby uzyskać następną stronę elementów wiersza rekonesans.</span><span class="sxs-lookup"><span data-stu-id="d40f0-190">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="d40f0-191">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d40f0-191">Request headers</span></span>

<span data-ttu-id="d40f0-192">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d40f0-192">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d40f0-193">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d40f0-193">Request body</span></span>

<span data-ttu-id="d40f0-194">Brak.</span><span class="sxs-lookup"><span data-stu-id="d40f0-194">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="d40f0-195">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d40f0-195">REST response</span></span>

<span data-ttu-id="d40f0-196">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="d40f0-196">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="d40f0-197">*Dla pozycji **line ItemType** wartość **Purchase** jest mapowana na **nową** , a **zwrot** wartości jest mapowany na **przycisk Anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="d40f0-197">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d40f0-198">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d40f0-198">Response success and error codes</span></span>

<span data-ttu-id="d40f0-199">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="d40f0-199">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d40f0-200">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d40f0-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d40f0-201">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d40f0-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="d40f0-202">Przykłady żądania-odpowiedź</span><span class="sxs-lookup"><span data-stu-id="d40f0-202">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="d40f0-203">Przykład żądania — odpowiedź 1</span><span class="sxs-lookup"><span data-stu-id="d40f0-203">Request-response example 1</span></span>

<span data-ttu-id="d40f0-204">Następujące szczegóły dotyczą tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="d40f0-204">The following details apply to this example:</span></span>

- <span data-ttu-id="d40f0-205">Dostawca: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="d40f0-205">Provider: **OneTime**</span></span>
- <span data-ttu-id="d40f0-206">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d40f0-206">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="d40f0-207">Okres: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="d40f0-207">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="d40f0-208">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="d40f0-208">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="d40f0-209">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="d40f0-209">Response example 1</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="d40f0-210">Przykład żądania — odpowiedź 2</span><span class="sxs-lookup"><span data-stu-id="d40f0-210">Request-response example 2</span></span>

<span data-ttu-id="d40f0-211">Następujące szczegóły dotyczą tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="d40f0-211">The following details apply to this example:</span></span>

- <span data-ttu-id="d40f0-212">Dostawca: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="d40f0-212">Provider: **OneTime**</span></span>
- <span data-ttu-id="d40f0-213">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d40f0-213">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="d40f0-214">Okres: **poprzedni**</span><span class="sxs-lookup"><span data-stu-id="d40f0-214">Period: **Previous**</span></span>
- <span data-ttu-id="d40f0-215">SeekOperation: **dalej**</span><span class="sxs-lookup"><span data-stu-id="d40f0-215">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="d40f0-216">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="d40f0-216">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="d40f0-217">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="d40f0-217">Response example 2</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a><span data-ttu-id="d40f0-218">Przykład żądania 3</span><span class="sxs-lookup"><span data-stu-id="d40f0-218">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="d40f0-219">Przykład odpowiedzi 3</span><span class="sxs-lookup"><span data-stu-id="d40f0-219">Response example 3</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
