---
title: Pobieranie wszystkich żądań obsługi dla klienta
description: Pobiera wszystkie żądania obsługi klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768473"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="5b016-103">Pobieranie wszystkich żądań obsługi dla klienta</span><span class="sxs-lookup"><span data-stu-id="5b016-103">Get all service requests for a customer</span></span>

<span data-ttu-id="5b016-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="5b016-104">**Applies To**</span></span>

- <span data-ttu-id="5b016-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="5b016-105">Partner Center</span></span>
- <span data-ttu-id="5b016-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="5b016-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5b016-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5b016-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5b016-108">Pobiera wszystkie żądania obsługi klienta.</span><span class="sxs-lookup"><span data-stu-id="5b016-108">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="5b016-109">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="5b016-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="5b016-110">Następnie wybierz pozycję **Zarządzanie usługami** na lewym pasku bocznym.</span><span class="sxs-lookup"><span data-stu-id="5b016-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="5b016-111">Żądania obsługi klienta są wyświetlane w obszarze **bilety pomocy technicznej**.</span><span class="sxs-lookup"><span data-stu-id="5b016-111">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b016-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b016-112">Prerequisites</span></span>

- <span data-ttu-id="5b016-113">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5b016-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5b016-114">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b016-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5b016-115">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b016-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5b016-116">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="5b016-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5b016-117">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="5b016-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5b016-118">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="5b016-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5b016-119">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="5b016-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5b016-120">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b016-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5b016-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5b016-121">C\#</span></span>

<span data-ttu-id="5b016-122">Aby wyświetlić listę wszystkich żądań obsługi klienta, Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="5b016-122">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="5b016-123">Następnie Wywołaj Właściwość [**Servicerequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) , a następnie metodę [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .</span><span class="sxs-lookup"><span data-stu-id="5b016-123">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="5b016-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b016-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5b016-125">**Project**: PartnerCenterSDK. FeaturesSamples **Klasa**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="5b016-125">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b016-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="5b016-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b016-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="5b016-127">Request syntax</span></span>

| <span data-ttu-id="5b016-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="5b016-128">Method</span></span>  | <span data-ttu-id="5b016-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="5b016-129">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b016-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="5b016-130">**GET**</span></span> | <span data-ttu-id="5b016-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/servicerequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="5b016-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5b016-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="5b016-132">URI parameter</span></span>

<span data-ttu-id="5b016-133">Użyj następującego parametru zapytania, aby pobrać wszystkie żądania obsługi dla klienta.</span><span class="sxs-lookup"><span data-stu-id="5b016-133">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="5b016-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5b016-134">Name</span></span>                   | <span data-ttu-id="5b016-135">Typ</span><span class="sxs-lookup"><span data-stu-id="5b016-135">Type</span></span>     | <span data-ttu-id="5b016-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="5b016-136">Required</span></span> | <span data-ttu-id="5b016-137">Opis</span><span class="sxs-lookup"><span data-stu-id="5b016-137">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="5b016-138">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="5b016-138">**customer-tenant-id**</span></span> | <span data-ttu-id="5b016-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="5b016-139">**guid**</span></span> | <span data-ttu-id="5b016-140">Y</span><span class="sxs-lookup"><span data-stu-id="5b016-140">Y</span></span>        | <span data-ttu-id="5b016-141">Identyfikator GUID odpowiadający klientowi...</span><span class="sxs-lookup"><span data-stu-id="5b016-141">A GUID corresponding to the customer..</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5b016-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="5b016-142">Request headers</span></span>

<span data-ttu-id="5b016-143">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5b016-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b016-144">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="5b016-144">Request body</span></span>

<span data-ttu-id="5b016-145">Brak.</span><span class="sxs-lookup"><span data-stu-id="5b016-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b016-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="5b016-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="5b016-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="5b016-147">REST response</span></span>

<span data-ttu-id="5b016-148">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **żądania obsługi** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5b016-148">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b016-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5b016-149">Response success and error codes</span></span>

<span data-ttu-id="5b016-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="5b016-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b016-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="5b016-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b016-152">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5b016-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b016-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="5b016-153">Response example</span></span>

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
