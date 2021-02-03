---
title: Odrzuć transfer
description: Jak odrzucić transfer subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e4a182ff92a21cf72ca1c2da9de7e211b433725f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767861"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="c4afe-103">Odrzuć transfer</span><span class="sxs-lookup"><span data-stu-id="c4afe-103">Reject a transfer</span></span>

<span data-ttu-id="c4afe-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="c4afe-104">**Applies to:**</span></span>

- <span data-ttu-id="c4afe-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="c4afe-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4afe-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c4afe-106">Prerequisites</span></span>

- <span data-ttu-id="c4afe-107">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c4afe-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c4afe-108">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c4afe-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c4afe-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c4afe-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c4afe-110">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="c4afe-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c4afe-111">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="c4afe-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c4afe-112">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="c4afe-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c4afe-113">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="c4afe-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c4afe-114">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c4afe-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c4afe-115">Identyfikator transferu dla istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="c4afe-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c4afe-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c4afe-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c4afe-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c4afe-117">Request syntax</span></span>

| <span data-ttu-id="c4afe-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="c4afe-118">Method</span></span>   | <span data-ttu-id="c4afe-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c4afe-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4afe-120">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="c4afe-120">**PATCH**</span></span> | <span data-ttu-id="c4afe-121">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Transfers/{transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c4afe-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="c4afe-122">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c4afe-122">URI parameter</span></span>

<span data-ttu-id="c4afe-123">Użyj następującego parametru ścieżki, aby zidentyfikować klienta i określić transfer, który ma zostać zaakceptowany.</span><span class="sxs-lookup"><span data-stu-id="c4afe-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="c4afe-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c4afe-124">Name</span></span>            | <span data-ttu-id="c4afe-125">Typ</span><span class="sxs-lookup"><span data-stu-id="c4afe-125">Type</span></span>     | <span data-ttu-id="c4afe-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c4afe-126">Required</span></span> | <span data-ttu-id="c4afe-127">Opis</span><span class="sxs-lookup"><span data-stu-id="c4afe-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="c4afe-128">**Identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="c4afe-128">**customer-id**</span></span> | <span data-ttu-id="c4afe-129">ciąg</span><span class="sxs-lookup"><span data-stu-id="c4afe-129">string</span></span>   | <span data-ttu-id="c4afe-130">Tak</span><span class="sxs-lookup"><span data-stu-id="c4afe-130">Yes</span></span>      | <span data-ttu-id="c4afe-131">Identyfikator GUID sformatowany przez klienta, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="c4afe-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="c4afe-132">**Identyfikator transferu**</span><span class="sxs-lookup"><span data-stu-id="c4afe-132">**transfer-id**</span></span> | <span data-ttu-id="c4afe-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="c4afe-133">string</span></span>   | <span data-ttu-id="c4afe-134">Tak</span><span class="sxs-lookup"><span data-stu-id="c4afe-134">Yes</span></span>      | <span data-ttu-id="c4afe-135">Identyfikator transferu w formacie GUID, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="c4afe-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="c4afe-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c4afe-136">Request headers</span></span>

<span data-ttu-id="c4afe-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c4afe-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c4afe-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c4afe-138">Request body</span></span>

<span data-ttu-id="c4afe-139">W tej tabeli opisano właściwości [TransferEntity](transfer-entity-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="c4afe-139">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="c4afe-140">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c4afe-140">Property</span></span>              | <span data-ttu-id="c4afe-141">Typ</span><span class="sxs-lookup"><span data-stu-id="c4afe-141">Type</span></span>          | <span data-ttu-id="c4afe-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c4afe-142">Required</span></span>  | <span data-ttu-id="c4afe-143">Opis</span><span class="sxs-lookup"><span data-stu-id="c4afe-143">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4afe-144">identyfikator</span><span class="sxs-lookup"><span data-stu-id="c4afe-144">id</span></span>                    | <span data-ttu-id="c4afe-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="c4afe-145">string</span></span>        | <span data-ttu-id="c4afe-146">Nie</span><span class="sxs-lookup"><span data-stu-id="c4afe-146">No</span></span>    | <span data-ttu-id="c4afe-147">Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="c4afe-147">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="c4afe-148">status</span><span class="sxs-lookup"><span data-stu-id="c4afe-148">status</span></span>                | <span data-ttu-id="c4afe-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="c4afe-149">string</span></span>        | <span data-ttu-id="c4afe-150">Nie</span><span class="sxs-lookup"><span data-stu-id="c4afe-150">No</span></span>    | <span data-ttu-id="c4afe-151">Stan transferEntity.</span><span class="sxs-lookup"><span data-stu-id="c4afe-151">The status of the transferEntity.</span></span> <span data-ttu-id="c4afe-152">Aby odrzucić transfer, wartość jest ustawiana jako "Odrzuć"</span><span class="sxs-lookup"><span data-stu-id="c4afe-152">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="c4afe-153">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c4afe-153">Request example</span></span>

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a><span data-ttu-id="c4afe-154">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c4afe-154">REST response</span></span>

<span data-ttu-id="c4afe-155">Jeśli to się powiedzie, ta metoda zwraca wypełniony zasób [TransferEntity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c4afe-155">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c4afe-156">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c4afe-156">Response success and error codes</span></span>

<span data-ttu-id="c4afe-157">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="c4afe-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c4afe-158">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c4afe-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c4afe-159">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c4afe-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c4afe-160">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c4afe-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
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
