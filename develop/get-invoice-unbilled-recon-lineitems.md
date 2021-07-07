---
title: Pobierz nienalizane elementy wiersza uzgodnień faktury
description: Możesz uzyskać kolekcję nienalicznych szczegółów elementu wiersza uzgodnień dla określonego okresu przy użyciu Partner Center API.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 5ab7dde0d78e8ff15bb1a960b16c8c925b0478ce
ms.sourcegitcommit: c5acfb373aa012eb3b6c17182f7ca56883502c6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/19/2021
ms.locfileid: "112391295"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="1047e-103">Pobierz nienalizane elementy wiersza uzgodnień faktury</span><span class="sxs-lookup"><span data-stu-id="1047e-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="1047e-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1047e-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1047e-105">Możesz użyć następujących metod, aby uzyskać kolekcję szczegółów dla nienaliczonych pozycji faktur (znanych także jako otwarte pozycje rozliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="1047e-105">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1047e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1047e-106">Prerequisites</span></span>

- <span data-ttu-id="1047e-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1047e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1047e-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1047e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1047e-109">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="1047e-109">An invoice identifier.</span></span> <span data-ttu-id="1047e-110">Identyfikuje fakturę, dla której mają zostać pobrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="1047e-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="1047e-111">C\#</span><span class="sxs-lookup"><span data-stu-id="1047e-111">C\#</span></span>

<span data-ttu-id="1047e-112">Aby uzyskać pozycje dla określonej faktury, pobierz obiekt faktury:</span><span class="sxs-lookup"><span data-stu-id="1047e-112">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="1047e-113">Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="1047e-113">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="1047e-114">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="1047e-114">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="1047e-115">Obiekt faktury zawiera wszystkie informacje dotyczące określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="1047e-115">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="1047e-116">**Dostawca** identyfikuje źródło nienaliczonych informacji szczegółowych (na przykład **OneTime).**</span><span class="sxs-lookup"><span data-stu-id="1047e-116">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="1047e-117">**InvoiceLineItemType** określa typ (na przykład **BillingLineItem).**</span><span class="sxs-lookup"><span data-stu-id="1047e-117">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="1047e-118">Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="1047e-118">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="1047e-119">Przekaż wartości BillingProvider i InvoiceLineItemType wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="1047e-119">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="1047e-120">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="1047e-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="1047e-121">Utwórz moduł wyliczający w celu przechodzenia przez kolekcję.</span><span class="sxs-lookup"><span data-stu-id="1047e-121">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="1047e-122">Aby uzyskać przykład, zobacz poniższy przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="1047e-122">For an example, see the following sample code.</span></span>

<span data-ttu-id="1047e-123">Poniższy przykładowy kod używa **pętli foreach** do przetwarzania kolekcji **InvoiceLineItems.**</span><span class="sxs-lookup"><span data-stu-id="1047e-123">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="1047e-124">Dla każdego typu **InvoiceLineItemType** pobierana jest oddzielna kolekcja elementów wierszy.</span><span class="sxs-lookup"><span data-stu-id="1047e-124">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

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

<span data-ttu-id="1047e-125">Aby uzyskać podobny przykład, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1047e-125">For a similar example, see:</span></span>

- <span data-ttu-id="1047e-126">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1047e-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1047e-127">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="1047e-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1047e-128">Klasa: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="1047e-128">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1047e-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1047e-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1047e-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1047e-130">Request syntax</span></span>

