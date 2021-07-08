---
title: Pobieranie listy zasad klienta
description: Pobieranie kolekcji zasad konfiguracji określonego klienta.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874588"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="8b33e-103">Pobieranie listy zasad klienta</span><span class="sxs-lookup"><span data-stu-id="8b33e-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="8b33e-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="8b33e-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="8b33e-105">W tym artykule opisano sposób pobierania kolekcji zasad konfiguracji określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="8b33e-105">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b33e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b33e-106">Prerequisites</span></span>

- <span data-ttu-id="8b33e-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8b33e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b33e-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b33e-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8b33e-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b33e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8b33e-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="8b33e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8b33e-111">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="8b33e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8b33e-112">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="8b33e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8b33e-113">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="8b33e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8b33e-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8b33e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="8b33e-115">C\#</span><span class="sxs-lookup"><span data-stu-id="8b33e-115">C\#</span></span>

<span data-ttu-id="8b33e-116">Aby uzyskać listę wszystkich zasad klienta:</span><span class="sxs-lookup"><span data-stu-id="8b33e-116">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="8b33e-117">Wywołaj [**metodę IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby pobrać interfejs do operacji na określonym kliencie.</span><span class="sxs-lookup"><span data-stu-id="8b33e-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="8b33e-118">Pobierz właściwość [**ConfigurationPolicies,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) aby uzyskać interfejs operacji zbierania zasad konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8b33e-118">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="8b33e-119">Wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) aby pobrać kolekcję zasad.</span><span class="sxs-lookup"><span data-stu-id="8b33e-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="8b33e-120">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="8b33e-120">For an example, see the following:</span></span>

- <span data-ttu-id="8b33e-121">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="8b33e-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="8b33e-122">Project: **zestaw SDK Centrum partnerskiego przykłady**</span><span class="sxs-lookup"><span data-stu-id="8b33e-122">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="8b33e-123">Klasa: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="8b33e-123">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="8b33e-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="8b33e-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8b33e-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="8b33e-125">Request syntax</span></span>

| <span data-ttu-id="8b33e-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="8b33e-126">Method</span></span>  | <span data-ttu-id="8b33e-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="8b33e-127">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b33e-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="8b33e-128">**GET**</span></span> | <span data-ttu-id="8b33e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8b33e-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="8b33e-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="8b33e-130">URI parameter</span></span>

<span data-ttu-id="8b33e-131">Podczas tworzenia żądania użyj następującego parametru ścieżki:</span><span class="sxs-lookup"><span data-stu-id="8b33e-131">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="8b33e-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8b33e-132">Name</span></span>        | <span data-ttu-id="8b33e-133">Typ</span><span class="sxs-lookup"><span data-stu-id="8b33e-133">Type</span></span>   | <span data-ttu-id="8b33e-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8b33e-134">Required</span></span> | <span data-ttu-id="8b33e-135">Opis</span><span class="sxs-lookup"><span data-stu-id="8b33e-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="8b33e-136">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="8b33e-136">customer-id</span></span> | <span data-ttu-id="8b33e-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="8b33e-137">string</span></span> | <span data-ttu-id="8b33e-138">Tak</span><span class="sxs-lookup"><span data-stu-id="8b33e-138">Yes</span></span>      | <span data-ttu-id="8b33e-139">Ciąg w formacie identyfikatora GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="8b33e-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8b33e-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="8b33e-140">Request headers</span></span>

<span data-ttu-id="8b33e-141">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8b33e-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8b33e-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="8b33e-142">Request body</span></span>

<span data-ttu-id="8b33e-143">Brak</span><span class="sxs-lookup"><span data-stu-id="8b33e-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="8b33e-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="8b33e-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="8b33e-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="8b33e-145">REST response</span></span>

<span data-ttu-id="8b33e-146">W przypadku powodzenia treść odpowiedzi zawiera kolekcję zasobów [ConfigurationPolicy.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="8b33e-146">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8b33e-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b33e-147">Response success and error codes</span></span>

<span data-ttu-id="8b33e-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="8b33e-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8b33e-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="8b33e-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8b33e-150">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8b33e-150">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8b33e-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8b33e-151">Response example</span></span>

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
