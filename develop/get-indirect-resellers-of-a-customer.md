---
title: Pobieranie odsprzedawców pośrednich klienta
description: Jak uzyskać listę odsprzedawców pośrednich, którzy mają relację z określonym klientem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446245"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="cb4b4-103">Pobieranie odsprzedawców pośrednich klienta</span><span class="sxs-lookup"><span data-stu-id="cb4b4-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="cb4b4-104">Jak uzyskać listę odsprzedawców pośrednich, którzy mają relację z określonym klientem.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-104">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb4b4-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb4b4-105">Prerequisites</span></span>

- <span data-ttu-id="cb4b4-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cb4b4-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb4b4-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="cb4b4-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb4b4-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cb4b4-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="cb4b4-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cb4b4-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="cb4b4-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cb4b4-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cb4b4-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cb4b4-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cb4b4-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="cb4b4-114">C\#</span><span class="sxs-lookup"><span data-stu-id="cb4b4-114">C\#</span></span>

<span data-ttu-id="cb4b4-115">Aby pobrać listę odsprzedawców pośrednich, z którymi określony klient ma relację, najpierw uzyskaj interfejs operacji zbierania danych klienta dla określonego klienta z właściwości [**partnerOperations.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) podając identyfikator klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-115">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="cb4b4-116">Następnie wywołaj [**metodę Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) lub [**Get \_ Async,**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) aby uzyskać listę odsprzedawców pośrednich.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-116">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="cb4b4-117">**Przykład:** [Aplikacja testowa konsoli](console-test-app.md)**Project**: zestaw SDK Centrum partnerskiego Samples **Class**: GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="cb4b4-117">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cb4b4-118">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="cb4b4-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb4b4-119">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="cb4b4-119">Request syntax</span></span>

| <span data-ttu-id="cb4b4-120">Metoda</span><span class="sxs-lookup"><span data-stu-id="cb4b4-120">Method</span></span>  | <span data-ttu-id="cb4b4-121">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="cb4b4-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb4b4-122">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="cb4b4-122">**GET**</span></span> | <span data-ttu-id="cb4b4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/relationships HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cb4b4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cb4b4-124">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="cb4b4-124">URI parameter</span></span>

<span data-ttu-id="cb4b4-125">Użyj następującego parametru ścieżki, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-125">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="cb4b4-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cb4b4-126">Name</span></span>        | <span data-ttu-id="cb4b4-127">Typ</span><span class="sxs-lookup"><span data-stu-id="cb4b4-127">Type</span></span>   | <span data-ttu-id="cb4b4-128">Wymagane</span><span class="sxs-lookup"><span data-stu-id="cb4b4-128">Required</span></span> | <span data-ttu-id="cb4b4-129">Opis</span><span class="sxs-lookup"><span data-stu-id="cb4b4-129">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="cb4b4-130">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="cb4b4-130">customer-id</span></span> | <span data-ttu-id="cb4b4-131">ciąg</span><span class="sxs-lookup"><span data-stu-id="cb4b4-131">string</span></span> | <span data-ttu-id="cb4b4-132">Tak</span><span class="sxs-lookup"><span data-stu-id="cb4b4-132">Yes</span></span>      | <span data-ttu-id="cb4b4-133">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-133">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cb4b4-134">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="cb4b4-134">Request headers</span></span>

<span data-ttu-id="cb4b4-135">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cb4b4-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb4b4-136">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="cb4b4-136">Request body</span></span>

<span data-ttu-id="cb4b4-137">Brak.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cb4b4-138">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="cb4b4-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="cb4b4-139">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="cb4b4-139">REST response</span></span>

<span data-ttu-id="cb4b4-140">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [PartnerRelationship](relationships-resources.md) w celu zidentyfikowania odsprzedawców.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-140">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb4b4-141">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cb4b4-141">Response success and error codes</span></span>

<span data-ttu-id="cb4b4-142">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cb4b4-143">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="cb4b4-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb4b4-144">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cb4b4-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="cb4b4-145">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="cb4b4-145">Response example</span></span>

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
