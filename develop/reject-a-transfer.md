---
title: Odrzucanie przeniesienia
description: Jak odrzucić przeniesienie subskrypcji dla klienta.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d09905979a89c9b2092462512c485524cd681d5f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445378"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="16756-103">Odrzucanie przeniesienia</span><span class="sxs-lookup"><span data-stu-id="16756-103">Reject a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16756-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16756-104">Prerequisites</span></span>

- <span data-ttu-id="16756-105">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="16756-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="16756-106">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16756-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="16756-107">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16756-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="16756-108">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="16756-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="16756-109">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="16756-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="16756-110">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="16756-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="16756-111">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="16756-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="16756-112">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="16756-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="16756-113">Identyfikator transferu dla istniejącego transferu.</span><span class="sxs-lookup"><span data-stu-id="16756-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="16756-114">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="16756-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="16756-115">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="16756-115">Request syntax</span></span>

| <span data-ttu-id="16756-116">Metoda</span><span class="sxs-lookup"><span data-stu-id="16756-116">Method</span></span>   | <span data-ttu-id="16756-117">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="16756-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="16756-118">**Patch**</span><span class="sxs-lookup"><span data-stu-id="16756-118">**PATCH**</span></span> | <span data-ttu-id="16756-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="16756-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="16756-120">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="16756-120">URI parameter</span></span>

<span data-ttu-id="16756-121">Użyj następującego parametru ścieżki, aby zidentyfikować klienta i określić transfer do zaakceptowania.</span><span class="sxs-lookup"><span data-stu-id="16756-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="16756-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="16756-122">Name</span></span>            | <span data-ttu-id="16756-123">Typ</span><span class="sxs-lookup"><span data-stu-id="16756-123">Type</span></span>     | <span data-ttu-id="16756-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="16756-124">Required</span></span> | <span data-ttu-id="16756-125">Opis</span><span class="sxs-lookup"><span data-stu-id="16756-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="16756-126">**identyfikator klienta**</span><span class="sxs-lookup"><span data-stu-id="16756-126">**customer-id**</span></span> | <span data-ttu-id="16756-127">ciąg</span><span class="sxs-lookup"><span data-stu-id="16756-127">string</span></span>   | <span data-ttu-id="16756-128">Tak</span><span class="sxs-lookup"><span data-stu-id="16756-128">Yes</span></span>      | <span data-ttu-id="16756-129">Identyfikator klienta sformatowany w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="16756-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="16756-130">**transfer-id**</span><span class="sxs-lookup"><span data-stu-id="16756-130">**transfer-id**</span></span> | <span data-ttu-id="16756-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="16756-131">string</span></span>   | <span data-ttu-id="16756-132">Tak</span><span class="sxs-lookup"><span data-stu-id="16756-132">Yes</span></span>      | <span data-ttu-id="16756-133">Identyfikator GUID sformatowany transfer-id, który identyfikuje transfer.</span><span class="sxs-lookup"><span data-stu-id="16756-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="16756-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="16756-134">Request headers</span></span>

<span data-ttu-id="16756-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="16756-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="16756-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="16756-136">Request body</span></span>

<span data-ttu-id="16756-137">W tej tabeli [opisano właściwości TransferEntity](transfer-entity-resources.md) w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="16756-137">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="16756-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="16756-138">Property</span></span>              | <span data-ttu-id="16756-139">Typ</span><span class="sxs-lookup"><span data-stu-id="16756-139">Type</span></span>          | <span data-ttu-id="16756-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="16756-140">Required</span></span>  | <span data-ttu-id="16756-141">Opis</span><span class="sxs-lookup"><span data-stu-id="16756-141">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="16756-142">identyfikator</span><span class="sxs-lookup"><span data-stu-id="16756-142">id</span></span>                    | <span data-ttu-id="16756-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="16756-143">string</span></span>        | <span data-ttu-id="16756-144">Nie</span><span class="sxs-lookup"><span data-stu-id="16756-144">No</span></span>    | <span data-ttu-id="16756-145">Identyfikator transferEntity, który jest dostarczany po pomyślnym utworzeniu obiektu transferEntity.</span><span class="sxs-lookup"><span data-stu-id="16756-145">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="16756-146">status</span><span class="sxs-lookup"><span data-stu-id="16756-146">status</span></span>                | <span data-ttu-id="16756-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="16756-147">string</span></span>        | <span data-ttu-id="16756-148">Nie</span><span class="sxs-lookup"><span data-stu-id="16756-148">No</span></span>    | <span data-ttu-id="16756-149">Stan transferEntity.</span><span class="sxs-lookup"><span data-stu-id="16756-149">The status of the transferEntity.</span></span> <span data-ttu-id="16756-150">Aby odrzucić przeniesienie, wartość należy ustawić jako "odrzuć"</span><span class="sxs-lookup"><span data-stu-id="16756-150">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="16756-151">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="16756-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="16756-152">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="16756-152">REST response</span></span>

<span data-ttu-id="16756-153">W przypadku powodzenia ta metoda zwraca wypełniony [zasób TransferEntity](transfer-entity-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="16756-153">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="16756-154">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="16756-154">Response success and error codes</span></span>

<span data-ttu-id="16756-155">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="16756-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="16756-156">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="16756-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="16756-157">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="16756-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="16756-158">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="16756-158">Response example</span></span>

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
