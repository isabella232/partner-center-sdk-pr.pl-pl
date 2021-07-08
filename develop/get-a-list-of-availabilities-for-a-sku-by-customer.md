---
title: Pobieranie listy dostępności dla jednostki SKU (według klientów)
description: Możesz uzyskać kolekcję dostępności dla określonego produktu i jednostki SKU przez klienta przy użyciu identyfikatorów klienta, produktu i jednostki SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874554"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="3a5b8-103">Pobieranie listy dostępności dla jednostki SKU (według klientów)</span><span class="sxs-lookup"><span data-stu-id="3a5b8-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="3a5b8-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3a5b8-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3a5b8-105">Aby uzyskać kolekcję dostępności dla określonego produktu i określonej wersji SKU dostępnej dla określonego klienta, można użyć następujących metod.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-105">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a5b8-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3a5b8-106">Prerequisites</span></span>

- <span data-ttu-id="3a5b8-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3a5b8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3a5b8-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3a5b8-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a5b8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3a5b8-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="3a5b8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3a5b8-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="3a5b8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3a5b8-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3a5b8-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3a5b8-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3a5b8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3a5b8-115">Identyfikator produktu **(product-id).**</span><span class="sxs-lookup"><span data-stu-id="3a5b8-115">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="3a5b8-116">Identyfikator jednostki SKU **(identyfikator jednostki SKU).**</span><span class="sxs-lookup"><span data-stu-id="3a5b8-116">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="3a5b8-117">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3a5b8-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3a5b8-118">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-118">Request syntax</span></span>

| <span data-ttu-id="3a5b8-119">Metoda</span><span class="sxs-lookup"><span data-stu-id="3a5b8-119">Method</span></span> | <span data-ttu-id="3a5b8-120">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-120">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a5b8-121">POST</span><span class="sxs-lookup"><span data-stu-id="3a5b8-121">POST</span></span>   | <span data-ttu-id="3a5b8-122">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3a5b8-122">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="3a5b8-123">Parametry URI żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-123">Request URI parameters</span></span>

| <span data-ttu-id="3a5b8-124">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3a5b8-124">Name</span></span>               | <span data-ttu-id="3a5b8-125">Typ</span><span class="sxs-lookup"><span data-stu-id="3a5b8-125">Type</span></span> | <span data-ttu-id="3a5b8-126">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3a5b8-126">Required</span></span> | <span data-ttu-id="3a5b8-127">Opis</span><span class="sxs-lookup"><span data-stu-id="3a5b8-127">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="3a5b8-128">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="3a5b8-128">customer-tenant-id</span></span> | <span data-ttu-id="3a5b8-129">GUID</span><span class="sxs-lookup"><span data-stu-id="3a5b8-129">GUID</span></span> | <span data-ttu-id="3a5b8-130">Tak</span><span class="sxs-lookup"><span data-stu-id="3a5b8-130">Yes</span></span> | <span data-ttu-id="3a5b8-131">Wartość jest identyfikatorem **customer-tenant-id** w formacie identyfikatora GUID, który jest identyfikatorem umożliwiającym określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-131">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="3a5b8-132">identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="3a5b8-132">product-id</span></span> | <span data-ttu-id="3a5b8-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="3a5b8-133">string</span></span> | <span data-ttu-id="3a5b8-134">Tak</span><span class="sxs-lookup"><span data-stu-id="3a5b8-134">Yes</span></span> | <span data-ttu-id="3a5b8-135">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-135">A string that identifies the product.</span></span> |
| <span data-ttu-id="3a5b8-136">identyfikator sku</span><span class="sxs-lookup"><span data-stu-id="3a5b8-136">sku-id</span></span> | <span data-ttu-id="3a5b8-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="3a5b8-137">string</span></span> | <span data-ttu-id="3a5b8-138">Tak</span><span class="sxs-lookup"><span data-stu-id="3a5b8-138">Yes</span></span> | <span data-ttu-id="3a5b8-139">Ciąg identyfikujący sku.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-139">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="3a5b8-140">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-140">Request header</span></span>

<span data-ttu-id="3a5b8-141">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3a5b8-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3a5b8-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-142">Request body</span></span>

<span data-ttu-id="3a5b8-143">Brak.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3a5b8-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3a5b8-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="3a5b8-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3a5b8-145">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3a5b8-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3a5b8-146">Response success and error codes</span></span>

<span data-ttu-id="3a5b8-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3a5b8-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3a5b8-149">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3a5b8-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="3a5b8-150">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="3a5b8-150">This method returns the following error codes:</span></span>

| <span data-ttu-id="3a5b8-151">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="3a5b8-151">HTTP Status Code</span></span> | <span data-ttu-id="3a5b8-152">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="3a5b8-152">Error code</span></span> | <span data-ttu-id="3a5b8-153">Opis</span><span class="sxs-lookup"><span data-stu-id="3a5b8-153">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="3a5b8-154">404</span><span class="sxs-lookup"><span data-stu-id="3a5b8-154">404</span></span> | <span data-ttu-id="3a5b8-155">400013</span><span class="sxs-lookup"><span data-stu-id="3a5b8-155">400013</span></span> | <span data-ttu-id="3a5b8-156">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="3a5b8-156">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="3a5b8-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3a5b8-157">Response example</span></span>

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
