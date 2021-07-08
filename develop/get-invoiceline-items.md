---
title: Pobieranie elementów wiersza faktury
description: Kolekcję szczegółów pozycji faktury (zamkniętego elementu wiersza rozliczeniowego) dla określonej faktury można uzyskać przy użyciu interfejsów API Partner Center.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 944dddef64ec980d92c292a7f5b9f5eb4e7cecb6
ms.sourcegitcommit: 15c6cfe72284cf5d4ea3535120e83e473c33f5ec
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/22/2021
ms.locfileid: "112443176"
---
# <a name="get-invoice-line-items"></a><span data-ttu-id="3d04f-103">Pobieranie elementów wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="3d04f-103">Get invoice line items</span></span>

<span data-ttu-id="3d04f-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3d04f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3d04f-105">Następujące metody umożliwia pobieranie szczegółów kolekcji pozycji faktur (nazywanych również zamkniętymi pozycjami rozliczeniowymi) dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-105">You can use the following methods to get collection details for of invoice line items (also known as closed billing line items) for a specified invoice.</span></span>

<span data-ttu-id="3d04f-106">*Z wyjątkiem poprawek błędów ten interfejs API nie jest już aktualizowany.*</span><span class="sxs-lookup"><span data-stu-id="3d04f-106">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="3d04f-107">Należy zaktualizować aplikacje w celu wywołania interfejsu API **onetime** zamiast witryny **Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="3d04f-107">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="3d04f-108">**Jednogodzinny interfejs** API zapewnia dodatkowe funkcje i będzie nadal aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="3d04f-108">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="3d04f-109">Należy używać funkcji **onetime do** wykonywania zapytań o wszystkie pozycje użycia komercyjnego zamiast elementów **platformy handlowej.**</span><span class="sxs-lookup"><span data-stu-id="3d04f-109">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="3d04f-110">Możesz też użyć linków w wywołaniu linków do oszacowania.</span><span class="sxs-lookup"><span data-stu-id="3d04f-110">Or, you can follow the links in the estimate links call.</span></span>

<span data-ttu-id="3d04f-111">Ten interfejs API  obsługuje również typy dostawców subskrypcji platformy **Azure** i pakietu **Office** dla platformy Microsoft Azure (MS-AZR-0145P) i ofert Office, dzięki czemu funkcja interfejsu API jest zgodna z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="3d04f-111">This API also supports the **provider** types of **azure** and **office** for Microsoft Azure (MS-AZR-0145P) subscriptions and Office offers, which makes the API feature backward compatible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d04f-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d04f-112">Prerequisites</span></span>

- <span data-ttu-id="3d04f-113">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3d04f-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3d04f-114">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3d04f-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3d04f-115">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-115">An invoice identifier.</span></span> <span data-ttu-id="3d04f-116">Pozwala to zidentyfikować fakturę, dla której mają zostać pobrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="3d04f-116">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="3d04f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="3d04f-117">C\#</span></span>

