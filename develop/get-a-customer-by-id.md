---
title: Pobieranie klienta według identyfikatora
description: Pobiera zasób Customer odpowiadający identyfikatorowi klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 196d653c789c4b4e1327f0c6e5d2531a18681a71
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874996"
---
# <a name="get-a-customer-by-id"></a><span data-ttu-id="e48f6-103">Pobieranie klienta według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="e48f6-103">Get a customer by ID</span></span>

<span data-ttu-id="e48f6-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e48f6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e48f6-105">Pobiera **zasób Customer** odpowiadający identyfikatorowi klienta.</span><span class="sxs-lookup"><span data-stu-id="e48f6-105">Gets a **Customer** resource that corresponds to a customer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e48f6-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e48f6-106">Prerequisites</span></span>

- <span data-ttu-id="e48f6-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e48f6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e48f6-108">Ten scenariusz obsługuje poświadczenia aplikacji i użytkownika lub uwierzytelnianie tylko dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e48f6-108">This scenario supports app+user credentials or app-only authentication.</span></span>

- <span data-ttu-id="e48f6-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e48f6-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e48f6-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e48f6-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e48f6-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="e48f6-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e48f6-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="e48f6-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e48f6-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="e48f6-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e48f6-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e48f6-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e48f6-115">C\#</span><span class="sxs-lookup"><span data-stu-id="e48f6-115">C\#</span></span>

<span data-ttu-id="e48f6-116">Aby uzyskać klienta według identyfikatora, użyj kolekcji [**IAggregatePartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) wywołaj metodę [**ById(),**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a następnie wywołaj metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) lub [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync)</span><span class="sxs-lookup"><span data-stu-id="e48f6-116">To get a customer by ID, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, then call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

Customer customerInfo = partnerOperations.Customers.ById(customerIdToRetrieve).Get();
```

<span data-ttu-id="e48f6-117">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e48f6-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e48f6-118">**Project:** PartnerSDK.FeatureSamples, **klasa**: CustomerInformation.cs</span><span class="sxs-lookup"><span data-stu-id="e48f6-118">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerInformation.cs</span></span>

## <a name="java"></a><span data-ttu-id="e48f6-119">Java</span><span class="sxs-lookup"><span data-stu-id="e48f6-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e48f6-120">Aby uzyskać klienta według identyfikatora, użyj funkcji **IAggregatePartner.getCustomers,** wywołaj funkcję **byId(),** a następnie wywołaj funkcję **get().**</span><span class="sxs-lookup"><span data-stu-id="e48f6-120">To get a customer by ID, use your **IAggregatePartner.getCustomers** function, call the **byId()** function, then call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerIdToRetrieve;

Customer customerInfo = partnerOperations.getCustomers().byId(customerIdToRetrieve).get();
```

## <a name="powershell"></a><span data-ttu-id="e48f6-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e48f6-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e48f6-122">Aby uzyskać klienta według identyfikatora, wykonaj polecenie [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) i określ **parametr CustomerId.**</span><span class="sxs-lookup"><span data-stu-id="e48f6-122">To get a customer by ID, execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command and specify the **CustomerId** parameter.</span></span>

```powershell
Get-PartnerCustomer -CustomerId '2ca7de6c-c05c-46b5-b689-32e53573a97a'
```

## <a name="rest-request"></a><span data-ttu-id="e48f6-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e48f6-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e48f6-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e48f6-124">Request syntax</span></span>

| <span data-ttu-id="e48f6-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="e48f6-125">Method</span></span>  | <span data-ttu-id="e48f6-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e48f6-126">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="e48f6-127">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="e48f6-127">**GET**</span></span> | <span data-ttu-id="e48f6-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e48f6-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e48f6-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="e48f6-129">URI parameter</span></span>

<span data-ttu-id="e48f6-130">Użyj następującego parametru zapytania dla określonego klienta.</span><span class="sxs-lookup"><span data-stu-id="e48f6-130">Use the following query parameter to a specific customer.</span></span>

| <span data-ttu-id="e48f6-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e48f6-131">Name</span></span>                   | <span data-ttu-id="e48f6-132">Typ</span><span class="sxs-lookup"><span data-stu-id="e48f6-132">Type</span></span>     | <span data-ttu-id="e48f6-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e48f6-133">Required</span></span> | <span data-ttu-id="e48f6-134">Opis</span><span class="sxs-lookup"><span data-stu-id="e48f6-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e48f6-135">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="e48f6-135">**customer-tenant-id**</span></span> | <span data-ttu-id="e48f6-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="e48f6-136">**guid**</span></span> | <span data-ttu-id="e48f6-137">Y</span><span class="sxs-lookup"><span data-stu-id="e48f6-137">Y</span></span>        | <span data-ttu-id="e48f6-138">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="e48f6-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e48f6-139">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e48f6-139">Request headers</span></span>

<span data-ttu-id="e48f6-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e48f6-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e48f6-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e48f6-141">Request body</span></span>

<span data-ttu-id="e48f6-142">Brak.</span><span class="sxs-lookup"><span data-stu-id="e48f6-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e48f6-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e48f6-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: a176c585-b5de-4d65-824c-67a6deb45cd9
MS-RequestId: 74ca1db9-df92-41c6-a362-a16433b0542b
```

## <a name="rest-response"></a><span data-ttu-id="e48f6-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e48f6-144">REST response</span></span>

<span data-ttu-id="e48f6-145">W przypadku powodzenia ta metoda zwraca [zasób Customer](customer-resources.md#customer) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e48f6-145">If successful, this method returns a [Customer](customer-resources.md#customer) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e48f6-146">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e48f6-146">Response success and error codes</span></span>

<span data-ttu-id="e48f6-147">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="e48f6-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e48f6-148">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e48f6-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e48f6-149">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e48f6-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e48f6-150">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e48f6-150">Response example</span></span>

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
