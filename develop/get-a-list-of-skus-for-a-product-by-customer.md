---
title: Uzyskiwanie listy jednostki SKU dla produktu (według klienta)
description: Pobiera kolekcję jednostki SKU dla określonego produktu przez klienta.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b76526d97ba9027897fc88954ba45186d58aefb8
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874163"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="ad130-103">Uzyskiwanie listy jednostki SKU dla produktu (według klienta)</span><span class="sxs-lookup"><span data-stu-id="ad130-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="ad130-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ad130-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ad130-105">Pobiera kolekcję jednostki SKU dla określonego produktu, który jest dostępny dla istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="ad130-105">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad130-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad130-106">Prerequisites</span></span>

- <span data-ttu-id="ad130-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ad130-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ad130-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad130-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ad130-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad130-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ad130-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="ad130-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ad130-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="ad130-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ad130-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="ad130-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ad130-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="ad130-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ad130-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ad130-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ad130-115">Identyfikator produktu **(product-id).**</span><span class="sxs-lookup"><span data-stu-id="ad130-115">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="ad130-116">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="ad130-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ad130-117">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-117">Request syntax</span></span>

| <span data-ttu-id="ad130-118">Metoda</span><span class="sxs-lookup"><span data-stu-id="ad130-118">Method</span></span> | <span data-ttu-id="ad130-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-119">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad130-120">POST</span><span class="sxs-lookup"><span data-stu-id="ad130-120">POST</span></span>   | <span data-ttu-id="ad130-121">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ad130-121">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="ad130-122">Parametr URI żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-122">Request URI parameter</span></span>

| <span data-ttu-id="ad130-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ad130-123">Name</span></span>               | <span data-ttu-id="ad130-124">Typ</span><span class="sxs-lookup"><span data-stu-id="ad130-124">Type</span></span> | <span data-ttu-id="ad130-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ad130-125">Required</span></span> | <span data-ttu-id="ad130-126">Opis</span><span class="sxs-lookup"><span data-stu-id="ad130-126">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="ad130-127">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="ad130-127">customer-tenant-id</span></span> | <span data-ttu-id="ad130-128">GUID</span><span class="sxs-lookup"><span data-stu-id="ad130-128">GUID</span></span> | <span data-ttu-id="ad130-129">Tak</span><span class="sxs-lookup"><span data-stu-id="ad130-129">Yes</span></span> | <span data-ttu-id="ad130-130">Wartość jest identyfikatorem **customer-tenant-id** w formacie IDENTYFIKATORA GUID, który jest identyfikatorem umożliwiającym określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="ad130-130">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="ad130-131">product-id</span><span class="sxs-lookup"><span data-stu-id="ad130-131">product-id</span></span> | <span data-ttu-id="ad130-132">ciąg</span><span class="sxs-lookup"><span data-stu-id="ad130-132">string</span></span> | <span data-ttu-id="ad130-133">Tak</span><span class="sxs-lookup"><span data-stu-id="ad130-133">Yes</span></span> | <span data-ttu-id="ad130-134">Ciąg identyfikujący produkt.</span><span class="sxs-lookup"><span data-stu-id="ad130-134">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="ad130-135">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-135">Request header</span></span>

<span data-ttu-id="ad130-136">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ad130-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ad130-137">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-137">Request body</span></span>

<span data-ttu-id="ad130-138">Brak.</span><span class="sxs-lookup"><span data-stu-id="ad130-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ad130-139">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="ad130-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="ad130-140">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="ad130-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ad130-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ad130-141">Response success and error codes</span></span>

<span data-ttu-id="ad130-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="ad130-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ad130-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="ad130-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ad130-144">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ad130-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="ad130-145">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="ad130-145">This method returns the following error codes:</span></span>

| <span data-ttu-id="ad130-146">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="ad130-146">HTTP Status Code</span></span> | <span data-ttu-id="ad130-147">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="ad130-147">Error code</span></span> | <span data-ttu-id="ad130-148">Opis</span><span class="sxs-lookup"><span data-stu-id="ad130-148">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="ad130-149">404</span><span class="sxs-lookup"><span data-stu-id="ad130-149">404</span></span> | <span data-ttu-id="ad130-150">400013</span><span class="sxs-lookup"><span data-stu-id="ad130-150">400013</span></span> | <span data-ttu-id="ad130-151">Nie znaleziono produktu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="ad130-151">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="ad130-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ad130-152">Response example</span></span>

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
