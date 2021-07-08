---
title: Pobieranie listy dostępnych licencji według grupy licencji
description: Jak uzyskać listę licencji dla określonych grup licencji dostępnych dla użytkowników określonego klienta.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: de59dfccf723c8f2411d9dadc51beb88688d5b02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874520"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="a7f80-103">Pobieranie listy dostępnych licencji według grupy licencji</span><span class="sxs-lookup"><span data-stu-id="a7f80-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="a7f80-104">Jak uzyskać listę licencji dla określonych grup licencji dostępnych dla użytkowników określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f80-104">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7f80-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a7f80-105">Prerequisites</span></span>

- <span data-ttu-id="a7f80-106">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a7f80-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a7f80-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a7f80-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a7f80-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a7f80-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a7f80-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="a7f80-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a7f80-110">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="a7f80-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a7f80-111">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="a7f80-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a7f80-112">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f80-112">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a7f80-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a7f80-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a7f80-114">Lista identyfikatorów grup licencji.</span><span class="sxs-lookup"><span data-stu-id="a7f80-114">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="a7f80-115">C\#</span><span class="sxs-lookup"><span data-stu-id="a7f80-115">C\#</span></span>

<span data-ttu-id="a7f80-116">Aby uzyskać listę dostępnych licencji dla określonych grup licencji, rozpocznij od wystąpienia listy typu [**LicenseGroupId,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) [a](/dotnet/api/system.collections.generic.list-1) następnie dodaj grupy licencji do listy.</span><span class="sxs-lookup"><span data-stu-id="a7f80-116">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="a7f80-117">Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f80-117">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="a7f80-118">Następnie pobierz wartość właściwości [**SubscribedSkus,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) aby pobrać interfejs dla operacji zbierania subskrybowanych przez klienta elementów SKU.</span><span class="sxs-lookup"><span data-stu-id="a7f80-118">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="a7f80-119">Na koniec przekaż listę grup licencji do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) aby pobrać listę subskrybowanych jednostek SKU ze szczegółami dostępnych jednostek licencji.</span><span class="sxs-lookup"><span data-stu-id="a7f80-119">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="a7f80-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a7f80-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a7f80-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a7f80-121">Request syntax</span></span>

| <span data-ttu-id="a7f80-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="a7f80-122">Method</span></span>  | <span data-ttu-id="a7f80-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a7f80-123">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a7f80-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a7f80-124">**GET**</span></span> | <span data-ttu-id="a7f80-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7f80-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="a7f80-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a7f80-126">**GET**</span></span> | <span data-ttu-id="a7f80-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7f80-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="a7f80-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="a7f80-128">**GET**</span></span> | <span data-ttu-id="a7f80-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a7f80-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a7f80-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="a7f80-130">URI parameter</span></span>

<span data-ttu-id="a7f80-131">Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klienta i grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="a7f80-131">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="a7f80-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a7f80-132">Name</span></span>            | <span data-ttu-id="a7f80-133">Typ</span><span class="sxs-lookup"><span data-stu-id="a7f80-133">Type</span></span>   | <span data-ttu-id="a7f80-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a7f80-134">Required</span></span> | <span data-ttu-id="a7f80-135">Opis</span><span class="sxs-lookup"><span data-stu-id="a7f80-135">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a7f80-136">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="a7f80-136">customer-id</span></span>     | <span data-ttu-id="a7f80-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="a7f80-137">string</span></span> | <span data-ttu-id="a7f80-138">Tak</span><span class="sxs-lookup"><span data-stu-id="a7f80-138">Yes</span></span>      | <span data-ttu-id="a7f80-139">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="a7f80-139">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="a7f80-140">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="a7f80-140">licenseGroupIds</span></span> | <span data-ttu-id="a7f80-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="a7f80-141">string</span></span> | <span data-ttu-id="a7f80-142">Nie</span><span class="sxs-lookup"><span data-stu-id="a7f80-142">No</span></span>       | <span data-ttu-id="a7f80-143">Wartość wyliczania, która wskazuje grupę licencji przypisanych licencji.</span><span class="sxs-lookup"><span data-stu-id="a7f80-143">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="a7f80-144">Prawidłowe wartości: Grupa1, Grupa2 Grupa1 — ta grupa ma wszystkie produkty, których licencją można zarządzać w Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a7f80-144">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="a7f80-145">Grupa2 — ta grupa ma tylko Minecraft licencji produktów.</span><span class="sxs-lookup"><span data-stu-id="a7f80-145">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a7f80-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a7f80-146">Request headers</span></span>

<span data-ttu-id="a7f80-147">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a7f80-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a7f80-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a7f80-148">Request body</span></span>

<span data-ttu-id="a7f80-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="a7f80-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a7f80-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a7f80-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a7f80-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a7f80-151">REST response</span></span>

<span data-ttu-id="a7f80-152">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów SubscribedSku.](license-resources.md#subscribedsku)</span><span class="sxs-lookup"><span data-stu-id="a7f80-152">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a7f80-153">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a7f80-153">Response success and error codes</span></span>

<span data-ttu-id="a7f80-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="a7f80-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a7f80-155">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a7f80-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a7f80-156">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a7f80-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a7f80-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a7f80-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="a7f80-158">Przykład odpowiedzi (nie znaleziono zgodnych jednostki SKU)</span><span class="sxs-lookup"><span data-stu-id="a7f80-158">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="a7f80-159">Jeśli nie można znaleźć pasujących subskrybowanych jednostki SKU dla określonych grup licencji, odpowiedź zawiera pustą kolekcję z elementem totalCount, którego wartość wynosi 0.</span><span class="sxs-lookup"><span data-stu-id="a7f80-159">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