<span data-ttu-id="1047e-131">W zależności od przypadku użycia możesz użyć następujących składni dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="1047e-131">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="1047e-132">Aby uzyskać więcej informacji, zobacz opisy poszczególnych składni.</span><span class="sxs-lookup"><span data-stu-id="1047e-132">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="1047e-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="1047e-133">Method</span></span>  | <span data-ttu-id="1047e-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1047e-134">Request URI</span></span>            | <span data-ttu-id="1047e-135">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="1047e-135">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1047e-136">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1047e-136">**GET**</span></span> | <span data-ttu-id="1047e-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator-faktury}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1047e-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="1047e-138">Użyj tej składni, aby zwrócić pełną listę wszystkich elementów wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="1047e-138">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="1047e-139">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1047e-139">**GET**</span></span> | <span data-ttu-id="1047e-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator faktury}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1047e-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="1047e-141">W przypadku dużych faktur użyj tej składni z określonym rozmiarem i przesunięciem na podstawie wartości 0, aby zwrócić stronicowane listy elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1047e-141">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="1047e-142">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1047e-142">**GET**</span></span> | <span data-ttu-id="1047e-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="1047e-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="1047e-144">Użyj tej składni, aby uzyskać następną stronę elementów wiersza uzgodnień przy użyciu polecenia `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="1047e-144">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1047e-145">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="1047e-145">URI parameters</span></span>

<span data-ttu-id="1047e-146">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="1047e-146">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="1047e-147">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1047e-147">Name</span></span>                   | <span data-ttu-id="1047e-148">Typ</span><span class="sxs-lookup"><span data-stu-id="1047e-148">Type</span></span>   | <span data-ttu-id="1047e-149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1047e-149">Required</span></span> | <span data-ttu-id="1047e-150">Opis</span><span class="sxs-lookup"><span data-stu-id="1047e-150">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="1047e-151">identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="1047e-151">invoice-id</span></span>             | <span data-ttu-id="1047e-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-152">string</span></span> | <span data-ttu-id="1047e-153">Tak</span><span class="sxs-lookup"><span data-stu-id="1047e-153">Yes</span></span>      | <span data-ttu-id="1047e-154">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="1047e-154">A string that identifies the invoice.</span></span> <span data-ttu-id="1047e-155">Użyj wartości "unbilled", aby uzyskać nienalizane oszacowania.</span><span class="sxs-lookup"><span data-stu-id="1047e-155">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="1047e-156">Dostawca</span><span class="sxs-lookup"><span data-stu-id="1047e-156">provider</span></span>               | <span data-ttu-id="1047e-157">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-157">string</span></span> | <span data-ttu-id="1047e-158">Tak</span><span class="sxs-lookup"><span data-stu-id="1047e-158">Yes</span></span>      | <span data-ttu-id="1047e-159">Dostawca: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="1047e-159">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="1047e-160">typ elementu wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="1047e-160">invoice-line-item-type</span></span> | <span data-ttu-id="1047e-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-161">string</span></span> | <span data-ttu-id="1047e-162">Tak</span><span class="sxs-lookup"><span data-stu-id="1047e-162">Yes</span></span>      | <span data-ttu-id="1047e-163">Typ szczegółów faktury: "BillingLineItems".</span><span class="sxs-lookup"><span data-stu-id="1047e-163">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="1047e-164">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="1047e-164">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="1047e-165">bool</span><span class="sxs-lookup"><span data-stu-id="1047e-165">bool</span></span>   | <span data-ttu-id="1047e-166">Nie</span><span class="sxs-lookup"><span data-stu-id="1047e-166">No</span></span>       | <span data-ttu-id="1047e-167">Wartość wskazująca, czy zwrócić pozycje z zastosowanymi środków uzyskane przez partnera.</span><span class="sxs-lookup"><span data-stu-id="1047e-167">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="1047e-168">Uwaga: ten parametr będzie stosowany tylko wtedy, gdy typ dostawcy to OneTime, a InvoiceLineItemType to UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="1047e-168">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="1047e-169">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1047e-169">currencyCode</span></span>           | <span data-ttu-id="1047e-170">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-170">string</span></span> | <span data-ttu-id="1047e-171">Tak</span><span class="sxs-lookup"><span data-stu-id="1047e-171">Yes</span></span>      | <span data-ttu-id="1047e-172">Kod waluty dla nienaliowanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1047e-172">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="1047e-173">period</span><span class="sxs-lookup"><span data-stu-id="1047e-173">period</span></span>                 | <span data-ttu-id="1047e-174">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-174">string</span></span> | <span data-ttu-id="1047e-175">Tak</span><span class="sxs-lookup"><span data-stu-id="1047e-175">Yes</span></span>      | <span data-ttu-id="1047e-176">Okres dla nienaliowanych rekonesencji.</span><span class="sxs-lookup"><span data-stu-id="1047e-176">The period for unbilled recon.</span></span> <span data-ttu-id="1047e-177">przykład: current, previous.</span><span class="sxs-lookup"><span data-stu-id="1047e-177">example: current, previous.</span></span>                      |
| <span data-ttu-id="1047e-178">size</span><span class="sxs-lookup"><span data-stu-id="1047e-178">size</span></span>                   | <span data-ttu-id="1047e-179">liczba</span><span class="sxs-lookup"><span data-stu-id="1047e-179">number</span></span> | <span data-ttu-id="1047e-180">Nie</span><span class="sxs-lookup"><span data-stu-id="1047e-180">No</span></span>       | <span data-ttu-id="1047e-181">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="1047e-181">The maximum number of items to return.</span></span> <span data-ttu-id="1047e-182">Domyślny rozmiar to 2000</span><span class="sxs-lookup"><span data-stu-id="1047e-182">Default size is 2000</span></span>                     |
| <span data-ttu-id="1047e-183">seekOperation</span><span class="sxs-lookup"><span data-stu-id="1047e-183">seekOperation</span></span>          | <span data-ttu-id="1047e-184">ciąg</span><span class="sxs-lookup"><span data-stu-id="1047e-184">string</span></span> | <span data-ttu-id="1047e-185">Nie</span><span class="sxs-lookup"><span data-stu-id="1047e-185">No</span></span>       | <span data-ttu-id="1047e-186">Ustaw wartość seekOperation=Next, aby uzyskać następną stronę elementów ponownego wiersza.</span><span class="sxs-lookup"><span data-stu-id="1047e-186">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="1047e-187">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1047e-187">Request headers</span></span>

<span data-ttu-id="1047e-188">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1047e-188">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1047e-189">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1047e-189">Request body</span></span>

<span data-ttu-id="1047e-190">Brak.</span><span class="sxs-lookup"><span data-stu-id="1047e-190">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="1047e-191">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1047e-191">REST response</span></span>

<span data-ttu-id="1047e-192">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="1047e-192">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="1047e-193">*W przypadku elementu wiersza **ChargeType** wartość **Zakup** jest mapowana na nowy, a wartość **Zwrot** jest mapowana na **anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="1047e-193">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1047e-194">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1047e-194">Response success and error codes</span></span>

<span data-ttu-id="1047e-195">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1047e-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1047e-196">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1047e-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1047e-197">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1047e-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="1047e-198">Przykłady żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1047e-198">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="1047e-199">Przykład żądania i odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="1047e-199">Request-response example 1</span></span>

<span data-ttu-id="1047e-200">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="1047e-200">The following details apply to this example:</span></span>

- <span data-ttu-id="1047e-201">Dostawca: **OneTime**</span><span class="sxs-lookup"><span data-stu-id="1047e-201">Provider: **OneTime**</span></span>
- <span data-ttu-id="1047e-202">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="1047e-202">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="1047e-203">Okres: **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1047e-203">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="1047e-204">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="1047e-204">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="1047e-205">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="1047e-205">Response example 1</span></span>

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
   "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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

### <a name="request-response-example-2"></a><span data-ttu-id="1047e-206">Przykład żądania i odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="1047e-206">Request-response example 2</span></span>

<span data-ttu-id="1047e-207">W tym przykładzie mają zastosowanie następujące szczegóły:</span><span class="sxs-lookup"><span data-stu-id="1047e-207">The following details apply to this example:</span></span>

- <span data-ttu-id="1047e-208">Dostawca: **OneTime**</span><span class="sxs-lookup"><span data-stu-id="1047e-208">Provider: **OneTime**</span></span>
- <span data-ttu-id="1047e-209">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="1047e-209">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="1047e-210">Okres: **Poprzedni**</span><span class="sxs-lookup"><span data-stu-id="1047e-210">Period: **Previous**</span></span>
- <span data-ttu-id="1047e-211">SeekOperation: **Dalej**</span><span class="sxs-lookup"><span data-stu-id="1047e-211">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="1047e-212">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="1047e-212">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="1047e-213">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="1047e-213">Response example 2</span></span>

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
   "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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

#### <a name="request-example-3"></a><span data-ttu-id="1047e-214">Przykład żądania 3</span><span class="sxs-lookup"><span data-stu-id="1047e-214">Request example 3</span></span>

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

#### <a name="response-example-3"></a><span data-ttu-id="1047e-215">Przykład odpowiedzi 3</span><span class="sxs-lookup"><span data-stu-id="1047e-215">Response example 3</span></span>

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
    "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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
