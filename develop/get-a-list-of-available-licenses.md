---
title: Pobieranie listy dostępnych licencji
description: Jak uzyskać listę licencji dostępnych dla użytkowników określonego klienta.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 02a6fccc2cf7f3f4dc929b96ec0f17e0f4a31b06
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874503"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="e30d4-103">Pobieranie listy dostępnych licencji</span><span class="sxs-lookup"><span data-stu-id="e30d4-103">Get a list of available licenses</span></span>

<span data-ttu-id="e30d4-104">W tym artykule opisano sposób uzyskania listy licencji dostępnych dla użytkowników określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="e30d4-104">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="e30d4-105">W poniższych przykładach zwracane są licencje dostępne w grupie **1**, czyli domyślnej grupie licencji reprezentującej licencje zarządzane przez usługę Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e30d4-105">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e30d4-106">Aby uzyskać dostępne licencje dla określonej grupy licencji, zobacz [Get a list of available licenses by license group (Uzyskiwanie](get-a-list-of-available-licenses-by-license-group.md)listy dostępnych licencji według grupy licencji).</span><span class="sxs-lookup"><span data-stu-id="e30d4-106">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e30d4-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e30d4-107">Prerequisites</span></span>

- <span data-ttu-id="e30d4-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e30d4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e30d4-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e30d4-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e30d4-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e30d4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e30d4-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e30d4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e30d4-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="e30d4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e30d4-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="e30d4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e30d4-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="e30d4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e30d4-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e30d4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e30d4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e30d4-116">C\#</span></span>

<span data-ttu-id="e30d4-117">Aby pobrać listę licencji dostępnych z domyślnej grupy licencji dla użytkowników klienta:</span><span class="sxs-lookup"><span data-stu-id="e30d4-117">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="e30d4-118">Użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="e30d4-118">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="e30d4-119">Pobierz wartość właściwości [**SubscribedSkus,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) aby pobrać interfejs dla operacji zbierania subskrybowanych przez klienta elementów SKU.</span><span class="sxs-lookup"><span data-stu-id="e30d4-119">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="e30d4-120">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) aby pobrać listę licencji.</span><span class="sxs-lookup"><span data-stu-id="e30d4-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="e30d4-121">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="e30d4-121">For an example, see the following:</span></span>

- <span data-ttu-id="e30d4-122">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e30d4-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="e30d4-123">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="e30d4-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="e30d4-124">Klasa: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="e30d4-124">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e30d4-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e30d4-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e30d4-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e30d4-126">Request syntax</span></span>

| <span data-ttu-id="e30d4-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="e30d4-127">Method</span></span>  | <span data-ttu-id="e30d4-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e30d4-128">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e30d4-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e30d4-129">**GET**</span></span> | <span data-ttu-id="e30d4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/subscribedskus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e30d4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="e30d4-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e30d4-131">URI parameter</span></span>

<span data-ttu-id="e30d4-132">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="e30d4-132">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="e30d4-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e30d4-133">Name</span></span>        | <span data-ttu-id="e30d4-134">Typ</span><span class="sxs-lookup"><span data-stu-id="e30d4-134">Type</span></span>   | <span data-ttu-id="e30d4-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e30d4-135">Required</span></span> | <span data-ttu-id="e30d4-136">Opis</span><span class="sxs-lookup"><span data-stu-id="e30d4-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e30d4-137">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="e30d4-137">customer-id</span></span> | <span data-ttu-id="e30d4-138">ciąg</span><span class="sxs-lookup"><span data-stu-id="e30d4-138">string</span></span> | <span data-ttu-id="e30d4-139">Tak</span><span class="sxs-lookup"><span data-stu-id="e30d4-139">Yes</span></span>      | <span data-ttu-id="e30d4-140">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="e30d4-140">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e30d4-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e30d4-141">Request headers</span></span>

<span data-ttu-id="e30d4-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e30d4-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e30d4-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e30d4-143">Request body</span></span>

<span data-ttu-id="e30d4-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="e30d4-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e30d4-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e30d4-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e30d4-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e30d4-146">REST response</span></span>

<span data-ttu-id="e30d4-147">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję [zasobów SubscribedSku.](license-resources.md#subscribedsku)</span><span class="sxs-lookup"><span data-stu-id="e30d4-147">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e30d4-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e30d4-148">Response success and error codes</span></span>

<span data-ttu-id="e30d4-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e30d4-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e30d4-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e30d4-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e30d4-151">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e30d4-151">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e30d4-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e30d4-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
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
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
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
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
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
