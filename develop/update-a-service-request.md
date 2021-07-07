---
title: Aktualizowanie żądania obsługi
description: Jak zaktualizować istniejące żądanie obsługi klienta, które Dostawca rozwiązań w chmurze do firmy Microsoft w imieniu klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: efa7b2a98b6f95a763ca6e3811c43cc655c18e2b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530093"
---
# <a name="update-a-service-request"></a><span data-ttu-id="9bd0f-103">Aktualizowanie żądania obsługi</span><span class="sxs-lookup"><span data-stu-id="9bd0f-103">Update a service request</span></span>

<span data-ttu-id="9bd0f-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9bd0f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9bd0f-105">Jak zaktualizować istniejące żądanie obsługi klienta, które Dostawca rozwiązań w chmurze do firmy Microsoft w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-105">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="9bd0f-106">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="9bd0f-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="9bd0f-107">Następnie wybierz pozycję **Zarządzanie usługami** na lewym pasku bocznym.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="9bd0f-108">W **nagłówku Żądania** pomocy technicznej wybierz odpowiednie żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-108">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="9bd0f-109">Aby zakończyć, należy wprowadzić żądane zmiany w żądaniu obsługi, a następnie wybrać pozycję **Prześlij.**</span><span class="sxs-lookup"><span data-stu-id="9bd0f-109">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bd0f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9bd0f-110">Prerequisites</span></span>

- <span data-ttu-id="9bd0f-111">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9bd0f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9bd0f-112">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9bd0f-113">Identyfikator żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-113">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="9bd0f-114">C\#</span><span class="sxs-lookup"><span data-stu-id="9bd0f-114">C\#</span></span>

<span data-ttu-id="9bd0f-115">Aby zaktualizować żądanie obsługi klienta, wywołaj metodę [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) z identyfikatorem żądania obsługi, aby zidentyfikować i zwrócić interfejs żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-115">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request ID to identify and return the service request interface.</span></span> <span data-ttu-id="9bd0f-116">Następnie wywołaj [**metodę IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) lub [**PatchAsync,**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) aby zaktualizować żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-116">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="9bd0f-117">Aby podać zaktualizowane wartości, utwórz nowy, pusty obiekt [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) i ustaw tylko wartości właściwości, które chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-117">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="9bd0f-118">Następnie przekaż ten obiekt w wywołaniu metody Patch lub PatchAsync.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-118">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="9bd0f-119">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9bd0f-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9bd0f-120">**Project:** zestaw SDK Centrum partnerskiego Samples Class : UpdatePartnerServiceRequest.cs **(Klasa przykładów zestaw SDK Centrum partnerskiego:** UpdatePartnerServiceRequest.cs)</span><span class="sxs-lookup"><span data-stu-id="9bd0f-120">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9bd0f-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9bd0f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9bd0f-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9bd0f-122">Request syntax</span></span>

| <span data-ttu-id="9bd0f-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="9bd0f-123">Method</span></span>    | <span data-ttu-id="9bd0f-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9bd0f-124">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="9bd0f-125">**Patch**</span><span class="sxs-lookup"><span data-stu-id="9bd0f-125">**PATCH**</span></span> | <span data-ttu-id="9bd0f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{identyfikator-żądania-usługi} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9bd0f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9bd0f-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9bd0f-127">URI parameter</span></span>

<span data-ttu-id="9bd0f-128">Użyj następującego parametru URI, aby zaktualizować żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-128">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="9bd0f-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9bd0f-129">Name</span></span>                  | <span data-ttu-id="9bd0f-130">Typ</span><span class="sxs-lookup"><span data-stu-id="9bd0f-130">Type</span></span>     | <span data-ttu-id="9bd0f-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9bd0f-131">Required</span></span> | <span data-ttu-id="9bd0f-132">Opis</span><span class="sxs-lookup"><span data-stu-id="9bd0f-132">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="9bd0f-133">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="9bd0f-133">**servicerequest-id**</span></span> | <span data-ttu-id="9bd0f-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="9bd0f-134">**guid**</span></span> | <span data-ttu-id="9bd0f-135">Y</span><span class="sxs-lookup"><span data-stu-id="9bd0f-135">Y</span></span>        | <span data-ttu-id="9bd0f-136">Identyfikator GUID, który identyfikuje żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-136">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9bd0f-137">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9bd0f-137">Request headers</span></span>

<span data-ttu-id="9bd0f-138">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9bd0f-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9bd0f-139">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9bd0f-139">Request body</span></span>

<span data-ttu-id="9bd0f-140">Treść żądania powinna zawierać [zasób ServiceRequest.](service-request-resources.md)</span><span class="sxs-lookup"><span data-stu-id="9bd0f-140">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="9bd0f-141">Jedynymi wymaganymi wartościami są te, które mają zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-141">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="9bd0f-142">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9bd0f-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9bd0f-143">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9bd0f-143">REST response</span></span>

<span data-ttu-id="9bd0f-144">W przypadku powodzenia ta metoda zwraca zasób **żądania obsługi** ze zaktualizowanymi właściwościami w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-144">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9bd0f-145">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9bd0f-145">Response success and error codes</span></span>

<span data-ttu-id="9bd0f-146">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9bd0f-147">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9bd0f-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9bd0f-148">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9bd0f-148">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9bd0f-149">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9bd0f-149">Response example</span></span>

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
