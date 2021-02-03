---
title: Pobieranie klienta według identyfikatora
description: Pobiera zasób klienta odpowiadający IDENTYFIKATORowi klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: dd4301dbb6f749b675fe624daf7f63751806f856
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768126"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="7b34f-103">Pobieranie klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="7b34f-103">Get a customer by ID</span></span>

<span data-ttu-id="7b34f-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="7b34f-104">**Applies To**</span></span>

- <span data-ttu-id="7b34f-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="7b34f-105">Partner Center</span></span>
- <span data-ttu-id="7b34f-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="7b34f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7b34f-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="7b34f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7b34f-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7b34f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7b34f-109">Pobiera zasób **klienta** ODPOWIADAjący identyfikatorowi klienta.</span><span class="sxs-lookup"><span data-stu-id="7b34f-109">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b34f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b34f-110">Prerequisites</span></span>

- <span data-ttu-id="7b34f-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7b34f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b34f-112">Ten scenariusz obsługuje poświadczenia aplikacji i użytkownika lub uwierzytelnianie tylko aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b34f-112">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="7b34f-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b34f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7b34f-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="7b34f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7b34f-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="7b34f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7b34f-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="7b34f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7b34f-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="7b34f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7b34f-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b34f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7b34f-119">C\#</span><span class="sxs-lookup"><span data-stu-id="7b34f-119">C\#</span></span>

<span data-ttu-id="7b34f-120">Aby uzyskać klienta według identyfikatora, Użyj kolekcji [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , a następnie wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) .</span><span class="sxs-lookup"><span data-stu-id="7b34f-120">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="7b34f-121">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b34f-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7b34f-122">**Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="7b34f-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="7b34f-123">Java</span><span class="sxs-lookup"><span data-stu-id="7b34f-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="7b34f-124">Aby uzyskać klienta według identyfikatora, użyj funkcji **IAggregatePartner. GetCustomers** , wywołaj funkcję **byId ()** , a następnie wywołaj funkcję **Get ()** .</span><span class="sxs-lookup"><span data-stu-id="7b34f-124">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="7b34f-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b34f-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7b34f-126">Aby uzyskać klienta według identyfikatora, należy wykonać polecenie [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) i określić parametr **CustomerID** .</span><span class="sxs-lookup"><span data-stu-id="7b34f-126">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="7b34f-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="7b34f-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b34f-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="7b34f-128">Request syntax</span></span>

| <span data-ttu-id="7b34f-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="7b34f-129">Method</span></span>  | <span data-ttu-id="7b34f-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="7b34f-130">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="7b34f-131">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="7b34f-131">**GET**</span></span> | <span data-ttu-id="7b34f-132">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7b34f-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7b34f-133">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="7b34f-133">URI parameter</span></span>

<span data-ttu-id="7b34f-134">Użyj następującego parametru zapytania do określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="7b34f-134">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="7b34f-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7b34f-135">Name</span></span>                   | <span data-ttu-id="7b34f-136">Typ</span><span class="sxs-lookup"><span data-stu-id="7b34f-136">Type</span></span>     | <span data-ttu-id="7b34f-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="7b34f-137">Required</span></span> | <span data-ttu-id="7b34f-138">Opis</span><span class="sxs-lookup"><span data-stu-id="7b34f-138">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b34f-139">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="7b34f-139">**customer-tenant-id**</span></span> | <span data-ttu-id="7b34f-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="7b34f-140">**guid**</span></span> | <span data-ttu-id="7b34f-141">Y</span><span class="sxs-lookup"><span data-stu-id="7b34f-141">Y</span></span>        | <span data-ttu-id="7b34f-142">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="7b34f-142">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7b34f-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="7b34f-143">Request headers</span></span>

<span data-ttu-id="7b34f-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7b34f-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7b34f-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="7b34f-145">Request body</span></span>

<span data-ttu-id="7b34f-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="7b34f-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7b34f-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="7b34f-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="7b34f-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="7b34f-148">REST response</span></span>

<span data-ttu-id="7b34f-149">Jeśli to się powiedzie, ta metoda zwraca zasób [klienta](customer-resources.md#customer) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7b34f-149">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b34f-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7b34f-150">Response success and error codes</span></span>

<span data-ttu-id="7b34f-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="7b34f-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b34f-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="7b34f-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b34f-153">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7b34f-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b34f-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="7b34f-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1530
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b

{
  "id": "eebd1b55-5360-4438-a11d-5c06918c3014",
  "commerceId": "99e6a635-48e7-424d-9059-c9db944e3c54",
  "companyProfile": {
    "tenantId": "eebd1b55-5360-4438-a11d-5c06918c3014",
    "domain": "abcdefgh1234.ccsctp.net",
    "companyName": "1kl as kjk",
    "address": {
      "country": "US",
      "region": "wa",
      "city": "redmond",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "phoneNumber": "1234567890"
    },
    "email": "a@a.com",
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/company",
        "method": "GET",
        "headers": []
      }
    },
    "attributes": {
      "objectType": "CustomerCompanyProfile"
    }
  },
  "billingProfile": {
    "id": "eeada110-69d6-4cc9-b093-75feb7ca9d3f",
    "firstName": "d0d89d776d03471c819bf772191ed728",
    "lastName": "kjkAJJAAAAAAAAAAAAAAAAAAAA",
    "email": "a@a.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "1kl as kjkAAAAAAAAAAAAAAAJJJJJJJJJJJAAAAAJJJJJJJJJJJAAJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJAJJJJJAJJAAAAJAJJAAAAAAAAAAAAAAAAAAAA",
    "defaultAddress": {
      "country": "US",
      "city": "redmond",
      "state": "WA",
      "addressLine1": "1 ms way",
      "postalCode": "98052",
      "firstName": "1kl as",
      "lastName": "kjk",
      "phoneNumber": "1234567890"
    },
    "links": {
      "self": {
        "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/profiles/billing",
        "method": "GET",
        "headers": [

        ]
      }
    },
    "attributes": {
      "etag": "-4242348048554929329",
      "objectType": "CustomerBillingProfile"
    }
  },
  "relationshipToPartner": "reseller",
  "allowDelegatedAccess": true,
  "customDomains": [
    "abcdefgh1234.ccsctp.net"
  ],
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Customer"
  }
}
```
