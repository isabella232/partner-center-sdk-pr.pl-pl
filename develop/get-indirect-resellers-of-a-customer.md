---
title: Pobieranie odsprzedawców pośrednich klienta
description: Jak uzyskać listę pośrednich odsprzedawcaów, które mają relację z określonym klientem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768334"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="0f444-103">Pobieranie odsprzedawców pośrednich klienta</span><span class="sxs-lookup"><span data-stu-id="0f444-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="0f444-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="0f444-104">**Applies To**</span></span>

- <span data-ttu-id="0f444-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0f444-105">Partner Center</span></span>

<span data-ttu-id="0f444-106">Jak uzyskać listę pośrednich odsprzedawcaów, które mają relację z określonym klientem.</span><span class="sxs-lookup"><span data-stu-id="0f444-106">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f444-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f444-107">Prerequisites</span></span>

- <span data-ttu-id="0f444-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0f444-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f444-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f444-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0f444-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f444-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0f444-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="0f444-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0f444-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="0f444-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0f444-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="0f444-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0f444-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="0f444-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0f444-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f444-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0f444-116">C\#</span><span class="sxs-lookup"><span data-stu-id="0f444-116">C\#</span></span>

<span data-ttu-id="0f444-117">Aby pobrać listę pośrednich odsprzedawcaów, z którymi określony klient ma relację, należy najpierw uzyskać interfejs do operacji zbierania danych klienta dla określonego klienta z właściwości [**partnerOperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) , podając identyfikator klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="0f444-117">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="0f444-118">Następnie Wywołaj [**relacje. Pobierz**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) lub [**Pobierz metodę \_ asynchroniczną**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) , aby uzyskać listę pośrednich odsprzedawcaów.</span><span class="sxs-lookup"><span data-stu-id="0f444-118">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="0f444-119">**Przykład**:**projekt** [aplikacji testowej konsoli](console-test-app.md): **Klasa** przykładów zestawu SDK Centrum partnerskiego: GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="0f444-119">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0f444-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0f444-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f444-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0f444-121">Request syntax</span></span>

| <span data-ttu-id="0f444-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="0f444-122">Method</span></span>  | <span data-ttu-id="0f444-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0f444-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f444-124">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0f444-124">**GET**</span></span> | <span data-ttu-id="0f444-125">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/Relationships http/1.1</span><span class="sxs-lookup"><span data-stu-id="0f444-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0f444-126">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0f444-126">URI parameter</span></span>

<span data-ttu-id="0f444-127">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="0f444-127">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="0f444-128">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0f444-128">Name</span></span>        | <span data-ttu-id="0f444-129">Typ</span><span class="sxs-lookup"><span data-stu-id="0f444-129">Type</span></span>   | <span data-ttu-id="0f444-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0f444-130">Required</span></span> | <span data-ttu-id="0f444-131">Opis</span><span class="sxs-lookup"><span data-stu-id="0f444-131">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="0f444-132">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="0f444-132">customer-id</span></span> | <span data-ttu-id="0f444-133">ciąg</span><span class="sxs-lookup"><span data-stu-id="0f444-133">string</span></span> | <span data-ttu-id="0f444-134">Tak</span><span class="sxs-lookup"><span data-stu-id="0f444-134">Yes</span></span>      | <span data-ttu-id="0f444-135">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="0f444-135">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f444-136">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0f444-136">Request headers</span></span>

<span data-ttu-id="0f444-137">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0f444-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f444-138">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0f444-138">Request body</span></span>

<span data-ttu-id="0f444-139">Brak.</span><span class="sxs-lookup"><span data-stu-id="0f444-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0f444-140">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0f444-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0f444-141">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0f444-141">REST response</span></span>

<span data-ttu-id="0f444-142">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerRelationship](relationships-resources.md) , aby zidentyfikować odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="0f444-142">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f444-143">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0f444-143">Response success and error codes</span></span>

<span data-ttu-id="0f444-144">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0f444-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f444-145">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0f444-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0f444-146">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f444-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f444-147">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0f444-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
