---
title: Uzyskiwanie faktury według identyfikatora
description: Pobiera fakturę przy użyciu identyfikatora faktury.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c888786a6b6ca941629bb7aac95227021c37a7fc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549165"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="3c75a-103">Uzyskiwanie faktury według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="3c75a-103">Get invoice by ID</span></span>

<span data-ttu-id="3c75a-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3c75a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3c75a-105">Pobiera fakturę przy użyciu identyfikatora faktury.</span><span class="sxs-lookup"><span data-stu-id="3c75a-105">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c75a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3c75a-106">Prerequisites</span></span>

- <span data-ttu-id="3c75a-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3c75a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3c75a-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c75a-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3c75a-109">Prawidłowy identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="3c75a-109">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="3c75a-110">C\#</span><span class="sxs-lookup"><span data-stu-id="3c75a-110">C\#</span></span>

<span data-ttu-id="3c75a-111">Aby uzyskać fakturę według identyfikatora:</span><span class="sxs-lookup"><span data-stu-id="3c75a-111">To get an invoice by ID:</span></span>

1. <span data-ttu-id="3c75a-112">Użyj **kolekcji IPartner.Invoices** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="3c75a-112">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="3c75a-113">Wywołaj **metody Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="3c75a-113">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="3c75a-114">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3c75a-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3c75a-115">**Project:** Klasa PartnerSDK.FeatureSample: GetInvoice.cs </span><span class="sxs-lookup"><span data-stu-id="3c75a-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3c75a-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3c75a-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3c75a-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3c75a-117">Request syntax</span></span>

| <span data-ttu-id="3c75a-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="3c75a-118">Method</span></span>  | <span data-ttu-id="3c75a-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3c75a-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="3c75a-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3c75a-120">**GET**</span></span> | <span data-ttu-id="3c75a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{identyfikator faktury} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3c75a-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="3c75a-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3c75a-122">URI parameter</span></span>

<span data-ttu-id="3c75a-123">Użyj następującego parametru zapytania, aby uzyskać fakturę.</span><span class="sxs-lookup"><span data-stu-id="3c75a-123">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="3c75a-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3c75a-124">Name</span></span>           | <span data-ttu-id="3c75a-125">Typ</span><span class="sxs-lookup"><span data-stu-id="3c75a-125">Type</span></span>       | <span data-ttu-id="3c75a-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3c75a-126">Required</span></span> | <span data-ttu-id="3c75a-127">Opis</span><span class="sxs-lookup"><span data-stu-id="3c75a-127">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3c75a-128">**identyfikator faktury**</span><span class="sxs-lookup"><span data-stu-id="3c75a-128">**invoice-id**</span></span> | <span data-ttu-id="3c75a-129">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="3c75a-129">**string**</span></span> | <span data-ttu-id="3c75a-130">Tak</span><span class="sxs-lookup"><span data-stu-id="3c75a-130">Yes</span></span>      | <span data-ttu-id="3c75a-131">Wartość to identyfikator **faktury,** który umożliwia odsprzedawcy filtrowanie wyników dla danej faktury.</span><span class="sxs-lookup"><span data-stu-id="3c75a-131">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3c75a-132">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3c75a-132">Request headers</span></span>

<span data-ttu-id="3c75a-133">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3c75a-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3c75a-134">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3c75a-134">Request body</span></span>

<span data-ttu-id="3c75a-135">Brak</span><span class="sxs-lookup"><span data-stu-id="3c75a-135">None</span></span>

### <a name="request-example"></a><span data-ttu-id="3c75a-136">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3c75a-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="3c75a-137">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3c75a-137">REST response</span></span>

<span data-ttu-id="3c75a-138">Jeśli to się powiedzie, ta metoda zwraca [zasób faktury](invoice-resources.md#invoice) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3c75a-138">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3c75a-139">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3c75a-139">Response success and error codes</span></span>

<span data-ttu-id="3c75a-140">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="3c75a-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3c75a-141">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3c75a-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3c75a-142">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3c75a-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3c75a-143">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3c75a-143">Response example</span></span>

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
