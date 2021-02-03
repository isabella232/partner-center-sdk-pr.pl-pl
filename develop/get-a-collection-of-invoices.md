---
title: Pobieranie kolekcji faktur
description: Jak pobrać kolekcję faktur partnera.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768066"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="b4b70-103">Pobieranie kolekcji faktur</span><span class="sxs-lookup"><span data-stu-id="b4b70-103">Get a collection of invoices</span></span>

<span data-ttu-id="b4b70-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="b4b70-104">**Applies To**</span></span>

- <span data-ttu-id="b4b70-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="b4b70-105">Partner Center</span></span>
- <span data-ttu-id="b4b70-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="b4b70-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b4b70-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="b4b70-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b4b70-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b4b70-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b4b70-109">Jak pobrać kolekcję faktur partnera.</span><span class="sxs-lookup"><span data-stu-id="b4b70-109">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4b70-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4b70-110">Prerequisites</span></span>

- <span data-ttu-id="b4b70-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b4b70-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b4b70-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b4b70-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="b4b70-113">C\#</span><span class="sxs-lookup"><span data-stu-id="b4b70-113">C\#</span></span>

<span data-ttu-id="b4b70-114">Aby uzyskać kolekcję wszystkich dostępnych faktur, [**Użyj właściwości Invoices, aby**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) uzyskać interfejs do fakturowania operacji, a następnie Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) w celu pobrania kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b4b70-114">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="b4b70-115">Aby uzyskać zebraną kolekcję faktur, najpierw Wywołaj metodę [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) i przekaż ją do rozmiaru strony, aby utworzyć obiekt [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) .</span><span class="sxs-lookup"><span data-stu-id="b4b70-115">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="b4b70-116">Następnie [**Użyj właściwości Invoices, aby**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) uzyskać interfejs do fakturowania operacji, a następnie przekaż obiekt IQuery do [**zapytania**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) lub metody [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) w celu wysłania żądania i pobrania pierwszej strony.</span><span class="sxs-lookup"><span data-stu-id="b4b70-116">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="b4b70-117">Następnie użyj właściwości [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) , aby uzyskać interfejs kolekcji obsługiwanych modułów wyliczających zbieranie zasobów, a następnie Wywołaj [**faktury. Utwórz**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) , aby utworzyć moduł wyliczający do przechodzenia z kolekcji faktur.</span><span class="sxs-lookup"><span data-stu-id="b4b70-117">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="b4b70-118">Na koniec Wykorzystaj moduł wyliczający do pobierania i pracy z każdą stroną faktur, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="b4b70-118">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="b4b70-119">Każde wywołanie [**następnej**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) metody wysyła żądanie do następnej strony faktur na podstawie rozmiaru strony.</span><span class="sxs-lookup"><span data-stu-id="b4b70-119">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

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

<span data-ttu-id="b4b70-120">Aby uzyskać nieco inny przykład, zobacz **przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4b70-120">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b4b70-121">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="b4b70-121">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="b4b70-122">Ten sam interfejs API jest używany w przypadku wszystkich nowoczesnych zakupów komercyjnych, a także licencji 145p i pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="b4b70-122">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="b4b70-123">Rozmiar i przesunięcie są brane pod uwagę tylko w przypadku starszych faktur.</span><span class="sxs-lookup"><span data-stu-id="b4b70-123">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="b4b70-124">W przypadku wszystkich nowoczesnych zakupów komercyjnych wartość przesunięcia & PageSize zostanie zignorowana.</span><span class="sxs-lookup"><span data-stu-id="b4b70-124">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="b4b70-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="b4b70-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b4b70-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="b4b70-126">Request syntax</span></span>

| <span data-ttu-id="b4b70-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="b4b70-127">Method</span></span>  | <span data-ttu-id="b4b70-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="b4b70-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b4b70-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="b4b70-129">**GET**</span></span> | <span data-ttu-id="b4b70-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices? size = {size} &offset = {offset} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b4b70-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="b4b70-131">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="b4b70-131">URI parameters</span></span>

<span data-ttu-id="b4b70-132">Podczas tworzenia żądania Użyj następujących parametrów zapytania.</span><span class="sxs-lookup"><span data-stu-id="b4b70-132">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="b4b70-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b4b70-133">Name</span></span>   | <span data-ttu-id="b4b70-134">Typ</span><span class="sxs-lookup"><span data-stu-id="b4b70-134">Type</span></span> | <span data-ttu-id="b4b70-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b4b70-135">Required</span></span> | <span data-ttu-id="b4b70-136">Opis</span><span class="sxs-lookup"><span data-stu-id="b4b70-136">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="b4b70-137">size</span><span class="sxs-lookup"><span data-stu-id="b4b70-137">size</span></span>   | <span data-ttu-id="b4b70-138">int</span><span class="sxs-lookup"><span data-stu-id="b4b70-138">int</span></span>  | <span data-ttu-id="b4b70-139">Nie</span><span class="sxs-lookup"><span data-stu-id="b4b70-139">No</span></span>       | <span data-ttu-id="b4b70-140">Liczba zasobów faktury do zwrócenia w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b4b70-140">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="b4b70-141">Ten parametr jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="b4b70-141">This parameter is optional.</span></span> |
| <span data-ttu-id="b4b70-142">przesunięcie</span><span class="sxs-lookup"><span data-stu-id="b4b70-142">offset</span></span> | <span data-ttu-id="b4b70-143">int</span><span class="sxs-lookup"><span data-stu-id="b4b70-143">int</span></span>  | <span data-ttu-id="b4b70-144">Nie</span><span class="sxs-lookup"><span data-stu-id="b4b70-144">No</span></span>       | <span data-ttu-id="b4b70-145">Indeks (liczony od zera) pierwszej faktury do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="b4b70-145">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="b4b70-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="b4b70-146">Request headers</span></span>

<span data-ttu-id="b4b70-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b4b70-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b4b70-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="b4b70-148">Request body</span></span>

<span data-ttu-id="b4b70-149">Brak</span><span class="sxs-lookup"><span data-stu-id="b4b70-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b4b70-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="b4b70-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b4b70-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="b4b70-151">REST response</span></span>

<span data-ttu-id="b4b70-152">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [faktury](invoice-resources.md#invoice) .</span><span class="sxs-lookup"><span data-stu-id="b4b70-152">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b4b70-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b4b70-153">Response success and error codes</span></span>

<span data-ttu-id="b4b70-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="b4b70-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b4b70-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="b4b70-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b4b70-156">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b4b70-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b4b70-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="b4b70-157">Response example</span></span>

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