<span data-ttu-id="3d04f-118">Aby uzyskać pozycje dla określonej faktury:</span><span class="sxs-lookup"><span data-stu-id="3d04f-118">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="3d04f-119">Wywołaj [**metodę ById,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) aby uzyskać interfejs do operacji na fakturze dla określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-119">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="3d04f-120">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) aby pobrać obiekt faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="3d04f-121">Obiekt faktury zawiera wszystkie informacje dotyczące określonej faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-121">The invoice object contains all of the information for the specified invoice.</span></span>
3. <span data-ttu-id="3d04f-122">Użyj właściwości [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) obiektu invoice, aby uzyskać dostęp do kolekcji obiektów [**InvoiceDetail,**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) z których każdy zawiera obiekt [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) i [**typ InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span><span class="sxs-lookup"><span data-stu-id="3d04f-122">Use the invoice object's [**InvoiceDetails**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoice.invoicedetails) property to get access to a collection of [**InvoiceDetail**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail) objects, each of which contains a [**BillingProvider**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.billingprovider) and an [**InvoiceLineItemType**](/dotnet/api/microsoft.store.partnercenter.models.invoices.invoicedetail.invoicelineitemtype).</span></span> <span data-ttu-id="3d04f-123">**BillingProvider** identyfikuje źródło szczegółowych informacji o fakturze (takich jak **Office,** **Azure,** **OneTime**), a **typ InvoiceLineItemType** określa typ (na przykład **BillingLineItem).**</span><span class="sxs-lookup"><span data-stu-id="3d04f-123">The **BillingProvider** identifies the source of the invoice detail information (such as **Office**, **Azure**, **OneTime**), and the **InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="3d04f-124">Poniższy przykładowy kod używa pętli **foreach** do przetwarzania kolekcji **InvoiceDetails.**</span><span class="sxs-lookup"><span data-stu-id="3d04f-124">The following example code uses a **foreach** loop to process the **InvoiceDetails** collection.</span></span> <span data-ttu-id="3d04f-125">Dla każdego wystąpienia **InvoiceDetail** pobierana jest oddzielna kolekcja elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="3d04f-125">A separate collection of line items is retrieved for each **InvoiceDetail** instance.</span></span>

<span data-ttu-id="3d04f-126">Aby uzyskać kolekcję elementów wiersza, które odpowiadają **wystąpieniu InvoiceDetail:**</span><span class="sxs-lookup"><span data-stu-id="3d04f-126">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="3d04f-127">Przekaż wartości **BillingProvider i** **InvoiceLineItemType** wystąpienia do metody [**By.**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by)</span><span class="sxs-lookup"><span data-stu-id="3d04f-127">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="3d04f-128">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) aby pobrać skojarzone elementy wiersza.</span><span class="sxs-lookup"><span data-stu-id="3d04f-128">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicelineitemcollection.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="3d04f-129">Utwórz moduł wyliczający, aby przejść przez kolekcję, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3d04f-129">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="3d04f-130">Podobny przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="3d04f-130">For a similar example, see the following:</span></span>

- <span data-ttu-id="3d04f-131">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3d04f-131">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3d04f-132">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="3d04f-132">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="3d04f-133">Klasa: **GetInvoiceLineItems.cs**</span><span class="sxs-lookup"><span data-stu-id="3d04f-133">Class: **GetInvoiceLineItems.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3d04f-134">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3d04f-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3d04f-135">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-135">Request syntax</span></span>

<span data-ttu-id="3d04f-136">Zamieć żądanie przy użyciu odpowiedniej składni dla dostawcy rozliczeń w swoim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="3d04f-136">Make your request using the appropriate syntax for the billing provider in your scenario.</span></span>

#### <a name="office"></a><span data-ttu-id="3d04f-137">Office</span><span class="sxs-lookup"><span data-stu-id="3d04f-137">Office</span></span>

<span data-ttu-id="3d04f-138">Następująca składnia ma zastosowanie, gdy dostawca rozliczeń jest **Office**.</span><span class="sxs-lookup"><span data-stu-id="3d04f-138">The following syntax applies when the billing provider is **Office**.</span></span>

| <span data-ttu-id="3d04f-139">Metoda</span><span class="sxs-lookup"><span data-stu-id="3d04f-139">Method</span></span>  | <span data-ttu-id="3d04f-140">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-140">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d04f-141">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d04f-141">**GET**</span></span> | <span data-ttu-id="3d04f-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator-faktury}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=office&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>                               |

#### <a name="microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="3d04f-143">Microsoft Azure subskrypcji (MS-AZR-0145P)</span><span class="sxs-lookup"><span data-stu-id="3d04f-143">Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="3d04f-144">Poniższe składnie mają zastosowanie, gdy dostawca rozliczeń ma subskrypcję Microsoft Azure (MS-AZR-0145P).</span><span class="sxs-lookup"><span data-stu-id="3d04f-144">The following syntaxes apply when the billing provider has a Microsoft Azure (MS-AZR-0145P) subscription.</span></span>

