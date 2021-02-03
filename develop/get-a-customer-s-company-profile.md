---
title: Pobieranie profilu firmy klienta
description: Pobiera profil firmy klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768122"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="f0a0c-103">Pobieranie profilu firmy klienta</span><span class="sxs-lookup"><span data-stu-id="f0a0c-103">Get a customer's company profile</span></span>

<span data-ttu-id="f0a0c-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="f0a0c-104">**Applies To**</span></span>

- <span data-ttu-id="f0a0c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="f0a0c-105">Partner Center</span></span>
- <span data-ttu-id="f0a0c-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="f0a0c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f0a0c-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="f0a0c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f0a0c-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f0a0c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f0a0c-109">Pobiera profil firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-109">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0a0c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0a0c-110">Prerequisites</span></span>

- <span data-ttu-id="f0a0c-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f0a0c-112">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f0a0c-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f0a0c-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f0a0c-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f0a0c-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f0a0c-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="f0a0c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f0a0c-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f0a0c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f0a0c-119">C\#</span></span>

<span data-ttu-id="f0a0c-120">Aby uzyskać profil firmy dla klienta, wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-120">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f0a0c-121">Następnie Pobierz Interfejs [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) klienta z właściwości [**Profile**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , aby uzyskać dostęp do jego właściwości firmowej.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-121">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="f0a0c-122">Następnie Pobierz Interfejs [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) z właściwości [**ICustomerProfileCollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) i wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="f0a0c-122">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="f0a0c-123">**Przykład**: [Pobierz zestaw SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-123">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="f0a0c-124">**Project**: PartnerSdk. FeatureSamples **Klasa**: GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="f0a0c-124">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="f0a0c-125">Java</span><span class="sxs-lookup"><span data-stu-id="f0a0c-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f0a0c-126">Aby uzyskać profil firmy dla klienta, wywołaj funkcję **IAggregatePartner. GetCustomers (). byId** z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-126">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="f0a0c-127">Następnie Pobierz Interfejs **ICustomerProfileCollection** klienta z funkcji [**getprofiles**], aby uzyskać dostęp do jej właściwości firmowej.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-127">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="f0a0c-128">Następnie Pobierz Interfejs **ICustomerReadonlyProfile** z funkcji **ICustomerProfileCollection. getcompany** i wywołaj funkcję **Get** .</span><span class="sxs-lookup"><span data-stu-id="f0a0c-128">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="f0a0c-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f0a0c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f0a0c-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f0a0c-130">Request syntax</span></span>

| <span data-ttu-id="f0a0c-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="f0a0c-131">Method</span></span>  | <span data-ttu-id="f0a0c-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f0a0c-132">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="f0a0c-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="f0a0c-133">**GET**</span></span> | <span data-ttu-id="f0a0c-134">*{baseURL}*/V1/Customers/{Customer-tenant-ID}/Profiles/Company http/1.1</span><span class="sxs-lookup"><span data-stu-id="f0a0c-134">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f0a0c-135">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="f0a0c-135">URI parameter</span></span>

<span data-ttu-id="f0a0c-136">Użyj następującego parametru zapytania, aby uzyskać profil firmy.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-136">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="f0a0c-137">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f0a0c-137">Name</span></span>                   | <span data-ttu-id="f0a0c-138">Typ</span><span class="sxs-lookup"><span data-stu-id="f0a0c-138">Type</span></span>     | <span data-ttu-id="f0a0c-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f0a0c-139">Required</span></span> | <span data-ttu-id="f0a0c-140">Opis</span><span class="sxs-lookup"><span data-stu-id="f0a0c-140">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0a0c-141">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f0a0c-141">**customer-tenant-id**</span></span> | <span data-ttu-id="f0a0c-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="f0a0c-142">**guid**</span></span> | <span data-ttu-id="f0a0c-143">Y</span><span class="sxs-lookup"><span data-stu-id="f0a0c-143">Y</span></span>        | <span data-ttu-id="f0a0c-144">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-144">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f0a0c-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f0a0c-145">Request headers</span></span>

<span data-ttu-id="f0a0c-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f0a0c-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f0a0c-147">Request body</span></span>

<span data-ttu-id="f0a0c-148">Brak</span><span class="sxs-lookup"><span data-stu-id="f0a0c-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f0a0c-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f0a0c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="f0a0c-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f0a0c-150">REST response</span></span>

<span data-ttu-id="f0a0c-151">Jeśli to się powiedzie, ta metoda zwraca informacje w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-151">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f0a0c-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0a0c-152">Response success and error codes</span></span>

<span data-ttu-id="f0a0c-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f0a0c-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f0a0c-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f0a0c-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f0a0c-155">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f0a0c-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f0a0c-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
