---
title: Pobieranie wszystkich żądań obsługi dla klienta
description: Pobiera wszystkie żądania obsługi klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ffcbbb9cf14b1b2a5b3becab541d3042c3cad508
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760678"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="278ba-103">Pobieranie wszystkich żądań obsługi dla klienta</span><span class="sxs-lookup"><span data-stu-id="278ba-103">Get all service requests for a customer</span></span>

<span data-ttu-id="278ba-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="278ba-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="278ba-105">Pobiera wszystkie żądania obsługi klienta.</span><span class="sxs-lookup"><span data-stu-id="278ba-105">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="278ba-106">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="278ba-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="278ba-107">Następnie wybierz pozycję **Zarządzanie usługami** na lewym pasku bocznym.</span><span class="sxs-lookup"><span data-stu-id="278ba-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="278ba-108">Żądania obsługi klienta są wyświetlane w obszarze **Bilety pomocy technicznej.**</span><span class="sxs-lookup"><span data-stu-id="278ba-108">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="278ba-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="278ba-109">Prerequisites</span></span>

- <span data-ttu-id="278ba-110">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="278ba-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="278ba-111">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="278ba-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="278ba-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="278ba-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="278ba-113">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="278ba-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="278ba-114">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="278ba-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="278ba-115">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="278ba-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="278ba-116">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="278ba-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="278ba-117">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="278ba-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="278ba-118">C\#</span><span class="sxs-lookup"><span data-stu-id="278ba-118">C\#</span></span>

<span data-ttu-id="278ba-119">Aby wyświetlić listę wszystkich żądań obsługi klienta, użyj kolekcji **IAggregatePartner.Customers** i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="278ba-119">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="278ba-120">Następnie wywołaj [**właściwość ServiceRequests,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) a następnie metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) lub [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="278ba-120">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="278ba-121">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="278ba-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="278ba-122">**Project:** PartnerCenterSDK.FeaturesKlasa Samples: CustomerManagedServices.cs </span><span class="sxs-lookup"><span data-stu-id="278ba-122">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="278ba-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="278ba-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="278ba-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="278ba-124">Request syntax</span></span>

| <span data-ttu-id="278ba-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="278ba-125">Method</span></span>  | <span data-ttu-id="278ba-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="278ba-126">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="278ba-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="278ba-127">**GET**</span></span> | <span data-ttu-id="278ba-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="278ba-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="278ba-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="278ba-129">URI parameter</span></span>

<span data-ttu-id="278ba-130">Użyj następującego parametru zapytania, aby pobrać wszystkie żądania obsługi dla klienta.</span><span class="sxs-lookup"><span data-stu-id="278ba-130">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="278ba-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="278ba-131">Name</span></span>                   | <span data-ttu-id="278ba-132">Typ</span><span class="sxs-lookup"><span data-stu-id="278ba-132">Type</span></span>     | <span data-ttu-id="278ba-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="278ba-133">Required</span></span> | <span data-ttu-id="278ba-134">Opis</span><span class="sxs-lookup"><span data-stu-id="278ba-134">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="278ba-135">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="278ba-135">**customer-tenant-id**</span></span> | <span data-ttu-id="278ba-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="278ba-136">**guid**</span></span> | <span data-ttu-id="278ba-137">Y</span><span class="sxs-lookup"><span data-stu-id="278ba-137">Y</span></span>        | <span data-ttu-id="278ba-138">Identyfikator GUID odpowiadający klientowi.</span><span class="sxs-lookup"><span data-stu-id="278ba-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="278ba-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="278ba-139">Request headers</span></span>

<span data-ttu-id="278ba-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="278ba-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="278ba-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="278ba-141">Request body</span></span>

<span data-ttu-id="278ba-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="278ba-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="278ba-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="278ba-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="278ba-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="278ba-144">REST response</span></span>

<span data-ttu-id="278ba-145">W przypadku powodzenia ta metoda zwraca kolekcję zasobów żądania **obsługi** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="278ba-145">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="278ba-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="278ba-146">Response success and error codes</span></span>

<span data-ttu-id="278ba-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="278ba-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="278ba-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="278ba-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="278ba-149">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="278ba-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="278ba-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="278ba-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
