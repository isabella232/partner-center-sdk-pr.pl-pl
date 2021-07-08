---
title: Pobieranie listy klientów
description: Jak uzyskać kolekcję zasobów reprezentujących wszystkich klientów partnera.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874350"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="47ef0-103">Pobieranie listy klientów</span><span class="sxs-lookup"><span data-stu-id="47ef0-103">Get a list of customers</span></span>

<span data-ttu-id="47ef0-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="47ef0-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="47ef0-105">W tym artykule opisano sposób pobierania kolekcji zasobów, które reprezentują wszystkich klientów partnera.</span><span class="sxs-lookup"><span data-stu-id="47ef0-105">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="47ef0-106">Tę operację można również wykonać na pulpicie nawigacyjnym Partner Center nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="47ef0-106">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="47ef0-107">Na stronie głównej w obszarze **Zarządzanie klientami** wybierz pozycję **Wyświetl klientów.**</span><span class="sxs-lookup"><span data-stu-id="47ef0-107">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="47ef0-108">Lub na pasku bocznym wybierz pozycję **Klienci**.</span><span class="sxs-lookup"><span data-stu-id="47ef0-108">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47ef0-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47ef0-109">Prerequisites</span></span>

- <span data-ttu-id="47ef0-110">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="47ef0-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="47ef0-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47ef0-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="47ef0-112">C\#</span><span class="sxs-lookup"><span data-stu-id="47ef0-112">C\#</span></span>

<span data-ttu-id="47ef0-113">Aby uzyskać listę wszystkich klientów:</span><span class="sxs-lookup"><span data-stu-id="47ef0-113">To get a list of all customers:</span></span>

1. <span data-ttu-id="47ef0-114">Użyj [**kolekcji IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) aby utworzyć **obiekt IPartner.**</span><span class="sxs-lookup"><span data-stu-id="47ef0-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="47ef0-115">Pobierz listę klientów przy użyciu [**metod Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) lub [**QueryAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="47ef0-115">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="47ef0-116">(Aby uzyskać instrukcje dotyczące tworzenia zapytania, zobacz [**klasę QueryFactory).**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory)</span><span class="sxs-lookup"><span data-stu-id="47ef0-116">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="47ef0-117">Przykład można znaleźć w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="47ef0-117">For an example, see the following:</span></span>

- <span data-ttu-id="47ef0-118">Przykład: [aplikacja testowa konsoli](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="47ef0-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="47ef0-119">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="47ef0-119">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="47ef0-120">Klasa: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="47ef0-120">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="47ef0-121">Java</span><span class="sxs-lookup"><span data-stu-id="47ef0-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="47ef0-122">Aby uzyskać listę wszystkich klientów:</span><span class="sxs-lookup"><span data-stu-id="47ef0-122">To get a list of all customers:</span></span>

1. <span data-ttu-id="47ef0-123">Użyj funkcji [**IAggregatePartner.getCustomers**], aby uzyskać odwołanie do operacji klienta.</span><span class="sxs-lookup"><span data-stu-id="47ef0-123">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="47ef0-124">Pobierz listę klientów przy użyciu **funkcji query().**</span><span class="sxs-lookup"><span data-stu-id="47ef0-124">Retrieve the customer list using the **query()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="47ef0-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47ef0-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="47ef0-126">Wykonaj polecenie [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) bez parametrów, aby uzyskać pełną listę klientów.</span><span class="sxs-lookup"><span data-stu-id="47ef0-126">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="47ef0-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="47ef0-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="47ef0-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="47ef0-128">Request syntax</span></span>

| <span data-ttu-id="47ef0-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="47ef0-129">Method</span></span>  | <span data-ttu-id="47ef0-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="47ef0-130">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="47ef0-131">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="47ef0-131">**GET**</span></span> | <span data-ttu-id="47ef0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="47ef0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="47ef0-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="47ef0-133">URI parameter</span></span>

<span data-ttu-id="47ef0-134">Użyj następującego parametru zapytania, aby uzyskać listę klientów.</span><span class="sxs-lookup"><span data-stu-id="47ef0-134">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="47ef0-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="47ef0-135">Name</span></span>     | <span data-ttu-id="47ef0-136">Typ</span><span class="sxs-lookup"><span data-stu-id="47ef0-136">Type</span></span>    | <span data-ttu-id="47ef0-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="47ef0-137">Required</span></span> | <span data-ttu-id="47ef0-138">Opis</span><span class="sxs-lookup"><span data-stu-id="47ef0-138">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="47ef0-139">**Rozmiar**</span><span class="sxs-lookup"><span data-stu-id="47ef0-139">**size**</span></span> | <span data-ttu-id="47ef0-140">**int**</span><span class="sxs-lookup"><span data-stu-id="47ef0-140">**int**</span></span> | <span data-ttu-id="47ef0-141">Y</span><span class="sxs-lookup"><span data-stu-id="47ef0-141">Y</span></span>        | <span data-ttu-id="47ef0-142">Liczba wyników, które mają być wyświetlane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="47ef0-142">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="47ef0-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="47ef0-143">Request headers</span></span>

<span data-ttu-id="47ef0-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="47ef0-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="47ef0-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="47ef0-145">Request body</span></span>

<span data-ttu-id="47ef0-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="47ef0-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="47ef0-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="47ef0-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="47ef0-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="47ef0-148">REST response</span></span>

<span data-ttu-id="47ef0-149">W przypadku powodzenia ta metoda zwraca kolekcję [zasobów](customer-resources.md#customer) klienta w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="47ef0-149">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="47ef0-150">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="47ef0-150">Response success and error codes</span></span>

<span data-ttu-id="47ef0-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="47ef0-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="47ef0-152">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="47ef0-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="47ef0-153">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="47ef0-153">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="47ef0-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="47ef0-154">Response example</span></span>

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
