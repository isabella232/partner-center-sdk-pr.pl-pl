---
title: Pobieranie linków do szacunkowych faktur
description: Możesz uzyskać kolekcję linków do szacowania, aby utworzyć zapytanie dotyczące szczegółów elementu wiersza uzgodnień.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 719becd3fac5605c4ad48ab86d483ba7903d65d8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549148"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="1d7db-103">Pobieranie linków do szacunkowych faktur</span><span class="sxs-lookup"><span data-stu-id="1d7db-103">Get invoice estimate links</span></span>

<span data-ttu-id="1d7db-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1d7db-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1d7db-105">Możesz uzyskać linki do szacowania, aby pomóc w zapytaniu o szczegółowe informacje dotyczące nienaliowanych elementów wiersza uzgodnień.</span><span class="sxs-lookup"><span data-stu-id="1d7db-105">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d7db-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1d7db-106">Prerequisites</span></span>

- <span data-ttu-id="1d7db-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1d7db-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1d7db-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1d7db-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1d7db-109">Identyfikator faktury.</span><span class="sxs-lookup"><span data-stu-id="1d7db-109">An invoice identifier.</span></span> <span data-ttu-id="1d7db-110">Identyfikuje fakturę, dla której mają zostać pobrane pozycje.</span><span class="sxs-lookup"><span data-stu-id="1d7db-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="1d7db-111">C\#</span><span class="sxs-lookup"><span data-stu-id="1d7db-111">C\#</span></span>

<span data-ttu-id="1d7db-112">Poniższy przykładowy kod pokazuje, jak uzyskać linki do szacowania w celu wykonywania zapytań o nienadane elementy wiersza dla danej waluty.</span><span class="sxs-lookup"><span data-stu-id="1d7db-112">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="1d7db-113">Odpowiedź zawiera linki do szacowania dla każdego okresu (na przykład bieżącego i poprzedniego miesiąca).</span><span class="sxs-lookup"><span data-stu-id="1d7db-113">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="1d7db-114">Podobny przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="1d7db-114">For a similar example, see the following:</span></span>

- <span data-ttu-id="1d7db-115">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1d7db-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1d7db-116">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="1d7db-116">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1d7db-117">Klasa: **GetEstimatesLinks.cs**</span><span class="sxs-lookup"><span data-stu-id="1d7db-117">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1d7db-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1d7db-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1d7db-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1d7db-119">Request syntax</span></span>

| <span data-ttu-id="1d7db-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="1d7db-120">Method</span></span>  | <span data-ttu-id="1d7db-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1d7db-121">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1d7db-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1d7db-122">**GET**</span></span> | <span data-ttu-id="1d7db-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1d7db-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1d7db-124">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="1d7db-124">URI parameters</span></span>

<span data-ttu-id="1d7db-125">Podczas tworzenia żądania użyj następującego parametru URI i zapytania.</span><span class="sxs-lookup"><span data-stu-id="1d7db-125">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="1d7db-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1d7db-126">Name</span></span>                   | <span data-ttu-id="1d7db-127">Typ</span><span class="sxs-lookup"><span data-stu-id="1d7db-127">Type</span></span>   | <span data-ttu-id="1d7db-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1d7db-128">Required</span></span> | <span data-ttu-id="1d7db-129">Opis</span><span class="sxs-lookup"><span data-stu-id="1d7db-129">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="1d7db-130">currencyCode</span><span class="sxs-lookup"><span data-stu-id="1d7db-130">currencyCode</span></span>           | <span data-ttu-id="1d7db-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="1d7db-131">string</span></span> | <span data-ttu-id="1d7db-132">Tak</span><span class="sxs-lookup"><span data-stu-id="1d7db-132">Yes</span></span>      | <span data-ttu-id="1d7db-133">Kod waluty dla nienaliowanych elementów wiersza.</span><span class="sxs-lookup"><span data-stu-id="1d7db-133">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="1d7db-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1d7db-134">Request headers</span></span>

<span data-ttu-id="1d7db-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1d7db-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1d7db-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1d7db-136">Request body</span></span>

<span data-ttu-id="1d7db-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="1d7db-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1d7db-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1d7db-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1d7db-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1d7db-139">REST response</span></span>

<span data-ttu-id="1d7db-140">Jeśli to się powiedzie, odpowiedź zawiera linki do pobierania nienalionych oszacowań.</span><span class="sxs-lookup"><span data-stu-id="1d7db-140">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1d7db-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1d7db-141">Response success and error codes</span></span>

<span data-ttu-id="1d7db-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1d7db-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1d7db-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1d7db-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1d7db-144">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1d7db-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1d7db-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1d7db-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
