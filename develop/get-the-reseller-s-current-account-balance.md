---
title: Pobieranie bieżącego salda konta partnera
description: Pobiera bieżące saldo konta partnera. Podsumowanie salda i łącznego kosztu faktury dla jednorazowych i jednorazowych opłat.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 110da433faa6ff4d3d068c6d68a6f497f4a2721a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767905"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="e4a87-104">Pobieranie bieżącego salda konta partnera</span><span class="sxs-lookup"><span data-stu-id="e4a87-104">Get the partner's current account balance</span></span>

<span data-ttu-id="e4a87-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e4a87-105">**Applies To**</span></span>

- <span data-ttu-id="e4a87-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e4a87-106">Partner Center</span></span>
- <span data-ttu-id="e4a87-107">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e4a87-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e4a87-108">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e4a87-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e4a87-109">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e4a87-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e4a87-110">Pobiera bieżące saldo konta partnera.</span><span class="sxs-lookup"><span data-stu-id="e4a87-110">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="e4a87-111">Podsumowanie salda i łącznego kosztu faktury dla jednorazowych i jednorazowych opłat.</span><span class="sxs-lookup"><span data-stu-id="e4a87-111">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4a87-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e4a87-112">Prerequisites</span></span>

- <span data-ttu-id="e4a87-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e4a87-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4a87-114">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4a87-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e4a87-115">C\#</span><span class="sxs-lookup"><span data-stu-id="e4a87-115">C\#</span></span>

<span data-ttu-id="e4a87-116">Aby pobrać saldo konta, Użyj kolekcji **IAggregatePartner. Revoices** , a następnie Wywołaj Właściwość **Summary** .</span><span class="sxs-lookup"><span data-stu-id="e4a87-116">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="e4a87-117">Następnie wywołaj funkcję **Get** i na koniec Wywołaj Właściwość **BalanceAmount** .</span><span class="sxs-lookup"><span data-stu-id="e4a87-117">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="e4a87-118">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e4a87-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e4a87-119">**Project**: PartnerSDK. FeatureSample **Klasa**: GetInvoiceSummary.cs</span><span class="sxs-lookup"><span data-stu-id="e4a87-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e4a87-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e4a87-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4a87-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e4a87-121">Request syntax</span></span>

| <span data-ttu-id="e4a87-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="e4a87-122">Method</span></span>  | <span data-ttu-id="e4a87-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e4a87-123">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="e4a87-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e4a87-124">**GET**</span></span> | <span data-ttu-id="e4a87-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/Summary http/1.1</span><span class="sxs-lookup"><span data-stu-id="e4a87-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="e4a87-126">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e4a87-126">Request headers</span></span>

<span data-ttu-id="e4a87-127">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e4a87-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4a87-128">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e4a87-128">Request body</span></span>

<span data-ttu-id="e4a87-129">Brak</span><span class="sxs-lookup"><span data-stu-id="e4a87-129">None</span></span>

### <a name="request-example"></a><span data-ttu-id="e4a87-130">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e4a87-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e4a87-131">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e4a87-131">REST response</span></span>

<span data-ttu-id="e4a87-132">Jeśli to się powiedzie, metoda zwraca zasób [InvoiceSummary](invoice-resources.md#invoicesummary) w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e4a87-132">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4a87-133">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4a87-133">Response success and error codes</span></span>

<span data-ttu-id="e4a87-134">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e4a87-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4a87-135">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e4a87-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4a87-136">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e4a87-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e4a87-137">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e4a87-137">Response example</span></span>

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
