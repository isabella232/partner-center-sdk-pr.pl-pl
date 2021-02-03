---
title: Pobieranie listy dostępności dla jednostki SKU (według klientów)
description: Możesz uzyskać kolekcję podaży dla określonego produktu i jednostki SKU przez klienta przy użyciu identyfikatorów klienta, produktu i jednostki SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5f4067916fea911963182954eed77f4e230e79d6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767958"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="62626-103">Pobieranie listy dostępności dla jednostki SKU (według klientów)</span><span class="sxs-lookup"><span data-stu-id="62626-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="62626-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="62626-104">**Applies to:**</span></span>

- <span data-ttu-id="62626-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="62626-105">Partner Center</span></span>
- <span data-ttu-id="62626-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="62626-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="62626-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="62626-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="62626-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="62626-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="62626-109">Korzystając z poniższych metod, można uzyskać kolekcję dostępności dla określonego produktu i jednostki SKU dostępnego dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="62626-109">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62626-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="62626-110">Prerequisites</span></span>

- <span data-ttu-id="62626-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="62626-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="62626-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="62626-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="62626-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62626-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="62626-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="62626-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="62626-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="62626-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="62626-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="62626-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="62626-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="62626-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="62626-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="62626-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="62626-119">Identyfikator produktu (**Identyfikator produktu**).</span><span class="sxs-lookup"><span data-stu-id="62626-119">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="62626-120">Identyfikator jednostki SKU (**SKU-ID**).</span><span class="sxs-lookup"><span data-stu-id="62626-120">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="62626-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="62626-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="62626-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="62626-122">Request syntax</span></span>

| <span data-ttu-id="62626-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="62626-123">Method</span></span> | <span data-ttu-id="62626-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="62626-124">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="62626-125">POST</span><span class="sxs-lookup"><span data-stu-id="62626-125">POST</span></span>   | <span data-ttu-id="62626-126">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/SKUs/{SKU-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="62626-126">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="62626-127">Parametry identyfikatora URI żądania</span><span class="sxs-lookup"><span data-stu-id="62626-127">Request URI parameters</span></span>

| <span data-ttu-id="62626-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="62626-128">Name</span></span>               | <span data-ttu-id="62626-129">Typ</span><span class="sxs-lookup"><span data-stu-id="62626-129">Type</span></span> | <span data-ttu-id="62626-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="62626-130">Required</span></span> | <span data-ttu-id="62626-131">Opis</span><span class="sxs-lookup"><span data-stu-id="62626-131">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="62626-132">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="62626-132">customer-tenant-id</span></span> | <span data-ttu-id="62626-133">GUID</span><span class="sxs-lookup"><span data-stu-id="62626-133">GUID</span></span> | <span data-ttu-id="62626-134">Tak</span><span class="sxs-lookup"><span data-stu-id="62626-134">Yes</span></span> | <span data-ttu-id="62626-135">Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="62626-135">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="62626-136">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="62626-136">product-id</span></span> | <span data-ttu-id="62626-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="62626-137">string</span></span> | <span data-ttu-id="62626-138">Tak</span><span class="sxs-lookup"><span data-stu-id="62626-138">Yes</span></span> | <span data-ttu-id="62626-139">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="62626-139">A string that identifies the product.</span></span> |
| <span data-ttu-id="62626-140">jednostka SKU — identyfikator</span><span class="sxs-lookup"><span data-stu-id="62626-140">sku-id</span></span> | <span data-ttu-id="62626-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="62626-141">string</span></span> | <span data-ttu-id="62626-142">Tak</span><span class="sxs-lookup"><span data-stu-id="62626-142">Yes</span></span> | <span data-ttu-id="62626-143">Ciąg, który identyfikuje jednostkę SKU.</span><span class="sxs-lookup"><span data-stu-id="62626-143">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="62626-144">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="62626-144">Request header</span></span>

<span data-ttu-id="62626-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="62626-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="62626-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="62626-146">Request body</span></span>

<span data-ttu-id="62626-147">Brak.</span><span class="sxs-lookup"><span data-stu-id="62626-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="62626-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="62626-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="62626-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="62626-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="62626-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="62626-150">Response success and error codes</span></span>

<span data-ttu-id="62626-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="62626-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="62626-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="62626-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="62626-153">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="62626-153">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="62626-154">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="62626-154">This method returns the following error codes:</span></span>

| <span data-ttu-id="62626-155">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="62626-155">HTTP Status Code</span></span> | <span data-ttu-id="62626-156">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="62626-156">Error code</span></span> | <span data-ttu-id="62626-157">Opis</span><span class="sxs-lookup"><span data-stu-id="62626-157">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="62626-158">404</span><span class="sxs-lookup"><span data-stu-id="62626-158">404</span></span> | <span data-ttu-id="62626-159">400013</span><span class="sxs-lookup"><span data-stu-id="62626-159">400013</span></span> | <span data-ttu-id="62626-160">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="62626-160">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="62626-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="62626-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
