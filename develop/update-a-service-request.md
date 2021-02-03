---
title: Aktualizowanie żądania obsługi
description: Jak zaktualizować istniejące żądanie obsługi klienta zgłoszone przez dostawcę rozwiązań w chmurze do firmy Microsoft w imieniu klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768369"
---
# <a name="update-a-service-request"></a><span data-ttu-id="fc39d-103">Aktualizowanie żądania obsługi</span><span class="sxs-lookup"><span data-stu-id="fc39d-103">Update a service request</span></span>

<span data-ttu-id="fc39d-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="fc39d-104">**Applies To**</span></span>

- <span data-ttu-id="fc39d-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="fc39d-105">Partner Center</span></span>
- <span data-ttu-id="fc39d-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="fc39d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fc39d-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fc39d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc39d-108">Jak zaktualizować istniejące żądanie obsługi klienta zgłoszone przez dostawcę rozwiązań w chmurze do firmy Microsoft w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="fc39d-108">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="fc39d-109">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="fc39d-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="fc39d-110">Następnie wybierz pozycję **Zarządzanie usługami** na lewym pasku bocznym.</span><span class="sxs-lookup"><span data-stu-id="fc39d-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="fc39d-111">W nagłówku **żądania pomocy technicznej** wybierz odpowiednie żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-111">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="fc39d-112">Aby zakończyć, wprowadź odpowiednie zmiany w żądaniu usługi, a następnie wybierz pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="fc39d-112">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc39d-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fc39d-113">Prerequisites</span></span>

- <span data-ttu-id="fc39d-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc39d-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc39d-115">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fc39d-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fc39d-116">Identyfikator żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-116">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="fc39d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="fc39d-117">C\#</span></span>

<span data-ttu-id="fc39d-118">Aby zaktualizować żądanie obsługi klienta, wywołaj metodę [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) z identyfikatorem żądania obsługi, aby zidentyfikować i zwrócić interfejs żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-118">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request id to identify and return the service request interface.</span></span> <span data-ttu-id="fc39d-119">Następnie Wywołaj metodę [**IServiceRequest. patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) lub [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) , aby zaktualizować żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-119">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="fc39d-120">Aby podać zaktualizowane wartości, Utwórz nowy, pusty obiekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) i ustaw tylko wartości właściwości, które chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="fc39d-120">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="fc39d-121">Następnie Przekaż ten obiekt w wywołaniu metody patch lub PatchAsync.</span><span class="sxs-lookup"><span data-stu-id="fc39d-121">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="fc39d-122">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc39d-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc39d-123">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="fc39d-123">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc39d-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="fc39d-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc39d-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="fc39d-125">Request syntax</span></span>

| <span data-ttu-id="fc39d-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="fc39d-126">Method</span></span>    | <span data-ttu-id="fc39d-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="fc39d-127">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc39d-128">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="fc39d-128">**PATCH**</span></span> | <span data-ttu-id="fc39d-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/servicerequests/{ServiceRequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="fc39d-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fc39d-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="fc39d-130">URI parameter</span></span>

<span data-ttu-id="fc39d-131">Aby zaktualizować żądanie obsługi, użyj następującego parametru identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="fc39d-131">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="fc39d-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="fc39d-132">Name</span></span>                  | <span data-ttu-id="fc39d-133">Typ</span><span class="sxs-lookup"><span data-stu-id="fc39d-133">Type</span></span>     | <span data-ttu-id="fc39d-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fc39d-134">Required</span></span> | <span data-ttu-id="fc39d-135">Opis</span><span class="sxs-lookup"><span data-stu-id="fc39d-135">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="fc39d-136">**Identyfikator żądania ServiceRequest**</span><span class="sxs-lookup"><span data-stu-id="fc39d-136">**servicerequest-id**</span></span> | <span data-ttu-id="fc39d-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="fc39d-137">**guid**</span></span> | <span data-ttu-id="fc39d-138">Y</span><span class="sxs-lookup"><span data-stu-id="fc39d-138">Y</span></span>        | <span data-ttu-id="fc39d-139">Identyfikator GUID, który identyfikuje żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-139">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc39d-140">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="fc39d-140">Request headers</span></span>

<span data-ttu-id="fc39d-141">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc39d-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc39d-142">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="fc39d-142">Request body</span></span>

<span data-ttu-id="fc39d-143">Treść żądania powinna zawierać zasób [ServiceRequest](service-request-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="fc39d-143">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="fc39d-144">Jedyne wymagane wartości to te, które mają zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="fc39d-144">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="fc39d-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="fc39d-145">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="fc39d-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="fc39d-146">REST response</span></span>

<span data-ttu-id="fc39d-147">Jeśli to się powiedzie, ta metoda zwraca zasób **żądania obsługi** ze zaktualizowanymi właściwościami w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fc39d-147">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc39d-148">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fc39d-148">Response success and error codes</span></span>

<span data-ttu-id="fc39d-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="fc39d-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc39d-150">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="fc39d-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc39d-151">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc39d-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc39d-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="fc39d-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
