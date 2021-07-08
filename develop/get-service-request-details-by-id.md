---
title: Uzyskiwanie szczegółów żądania obsługi według identyfikatora.
description: Jak pobrać szczegóły istniejącego żądania obsługi klienta według identyfikatora.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66488cf9592d630cb1f0237d379e8df5ead6a3a8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548774"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="52356-103">Pobieranie szczegółów żądania obsługi według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="52356-103">Get service request details by ID</span></span>

<span data-ttu-id="52356-104">**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="52356-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52356-105">Jak pobrać szczegóły istniejącego żądania obsługi klienta przy użyciu identyfikatora żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="52356-105">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52356-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52356-106">Prerequisites</span></span>

- <span data-ttu-id="52356-107">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="52356-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52356-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52356-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="52356-109">Identyfikator żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="52356-109">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="52356-110">C\#</span><span class="sxs-lookup"><span data-stu-id="52356-110">C\#</span></span>

<span data-ttu-id="52356-111">Aby pobrać szczegóły istniejącego żądania obsługi klienta, wywołaj metodę [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) i przekaż element [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) w celu zidentyfikowania i zwrócenia interfejsu do określonego obiektu [**ServiceRequest.**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest)</span><span class="sxs-lookup"><span data-stu-id="52356-111">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="52356-112">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="52356-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52356-113">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="52356-113">Request syntax</span></span>

| <span data-ttu-id="52356-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="52356-114">Method</span></span>    | <span data-ttu-id="52356-115">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="52356-115">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="52356-116">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="52356-116">**GET**</span></span> | <span data-ttu-id="52356-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{identyfikator-żądania-usługi} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="52356-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="52356-118">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="52356-118">URI parameter</span></span>

<span data-ttu-id="52356-119">Użyj następującego parametru URI, aby uzyskać określone żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="52356-119">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="52356-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="52356-120">Name</span></span>                  | <span data-ttu-id="52356-121">Typ</span><span class="sxs-lookup"><span data-stu-id="52356-121">Type</span></span>     | <span data-ttu-id="52356-122">Wymagane</span><span class="sxs-lookup"><span data-stu-id="52356-122">Required</span></span> | <span data-ttu-id="52356-123">Opis</span><span class="sxs-lookup"><span data-stu-id="52356-123">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="52356-124">**identyfikator servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="52356-124">**servicerequest-id**</span></span> | <span data-ttu-id="52356-125">**guid**</span><span class="sxs-lookup"><span data-stu-id="52356-125">**guid**</span></span> | <span data-ttu-id="52356-126">Y</span><span class="sxs-lookup"><span data-stu-id="52356-126">Y</span></span>        | <span data-ttu-id="52356-127">Identyfikator GUID, który identyfikuje żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="52356-127">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="52356-128">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="52356-128">Request headers</span></span>

<span data-ttu-id="52356-129">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="52356-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52356-130">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="52356-130">Request body</span></span>

<span data-ttu-id="52356-131">Brak.</span><span class="sxs-lookup"><span data-stu-id="52356-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52356-132">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="52356-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="52356-133">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="52356-133">REST response</span></span>

<span data-ttu-id="52356-134">W przypadku powodzenia ta metoda zwraca zasób **żądania obsługi** w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="52356-134">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52356-135">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52356-135">Response success and error codes</span></span>

<span data-ttu-id="52356-136">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="52356-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52356-137">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="52356-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52356-138">Aby uzyskać pełną listę, zobacz Partner Center REST Error Codes (Kody [błędów REST).](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="52356-138">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52356-139">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="52356-139">Response example</span></span>

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
