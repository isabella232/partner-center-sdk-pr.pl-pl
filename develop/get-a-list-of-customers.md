---
title: Pobieranie listy klientów
description: Jak uzyskać zbiór zasobów reprezentujących wszystkich klientów partnerskich.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768294"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="92539-103">Pobieranie listy klientów</span><span class="sxs-lookup"><span data-stu-id="92539-103">Get a list of customers</span></span>

<span data-ttu-id="92539-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="92539-104">**Applies to:**</span></span>

- <span data-ttu-id="92539-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="92539-105">Partner Center</span></span>
- <span data-ttu-id="92539-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="92539-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="92539-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="92539-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="92539-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="92539-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="92539-109">W tym artykule opisano, jak uzyskać kolekcję zasobów reprezentujących wszystkich klientów partnerskich.</span><span class="sxs-lookup"><span data-stu-id="92539-109">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="92539-110">Tę operację można także wykonać na pulpicie nawigacyjnym Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="92539-110">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="92539-111">Na stronie głównej w obszarze **Zarządzanie klientami** wybierz pozycję **Wyświetl klientów**.</span><span class="sxs-lookup"><span data-stu-id="92539-111">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="92539-112">Na pasku bocznym wybierz pozycję **klienci**.</span><span class="sxs-lookup"><span data-stu-id="92539-112">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92539-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92539-113">Prerequisites</span></span>

- <span data-ttu-id="92539-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="92539-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="92539-115">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92539-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="92539-116">C\#</span><span class="sxs-lookup"><span data-stu-id="92539-116">C\#</span></span>

<span data-ttu-id="92539-117">Aby uzyskać listę wszystkich klientów:</span><span class="sxs-lookup"><span data-stu-id="92539-117">To get a list of all customers:</span></span>

1. <span data-ttu-id="92539-118">Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , aby utworzyć obiekt **IPartner** .</span><span class="sxs-lookup"><span data-stu-id="92539-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="92539-119">Pobierz listę klientów przy użyciu metod [**Query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .</span><span class="sxs-lookup"><span data-stu-id="92539-119">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="92539-120">(Aby uzyskać instrukcje dotyczące tworzenia zapytania, zobacz Klasa [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) ).</span><span class="sxs-lookup"><span data-stu-id="92539-120">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="92539-121">Aby zapoznać się z przykładem, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="92539-121">For an example, see the following:</span></span>

- <span data-ttu-id="92539-122">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="92539-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="92539-123">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="92539-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="92539-124">Klasa: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="92539-124">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="92539-125">Java</span><span class="sxs-lookup"><span data-stu-id="92539-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="92539-126">Aby uzyskać listę wszystkich klientów:</span><span class="sxs-lookup"><span data-stu-id="92539-126">To get a list of all customers:</span></span>

1. <span data-ttu-id="92539-127">Użyj funkcji [**IAggregatePartner. GetCustomers**], aby uzyskać odwołanie do operacji klienta.</span><span class="sxs-lookup"><span data-stu-id="92539-127">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="92539-128">Pobierz listę klientów przy użyciu funkcji **Query ()** .</span><span class="sxs-lookup"><span data-stu-id="92539-128">Retrieve the customer list using the **query()** function.</span></span>

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="92539-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92539-129">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="92539-130">Wykonaj polecenie [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) bez parametrów, aby uzyskać pełną listę klientów.</span><span class="sxs-lookup"><span data-stu-id="92539-130">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="92539-131">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="92539-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="92539-132">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="92539-132">Request syntax</span></span>

| <span data-ttu-id="92539-133">Metoda</span><span class="sxs-lookup"><span data-stu-id="92539-133">Method</span></span>  | <span data-ttu-id="92539-134">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="92539-134">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="92539-135">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="92539-135">**GET**</span></span> | <span data-ttu-id="92539-136">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers? size = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="92539-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="92539-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="92539-137">URI parameter</span></span>

<span data-ttu-id="92539-138">Użyj następującego parametru zapytania, aby uzyskać listę klientów.</span><span class="sxs-lookup"><span data-stu-id="92539-138">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="92539-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="92539-139">Name</span></span>     | <span data-ttu-id="92539-140">Typ</span><span class="sxs-lookup"><span data-stu-id="92539-140">Type</span></span>    | <span data-ttu-id="92539-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="92539-141">Required</span></span> | <span data-ttu-id="92539-142">Opis</span><span class="sxs-lookup"><span data-stu-id="92539-142">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="92539-143">**zmienia**</span><span class="sxs-lookup"><span data-stu-id="92539-143">**size**</span></span> | <span data-ttu-id="92539-144">**int**</span><span class="sxs-lookup"><span data-stu-id="92539-144">**int**</span></span> | <span data-ttu-id="92539-145">Y</span><span class="sxs-lookup"><span data-stu-id="92539-145">Y</span></span>        | <span data-ttu-id="92539-146">Liczba wyników do wyświetlenia w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="92539-146">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="92539-147">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="92539-147">Request headers</span></span>

<span data-ttu-id="92539-148">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="92539-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="92539-149">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="92539-149">Request body</span></span>

<span data-ttu-id="92539-150">Brak.</span><span class="sxs-lookup"><span data-stu-id="92539-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="92539-151">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="92539-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="92539-152">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="92539-152">REST response</span></span>

<span data-ttu-id="92539-153">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [klienta](customer-resources.md#customer) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="92539-153">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="92539-154">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="92539-154">Response success and error codes</span></span>

<span data-ttu-id="92539-155">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="92539-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="92539-156">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="92539-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="92539-157">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="92539-157">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="92539-158">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="92539-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
