---
title: Pobieranie listy produktów (według klientów)
description: Identyfikator klienta umożliwia pobieranie kolekcji produktów według klienta.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874197"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="751fa-103">Pobieranie listy produktów (według klientów)</span><span class="sxs-lookup"><span data-stu-id="751fa-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="751fa-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="751fa-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="751fa-105">Aby uzyskać kolekcję produktów dla istniejącego klienta, można użyć następujących metod.</span><span class="sxs-lookup"><span data-stu-id="751fa-105">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="751fa-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="751fa-106">Prerequisites</span></span>

- <span data-ttu-id="751fa-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="751fa-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="751fa-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="751fa-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="751fa-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="751fa-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="751fa-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="751fa-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="751fa-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="751fa-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="751fa-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="751fa-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="751fa-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="751fa-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="751fa-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="751fa-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="751fa-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="751fa-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="751fa-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-116">Request syntax</span></span>

| <span data-ttu-id="751fa-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="751fa-117">Method</span></span> | <span data-ttu-id="751fa-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-118">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="751fa-119">POST</span><span class="sxs-lookup"><span data-stu-id="751fa-119">POST</span></span>   | <span data-ttu-id="751fa-120">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="751fa-120">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="751fa-121">Parametry URI żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-121">Request URI parameters</span></span>

| <span data-ttu-id="751fa-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="751fa-122">Name</span></span>               | <span data-ttu-id="751fa-123">Typ</span><span class="sxs-lookup"><span data-stu-id="751fa-123">Type</span></span> | <span data-ttu-id="751fa-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="751fa-124">Required</span></span> | <span data-ttu-id="751fa-125">Opis</span><span class="sxs-lookup"><span data-stu-id="751fa-125">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="751fa-126">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="751fa-126">**customer-tenant-id**</span></span> | <span data-ttu-id="751fa-127">GUID</span><span class="sxs-lookup"><span data-stu-id="751fa-127">GUID</span></span> | <span data-ttu-id="751fa-128">Tak</span><span class="sxs-lookup"><span data-stu-id="751fa-128">Yes</span></span> | <span data-ttu-id="751fa-129">Wartość jest identyfikatorem **customer-tenant-id** w formacie IDENTYFIKATORA GUID, który jest identyfikatorem umożliwiającym określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="751fa-129">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="751fa-130">**targetView**</span><span class="sxs-lookup"><span data-stu-id="751fa-130">**targetView**</span></span> | <span data-ttu-id="751fa-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="751fa-131">string</span></span> | <span data-ttu-id="751fa-132">Tak</span><span class="sxs-lookup"><span data-stu-id="751fa-132">Yes</span></span> | <span data-ttu-id="751fa-133">Identyfikuje widok docelowy wykazu.</span><span class="sxs-lookup"><span data-stu-id="751fa-133">Identifies the target view of the catalog.</span></span> <span data-ttu-id="751fa-134">Obsługiwane wartości to:</span><span class="sxs-lookup"><span data-stu-id="751fa-134">The supported values are:</span></span> <br/><br/><span data-ttu-id="751fa-135">**Azure**, która zawiera wszystkie elementy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="751fa-135">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="751fa-136">**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="751fa-136">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="751fa-137">**AzureReservationsVM,** która zawiera wszystkie elementy rezerwacji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="751fa-137">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="751fa-138">**AzureReservationsSQL**, który zawiera wszystkie SQL elementów rezerwacji</span><span class="sxs-lookup"><span data-stu-id="751fa-138">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="751fa-139">**AzureReservationsCosmosDb,** która zawiera wszystkie Cosmos rezerwacji bazy danych</span><span class="sxs-lookup"><span data-stu-id="751fa-139">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="751fa-140">**MicrosoftAzure**, który zawiera elementy dla Microsoft Azure subskrypcji **(MS-AZR-0145P)** i plany platformy Azure</span><span class="sxs-lookup"><span data-stu-id="751fa-140">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="751fa-141">**OnlineServices**, która obejmuje wszystkie elementy usługi online, w tym produkty platformy handlowej</span><span class="sxs-lookup"><span data-stu-id="751fa-141">**OnlineServices**, which includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="751fa-142">**Oprogramowanie**, które obejmuje wszystkie elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="751fa-142">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="751fa-143">**SoftwareSUSELinux**, który zawiera wszystkie elementy oprogramowania SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="751fa-143">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="751fa-144">**SoftwarePerpetual**, który obejmuje wszystkie elementy oprogramowania bezterminowego</span><span class="sxs-lookup"><span data-stu-id="751fa-144">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="751fa-145">**SoftwareSubscriptions**, która obejmuje wszystkie elementy subskrypcji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="751fa-145">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="751fa-146">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-146">Request header</span></span>

<span data-ttu-id="751fa-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="751fa-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="751fa-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-148">Request body</span></span>

<span data-ttu-id="751fa-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="751fa-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="751fa-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="751fa-150">Request example</span></span>

<span data-ttu-id="751fa-151">Żądanie listy produktów opartych na użyciu platformy Azure dostępnych dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="751fa-151">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="751fa-152">Produkty dla obu Microsoft Azure (MS-AZR-0145P) i planów platformy Azure będą zwracane dla klientów w chmurze publicznej:</span><span class="sxs-lookup"><span data-stu-id="751fa-152">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="751fa-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="751fa-153">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="751fa-154">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="751fa-154">Response success and error codes</span></span>

<span data-ttu-id="751fa-155">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="751fa-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="751fa-156">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="751fa-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="751fa-157">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="751fa-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="751fa-158">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="751fa-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="751fa-159">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="751fa-159">HTTP Status Code</span></span> | <span data-ttu-id="751fa-160">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="751fa-160">Error code</span></span>   | <span data-ttu-id="751fa-161">Opis</span><span class="sxs-lookup"><span data-stu-id="751fa-161">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="751fa-162">403</span><span class="sxs-lookup"><span data-stu-id="751fa-162">403</span></span> | <span data-ttu-id="751fa-163">400036</span><span class="sxs-lookup"><span data-stu-id="751fa-163">400036</span></span> | <span data-ttu-id="751fa-164">Dostęp do żądanego obiektu targetView nie jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="751fa-164">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="751fa-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="751fa-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
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
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
