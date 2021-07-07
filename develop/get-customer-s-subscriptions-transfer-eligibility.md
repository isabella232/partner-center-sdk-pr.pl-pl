---
title: Pobieranie uprawnień klienta do przeniesienia subskrypcji
description: Jak uzyskać kolekcję subskrypcji klienta, które kwalifikują się do przeniesienia lub są do nich do przekazania.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: fe8af76d1e1456754dec79291ec0853fb253d108
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446296"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="fdc4a-103">Pobieranie uprawnień klienta do przeniesienia subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fdc4a-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="fdc4a-104">Jak uzyskać kolekcję subskrypcji klienta, które kwalifikują się do przeniesienia lub nie są uprawnione do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-104">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdc4a-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fdc4a-105">Prerequisites</span></span>

- <span data-ttu-id="fdc4a-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fdc4a-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fdc4a-107">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fdc4a-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fdc4a-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fdc4a-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fdc4a-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fdc4a-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="fdc4a-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fdc4a-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fdc4a-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fdc4a-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fdc4a-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="fdc4a-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fdc4a-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fdc4a-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fdc4a-115">Request syntax</span></span>

| <span data-ttu-id="fdc4a-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="fdc4a-116">Method</span></span>  | <span data-ttu-id="fdc4a-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fdc4a-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fdc4a-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="fdc4a-118">**GET**</span></span> | <span data-ttu-id="fdc4a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transfereligibility?transferType={transfer-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fdc4a-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fdc4a-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fdc4a-120">URI parameter</span></span>

<span data-ttu-id="fdc4a-121">W tej tabeli wymieniono parametr zapytania wymagany do uzyskania wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-121">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="fdc4a-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fdc4a-122">Name</span></span>               | <span data-ttu-id="fdc4a-123">Typ</span><span class="sxs-lookup"><span data-stu-id="fdc4a-123">Type</span></span>   | <span data-ttu-id="fdc4a-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fdc4a-124">Required</span></span> | <span data-ttu-id="fdc4a-125">Opis</span><span class="sxs-lookup"><span data-stu-id="fdc4a-125">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="fdc4a-126">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="fdc4a-126">customer-tenant-id</span></span> | <span data-ttu-id="fdc4a-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdc4a-127">string</span></span> | <span data-ttu-id="fdc4a-128">Tak</span><span class="sxs-lookup"><span data-stu-id="fdc4a-128">Yes</span></span>      | <span data-ttu-id="fdc4a-129">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-129">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="fdc4a-130">transfer-type</span><span class="sxs-lookup"><span data-stu-id="fdc4a-130">transfer-type</span></span>      | <span data-ttu-id="fdc4a-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="fdc4a-131">string</span></span> | <span data-ttu-id="fdc4a-132">Tak</span><span class="sxs-lookup"><span data-stu-id="fdc4a-132">Yes</span></span>      | <span data-ttu-id="fdc4a-133">Typ transferu, który jest zamierzony.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-133">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="fdc4a-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fdc4a-134">Request headers</span></span>

<span data-ttu-id="fdc4a-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fdc4a-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fdc4a-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fdc4a-136">Request body</span></span>

<span data-ttu-id="fdc4a-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fdc4a-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fdc4a-138">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="fdc4a-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fdc4a-139">REST response</span></span>

<span data-ttu-id="fdc4a-140">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [Uprawnień](transfer-eligibility-resources.md) do przeniesienia w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-140">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fdc4a-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fdc4a-141">Response success and error codes</span></span>

<span data-ttu-id="fdc4a-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fdc4a-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fdc4a-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fdc4a-144">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fdc4a-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fdc4a-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fdc4a-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
