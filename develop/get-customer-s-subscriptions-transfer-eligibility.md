---
title: Pobieranie uprawnień klienta do przeniesienia subskrypcji
description: Jak uzyskać kolekcję subskrypcji klienta, które są uprawnione/ineligibile do przeniesienia.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 43086a32fa0dbbdecf65aac167c687f26fc4c2c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767702"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="7519b-103">Pobieranie uprawnień klienta do przeniesienia subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7519b-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="7519b-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="7519b-104">**Applies To**</span></span>

- <span data-ttu-id="7519b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="7519b-105">Partner Center</span></span>

<span data-ttu-id="7519b-106">Jak uzyskać kolekcję subskrypcji klienta uprawniających/niekwalifikujących się do przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="7519b-106">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7519b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7519b-107">Prerequisites</span></span>

- <span data-ttu-id="7519b-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7519b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7519b-109">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7519b-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7519b-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7519b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7519b-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="7519b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7519b-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="7519b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7519b-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="7519b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7519b-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="7519b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7519b-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7519b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="7519b-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7519b-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7519b-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7519b-117">Request syntax</span></span>

| <span data-ttu-id="7519b-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="7519b-118">Method</span></span>  | <span data-ttu-id="7519b-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7519b-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7519b-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="7519b-120">**GET**</span></span> | <span data-ttu-id="7519b-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/transferseligibility? typ transferu = {transfer-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7519b-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7519b-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7519b-122">URI parameter</span></span>

<span data-ttu-id="7519b-123">Ta tabela zawiera listę wymaganych parametrów zapytania w celu uzyskania wszystkich subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7519b-123">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="7519b-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7519b-124">Name</span></span>               | <span data-ttu-id="7519b-125">Typ</span><span class="sxs-lookup"><span data-stu-id="7519b-125">Type</span></span>   | <span data-ttu-id="7519b-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7519b-126">Required</span></span> | <span data-ttu-id="7519b-127">Opis</span><span class="sxs-lookup"><span data-stu-id="7519b-127">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7519b-128">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="7519b-128">customer-tenant-id</span></span> | <span data-ttu-id="7519b-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="7519b-129">string</span></span> | <span data-ttu-id="7519b-130">Tak</span><span class="sxs-lookup"><span data-stu-id="7519b-130">Yes</span></span>      | <span data-ttu-id="7519b-131">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="7519b-131">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="7519b-132">Typ transferu</span><span class="sxs-lookup"><span data-stu-id="7519b-132">transfer-type</span></span>      | <span data-ttu-id="7519b-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="7519b-133">string</span></span> | <span data-ttu-id="7519b-134">Tak</span><span class="sxs-lookup"><span data-stu-id="7519b-134">Yes</span></span>      | <span data-ttu-id="7519b-135">Typ transferu, który jest przeznaczony.</span><span class="sxs-lookup"><span data-stu-id="7519b-135">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="7519b-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7519b-136">Request headers</span></span>

<span data-ttu-id="7519b-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7519b-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7519b-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7519b-138">Request body</span></span>

<span data-ttu-id="7519b-139">Brak.</span><span class="sxs-lookup"><span data-stu-id="7519b-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7519b-140">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7519b-140">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="7519b-141">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7519b-141">REST response</span></span>

<span data-ttu-id="7519b-142">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [TransferEligibility](transfer-eligibility-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7519b-142">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7519b-143">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7519b-143">Response success and error codes</span></span>

<span data-ttu-id="7519b-144">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="7519b-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7519b-145">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7519b-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7519b-146">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7519b-146">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7519b-147">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7519b-147">Response example</span></span>

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
