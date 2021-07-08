---
title: Pobieranie profilu firmy klienta
description: Pobiera profil firmy klienta.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: a1c0c8401207f4b0bb33755a8eabc66de0ad9ff9
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874979"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="c2211-103">Pobieranie profilu firmy klienta</span><span class="sxs-lookup"><span data-stu-id="c2211-103">Get a customer's company profile</span></span>

<span data-ttu-id="c2211-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="c2211-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c2211-105">Pobiera profil firmy klienta.</span><span class="sxs-lookup"><span data-stu-id="c2211-105">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2211-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c2211-106">Prerequisites</span></span>

- <span data-ttu-id="c2211-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c2211-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c2211-108">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2211-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c2211-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c2211-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c2211-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c2211-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c2211-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="c2211-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c2211-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="c2211-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c2211-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="c2211-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c2211-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c2211-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c2211-115">C\#</span><span class="sxs-lookup"><span data-stu-id="c2211-115">C\#</span></span>

<span data-ttu-id="c2211-116">Aby uzyskać profil firmy dla klienta, wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="c2211-116">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="c2211-117">Następnie pobierz interfejs [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) klienta z właściwości [**Profiles,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) aby uzyskać dostęp do jego właściwości Company.</span><span class="sxs-lookup"><span data-stu-id="c2211-117">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="c2211-118">Następnie pobierz interfejs [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) z właściwości [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) i wywołaj jego metody [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) lub [**GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="c2211-118">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="c2211-119">**Przykład:** [pobierz zestaw SDK Centrum partnerskiego](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="c2211-119">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="c2211-120">**Project:** PartnerSdk.FeatureSamples, **klasa**: GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="c2211-120">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="c2211-121">Java</span><span class="sxs-lookup"><span data-stu-id="c2211-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="c2211-122">Aby uzyskać profil firmy dla klienta, wywołaj funkcję **IAggregatePartner.getCustomers().byId** z identyfikatorem klienta w celu zidentyfikowania klienta.</span><span class="sxs-lookup"><span data-stu-id="c2211-122">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="c2211-123">Następnie pobierz interfejs **ICustomerProfileCollection** klienta z funkcji [**getProfiles**], aby uzyskać dostęp do jego właściwości Company.</span><span class="sxs-lookup"><span data-stu-id="c2211-123">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="c2211-124">Następnie pobierz **interfejs ICustomerReadonlyProfile** z funkcji **ICustomerProfileCollection.getCompany** i wywołaj **funkcję get.**</span><span class="sxs-lookup"><span data-stu-id="c2211-124">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="c2211-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="c2211-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c2211-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="c2211-126">Request syntax</span></span>

| <span data-ttu-id="c2211-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="c2211-127">Method</span></span>  | <span data-ttu-id="c2211-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="c2211-128">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="c2211-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="c2211-129">**GET**</span></span> | <span data-ttu-id="c2211-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c2211-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c2211-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="c2211-131">URI parameter</span></span>

<span data-ttu-id="c2211-132">Użyj następującego parametru zapytania, aby pobrać profil firmy.</span><span class="sxs-lookup"><span data-stu-id="c2211-132">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="c2211-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c2211-133">Name</span></span>                   | <span data-ttu-id="c2211-134">Typ</span><span class="sxs-lookup"><span data-stu-id="c2211-134">Type</span></span>     | <span data-ttu-id="c2211-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c2211-135">Required</span></span> | <span data-ttu-id="c2211-136">Opis</span><span class="sxs-lookup"><span data-stu-id="c2211-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2211-137">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="c2211-137">**customer-tenant-id**</span></span> | <span data-ttu-id="c2211-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="c2211-138">**guid**</span></span> | <span data-ttu-id="c2211-139">Y</span><span class="sxs-lookup"><span data-stu-id="c2211-139">Y</span></span>        | <span data-ttu-id="c2211-140">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="c2211-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c2211-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="c2211-141">Request headers</span></span>

<span data-ttu-id="c2211-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c2211-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c2211-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="c2211-143">Request body</span></span>

<span data-ttu-id="c2211-144">Brak</span><span class="sxs-lookup"><span data-stu-id="c2211-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="c2211-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="c2211-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c2211-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="c2211-146">REST response</span></span>

<span data-ttu-id="c2211-147">W przypadku powodzenia ta metoda zwraca informacje w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c2211-147">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c2211-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c2211-148">Response success and error codes</span></span>

<span data-ttu-id="c2211-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="c2211-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c2211-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="c2211-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c2211-151">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c2211-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c2211-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c2211-152">Response example</span></span>

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
