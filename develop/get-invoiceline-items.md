---
title: Pobieranie elementów wiersza faktury
description: Możesz uzyskać informacje o kolekcji pozycji wiersza faktury (zamknięty element linii rozliczeniowej) dla określonej faktury przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e797f549e1344268c8167259a231122e7c669a2e
ms.sourcegitcommit: 9f8ba784171ab4f980ed0c60ef6f2323849c4a98
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2021
ms.locfileid: "100499902"
---
# <a name="get-invoice-line-items"></a><span data-ttu-id="d471c-103">Pobieranie elementów wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="d471c-103">Get invoice line items</span></span>

<span data-ttu-id="d471c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="d471c-104">**Applies to:**</span></span>

- <span data-ttu-id="d471c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="d471c-105">Partner Center</span></span>
- <span data-ttu-id="d471c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d471c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d471c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="d471c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d471c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d471c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d471c-109">Przy użyciu poniższych metod można pobrać szczegóły kolekcji dla elementów wiersza faktury (znanych także jako zamknięte elementy wierszy rozliczeń) dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-109">You can use the following methods to get a collection details for of invoice line items (also known as closed billing line items) for a specified invoice.</span></span>

<span data-ttu-id="d471c-110">*Ten interfejs API nie jest już aktualizowany, z wyjątkiem poprawek błędów.*</span><span class="sxs-lookup"><span data-stu-id="d471c-110">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="d471c-111">Aplikacje należy zaktualizować w taki sposób, aby wywoływać interfejs API **jednorazowej** zamiast **witryny Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d471c-111">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="d471c-112">Interfejs API **jednorazowej** zapewnia dodatkową funkcjonalność i będzie nadal aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="d471c-112">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="d471c-113">Należy używać **jednorazowej** do wysyłania zapytań do wszystkich elementów linii zużycia komercyjnego, a nie z **witryny Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d471c-113">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="d471c-114">Można też użyć linków w wywołaniu łączy.</span><span class="sxs-lookup"><span data-stu-id="d471c-114">Or, you can follow the links in the estimate links call.</span></span>

<span data-ttu-id="d471c-115">Ten interfejs API obsługuje również typy **dostawców** subskrypcji **platformy Azure** i **pakietu Office** dla Microsoft Azure (MS-AZR-0145P) i oferty pakietu Office, dzięki czemu funkcja interfejsu API jest zgodna z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="d471c-115">This API also supports the **provider** types of **azure** and **office** for Microsoft Azure (MS-AZR-0145P) subscriptions and Office offers, which makes the API feature backward compatible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d471c-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d471c-116">Prerequisites</span></span>

- <span data-ttu-id="d471c-117">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d471c-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d471c-118">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d471c-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d471c-119">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-119">An invoice identifier.</span></span> <span data-ttu-id="d471c-120">Identyfikuje fakturę, dla której mają zostać pobrane elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="d471c-120">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="d471c-121">C\#</span><span class="sxs-lookup"><span data-stu-id="d471c-121">C\#</span></span>

