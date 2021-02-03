---
title: Pobieranie listy zasad klienta
description: Jak pobrać kolekcję zasad konfiguracji określonych klientów.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 16886b1adca393ed2967f2a4fe74a379bef1c1c7
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768101"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="904e8-103">Pobieranie listy zasad klienta</span><span class="sxs-lookup"><span data-stu-id="904e8-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="904e8-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="904e8-104">**Applies to:**</span></span>

- <span data-ttu-id="904e8-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="904e8-105">Partner Center</span></span>
- <span data-ttu-id="904e8-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="904e8-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="904e8-107">W tym artykule opisano sposób pobierania kolekcji zasad konfiguracji określonych klientów.</span><span class="sxs-lookup"><span data-stu-id="904e8-107">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="904e8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="904e8-108">Prerequisites</span></span>

- <span data-ttu-id="904e8-109">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="904e8-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="904e8-110">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="904e8-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="904e8-111">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="904e8-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="904e8-112">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="904e8-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="904e8-113">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="904e8-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="904e8-114">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="904e8-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="904e8-115">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="904e8-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="904e8-116">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="904e8-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="904e8-117">C\#</span><span class="sxs-lookup"><span data-stu-id="904e8-117">C\#</span></span>

<span data-ttu-id="904e8-118">Aby uzyskać listę wszystkich zasad klienta:</span><span class="sxs-lookup"><span data-stu-id="904e8-118">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="904e8-119">Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="904e8-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="904e8-120">Pobierz Właściwość [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) , aby uzyskać interfejs do operacji zbierania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="904e8-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="904e8-121">Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) , aby pobrać kolekcję zasad.</span><span class="sxs-lookup"><span data-stu-id="904e8-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="904e8-122">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="904e8-122">For an example, see the following:</span></span>

- <span data-ttu-id="904e8-123">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="904e8-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="904e8-124">Projekt: **przykłady dla zestawu SDK Centrum partnerskiego**</span><span class="sxs-lookup"><span data-stu-id="904e8-124">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="904e8-125">Klasa: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="904e8-125">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="904e8-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="904e8-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="904e8-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="904e8-127">Request syntax</span></span>

| <span data-ttu-id="904e8-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="904e8-128">Method</span></span>  | <span data-ttu-id="904e8-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="904e8-129">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="904e8-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="904e8-130">**GET**</span></span> | <span data-ttu-id="904e8-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="904e8-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="904e8-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="904e8-132">URI parameter</span></span>

<span data-ttu-id="904e8-133">Podczas tworzenia żądania Użyj następującego parametru ścieżki:</span><span class="sxs-lookup"><span data-stu-id="904e8-133">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="904e8-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="904e8-134">Name</span></span>        | <span data-ttu-id="904e8-135">Typ</span><span class="sxs-lookup"><span data-stu-id="904e8-135">Type</span></span>   | <span data-ttu-id="904e8-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="904e8-136">Required</span></span> | <span data-ttu-id="904e8-137">Opis</span><span class="sxs-lookup"><span data-stu-id="904e8-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="904e8-138">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="904e8-138">customer-id</span></span> | <span data-ttu-id="904e8-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="904e8-139">string</span></span> | <span data-ttu-id="904e8-140">Tak</span><span class="sxs-lookup"><span data-stu-id="904e8-140">Yes</span></span>      | <span data-ttu-id="904e8-141">Ciąg sformatowany przez identyfikator GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="904e8-141">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="904e8-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="904e8-142">Request headers</span></span>

<span data-ttu-id="904e8-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="904e8-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="904e8-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="904e8-144">Request body</span></span>

<span data-ttu-id="904e8-145">Brak</span><span class="sxs-lookup"><span data-stu-id="904e8-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="904e8-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="904e8-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="904e8-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="904e8-147">REST response</span></span>

<span data-ttu-id="904e8-148">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) .</span><span class="sxs-lookup"><span data-stu-id="904e8-148">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="904e8-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="904e8-149">Response success and error codes</span></span>

<span data-ttu-id="904e8-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="904e8-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="904e8-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="904e8-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="904e8-152">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="904e8-152">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="904e8-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="904e8-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