| <span data-ttu-id="3d04f-145">Metoda</span><span class="sxs-lookup"><span data-stu-id="3d04f-145">Method</span></span>  | <span data-ttu-id="3d04f-146">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-146">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d04f-147">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d04f-147">**GET**</span></span> | <span data-ttu-id="3d04f-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator faktury}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=billinglineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |
| <span data-ttu-id="3d04f-149">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d04f-149">**GET**</span></span> | <span data-ttu-id="3d04f-150">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-150">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=azure&invoicelineitemtype=usagelineitems&size={size}&offset={offset} HTTP/1.1</span></span>  |

##### <a name="onetime"></a><span data-ttu-id="3d04f-151">OneTime</span><span class="sxs-lookup"><span data-stu-id="3d04f-151">OneTime</span></span>

<span data-ttu-id="3d04f-152">Następujące składnie mają zastosowanie, gdy dostawca rozliczeń to **OneTime**.</span><span class="sxs-lookup"><span data-stu-id="3d04f-152">The following syntaxes apply when the billing provider is **OneTime**.</span></span> <span data-ttu-id="3d04f-153">Obejmuje to opłaty za rezerwacje platformy Azure, oprogramowanie, plany platformy Azure i produkty platformy handlowej.</span><span class="sxs-lookup"><span data-stu-id="3d04f-153">This includes charges for Azure reservations, software, Azure plans, and commercial marketplace products.</span></span>

| <span data-ttu-id="3d04f-154">Metoda</span><span class="sxs-lookup"><span data-stu-id="3d04f-154">Method</span></span>  | <span data-ttu-id="3d04f-155">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-155">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d04f-156">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d04f-156">**GET**</span></span> | <span data-ttu-id="3d04f-157">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator-faktury}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-157">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="3d04f-158">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3d04f-158">**GET**</span></span> | <span data-ttu-id="3d04f-159">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator-faktury}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="3d04f-159">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/onetime/billinglineitems&size={size}?seekOperation=Next</span></span>                           |

#### <a name="previous-syntaxes"></a><span data-ttu-id="3d04f-160">Poprzednie składnie</span><span class="sxs-lookup"><span data-stu-id="3d04f-160">Previous syntaxes</span></span>

<span data-ttu-id="3d04f-161">Jeśli używasz następujących składni, upewnij się, że używasz odpowiedniej składni dla twojego przypadku użycia.</span><span class="sxs-lookup"><span data-stu-id="3d04f-161">If you are using the following syntaxes, be sure to use the appropriate syntax for your use case.</span></span>

<span data-ttu-id="3d04f-162">*Z wyjątkiem poprawek błędów ten interfejs API nie jest już aktualizowany.*</span><span class="sxs-lookup"><span data-stu-id="3d04f-162">*Except for bug fixes, this API is no longer being updated.*</span></span> <span data-ttu-id="3d04f-163">Należy zaktualizować aplikacje w celu wywołania interfejsu API **onetime** zamiast witryny **Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="3d04f-163">You should update your applications to call the **onetime** API instead of **marketplace**.</span></span> <span data-ttu-id="3d04f-164">**Jednogodzinny interfejs** API zapewnia dodatkowe funkcje i będzie nadal aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="3d04f-164">The **onetime** API provides additional functionality, and will continue to be updated.</span></span>

<span data-ttu-id="3d04f-165">Należy używać funkcji **onetime do** wykonywania zapytań o wszystkie pozycje użycia komercyjnego zamiast elementów **platformy handlowej.**</span><span class="sxs-lookup"><span data-stu-id="3d04f-165">You should use **onetime** to query all commercial consumption line items instead of **marketplace**.</span></span> <span data-ttu-id="3d04f-166">Możesz też użyć linków w wywołaniu linków do oszacowania.</span><span class="sxs-lookup"><span data-stu-id="3d04f-166">Or, you can follow the links in the estimate links call.</span></span>

