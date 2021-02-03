---
title: Pobierz fakturę według identyfikatora
description: Pobiera daną fakturę przy użyciu identyfikatora faktury.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 17880265d06e8e5eaacc5470d83c49defd10ad51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767686"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="cef4e-103">Pobierz fakturę według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="cef4e-103">Get invoice by ID</span></span>

<span data-ttu-id="cef4e-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="cef4e-104">**Applies to:**</span></span>

- <span data-ttu-id="cef4e-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="cef4e-105">Partner Center</span></span>
- <span data-ttu-id="cef4e-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="cef4e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cef4e-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="cef4e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cef4e-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="cef4e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cef4e-109">Pobiera daną fakturę przy użyciu identyfikatora faktury.</span><span class="sxs-lookup"><span data-stu-id="cef4e-109">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cef4e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cef4e-110">Prerequisites</span></span>

- <span data-ttu-id="cef4e-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cef4e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cef4e-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cef4e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cef4e-113">Prawidłowy identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="cef4e-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="cef4e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="cef4e-114">C\#</span></span>

<span data-ttu-id="cef4e-115">Aby uzyskać fakturę według identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="cef4e-115">To get an invoice by ID:</span></span>

1. <span data-ttu-id="cef4e-116">Użyj kolekcji **IPartner. faktur** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="cef4e-116">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="cef4e-117">Wywołaj metody **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="cef4e-117">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="cef4e-118">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cef4e-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cef4e-119">**Project**: PartnerSDK. FeatureSample **Klasa**: GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="cef4e-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cef4e-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cef4e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cef4e-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cef4e-121">Request syntax</span></span>

| <span data-ttu-id="cef4e-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="cef4e-122">Method</span></span>  | <span data-ttu-id="cef4e-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cef4e-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="cef4e-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cef4e-124">**GET**</span></span> | <span data-ttu-id="cef4e-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{Invoice-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cef4e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="cef4e-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cef4e-126">URI parameter</span></span>

<span data-ttu-id="cef4e-127">Użyj następującego parametru zapytania, aby pobrać fakturę.</span><span class="sxs-lookup"><span data-stu-id="cef4e-127">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="cef4e-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cef4e-128">Name</span></span>           | <span data-ttu-id="cef4e-129">Typ</span><span class="sxs-lookup"><span data-stu-id="cef4e-129">Type</span></span>       | <span data-ttu-id="cef4e-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cef4e-130">Required</span></span> | <span data-ttu-id="cef4e-131">Opis</span><span class="sxs-lookup"><span data-stu-id="cef4e-131">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cef4e-132">**Identyfikator faktury**</span><span class="sxs-lookup"><span data-stu-id="cef4e-132">**invoice-id**</span></span> | <span data-ttu-id="cef4e-133">**parametry**</span><span class="sxs-lookup"><span data-stu-id="cef4e-133">**string**</span></span> | <span data-ttu-id="cef4e-134">Tak</span><span class="sxs-lookup"><span data-stu-id="cef4e-134">Yes</span></span>      | <span data-ttu-id="cef4e-135">Wartość jest **identyfikatorem faktury** , który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="cef4e-135">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cef4e-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cef4e-136">Request headers</span></span>

<span data-ttu-id="cef4e-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cef4e-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cef4e-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cef4e-138">Request body</span></span>

<span data-ttu-id="cef4e-139">Brak</span><span class="sxs-lookup"><span data-stu-id="cef4e-139">None</span></span>

### <a name="request-example"></a><span data-ttu-id="cef4e-140">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cef4e-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="cef4e-141">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cef4e-141">REST response</span></span>

<span data-ttu-id="cef4e-142">Jeśli to się powiedzie, ta metoda zwraca zasób [faktury](invoice-resources.md#invoice) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="cef4e-142">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cef4e-143">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cef4e-143">Response success and error codes</span></span>

<span data-ttu-id="cef4e-144">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="cef4e-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cef4e-145">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cef4e-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cef4e-146">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cef4e-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cef4e-147">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cef4e-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
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
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
