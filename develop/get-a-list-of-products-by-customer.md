---
title: Pobieranie listy produktów (według klientów)
description: Możesz użyć identyfikatora klienta, aby uzyskać kolekcję produktów przez klienta.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 98a099c458535123f675c6452db950b087b9f387
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768174"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="d82ab-103">Pobieranie listy produktów (według klientów)</span><span class="sxs-lookup"><span data-stu-id="d82ab-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="d82ab-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="d82ab-104">**Applies to:**</span></span>

- <span data-ttu-id="d82ab-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="d82ab-105">Partner Center</span></span>
- <span data-ttu-id="d82ab-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="d82ab-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d82ab-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="d82ab-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d82ab-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d82ab-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d82ab-109">Poniższe metody umożliwiają pobranie kolekcji produktów dla istniejącego klienta.</span><span class="sxs-lookup"><span data-stu-id="d82ab-109">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d82ab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d82ab-110">Prerequisites</span></span>

- <span data-ttu-id="d82ab-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d82ab-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d82ab-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d82ab-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d82ab-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d82ab-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="d82ab-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d82ab-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d82ab-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="d82ab-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d82ab-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="d82ab-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d82ab-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d82ab-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="d82ab-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="d82ab-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d82ab-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-120">Request syntax</span></span>

| <span data-ttu-id="d82ab-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="d82ab-121">Method</span></span> | <span data-ttu-id="d82ab-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-122">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d82ab-123">POST</span><span class="sxs-lookup"><span data-stu-id="d82ab-123">POST</span></span>   | <span data-ttu-id="d82ab-124">[*\{ baseURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Products? targetViewd = {targetView} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d82ab-124">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="d82ab-125">Parametry identyfikatora URI żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-125">Request URI parameters</span></span>

| <span data-ttu-id="d82ab-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d82ab-126">Name</span></span>               | <span data-ttu-id="d82ab-127">Typ</span><span class="sxs-lookup"><span data-stu-id="d82ab-127">Type</span></span> | <span data-ttu-id="d82ab-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d82ab-128">Required</span></span> | <span data-ttu-id="d82ab-129">Opis</span><span class="sxs-lookup"><span data-stu-id="d82ab-129">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="d82ab-130">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="d82ab-130">**customer-tenant-id**</span></span> | <span data-ttu-id="d82ab-131">GUID</span><span class="sxs-lookup"><span data-stu-id="d82ab-131">GUID</span></span> | <span data-ttu-id="d82ab-132">Tak</span><span class="sxs-lookup"><span data-stu-id="d82ab-132">Yes</span></span> | <span data-ttu-id="d82ab-133">Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta.</span><span class="sxs-lookup"><span data-stu-id="d82ab-133">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="d82ab-134">**targetView**</span><span class="sxs-lookup"><span data-stu-id="d82ab-134">**targetView**</span></span> | <span data-ttu-id="d82ab-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="d82ab-135">string</span></span> | <span data-ttu-id="d82ab-136">Tak</span><span class="sxs-lookup"><span data-stu-id="d82ab-136">Yes</span></span> | <span data-ttu-id="d82ab-137">Identyfikuje widok docelowy wykazu.</span><span class="sxs-lookup"><span data-stu-id="d82ab-137">Identifies the target view of the catalog.</span></span> <span data-ttu-id="d82ab-138">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="d82ab-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="d82ab-139">**Azure**, w tym wszystkie elementy platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d82ab-139">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="d82ab-140">**AzureReservations**, która obejmuje wszystkie elementy rezerwacji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d82ab-140">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="d82ab-141">**AzureReservationsVM**, w tym wszystkie elementy rezerwacji maszyny wirtualnej (VM)</span><span class="sxs-lookup"><span data-stu-id="d82ab-141">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="d82ab-142">**AzureReservationsSQL**, która obejmuje wszystkie elementy rezerwacji SQL</span><span class="sxs-lookup"><span data-stu-id="d82ab-142">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="d82ab-143">**AzureReservationsCosmosDb**, która obejmuje wszystkie elementy zastrzeżeń bazy danych Cosmos</span><span class="sxs-lookup"><span data-stu-id="d82ab-143">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="d82ab-144">**MicrosoftAzure**, w tym elementy subskrypcji Microsoft Azure (**MS-AZR-0145P**) i plany platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d82ab-144">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="d82ab-145">**OnlineServices** obejmujący wszystkie elementy usługi online, w tym komercyjne produkty Marketplace</span><span class="sxs-lookup"><span data-stu-id="d82ab-145">**OnlineServices**, which  includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="d82ab-146">**Oprogramowanie**, które obejmuje wszystkie elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="d82ab-146">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="d82ab-147">**SoftwareSUSELinux**, który obejmuje wszystkie elementy oprogramowania SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="d82ab-147">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="d82ab-148">**SoftwarePerpetual**, który obejmuje wszystkie bezterminowe elementy oprogramowania</span><span class="sxs-lookup"><span data-stu-id="d82ab-148">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="d82ab-149">**SoftwareSubscriptions** obejmujący wszystkie elementy subskrypcji oprogramowania</span><span class="sxs-lookup"><span data-stu-id="d82ab-149">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="d82ab-150">Nagłówek żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-150">Request header</span></span>

<span data-ttu-id="d82ab-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d82ab-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-152">Request body</span></span>

<span data-ttu-id="d82ab-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="d82ab-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d82ab-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="d82ab-154">Request example</span></span>

<span data-ttu-id="d82ab-155">Żądanie listy produktów opartych na użyciu platformy Azure dostępnych dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="d82ab-155">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="d82ab-156">Produkty dla obu Microsoft Azure (MS-AZR-0145P) i plany platformy Azure zostaną zwrócone dla klientów w chmurze publicznej:</span><span class="sxs-lookup"><span data-stu-id="d82ab-156">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="d82ab-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="d82ab-157">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d82ab-158">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d82ab-158">Response success and error codes</span></span>

<span data-ttu-id="d82ab-159">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="d82ab-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d82ab-160">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d82ab-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d82ab-161">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d82ab-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="d82ab-162">Ta metoda zwraca następujące kody błędów:</span><span class="sxs-lookup"><span data-stu-id="d82ab-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="d82ab-163">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="d82ab-163">HTTP Status Code</span></span> | <span data-ttu-id="d82ab-164">Kod błędu</span><span class="sxs-lookup"><span data-stu-id="d82ab-164">Error code</span></span>   | <span data-ttu-id="d82ab-165">Opis</span><span class="sxs-lookup"><span data-stu-id="d82ab-165">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="d82ab-166">403</span><span class="sxs-lookup"><span data-stu-id="d82ab-166">403</span></span> | <span data-ttu-id="d82ab-167">400036</span><span class="sxs-lookup"><span data-stu-id="d82ab-167">400036</span></span> | <span data-ttu-id="d82ab-168">Nie można uzyskać dostępu do żądanego targetView.</span><span class="sxs-lookup"><span data-stu-id="d82ab-168">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="d82ab-169">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d82ab-169">Response example</span></span>

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