| <span data-ttu-id="3d04f-167">Metoda</span><span class="sxs-lookup"><span data-stu-id="3d04f-167">Method</span></span> | <span data-ttu-id="3d04f-168">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-168">Request URI</span></span> | <span data-ttu-id="3d04f-169">Opis przypadku użycia składni</span><span class="sxs-lookup"><span data-stu-id="3d04f-169">Description of syntax use case</span></span> |
| ------ | ----------- | -------------------------------- |
| <span data-ttu-id="3d04f-170">GET</span><span class="sxs-lookup"><span data-stu-id="3d04f-170">GET</span></span> | <span data-ttu-id="3d04f-171">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator faktury}/lineitems/{dostawca-rozliczeń}/{typ-elementu-wiersza-faktury} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-171">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type} HTTP/1.1</span></span>                              | <span data-ttu-id="3d04f-172">Ta składnia umożliwia zwrócenie pełnej listy wszystkich pozycji dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-172">You can use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="3d04f-173">GET</span><span class="sxs-lookup"><span data-stu-id="3d04f-173">GET</span></span> | <span data-ttu-id="3d04f-174">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator faktury}/lineitems/{dostawca-rozliczeń}/{typ-elementu-wiersza-faktury}?size={rozmiar}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3d04f-174">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/{billing-provider}/{invoice-line-item-type}?size={size}&offset={offset} HTTP/1.1</span></span>  | <span data-ttu-id="3d04f-175">W przypadku dużych faktur można użyć tej składni z określonym rozmiarem i przesunięciem 0 w celu zwrócenia stronicowej listy elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="3d04f-175">For large invoices, you can use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="3d04f-176">GET</span><span class="sxs-lookup"><span data-stu-id="3d04f-176">GET</span></span> | <span data-ttu-id="3d04f-177">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="3d04f-177">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems/OneTime/{invoice-line-item-type}?seekOperation=Next</span></span>                               | <span data-ttu-id="3d04f-178">Tej składni można użyć dla faktury z wartością dostawcy rozliczeń **OneTime** i ustawić **wartość seekOperation** na **Dalej,** aby uzyskać następną stronę pozycji faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-178">You can use this syntax for an invoice with a billing-provider value of **OneTime** and set **seekOperation** to **Next** to get the next page of invoice line items.</span></span> |

##### <a name="uri-parameters"></a><span data-ttu-id="3d04f-179">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="3d04f-179">URI parameters</span></span>