<span data-ttu-id="d471c-122">Aby pobrać elementy wiersza dla określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="d471c-122">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="d471c-123">Wywołaj metodę [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) , aby uzyskać interfejs do fakturowania operacji dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-123">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="d471c-124">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) , aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="d471c-125">Obiekt Invoice zawiera wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-125">The invoice object contains all of the information for the specified invoice.</span></span>
3. <span data-ttu-id="d471c-126">Użyj właściwości [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) obiektu faktury, aby uzyskać dostęp do kolekcji obiektów [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) , z których każdy zawiera [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) i [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span><span class="sxs-lookup"><span data-stu-id="d471c-126">Use the invoice object's [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span></span> <span data-ttu-id="d471c-127">**BillingProvider** identyfikuje źródło informacji szczegółowych faktury (takich jak **Office**, **Azure**, **jednorazowej**), a **InvoiceLineItemType** określa typ (na przykład **BillingLineItem**).</span><span class="sxs-lookup"><span data-stu-id="d471c-127">The **BillingProvider** identifies the source of the invoice detail information (such as **Office**, **Azure**, **OneTime**), and the **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="d471c-128">Poniższy przykładowy kod używa pętli **foreach** do przetwarzania kolekcji **InvoiceDetails** .</span><span class="sxs-lookup"><span data-stu-id="d471c-128">The following example code uses a **foreach** loop to process the **InvoiceDetails** collection.</span></span> <span data-ttu-id="d471c-129">Dla każdego wystąpienia **InvoiceDetail** pobierana jest oddzielna Kolekcja elementów wierszy.</span><span class="sxs-lookup"><span data-stu-id="d471c-129">A separate collection of line items is retrieved for each **InvoiceDetail** instance.</span></span>

<span data-ttu-id="d471c-130">Aby uzyskać kolekcję elementów wierszy, które odpowiadają wystąpieniu **InvoiceDetail** :</span><span class="sxs-lookup"><span data-stu-id="d471c-130">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="d471c-131">Przekaż **BillingProvider** i **InvoiceLineItemType** wystąpienia do metody [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .</span><span class="sxs-lookup"><span data-stu-id="d471c-131">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="d471c-132">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) , aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="d471c-132">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="d471c-133">Utwórz moduł wyliczający, który przejdzie do kolekcji, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d471c-133">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;
// string invoiceId;

// Retrieve the invoice.
var invoiceOperations = partnerOperations.Invoices.ById(invoiceId);
var invoice = invoiceOperations.Get();

foreach (var invoiceDetail in invoice.InvoiceDetails)
{
    Console.WriteLine(string.Format("Getting invoice line item for product {0} and line item type {1}",
        invoiceDetail.BillingProvider,
        invoiceDetail.InvoiceLineItemType));

    // Is this an unpaged or paged request?
    bool isUnPaged = (this.invoicePageSize <= 0);

    // If the scenario is unpaged, get all the invoice line items, otherwise get the first page.
    var invoiceLineItemsCollection =
        (isUnPaged)
        ? invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get()
        : invoiceOperations.By(invoiceDetail.BillingProvider, invoiceDetail.InvoiceLineItemType).Get(this.invoicePageSize, 0);

    // Create an enumerator for traversing the line items collection.
    var invoiceLineItemEnumerator =
        partnerOperations.Enumerators.InvoiceLineItems.Create(invoiceLineItemsCollection);

    while (invoiceLineItemEnumerator.HasValue)
    {
        // invoiceLineItemEnumerator.Current contains a collection
        // of line items.
        Console.WriteLine(String.Format("invoiceLineItemEnumerator.Current has {0} line items.",
            invoiceLineItemEnumerator.Current.TotalCount));
        //
        // Insert code here to work with the line items.
        //
        Console.WriteLine();
        Console.Write("Press any key to retrieve the next invoice line items page");
        Console.ReadKey();

        // Get the next list of invoice line items.
        invoiceLineItemEnumerator.Next();
    }
}
```

<span data-ttu-id="d471c-134">Podobny przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="d471c-134">For a similar example, see the following:</span></span>

- <span data-ttu-id="d471c-135">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d471c-135">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d471c-136">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="d471c-136">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="d471c-137">Klasa: **GetInvoiceLineItems.cs**</span><span class="sxs-lookup"><span data-stu-id="d471c-137">Class: **GetInvoiceLineItems.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d471c-138">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d471c-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d471c-139">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-139">Request syntax</span></span>

<span data-ttu-id="d471c-140">Prześlij żądanie przy użyciu odpowiedniej składni dla dostawcy rozliczeń w danym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="d471c-140">Make your request using the appropriate syntax for the billing provider in your scenario.</span></span>

#### <a name="office"></a><span data-ttu-id="d471c-141">Office</span><span class="sxs-lookup"><span data-stu-id="d471c-141">Office</span></span>

<span data-ttu-id="d471c-142">Następująca składnia ma zastosowanie, gdy dostawca rozliczeń to **pakiet Office**.</span><span class="sxs-lookup"><span data-stu-id="d471c-142">The following syntax applies when the billing provider is **Office**.</span></span>

| <span data-ttu-id="d471c-143">Metoda</span><span class="sxs-lookup"><span data-stu-id="d471c-143">Method</span></span>  | <span data-ttu-id="d471c-144">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-144">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d471c-145">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d471c-145">**GET**</span></span> | <span data-ttu-id="d471c-146">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Office&invoicelineitemtype = billinglineitems&size = {size} &offset = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="d471c-147">Subskrypcja Microsoft Azure (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="d471c-147">Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="d471c-148">Poniższe składnie są stosowane, gdy dostawca rozliczeń ma subskrypcję Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="d471c-148">The following syntaxes apply when the billing provider has a Microsoft Azure (MS-AZR-0145P) subscription.</span></span>

| <span data-ttu-id="d471c-149">Metoda</span><span class="sxs-lookup"><span data-stu-id="d471c-149">Method</span></span>  | <span data-ttu-id="d471c-150">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-150">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d471c-151">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d471c-151">**GET**</span></span> | <span data-ttu-id="d471c-152">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = billinglineitems&size = {size} &offset = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-152">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |
| <span data-ttu-id="d471c-153">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d471c-153">**GET**</span></span> | <span data-ttu-id="d471c-154">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = Azure&invoicelineitemtype = usagelineitems&size = {size} &offset = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-154">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |

##### <a name="onetime"></a><span data-ttu-id="d471c-155">Jednorazowej</span><span class="sxs-lookup"><span data-stu-id="d471c-155">OneTime</span></span>

<span data-ttu-id="d471c-156">Poniższe składnie są stosowane, gdy dostawca rozliczeń jest **jednorazowej**.</span><span class="sxs-lookup"><span data-stu-id="d471c-156">The following syntaxes apply when the billing provider is **OneTime**.</span></span> <span data-ttu-id="d471c-157">Obejmuje to opłaty za rezerwacje, oprogramowanie, plany platformy Azure i komercyjne produkty korporacyjne platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d471c-157">This includes charges for Azure reservations, software, Azure plans, and commercial marketplace products.</span></span>

| <span data-ttu-id="d471c-158">Metoda</span><span class="sxs-lookup"><span data-stu-id="d471c-158">Method</span></span>  | <span data-ttu-id="d471c-159">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-159">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d471c-160">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d471c-160">**GET**</span></span> | <span data-ttu-id="d471c-161">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems? Provider = jednorazowej&invoicelineitemtype = billinglineitems&size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-161">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="d471c-162">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="d471c-162">**GET**</span></span> | <span data-ttu-id="d471c-163">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/onetime/billinglineitems&size = {size}? SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="d471c-163">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span></span>                           |

#### <a name="previous-syntaxes"></a><span data-ttu-id="d471c-164">Poprzednie składnie</span><span class="sxs-lookup"><span data-stu-id="d471c-164">Previous syntaxes</span></span>

<span data-ttu-id="d471c-165">Jeśli używasz następujących składni, pamiętaj, aby użyć odpowiedniej składni dla przypadku użycia.</span><span class="sxs-lookup"><span data-stu-id="d471c-165">If you are using the following syntaxes, be sure to use the appropriate syntax for your use case.</span></span>

<span data-ttu-id="d471c-166">*Ten interfejs API nie jest już aktualizowany, z wyjątkiem poprawek błędów.*</span><span class="sxs-lookup"><span data-stu-id="d471c-166">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="d471c-167">Aplikacje należy zaktualizować w taki sposób, aby wywoływać interfejs API **jednorazowej** zamiast **witryny Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d471c-167">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="d471c-168">Interfejs API **jednorazowej** zapewnia dodatkową funkcjonalność i będzie nadal aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="d471c-168">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="d471c-169">Należy używać **jednorazowej** do wysyłania zapytań do wszystkich elementów linii zużycia komercyjnego, a nie z **witryny Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d471c-169">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="d471c-170">Można też użyć linków w wywołaniu łączy.</span><span class="sxs-lookup"><span data-stu-id="d471c-170">Or, you can follow the links in the estimate links call.</span></span>

| <span data-ttu-id="d471c-171">Metoda</span><span class="sxs-lookup"><span data-stu-id="d471c-171">Method</span></span> | <span data-ttu-id="d471c-172">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-172">Request URI</span></span> | <span data-ttu-id="d471c-173">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="d471c-173">Description of syntax use case</span></span> |
| ------ | ----------- | -------------------------------- |
| <span data-ttu-id="d471c-174">GET</span><span class="sxs-lookup"><span data-stu-id="d471c-174">GET</span></span> | <span data-ttu-id="d471c-175">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-175">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1</span></span>                              | <span data-ttu-id="d471c-176">Możesz użyć tej składni, aby zwrócić pełną listę każdego elementu wiersza dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-176">You can use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="d471c-177">GET</span><span class="sxs-lookup"><span data-stu-id="d471c-177">GET</span></span> | <span data-ttu-id="d471c-178">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/{Billing-Provider}/{Invoice-line-Item-Type}? size = {size} &offset = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d471c-178">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1</span></span>  | <span data-ttu-id="d471c-179">W przypadku dużych faktur można użyć tej składni z określonym rozmiarem i przesunięciu na 0, aby zwrócić stronicowaną listę elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="d471c-179">For large invoices, you can use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="d471c-180">GET</span><span class="sxs-lookup"><span data-stu-id="d471c-180">GET</span></span> | <span data-ttu-id="d471c-181">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID}/LineItems/onetime/{Invoice-line-Item-Type}? SeekOperation = Next</span><span class="sxs-lookup"><span data-stu-id="d471c-181">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span></span>                               | <span data-ttu-id="d471c-182">Możesz użyć tej składni dla faktury z wartością dostawcy rozliczeń **jednorazowej** i ustawić **SeekOperation** , aby **dalej** uzyskać następną stronę elementów wiersza faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-182">You can use this syntax for an invoice with a billing-provider value of **OneTime** and set **seekOperation** to **Next** to get the next page of invoice line items.</span></span> |

##### <a name="uri-parameters"></a><span data-ttu-id="d471c-183">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="d471c-183">URI parameters</span></span>

<span data-ttu-id="d471c-184">Podczas tworzenia żądania Użyj następujących parametrów URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="d471c-184">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="d471c-185">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d471c-185">Name</span></span>                   | <span data-ttu-id="d471c-186">Typ</span><span class="sxs-lookup"><span data-stu-id="d471c-186">Type</span></span>   | <span data-ttu-id="d471c-187">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d471c-187">Required</span></span> | <span data-ttu-id="d471c-188">Opis</span><span class="sxs-lookup"><span data-stu-id="d471c-188">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="d471c-189">Identyfikator faktury</span><span class="sxs-lookup"><span data-stu-id="d471c-189">invoice-id</span></span>             | <span data-ttu-id="d471c-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="d471c-190">string</span></span> | <span data-ttu-id="d471c-191">Tak</span><span class="sxs-lookup"><span data-stu-id="d471c-191">Yes</span></span>      | <span data-ttu-id="d471c-192">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="d471c-192">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="d471c-193">rozliczenia — dostawca</span><span class="sxs-lookup"><span data-stu-id="d471c-193">billing-provider</span></span>       | <span data-ttu-id="d471c-194">ciąg</span><span class="sxs-lookup"><span data-stu-id="d471c-194">string</span></span> | <span data-ttu-id="d471c-195">Tak</span><span class="sxs-lookup"><span data-stu-id="d471c-195">Yes</span></span>      | <span data-ttu-id="d471c-196">Dostawca rozliczeń: "Office", "Azure", "jednorazowej".</span><span class="sxs-lookup"><span data-stu-id="d471c-196">The billing provider: "Office", "Azure", "OneTime".</span></span> <span data-ttu-id="d471c-197">W starszej wersji istnieją osobne modele danych dla transakcji pakietu Office & platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d471c-197">In the legacy, we have separate data models for Office & Azure transactions.</span></span> <span data-ttu-id="d471c-198">Jednak nowoczesny ma jeden model danych dla wszystkich transakcji przefiltrowanych przez wartość "jednorazowej".</span><span class="sxs-lookup"><span data-stu-id="d471c-198">However, the modern has one single data model across all transactions filtered through the "OneTime" value.</span></span>            |
| <span data-ttu-id="d471c-199">Typ faktury-wiersz-element</span><span class="sxs-lookup"><span data-stu-id="d471c-199">invoice-line-item-type</span></span> | <span data-ttu-id="d471c-200">ciąg</span><span class="sxs-lookup"><span data-stu-id="d471c-200">string</span></span> | <span data-ttu-id="d471c-201">Tak</span><span class="sxs-lookup"><span data-stu-id="d471c-201">Yes</span></span>      | <span data-ttu-id="d471c-202">Typ faktury szczegóły: "BillingLineItems", "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="d471c-202">The type of invoice detail: "BillingLineItems", "UsageLineItems".</span></span> |
| <span data-ttu-id="d471c-203">size</span><span class="sxs-lookup"><span data-stu-id="d471c-203">size</span></span>                   | <span data-ttu-id="d471c-204">liczba</span><span class="sxs-lookup"><span data-stu-id="d471c-204">number</span></span> | <span data-ttu-id="d471c-205">Nie</span><span class="sxs-lookup"><span data-stu-id="d471c-205">No</span></span>       | <span data-ttu-id="d471c-206">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="d471c-206">The maximum number of items to return.</span></span> <span data-ttu-id="d471c-207">Domyślny maksymalny rozmiar = 2000</span><span class="sxs-lookup"><span data-stu-id="d471c-207">Default max size = 2000</span></span>    |
| <span data-ttu-id="d471c-208">przesunięcie</span><span class="sxs-lookup"><span data-stu-id="d471c-208">offset</span></span>                 | <span data-ttu-id="d471c-209">liczba</span><span class="sxs-lookup"><span data-stu-id="d471c-209">number</span></span> | <span data-ttu-id="d471c-210">Nie</span><span class="sxs-lookup"><span data-stu-id="d471c-210">No</span></span>       | <span data-ttu-id="d471c-211">Indeks (liczony od zera) elementu pierwszego wiersza do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="d471c-211">The zero-based index of the first line item to return.</span></span>            |
| <span data-ttu-id="d471c-212">seekOperation</span><span class="sxs-lookup"><span data-stu-id="d471c-212">seekOperation</span></span>          | <span data-ttu-id="d471c-213">ciąg</span><span class="sxs-lookup"><span data-stu-id="d471c-213">string</span></span> | <span data-ttu-id="d471c-214">Nie</span><span class="sxs-lookup"><span data-stu-id="d471c-214">No</span></span>       | <span data-ttu-id="d471c-215">Jeśli **dostawca rozliczeń** jest równy **jednorazowej**, ustaw wartość **seekOperation** równą **Next** , aby uzyskać następną stronę elementów wiersza faktury.</span><span class="sxs-lookup"><span data-stu-id="d471c-215">If **billing-provider** equals **OneTime**, set **seekOperation** equal to **Next** to get the next page of invoice line items.</span></span> |
| <span data-ttu-id="d471c-216">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="d471c-216">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="d471c-217">bool</span><span class="sxs-lookup"><span data-stu-id="d471c-217">bool</span></span> | <span data-ttu-id="d471c-218">Nie</span><span class="sxs-lookup"><span data-stu-id="d471c-218">No</span></span> | <span data-ttu-id="d471c-219">Wartość wskazująca, czy zwrócić elementy wiersza z zastosowaniem środków uzyskanych przez partnera.</span><span class="sxs-lookup"><span data-stu-id="d471c-219">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="d471c-220">Uwaga: ten parametr zostanie zastosowany tylko wtedy, gdy typ dostawcy rozliczeń to jednorazowej, a InvoiceLineItemType to UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="d471c-220">Note: this parameter will be only applied when billing provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d471c-221">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="d471c-221">Request headers</span></span>

<span data-ttu-id="d471c-222">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d471c-222">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d471c-223">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d471c-223">Request body</span></span>

<span data-ttu-id="d471c-224">Brak.</span><span class="sxs-lookup"><span data-stu-id="d471c-224">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="d471c-225">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d471c-225">REST response</span></span>

<span data-ttu-id="d471c-226">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="d471c-226">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="d471c-227">*Dla pozycji **line ItemType** wartość **Purchase** jest mapowana na **nową**. **Zwrot** wartości jest mapowany na **Anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="d471c-227">*For the line item **ChargeType**, the value **Purchase** is mapped to **New**. The value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d471c-228">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d471c-228">Response success and error codes</span></span>

<span data-ttu-id="d471c-229">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="d471c-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d471c-230">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d471c-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d471c-231">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d471c-231">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="rest-request-response-examples"></a><span data-ttu-id="d471c-232">Przykłady żądania REST — odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d471c-232">REST request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="d471c-233">Przykład żądania — odpowiedź 1</span><span class="sxs-lookup"><span data-stu-id="d471c-233">Request-response example 1</span></span>

<span data-ttu-id="d471c-234">W tym przykładzie szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="d471c-234">In this example, the details are as follows:</span></span>

- <span data-ttu-id="d471c-235">**BillingProvider**: **Office**</span><span class="sxs-lookup"><span data-stu-id="d471c-235">**BillingProvider**: **Office**</span></span>
- <span data-ttu-id="d471c-236">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d471c-236">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="d471c-237">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="d471c-237">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="d471c-238">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="d471c-238">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [{
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045559164136",
            "subscriptionId": "4KIKawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "1F58ACD7-FE51-4705-9567-D009C9ADA150",
            "offerId": "AAA5B3F0-0EE2-431B-A42F-3F18F3C6D540",
            "durableOfferId": "2F707C7C-2433-49A5-A437-9CA7CF40D3EB",
            "offerName": "EXCHANGE ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionDescription": "EXCHANGE ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-12T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-12T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 3,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }, {
            "partnerId": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "customerId": "74221236-D09C-4870-AC1D-33E155E9AEBE",
            "customerName": "TSTAGIN1CUST190",
            "mpnId": 4391507,
            "tier2MpnId": -1,
            "orderId": "567735045564795186",
            "subscriptionId": "Ik4YawEAAAAAAAEA",
            "syndicationPartnerSubscriptionNumber": "D8A8F773-9D3E-4244-8797-3182075F09FA",
            "offerId": "618B53FE-9B99-428B-9745-F706AEAF3979",
            "durableOfferId": "69C67983-CF78-4102-83F6-3E5FD246864F",
            "offerName": "SHAREPOINT ONLINE (PLAN 2)",
            "domainName": "TStagin1Cust190.onmicrosoft.com",
            "billingCycleType": "MONTHLY",
            "subscriptionName": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionDescription": "SHAREPOINT ONLINE (PLAN 2)",
            "subscriptionStartDate": "2017-05-13T00:00:00",
            "subscriptionEndDate": "2018-06-10T00:00:00",
            "chargeStartDate": "2017-05-13T00:00:00",
            "chargeEndDate": "2017-06-09T00:00:00",
            "chargeType": "New",
            "unitPrice": 0.0,
            "quantity": 1,
            "amount": 0.0,
            "totalOtherDiscount": 0.0,
            "subtotal": 0.0,
            "tax": 0.0,
            "totalForCustomer": 0.0,
            "currency": "USD",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "office",
            "attributes": {
                "objectType": "LicenseBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Office&nvoicelineitemtype=BillingLineItems&size=2&offset=",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="d471c-239">Przykład żądania — odpowiedź 2</span><span class="sxs-lookup"><span data-stu-id="d471c-239">Request-response example 2</span></span>

<span data-ttu-id="d471c-240">W poniższym przykładzie szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="d471c-240">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="d471c-241">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="d471c-241">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="d471c-242">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d471c-242">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="d471c-243">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="d471c-243">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="d471c-244">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="d471c-244">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 745,
            "listPrice": 0.085,
            "currency": "USD",
            "pretaxCharges": 63.33,
            "taxAmount": 6.34,
            "postTaxTotal": 69.67,
            "pretaxEffectiveRate": 0.08500671,
            "postTaxEffectiveRate": 0.09351677,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac000000",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Azure App Service",
            "serviceType": "Standard Plan",
            "resourceGuid": "505db374-df8a-44df-9d8c-13c14b61dee1",
            "resourceName": "S1",
            "region": "",
            "consumedQuantity": 745,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 Hour",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        },
        {
            "detailLineItemId": 1,
            "sku": "7UD-00001",
            "includedQuantity": 0,
            "overageQuantity": 0.000882,
            "listPrice": 0.0383,
            "currency": "USD",
            "pretaxCharges": 0,
            "taxAmount": 0,
            "postTaxTotal": 0,
            "pretaxEffectiveRate": 0,
            "postTaxEffectiveRate": 0,
            "chargeType": "Assess usage fee for current cycle",
            "invoiceLineItemType": "billing_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E87E26A",
            "partnerName": "TEST_TEST_Big foot consulting",
            "partnerBillableAccountId": "1010578050",
            "customerId": "65726577-c208-40fd-9735-8c85ac9cac68",
            "domainName": "600test.onmicrosoft.com",
            "customerCompanyName": "601 tests",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "87f4b92f-a490-485e-ad34-5b70cb000000",
            "subscriptionName": "Microsoft Azure",
            "subscriptionDescription": "Microsoft Azure",
            "billingCycleType": "Monthly",
            "orderId": "568297985427000000",
            "serviceName": "Storage",
            "serviceType": "Standard Page Blob",
            "resourceGuid": "d23a5753-ff85-4ddf-af28-8cc5cf2d3882",
            "resourceName": "LRS Data Stored",
            "region": "",
            "consumedQuantity": 0.000882,
            "chargeStartDate": "2019-08-02T00:00:00",
            "chargeEndDate": "2019-09-01T00:00:00",
            "unit": "1 GB/Month",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "UsageBasedLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=BillingLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-3"></a><span data-ttu-id="d471c-245">Przykład żądania — odpowiedź 3</span><span class="sxs-lookup"><span data-stu-id="d471c-245">Request-response example 3</span></span>

<span data-ttu-id="d471c-246">W poniższym przykładzie szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="d471c-246">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="d471c-247">**BillingProvider**: **Azure**</span><span class="sxs-lookup"><span data-stu-id="d471c-247">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="d471c-248">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="d471c-248">**InvoiceLineItemType**: **UsageLineItems**</span></span>

#### <a name="request-example-3"></a><span data-ttu-id="d471c-249">Przykład żądania 3</span><span class="sxs-lookup"><span data-stu-id="d471c-249">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="d471c-250">Przykład odpowiedzi 3</span><span class="sxs-lookup"><span data-stu-id="d471c-250">Response example 3</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 2,
    "items": [
        {
            "customerBillableAccount": "1439508127",
            "usageDate": "2019-08-05T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "9E9B71BA-3442-458B-B519-E1CCF72FBB54",
            "domainName": "test600.onmicrosoft.com",
            "customerCompanyName": "600 TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "F9BA6DA0-6DAC-4F88-B623-313C9B9C117A",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985577171353",
            "serviceName": "STORAGE",
            "serviceType": "STANDARD PAGE BLOB",
            "resourceGuid": "9CC63CF8-6593-410A-B0E7-26A4EF71E8B3",
            "resourceName": "DISK DELETE OPERATIONS",
            "region": "",
            "consumedQuantity": 2.9616,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "10K",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        },
        {
            "customerBillableAccount": "1307536861",
            "usageDate": "2019-08-10T00:00:00",
            "invoiceLineItemType": "usage_line_items",
            "partnerId": "1F5CCB06-8E36-4A74-A74C-FCAA9E000000",
            "partnerName": "TEST_TEST_BIG FOOT CONSULTING",
            "partnerBillableAccountId": "1010578050",
            "customerId": "EB53B7BD-267E-440E-B3C0-8F0B40000000",
            "domainName": "brandontest.onmicrosoft.com",
            "customerCompanyName": "BRANDON'S TEST",
            "mpnId": 4390934,
            "tier2MpnId": -1,
            "invoiceNumber": "1234000000",
            "subscriptionId": "62D22561-AB15-41E5-AD59-99025C000000",
            "subscriptionName": "MICROSOFT AZURE",
            "subscriptionDescription": "MICROSOFT AZURE",
            "billingCycleType": "MONTHLY",
            "orderId": "568297985605838583",
            "serviceName": "VIRTUAL MACHINES",
            "serviceType": "D/DS SERIES WINDOWS",
            "resourceGuid": "62C64B6C-4033-4E20-AB33-9E81271AC12A",
            "resourceName": "D1/DS1",
            "region": "US WEST",
            "consumedQuantity": 24,
            "chargeStartDate": "2019-08-05T00:00:00",
            "chargeEndDate": "2019-09-04T00:00:00",
            "unit": "1 HOUR",
            "billingProvider": "azure",
            "attributes": {
                "objectType": "DailyUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/1234000000/lineitems?provider=Azure&invoicelineitemtype=UsageLineItems&size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-4"></a><span data-ttu-id="d471c-251">Przykład żądania-odpowiedź 4</span><span class="sxs-lookup"><span data-stu-id="d471c-251">Request-response example 4</span></span>

<span data-ttu-id="d471c-252">W poniższym przykładzie szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="d471c-252">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="d471c-253">**BillingProvider**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="d471c-253">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="d471c-254">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d471c-254">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-4"></a><span data-ttu-id="d471c-255">Przykład żądania 4</span><span class="sxs-lookup"><span data-stu-id="d471c-255">Request example 4</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?size=2&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-4"></a><span data-ttu-id="d471c-256">Przykład odpowiedzi 4</span><span class="sxs-lookup"><span data-stu-id="d471c-256">Response example 4</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

 {
    "continuationToken": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7",
    "totalCount": 2,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 431.8,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 431.8,
            "taxTotal": 38.87,
            "totalForCustomer": 470.67,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234278124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0159369774,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "billingFrequency": "Monthly",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f4badc2",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38cbb28e",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "QDOx5ZN3YR9uYhm4M1MGQJ_0nievUOrx1",
            "orderDate": "2018-02-08T22:31:42.9397946Z",
            "productId": "productid",
            "skuId": "skuid",
            "availabilityId": "availabilityid",
            "productName": "TEST PRODUCT",
            "skuName": "TEST SKU TITLE",
            "chargeType": "New",
            "unitPrice": 26.35,
            "effectiveUnitPrice": 496.07,
            "unitType": "1 Hour",
            "quantity": 1,
            "subtotal": 26.35,
            "taxTotal": 2.37,
            "totalForCustomer": 28.72,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232ea904a",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234578124b8",
            "priceAdjustmentDescription": "[\"100.0% Tier 1 Discount\"]",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7"
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-5"></a><span data-ttu-id="d471c-257">Przykład żądania — odpowiedź 5</span><span class="sxs-lookup"><span data-stu-id="d471c-257">Request-response example 5</span></span>

<span data-ttu-id="d471c-258">W poniższym przykładzie jest stronicowanie przy użyciu tokenu kontynuacji.</span><span class="sxs-lookup"><span data-stu-id="d471c-258">In the following example, there is paging using a continuation token.</span></span> <span data-ttu-id="d471c-259">Szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="d471c-259">The details are as follows:</span></span>

- <span data-ttu-id="d471c-260">**BillingProvider**: **jednorazowej**</span><span class="sxs-lookup"><span data-stu-id="d471c-260">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="d471c-261">**InvoiceLineItemType**: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="d471c-261">**InvoiceLineItemType**: **BillingLineItems**</span></span>
- <span data-ttu-id="d471c-262">**SeekOperation**: **dalej**</span><span class="sxs-lookup"><span data-stu-id="d471c-262">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-5"></a><span data-ttu-id="d471c-263">Przykład żądania 5</span><span class="sxs-lookup"><span data-stu-id="d471c-263">Request example 5</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/G000024135/lineitems/OneTime/BillingLineItems?seekOperation=Next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-5"></a><span data-ttu-id="d471c-264">Przykład odpowiedzi 5</span><span class="sxs-lookup"><span data-stu-id="d471c-264">Response example 5</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda03fe54
MS-RequestId: 1eb2ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Thu, 07 Sep 2017 23:31:09 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "6480d686-cfb4-424d-a945-6b9b9f000000",
            "customerId": "org:9060d13d-c5ed-482e-b059-a15a38000000",
            "customerName": "recipientCustomerName",
            "customerDomainName": "recipientCustomerDomain",
            "invoiceNumber": "1234000000",
            "quoteId": "abcd12345678",
            "mpnId": "4870137",
            "resellerMpnId": 0,
            "orderId": "NeqT31Kziwf8gkCXM9YQToWTqU-9Jbm81",
            "orderDate": "2018-02-08T22:31:47.1751688Z",
            "productId": "DZH318Z0BQ3P",
            "skuId": "001F",
            "availabilityId": "DZH318Z0DR0H",
            "productName": "Reserved VM Instance, Standard_D1, AP East, 3 years",
            "skuName": "D Series",
            "chargeType": "New",
            "unitPrice": 1447,
            "effectiveUnitPrice": 496.07,
            "unitType": "Seats",
            "quantity": 1,
            "subtotal": 1447,
            "taxTotal": 130.24,
            "totalForCustomer": 1577.24,
            "currency": "USD",
            "providerName": "Test Networks Inc",
            "providerId": "12343810",
            "subscriptionDescription": "",
            "subscriptionId": "281e26fe-9ce7-415b-911c-f39232000000",
            "subscriptionStartDate": "2019-01-03T19:53:55.1292512+00:00",
            "subscriptionEndDate": "2019-02-02T19:53:55.1292512+00:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "1234568124b8",
            "priceAdjustmentDescription": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-09-30T23:59:59Z",
            "billableQuantity": 0.0130687981,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "",
            "billingFrequency": "Monthly",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/G000024135/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
