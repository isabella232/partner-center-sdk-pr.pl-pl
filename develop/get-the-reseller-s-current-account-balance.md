---
title: Pobieranie bieżącego salda konta partnera
description: Pobiera bieżące saldo konta partnera. Podsumowanie salda i łącznych opłat na fakturze dla opłat cyklicznych i jednorazowych.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a04ab63482ec9d06e2fe47d2b6ce1bc6a5fd5f27
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548502"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="80997-104">Pobieranie bieżącego salda konta partnera</span><span class="sxs-lookup"><span data-stu-id="80997-104">Get the partner's current account balance</span></span>

<span data-ttu-id="80997-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="80997-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="80997-106">Pobiera bieżące saldo konta partnera.</span><span class="sxs-lookup"><span data-stu-id="80997-106">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="80997-107">Podsumowanie salda i łącznych opłat na fakturze dla opłat cyklicznych i jednorazowych.</span><span class="sxs-lookup"><span data-stu-id="80997-107">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80997-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80997-108">Prerequisites</span></span>

- <span data-ttu-id="80997-109">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="80997-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80997-110">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80997-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="80997-111">C\#</span><span class="sxs-lookup"><span data-stu-id="80997-111">C\#</span></span>

<span data-ttu-id="80997-112">Aby pobrać saldo konta, użyj **kolekcji IAggregatePartner.Invoices,** a następnie wywołaj **właściwość Summary.**</span><span class="sxs-lookup"><span data-stu-id="80997-112">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="80997-113">Następnie wywołaj **funkcję Get** i na koniec wywołaj **właściwość BalanceAmount.**</span><span class="sxs-lookup"><span data-stu-id="80997-113">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="80997-114">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80997-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80997-115">**Project:** Klasa PartnerSDK.FeatureSample: GetInvoiceSummary.cs </span><span class="sxs-lookup"><span data-stu-id="80997-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80997-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="80997-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80997-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="80997-117">Request syntax</span></span>

| <span data-ttu-id="80997-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="80997-118">Method</span></span>  | <span data-ttu-id="80997-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="80997-119">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="80997-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="80997-120">**GET**</span></span> | <span data-ttu-id="80997-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="80997-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="80997-122">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="80997-122">Request headers</span></span>

<span data-ttu-id="80997-123">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="80997-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80997-124">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="80997-124">Request body</span></span>

<span data-ttu-id="80997-125">Brak</span><span class="sxs-lookup"><span data-stu-id="80997-125">None</span></span>

### <a name="request-example"></a><span data-ttu-id="80997-126">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="80997-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="80997-127">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="80997-127">REST response</span></span>

<span data-ttu-id="80997-128">W przypadku powodzenia ta metoda zwraca [zasób InvoiceSummary](invoice-resources.md#invoicesummary) w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="80997-128">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80997-129">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="80997-129">Response success and error codes</span></span>

<span data-ttu-id="80997-130">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="80997-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80997-131">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="80997-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80997-132">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80997-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80997-133">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="80997-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
```
