---
title: Pobierz szczegóły transferu według identyfikatora
description: Jak uzyskać szczegółowe informacje dotyczące transferu subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c39e9483f1e51469981b0d6fa2541a6372ff2dac
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767814"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="531d6-103">Pobierz szczegóły transferu według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="531d6-103">Get transfer details by id</span></span>

<span data-ttu-id="531d6-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="531d6-104">**Applies to:**</span></span>

- <span data-ttu-id="531d6-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="531d6-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="531d6-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="531d6-106">Prerequisites</span></span>

- <span data-ttu-id="531d6-107">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="531d6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="531d6-108">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="531d6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="531d6-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="531d6-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="531d6-110">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="531d6-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="531d6-111">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="531d6-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="531d6-112">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="531d6-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="531d6-113">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="531d6-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="531d6-114">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="531d6-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="531d6-115">Identyfikator transferu dla istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="531d6-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="531d6-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="531d6-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="531d6-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="531d6-117">Request syntax</span></span>

| <span data-ttu-id="531d6-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="531d6-118">Method</span></span>   | <span data-ttu-id="531d6-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="531d6-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="531d6-120">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="531d6-120">**GET**</span></span> | <span data-ttu-id="531d6-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="531d6-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="531d6-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="531d6-122">URI parameter</span></span>

<span data-ttu-id="531d6-123">Użyj następującego parametru ścieżki, aby zidentyfikować klienta i określić transfer, który ma zostać zaakceptowany.</span><span class="sxs-lookup"><span data-stu-id="531d6-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="531d6-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="531d6-124">Name</span></span>            | <span data-ttu-id="531d6-125">Typ</span><span class="sxs-lookup"><span data-stu-id="531d6-125">Type</span></span>     | <span data-ttu-id="531d6-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="531d6-126">Required</span></span> | <span data-ttu-id="531d6-127">Opis</span><span class="sxs-lookup"><span data-stu-id="531d6-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="531d6-128">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="531d6-128">**customer-id**</span></span> | <span data-ttu-id="531d6-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="531d6-129">string</span></span>   | <span data-ttu-id="531d6-130">Tak</span><span class="sxs-lookup"><span data-stu-id="531d6-130">Yes</span></span>      | <span data-ttu-id="531d6-131">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="531d6-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="531d6-132">**Identyfikator transferu**</span><span class="sxs-lookup"><span data-stu-id="531d6-132">**transfer-id**</span></span> | <span data-ttu-id="531d6-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="531d6-133">string</span></span>   | <span data-ttu-id="531d6-134">Tak</span><span class="sxs-lookup"><span data-stu-id="531d6-134">Yes</span></span>      | <span data-ttu-id="531d6-135">Identyfikator transferu w formacie GUID, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="531d6-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="531d6-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="531d6-136">Request headers</span></span>

<span data-ttu-id="531d6-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="531d6-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="531d6-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="531d6-138">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="531d6-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="531d6-139">REST response</span></span>

<span data-ttu-id="531d6-140">Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [TransferEntity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="531d6-140">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="531d6-141">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="531d6-141">Response success and error codes</span></span>

<span data-ttu-id="531d6-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="531d6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="531d6-143">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="531d6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="531d6-144">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="531d6-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="531d6-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="531d6-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1501
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
X-Locale: en-US
Date: Fri, 27 Mar 2020 18:25:25 GMT

{
  "id": "46e8ed67-8adf-4f65-b3d8-d31318080556",
  "status": "Active",
  "createdTime": "2020-03-27T18:22:33.2875302Z",
  "lastModifiedTime": "2020-03-27T18:22:33Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "75B71186-73C3-45B4-A403-281C0D7EB032",
      "offerId": "F72752C8-3E37-4C9B-A1A0-69E8442068DC",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central Team Member",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 1,
      "subscriptionId": "1FB4CB0A-EB79-4300-9E87-7D486054888A",
      "offerId": "88F9EB8A-0636-45E8-A601-553E0A48AA9E",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central External Accountant",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 2,
      "subscriptionId": "08AB3010-B647-402E-8955-B6C0FB364D8F",
      "offerId": "4D8F3B90-29B3-4E7B-B37C-4A435DDEF1D9",
      "billingCycle": "annual",
      "friendlyName": "Common Area Phone",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}

```
