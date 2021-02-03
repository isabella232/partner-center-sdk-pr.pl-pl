---
title: Pobierz szczegóły żądania obsługi według identyfikatora.
description: Jak pobrać szczegóły istniejącego żądania obsługi klienta według identyfikatora.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c79fd3f5e5609a1893891e9b2a8078f8678497b3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768474"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="3f450-103">Pobieranie szczegółów żądania obsługi według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="3f450-103">Get service request details by ID</span></span>

<span data-ttu-id="3f450-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="3f450-104">**Applies To**</span></span>

- <span data-ttu-id="3f450-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="3f450-105">Partner Center</span></span>
- <span data-ttu-id="3f450-106">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="3f450-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3f450-107">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3f450-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3f450-108">Jak pobrać szczegóły istniejącego żądania obsługi klienta przy użyciu identyfikatora żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="3f450-108">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f450-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3f450-109">Prerequisites</span></span>

- <span data-ttu-id="3f450-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3f450-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f450-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3f450-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3f450-112">Identyfikator żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="3f450-112">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="3f450-113">C\#</span><span class="sxs-lookup"><span data-stu-id="3f450-113">C\#</span></span>

<span data-ttu-id="3f450-114">Aby pobrać szczegóły istniejącego żądania obsługi klienta, wywołaj metodę [**IServiceRequestCollection. ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) i przekaż element [**ServiceRequest.ID**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) , aby zidentyfikować i zwrócić interfejs do określonego obiektu [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) .</span><span class="sxs-lookup"><span data-stu-id="3f450-114">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a><span data-ttu-id="3f450-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="3f450-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f450-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="3f450-116">Request syntax</span></span>

| <span data-ttu-id="3f450-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="3f450-117">Method</span></span>    | <span data-ttu-id="3f450-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="3f450-118">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="3f450-119">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="3f450-119">**GET**</span></span> | <span data-ttu-id="3f450-120">[*{baseURL}*](partner-center-rest-urls.md)/V1/servicerequests/{ServiceRequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3f450-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="3f450-121">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="3f450-121">URI parameter</span></span>

<span data-ttu-id="3f450-122">Użyj następującego parametru identyfikatora URI, aby uzyskać określone żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="3f450-122">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="3f450-123">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3f450-123">Name</span></span>                  | <span data-ttu-id="3f450-124">Typ</span><span class="sxs-lookup"><span data-stu-id="3f450-124">Type</span></span>     | <span data-ttu-id="3f450-125">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3f450-125">Required</span></span> | <span data-ttu-id="3f450-126">Opis</span><span class="sxs-lookup"><span data-stu-id="3f450-126">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="3f450-127">**Identyfikator żądania ServiceRequest**</span><span class="sxs-lookup"><span data-stu-id="3f450-127">**servicerequest-id**</span></span> | <span data-ttu-id="3f450-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="3f450-128">**guid**</span></span> | <span data-ttu-id="3f450-129">Y</span><span class="sxs-lookup"><span data-stu-id="3f450-129">Y</span></span>        | <span data-ttu-id="3f450-130">Identyfikator GUID, który identyfikuje żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="3f450-130">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3f450-131">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="3f450-131">Request headers</span></span>

<span data-ttu-id="3f450-132">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3f450-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f450-133">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="3f450-133">Request body</span></span>

<span data-ttu-id="3f450-134">Brak.</span><span class="sxs-lookup"><span data-stu-id="3f450-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3f450-135">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="3f450-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3f450-136">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="3f450-136">REST response</span></span>

<span data-ttu-id="3f450-137">Jeśli to się powiedzie, ta metoda zwraca zasób **żądania obsługi** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3f450-137">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f450-138">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3f450-138">Response success and error codes</span></span>

<span data-ttu-id="3f450-139">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="3f450-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f450-140">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="3f450-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f450-141">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3f450-141">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f450-142">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3f450-142">Response example</span></span>

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