<span data-ttu-id="3d04f-180">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="3d04f-180">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="3d04f-181">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3d04f-181">Name</span></span>                   | <span data-ttu-id="3d04f-182">Typ</span><span class="sxs-lookup"><span data-stu-id="3d04f-182">Type</span></span>   | <span data-ttu-id="3d04f-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3d04f-183">Required</span></span> | <span data-ttu-id="3d04f-184">Opis</span><span class="sxs-lookup"><span data-stu-id="3d04f-184">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="3d04f-185">invoice-id</span><span class="sxs-lookup"><span data-stu-id="3d04f-185">invoice-id</span></span>             | <span data-ttu-id="3d04f-186">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d04f-186">string</span></span> | <span data-ttu-id="3d04f-187">Tak</span><span class="sxs-lookup"><span data-stu-id="3d04f-187">Yes</span></span>      | <span data-ttu-id="3d04f-188">Ciąg, który identyfikuje fakturę.</span><span class="sxs-lookup"><span data-stu-id="3d04f-188">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="3d04f-189">dostawca rozliczeń</span><span class="sxs-lookup"><span data-stu-id="3d04f-189">billing-provider</span></span>       | <span data-ttu-id="3d04f-190">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d04f-190">string</span></span> | <span data-ttu-id="3d04f-191">Tak</span><span class="sxs-lookup"><span data-stu-id="3d04f-191">Yes</span></span>      | <span data-ttu-id="3d04f-192">Dostawca rozliczeń: "Office", "Azure", "OneTime".</span><span class="sxs-lookup"><span data-stu-id="3d04f-192">The billing provider: "Office", "Azure", "OneTime".</span></span> <span data-ttu-id="3d04f-193">W starszej wersji mamy oddzielne modele danych dla Office & platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d04f-193">In the legacy, we have separate data models for Office & Azure transactions.</span></span> <span data-ttu-id="3d04f-194">Jednak nowoczesna ma jeden model danych dla wszystkich transakcji przefiltrowanych za pomocą wartości "OneTime".</span><span class="sxs-lookup"><span data-stu-id="3d04f-194">However, the modern has one single data model across all transactions filtered through the "OneTime" value.</span></span>            |
| <span data-ttu-id="3d04f-195">typ-elementu-wiersza faktury</span><span class="sxs-lookup"><span data-stu-id="3d04f-195">invoice-line-item-type</span></span> | <span data-ttu-id="3d04f-196">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d04f-196">string</span></span> | <span data-ttu-id="3d04f-197">Tak</span><span class="sxs-lookup"><span data-stu-id="3d04f-197">Yes</span></span>      | <span data-ttu-id="3d04f-198">Typ szczegółów faktury: "BillingLineItems", "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="3d04f-198">The type of invoice detail: "BillingLineItems", "UsageLineItems".</span></span> |
| <span data-ttu-id="3d04f-199">size</span><span class="sxs-lookup"><span data-stu-id="3d04f-199">size</span></span>                   | <span data-ttu-id="3d04f-200">liczba</span><span class="sxs-lookup"><span data-stu-id="3d04f-200">number</span></span> | <span data-ttu-id="3d04f-201">Nie</span><span class="sxs-lookup"><span data-stu-id="3d04f-201">No</span></span>       | <span data-ttu-id="3d04f-202">Maksymalna liczba elementów do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="3d04f-202">The maximum number of items to return.</span></span> <span data-ttu-id="3d04f-203">Domyślny maksymalny rozmiar = 2000</span><span class="sxs-lookup"><span data-stu-id="3d04f-203">Default max size = 2000</span></span>    |
| <span data-ttu-id="3d04f-204">przesunięcie</span><span class="sxs-lookup"><span data-stu-id="3d04f-204">offset</span></span>                 | <span data-ttu-id="3d04f-205">liczba</span><span class="sxs-lookup"><span data-stu-id="3d04f-205">number</span></span> | <span data-ttu-id="3d04f-206">Nie</span><span class="sxs-lookup"><span data-stu-id="3d04f-206">No</span></span>       | <span data-ttu-id="3d04f-207">Indeks pierwszego wiersza, który ma być zwracany od zera.</span><span class="sxs-lookup"><span data-stu-id="3d04f-207">The zero-based index of the first line item to return.</span></span>            |
| <span data-ttu-id="3d04f-208">seekOperation</span><span class="sxs-lookup"><span data-stu-id="3d04f-208">seekOperation</span></span>          | <span data-ttu-id="3d04f-209">ciąg</span><span class="sxs-lookup"><span data-stu-id="3d04f-209">string</span></span> | <span data-ttu-id="3d04f-210">Nie</span><span class="sxs-lookup"><span data-stu-id="3d04f-210">No</span></span>       | <span data-ttu-id="3d04f-211">Jeśli **dostawca rozliczeń ma** wartość **OneTime,** ustaw **wartość seekOperation** równą **Dalej,** aby pobrać następną stronę pozycji faktury.</span><span class="sxs-lookup"><span data-stu-id="3d04f-211">If **billing-provider** equals **OneTime**, set **seekOperation** equal to **Next** to get the next page of invoice line items.</span></span> |
| <span data-ttu-id="3d04f-212">hasPartnerEarnedCredit</span><span class="sxs-lookup"><span data-stu-id="3d04f-212">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="3d04f-213">bool</span><span class="sxs-lookup"><span data-stu-id="3d04f-213">bool</span></span> | <span data-ttu-id="3d04f-214">Nie</span><span class="sxs-lookup"><span data-stu-id="3d04f-214">No</span></span> | <span data-ttu-id="3d04f-215">Wartość wskazująca, czy zwrócić pozycje z zastosowanymi środków uzyskane przez partnera.</span><span class="sxs-lookup"><span data-stu-id="3d04f-215">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="3d04f-216">Uwaga: ten parametr będzie stosowany tylko wtedy, gdy typ dostawcy rozliczeń to OneTime, a InvoiceLineItemType to UsageLineItems.</span><span class="sxs-lookup"><span data-stu-id="3d04f-216">Note: this parameter will be only applied when billing provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3d04f-217">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3d04f-217">Request headers</span></span>

