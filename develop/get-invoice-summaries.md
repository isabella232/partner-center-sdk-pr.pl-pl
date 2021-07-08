---
title: Pobieranie podsumowania faktur
description: Możesz użyć zasobu podsumowań faktur dla każdego typu waluty, aby wyświetlić saldo i łączne opłaty zarówno opłat cyklicznych, jak i jednorazowych.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: fb6ff839c56c7b0b77a9904abf05d95ca0500b00
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549114"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="a62d2-103">Pobieranie podsumowania faktur</span><span class="sxs-lookup"><span data-stu-id="a62d2-103">Get invoice summaries</span></span>

<span data-ttu-id="a62d2-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a62d2-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a62d2-105">Możesz użyć funkcji **InvoiceSummaries,** aby pobrać podsumowanie faktury, które pokazuje saldo i łączne opłaty zarówno opłat cyklicznych, jak i jednorazowych.</span><span class="sxs-lookup"><span data-stu-id="a62d2-105">You can use the **InvoiceSummaries** to retrieve an invoice summary that shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="a62d2-106">Zasób **InvoiceSummaries** zawiera podsumowanie faktury dla każdego typu waluty.</span><span class="sxs-lookup"><span data-stu-id="a62d2-106">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a62d2-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a62d2-107">Prerequisites</span></span>

- <span data-ttu-id="a62d2-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a62d2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a62d2-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a62d2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a62d2-110">Prawidłowy identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="a62d2-110">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="a62d2-111">C\#</span><span class="sxs-lookup"><span data-stu-id="a62d2-111">C\#</span></span>

<span data-ttu-id="a62d2-112">Aby pobrać [**kolekcję InvoiceSummaries**](invoice-resources.md#invoicesummaries) zawierającą element [**InvoiceSummary**](invoice-resources.md#invoicesummary) dla każdego typu waluty:</span><span class="sxs-lookup"><span data-stu-id="a62d2-112">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="a62d2-113">Użyj **kolekcji IAggregatePartner.Invoices,** aby wywołać **właściwość Summaries.**</span><span class="sxs-lookup"><span data-stu-id="a62d2-113">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="a62d2-114">Wywołaj **metodę Get().**</span><span class="sxs-lookup"><span data-stu-id="a62d2-114">Call the **Get()** method.</span></span>
3. <span data-ttu-id="a62d2-115">Aby uzyskać saldo pojedynczego obiektu [**InvoiceSummary,**](invoice-resources.md#invoicesummary)uzyskaj dostęp do właściwości **BalanceAmount** dla tego członka kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a62d2-115">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="a62d2-116">Aby uzyskać więcej informacji, zobacz następujący przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="a62d2-116">For more information, see the following example code:</span></span>

- <span data-ttu-id="a62d2-117">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a62d2-117">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a62d2-118">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="a62d2-118">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="a62d2-119">Klasa: **GetInvoiceSummaries.cs**</span><span class="sxs-lookup"><span data-stu-id="a62d2-119">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a62d2-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a62d2-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a62d2-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a62d2-121">Request syntax</span></span>

| <span data-ttu-id="a62d2-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="a62d2-122">Method</span></span>  | <span data-ttu-id="a62d2-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a62d2-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a62d2-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a62d2-124">**GET**</span></span> | <span data-ttu-id="a62d2-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a62d2-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="a62d2-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a62d2-126">URI parameter</span></span>

<span data-ttu-id="a62d2-127">Brak.</span><span class="sxs-lookup"><span data-stu-id="a62d2-127">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="a62d2-128">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a62d2-128">Request headers</span></span>

<span data-ttu-id="a62d2-129">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a62d2-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a62d2-130">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a62d2-130">Request body</span></span>

<span data-ttu-id="a62d2-131">Brak.</span><span class="sxs-lookup"><span data-stu-id="a62d2-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a62d2-132">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a62d2-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a62d2-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a62d2-133">REST response</span></span>

<span data-ttu-id="a62d2-134">W przypadku powodzenia ta metoda zwraca [**zasób InvoiceSummaries**](invoice-resources.md#invoicesummaries) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a62d2-134">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a62d2-135">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a62d2-135">Response success and error codes</span></span>

<span data-ttu-id="a62d2-136">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="a62d2-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a62d2-137">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a62d2-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a62d2-138">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a62d2-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a62d2-139">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a62d2-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "totalCount": 3,
    "items": [
        {
            "balanceAmount": 751094.39,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
            "lastPaymentDate": "2017-01-01T12:00:00Z",
            "lastPaymentAmount": 1000,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "Recurring",
                    "summary": {
                        "balanceAmount": 202955.87,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2017-02-27T00:00:00Z",
                        "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                        "lastPaymentDate": "2017-01-01T12:00:00Z",
                        "lastPaymentAmount": 1000,
                        "latestInvoiceDate": "0001-01-01T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                },
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 548138.52,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1230.33,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1230.33,
                        "currencyCode": "CHF",
                        "currencySymbol": "CHF",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1001.12,
            "currencyCode": "EUR",
            "currencySymbol": "€",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1001.12,
                        "currencyCode": "EUR",
                        "currencySymbol": "€",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summaries",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
