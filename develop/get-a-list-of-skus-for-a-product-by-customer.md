---
title: Pobierz listę jednostek SKU dla produktu (przez klienta)
description: Pobiera kolekcję jednostek SKU dla określonego produktu przez klienta.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6b9c9bcd52798006d7f686405f059192a722c7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767938"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="1140b-103">Pobierz listę jednostek SKU dla produktu (przez klienta)</span><span class="sxs-lookup"><span data-stu-id="1140b-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="1140b-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="1140b-104">**Applies To**</span></span>

- <span data-ttu-id="1140b-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="1140b-105">Partner Center</span></span>
- <span data-ttu-id="1140b-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="1140b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="1140b-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="1140b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1140b-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1140b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1140b-109">Pobiera kolekcję jednostek SKU dla określonego produktu, który jest dostępny dla istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="1140b-109">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1140b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1140b-110">Prerequisites</span></span>

- <span data-ttu-id="1140b-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1140b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1140b-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1140b-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1140b-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1140b-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1140b-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="1140b-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1140b-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="1140b-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1140b-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="1140b-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1140b-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="1140b-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1140b-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1140b-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1140b-119">Identyfikator produktu (**Identyfikator produktu**).</span><span class="sxs-lookup"><span data-stu-id="1140b-119">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="1140b-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1140b-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1140b-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-121">Request syntax</span></span>

| <span data-ttu-id="1140b-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="1140b-122">Method</span></span> | <span data-ttu-id="1140b-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-123">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1140b-124">POST</span><span class="sxs-lookup"><span data-stu-id="1140b-124">POST</span></span>   | <span data-ttu-id="1140b-125">[*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/SKUs http/1.1</span><span class="sxs-lookup"><span data-stu-id="1140b-125">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="1140b-126">Parametr identyfikatora URI żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-126">Request URI parameter</span></span>

| <span data-ttu-id="1140b-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1140b-127">Name</span></span>               | <span data-ttu-id="1140b-128">Typ</span><span class="sxs-lookup"><span data-stu-id="1140b-128">Type</span></span> | <span data-ttu-id="1140b-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1140b-129">Required</span></span> | <span data-ttu-id="1140b-130">Opis</span><span class="sxs-lookup"><span data-stu-id="1140b-130">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="1140b-131">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="1140b-131">customer-tenant-id</span></span> | <span data-ttu-id="1140b-132">GUID</span><span class="sxs-lookup"><span data-stu-id="1140b-132">GUID</span></span> | <span data-ttu-id="1140b-133">Tak</span><span class="sxs-lookup"><span data-stu-id="1140b-133">Yes</span></span> | <span data-ttu-id="1140b-134">Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="1140b-134">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="1140b-135">Identyfikator produktu</span><span class="sxs-lookup"><span data-stu-id="1140b-135">product-id</span></span> | <span data-ttu-id="1140b-136">ciąg</span><span class="sxs-lookup"><span data-stu-id="1140b-136">string</span></span> | <span data-ttu-id="1140b-137">Tak</span><span class="sxs-lookup"><span data-stu-id="1140b-137">Yes</span></span> | <span data-ttu-id="1140b-138">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="1140b-138">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="1140b-139">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-139">Request header</span></span>

<span data-ttu-id="1140b-140">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1140b-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1140b-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-141">Request body</span></span>

<span data-ttu-id="1140b-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="1140b-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1140b-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1140b-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="1140b-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1140b-144">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1140b-145">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1140b-145">Response success and error codes</span></span>

<span data-ttu-id="1140b-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="1140b-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1140b-147">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1140b-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1140b-148">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1140b-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="1140b-149">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="1140b-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="1140b-150">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="1140b-150">HTTP Status Code</span></span> | <span data-ttu-id="1140b-151">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="1140b-151">Error code</span></span> | <span data-ttu-id="1140b-152">Opis</span><span class="sxs-lookup"><span data-stu-id="1140b-152">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="1140b-153">404</span><span class="sxs-lookup"><span data-stu-id="1140b-153">404</span></span> | <span data-ttu-id="1140b-154">400013</span><span class="sxs-lookup"><span data-stu-id="1140b-154">400013</span></span> | <span data-ttu-id="1140b-155">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="1140b-155">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="1140b-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1140b-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