<span data-ttu-id="3d04f-218">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3d04f-218">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3d04f-219">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3d04f-219">Request body</span></span>

<span data-ttu-id="3d04f-220">Brak.</span><span class="sxs-lookup"><span data-stu-id="3d04f-220">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="3d04f-221">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3d04f-221">REST response</span></span>

<span data-ttu-id="3d04f-222">Jeśli to się powiedzie, odpowiedź zawiera kolekcję szczegółów elementu wiersza.</span><span class="sxs-lookup"><span data-stu-id="3d04f-222">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="3d04f-223">*W przypadku elementu wiersza **ChargeType** wartość **Zakup** jest mapowana na **nowy**. Wartość Zwrot **jest** mapowana na **anuluj**.*</span><span class="sxs-lookup"><span data-stu-id="3d04f-223">*For the line item **ChargeType**, the value **Purchase** is mapped to **New**. The value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3d04f-224">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3d04f-224">Response success and error codes</span></span>

<span data-ttu-id="3d04f-225">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="3d04f-225">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3d04f-226">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3d04f-226">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3d04f-227">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3d04f-227">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="rest-request-response-examples"></a><span data-ttu-id="3d04f-228">Przykłady żądań i odpowiedzi REST</span><span class="sxs-lookup"><span data-stu-id="3d04f-228">REST request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="3d04f-229">Przykład żądania i odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="3d04f-229">Request-response example 1</span></span>

<span data-ttu-id="3d04f-230">W tym przykładzie szczegółowe informacje są następujące:</span><span class="sxs-lookup"><span data-stu-id="3d04f-230">In this example, the details are as follows:</span></span>

- <span data-ttu-id="3d04f-231">**BillingProvider**: **Office**</span><span class="sxs-lookup"><span data-stu-id="3d04f-231">**BillingProvider**: **Office**</span></span>
- <span data-ttu-id="3d04f-232">**InvoiceLineItemType:** **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3d04f-232">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="3d04f-233">Przykład żądania 1</span><span class="sxs-lookup"><span data-stu-id="3d04f-233">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="3d04f-234">Przykład odpowiedzi 1</span><span class="sxs-lookup"><span data-stu-id="3d04f-234">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="3d04f-235">Przykład żądania i odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="3d04f-235">Request-response example 2</span></span>

<span data-ttu-id="3d04f-236">W poniższym przykładzie szczegółowe informacje są następujące:</span><span class="sxs-lookup"><span data-stu-id="3d04f-236">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="3d04f-237">**BillingProvider:** **Azure**</span><span class="sxs-lookup"><span data-stu-id="3d04f-237">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="3d04f-238">**InvoiceLineItemType:** **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3d04f-238">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="3d04f-239">Przykład żądania 2</span><span class="sxs-lookup"><span data-stu-id="3d04f-239">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="3d04f-240">Przykład odpowiedzi 2</span><span class="sxs-lookup"><span data-stu-id="3d04f-240">Response example 2</span></span>

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

### <a name="request-response-example-3"></a><span data-ttu-id="3d04f-241">Przykład żądania i odpowiedzi 3</span><span class="sxs-lookup"><span data-stu-id="3d04f-241">Request-response example 3</span></span>

<span data-ttu-id="3d04f-242">W poniższym przykładzie szczegółowe informacje są następujące:</span><span class="sxs-lookup"><span data-stu-id="3d04f-242">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="3d04f-243">**BillingProvider:** **Azure**</span><span class="sxs-lookup"><span data-stu-id="3d04f-243">**BillingProvider**: **Azure**</span></span>
- <span data-ttu-id="3d04f-244">**InvoiceLineItemType**: **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="3d04f-244">**InvoiceLineItemType**: **UsageLineItems**</span></span>

