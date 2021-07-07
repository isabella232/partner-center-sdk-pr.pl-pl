---
title: Uzyskiwanie szczegółów przeniesienia według identyfikatora
description: Jak uzyskać szczegółowe informacje o przeniesieniu subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1347f95debec458b8c70c5e803cef6203ad34818
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445939"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="046c2-103">Uzyskiwanie szczegółów przeniesienia według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="046c2-103">Get transfer details by ID</span></span>

## <a name="prerequisites"></a><span data-ttu-id="046c2-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="046c2-104">Prerequisites</span></span>

- <span data-ttu-id="046c2-105">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="046c2-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="046c2-106">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="046c2-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="046c2-107">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="046c2-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="046c2-108">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="046c2-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="046c2-109">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="046c2-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="046c2-110">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="046c2-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="046c2-111">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="046c2-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="046c2-112">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="046c2-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="046c2-113">Identyfikator przeniesienia istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="046c2-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="046c2-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="046c2-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="046c2-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="046c2-115">Request syntax</span></span>

| <span data-ttu-id="046c2-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="046c2-116">Method</span></span>   | <span data-ttu-id="046c2-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="046c2-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="046c2-118">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="046c2-118">**GET**</span></span> | <span data-ttu-id="046c2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="046c2-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="046c2-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="046c2-120">URI parameter</span></span>

<span data-ttu-id="046c2-121">Użyj następującego parametru ścieżki, aby zidentyfikować klienta i określić transfer do zaakceptowania.</span><span class="sxs-lookup"><span data-stu-id="046c2-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="046c2-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="046c2-122">Name</span></span>            | <span data-ttu-id="046c2-123">Typ</span><span class="sxs-lookup"><span data-stu-id="046c2-123">Type</span></span>     | <span data-ttu-id="046c2-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="046c2-124">Required</span></span> | <span data-ttu-id="046c2-125">Opis</span><span class="sxs-lookup"><span data-stu-id="046c2-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="046c2-126">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="046c2-126">**customer-id**</span></span> | <span data-ttu-id="046c2-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="046c2-127">string</span></span>   | <span data-ttu-id="046c2-128">Tak</span><span class="sxs-lookup"><span data-stu-id="046c2-128">Yes</span></span>      | <span data-ttu-id="046c2-129">Identyfikator GUID sformatowany jako identyfikator klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="046c2-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="046c2-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="046c2-130">**transfer-id**</span></span> | <span data-ttu-id="046c2-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="046c2-131">string</span></span>   | <span data-ttu-id="046c2-132">Tak</span><span class="sxs-lookup"><span data-stu-id="046c2-132">Yes</span></span>      | <span data-ttu-id="046c2-133">Identyfikator GUID sformatowany transfer-id, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="046c2-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="046c2-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="046c2-134">Request headers</span></span>

<span data-ttu-id="046c2-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="046c2-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="046c2-136">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="046c2-136">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="046c2-137">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="046c2-137">REST response</span></span>

<span data-ttu-id="046c2-138">Jeśli to się powiedzie, ta metoda zwraca wypełniony [zasób TransferEntity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="046c2-138">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="046c2-139">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="046c2-139">Response success and error codes</span></span>

<span data-ttu-id="046c2-140">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="046c2-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="046c2-141">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="046c2-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="046c2-142">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="046c2-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="046c2-143">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="046c2-143">Response example</span></span>

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
