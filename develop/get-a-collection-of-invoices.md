---
title: Pobieranie kolekcji faktur
description: Jak pobrać kolekcję faktur partnera.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 7698d85df3341ae4cbff0377bd0a1bb47cd36740
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906445"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="c7062-103">Pobieranie kolekcji faktur</span><span class="sxs-lookup"><span data-stu-id="c7062-103">Get a collection of invoices</span></span>

<span data-ttu-id="c7062-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c7062-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c7062-105">Jak pobrać kolekcję faktur partnera.</span><span class="sxs-lookup"><span data-stu-id="c7062-105">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7062-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7062-106">Prerequisites</span></span>

- <span data-ttu-id="c7062-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c7062-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c7062-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7062-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c7062-109">C\#</span><span class="sxs-lookup"><span data-stu-id="c7062-109">C\#</span></span>

<span data-ttu-id="c7062-110">Aby uzyskać kolekcję wszystkich dostępnych faktur, użyj właściwości [**Invoices,**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) aby uzyskać interfejs do operacji na fakturze, a następnie wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) aby pobrać kolekcję.</span><span class="sxs-lookup"><span data-stu-id="c7062-110">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="c7062-111">Aby uzyskać stronicowane kolekcje faktur, najpierw wywołaj metodę [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) i przekaż jej rozmiar strony, aby utworzyć [**obiekt IQuery.**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery)</span><span class="sxs-lookup"><span data-stu-id="c7062-111">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="c7062-112">Następnie użyj właściwości [**Invoices,**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) aby uzyskać interfejs do operacji na fakturze, a następnie przekaż obiekt IQuery do metody [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) lub [**QueryAsync,**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) aby wysłać żądanie i uzyskać pierwszą stronę.</span><span class="sxs-lookup"><span data-stu-id="c7062-112">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="c7062-113">Następnie użyj właściwości [**Enumerators,**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) aby uzyskać interfejs do kolekcji obsługiwanych wyliczeń kolekcji zasobów, a następnie wywołaj właściwość [**Invoices.Create,**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) aby utworzyć moduł wyliczający do przechodzenia przez kolekcję faktur.</span><span class="sxs-lookup"><span data-stu-id="c7062-113">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="c7062-114">Na koniec użyj modułu wyliczania, aby pobrać i pracować z każdą stroną faktur, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="c7062-114">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="c7062-115">Każde wywołanie metody [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) wysyła żądanie dotyczące następnej strony faktur na podstawie rozmiaru strony.</span><span class="sxs-lookup"><span data-stu-id="c7062-115">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

<span data-ttu-id="c7062-116">Nieco inny przykład można znaleźć w teście **Przykład:** [Aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c7062-116">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c7062-117">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="c7062-117">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="c7062-118">Ten sam interfejs API jest używany dla wszystkich nowoczesnych zakupów komercyjnych, a także licencji 145p i Office komercyjnych.</span><span class="sxs-lookup"><span data-stu-id="c7062-118">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="c7062-119">Rozmiar i przesunięcie są rozważane tylko w przypadku starszych faktur.</span><span class="sxs-lookup"><span data-stu-id="c7062-119">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="c7062-120">W przypadku wszystkich nowoczesnych zakupów komercyjnych przesunięcie & stronicowania zostanie zignorowane.</span><span class="sxs-lookup"><span data-stu-id="c7062-120">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c7062-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c7062-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c7062-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c7062-122">Request syntax</span></span>

| <span data-ttu-id="c7062-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="c7062-123">Method</span></span>  | <span data-ttu-id="c7062-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c7062-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c7062-125">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c7062-125">**GET**</span></span> | <span data-ttu-id="c7062-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c7062-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="c7062-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="c7062-127">URI parameters</span></span>

<span data-ttu-id="c7062-128">Podczas tworzenia żądania użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="c7062-128">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="c7062-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c7062-129">Name</span></span>   | <span data-ttu-id="c7062-130">Typ</span><span class="sxs-lookup"><span data-stu-id="c7062-130">Type</span></span> | <span data-ttu-id="c7062-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c7062-131">Required</span></span> | <span data-ttu-id="c7062-132">Opis</span><span class="sxs-lookup"><span data-stu-id="c7062-132">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="c7062-133">size</span><span class="sxs-lookup"><span data-stu-id="c7062-133">size</span></span>   | <span data-ttu-id="c7062-134">int</span><span class="sxs-lookup"><span data-stu-id="c7062-134">int</span></span>  | <span data-ttu-id="c7062-135">Nie</span><span class="sxs-lookup"><span data-stu-id="c7062-135">No</span></span>       | <span data-ttu-id="c7062-136">Liczba zasobów faktury do zwrócenia w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c7062-136">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="c7062-137">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c7062-137">This parameter is optional.</span></span> |
| <span data-ttu-id="c7062-138">przesunięcie</span><span class="sxs-lookup"><span data-stu-id="c7062-138">offset</span></span> | <span data-ttu-id="c7062-139">int</span><span class="sxs-lookup"><span data-stu-id="c7062-139">int</span></span>  | <span data-ttu-id="c7062-140">Nie</span><span class="sxs-lookup"><span data-stu-id="c7062-140">No</span></span>       | <span data-ttu-id="c7062-141">Od zera indeks pierwszej faktury do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="c7062-141">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="c7062-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c7062-142">Request headers</span></span>

<span data-ttu-id="c7062-143">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c7062-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c7062-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c7062-144">Request body</span></span>

<span data-ttu-id="c7062-145">Brak</span><span class="sxs-lookup"><span data-stu-id="c7062-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="c7062-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c7062-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c7062-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c7062-147">REST response</span></span>

<span data-ttu-id="c7062-148">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [faktury.](invoice-resources.md#invoice)</span><span class="sxs-lookup"><span data-stu-id="c7062-148">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c7062-149">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c7062-149">Response success and error codes</span></span>

<span data-ttu-id="c7062-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c7062-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c7062-151">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c7062-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c7062-152">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c7062-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c7062-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c7062-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