#### <a name="request-example-3"></a><span data-ttu-id="3d04f-245">Przykład żądania 3</span><span class="sxs-lookup"><span data-stu-id="3d04f-245">Request example 3</span></span>

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

#### <a name="response-example-3"></a><span data-ttu-id="3d04f-246">Przykład odpowiedzi 3</span><span class="sxs-lookup"><span data-stu-id="3d04f-246">Response example 3</span></span>

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

### <a name="request-response-example-4"></a><span data-ttu-id="3d04f-247">Przykład żądania i odpowiedzi 4</span><span class="sxs-lookup"><span data-stu-id="3d04f-247">Request-response example 4</span></span>

<span data-ttu-id="3d04f-248">W poniższym przykładzie szczegółowe informacje są następujące:</span><span class="sxs-lookup"><span data-stu-id="3d04f-248">In the following example, the details are as follows:</span></span>

- <span data-ttu-id="3d04f-249">**BillingProvider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="3d04f-249">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="3d04f-250">**InvoiceLineItemType:** **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3d04f-250">**InvoiceLineItemType**: **BillingLineItems**</span></span>

#### <a name="request-example-4"></a><span data-ttu-id="3d04f-251">Przykład żądania 4</span><span class="sxs-lookup"><span data-stu-id="3d04f-251">Request example 4</span></span>

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

#### <a name="response-example-4"></a><span data-ttu-id="3d04f-252">Przykład odpowiedzi 4</span><span class="sxs-lookup"><span data-stu-id="3d04f-252">Response example 4</span></span>

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
    {
    {
    "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "G000773581",
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
            "invoiceNumber": "G000773581",
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
            "taxTotal": "73",
            "totalForCustomer": "793",
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
            "invoiceNumber": "T000773581",
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
            "uri": "/invoices/G000773581/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/G000773581/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2?seekOperation=Next",
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

### <a name="request-response-example-5"></a><span data-ttu-id="3d04f-253">Przykład żądania i odpowiedzi 5</span><span class="sxs-lookup"><span data-stu-id="3d04f-253">Request-response example 5</span></span>

<span data-ttu-id="3d04f-254">W poniższym przykładzie jest stronicowanie przy użyciu tokenu kontynuacji.</span><span class="sxs-lookup"><span data-stu-id="3d04f-254">In the following example, there is paging using a continuation token.</span></span> <span data-ttu-id="3d04f-255">Szczegóły są następujące:</span><span class="sxs-lookup"><span data-stu-id="3d04f-255">The details are as follows:</span></span>

- <span data-ttu-id="3d04f-256">**BillingProvider:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="3d04f-256">**BillingProvider**: **OneTime**</span></span>
- <span data-ttu-id="3d04f-257">**InvoiceLineItemType:** **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="3d04f-257">**InvoiceLineItemType**: **BillingLineItems**</span></span>
- <span data-ttu-id="3d04f-258">**SeekOperation:** **Dalej**</span><span class="sxs-lookup"><span data-stu-id="3d04f-258">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-5"></a><span data-ttu-id="3d04f-259">Przykład żądania 5</span><span class="sxs-lookup"><span data-stu-id="3d04f-259">Request example 5</span></span>

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

#### <a name="response-example-5"></a><span data-ttu-id="3d04f-260">Przykład odpowiedzi 5</span><span class="sxs-lookup"><span data-stu-id="3d04f-260">Response example 5</span></span>

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
    {
    {
    "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "G000773581",
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
            "invoiceNumber": "G000773581",
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
            "taxTotal": "73",
            "totalForCustomer": "793",
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
            "invoiceNumber": "T000773581",
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
            "uri": "/invoices/G000773581/lineitems?provider=OneTime&nvoicelineitemtype=BillingLineItems&size=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}

```
