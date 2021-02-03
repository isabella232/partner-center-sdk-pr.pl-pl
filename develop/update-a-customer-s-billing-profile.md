---
title: Aktualizowanie profilu rozliczeniowego klienta
description: Aktualizuje profil rozliczeń klienta, w tym adres skojarzony z profilem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: adf4e3de9941fded632e0561624d91d854c5aa24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768393"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="0c4a0-103">Aktualizowanie profilu rozliczeniowego klienta</span><span class="sxs-lookup"><span data-stu-id="0c4a0-103">Update a customer's billing profile</span></span>

<span data-ttu-id="0c4a0-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="0c4a0-104">**Applies To**</span></span>

- <span data-ttu-id="0c4a0-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="0c4a0-105">Partner Center</span></span>
- <span data-ttu-id="0c4a0-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="0c4a0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0c4a0-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="0c4a0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0c4a0-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0c4a0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0c4a0-109">Aktualizuje profil rozliczeń klienta, w tym adres skojarzony z profilem.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-109">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c4a0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0c4a0-110">Prerequisites</span></span>

- <span data-ttu-id="0c4a0-111">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0c4a0-112">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0c4a0-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0c4a0-114">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0c4a0-115">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0c4a0-116">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0c4a0-117">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="0c4a0-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0c4a0-118">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0c4a0-119">C\#</span><span class="sxs-lookup"><span data-stu-id="0c4a0-119">C\#</span></span>

<span data-ttu-id="0c4a0-120">Aby zaktualizować profil rozliczeń klienta, Pobierz profil rozliczeń i zaktualizuj właściwości w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-120">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="0c4a0-121">Następnie Pobierz kolekcję [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) , a następnie Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="0c4a0-121">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="0c4a0-122">Następnie Wywołaj Właściwość [**Profile**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , a następnie właściwość [**rozliczenia**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) .</span><span class="sxs-lookup"><span data-stu-id="0c4a0-122">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="0c4a0-123">Następnie Zakończ, wywołując metody [**Update ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) lub [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) .</span><span class="sxs-lookup"><span data-stu-id="0c4a0-123">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="0c4a0-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0c4a0-125">**Project**: PartnerSDK. FeatureSamples **Klasa**: UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="0c4a0-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0c4a0-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0c4a0-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0c4a0-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0c4a0-127">Request syntax</span></span>

| <span data-ttu-id="0c4a0-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="0c4a0-128">Method</span></span>  | <span data-ttu-id="0c4a0-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0c4a0-129">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c4a0-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="0c4a0-130">**PUT**</span></span> | <span data-ttu-id="0c4a0-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="0c4a0-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0c4a0-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0c4a0-132">URI parameter</span></span>

<span data-ttu-id="0c4a0-133">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-133">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="0c4a0-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0c4a0-134">Name</span></span>                   | <span data-ttu-id="0c4a0-135">Typ</span><span class="sxs-lookup"><span data-stu-id="0c4a0-135">Type</span></span>     | <span data-ttu-id="0c4a0-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0c4a0-136">Required</span></span> | <span data-ttu-id="0c4a0-137">Opis</span><span class="sxs-lookup"><span data-stu-id="0c4a0-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0c4a0-138">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="0c4a0-138">**customer-tenant-id**</span></span> | <span data-ttu-id="0c4a0-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="0c4a0-139">**guid**</span></span> | <span data-ttu-id="0c4a0-140">Y</span><span class="sxs-lookup"><span data-stu-id="0c4a0-140">Y</span></span>        | <span data-ttu-id="0c4a0-141">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0c4a0-142">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0c4a0-142">Request headers</span></span>

- <span data-ttu-id="0c4a0-143">**If-Match: element**" &lt; ETag &gt; " jest wymagany do wykrywania współbieżności.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-143">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="0c4a0-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0c4a0-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0c4a0-145">Request body</span></span>

<span data-ttu-id="0c4a0-146">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-146">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0c4a0-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0c4a0-147">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
Content-Type: application/json
Content-Length: 639
Expect: 100-continue

{
    "Id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "FirstName": "FirstName",
    "LastName": "LastName",
    "Email": "email@sample.com",
    "Culture": "en-US",
    "Language": "en",
    "CompanyName": "CompanyName",
    "DefaultAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "One Microsoft Way",
        "AddressLine2": null,
        "PostalCode": "98052",
        "FirstName": "FirstName",
        "LastName": "LastName",
        "PhoneNumber": "4255555555"
    },
    "Links": {
        "Self": {
            "Uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "CustomerBillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="0c4a0-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0c4a0-148">REST response</span></span>

<span data-ttu-id="0c4a0-149">Jeśli to się powiedzie, ta metoda zwraca zaktualizowane właściwości zasobów [profilu](profile-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-149">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="0c4a0-150">To wywołanie wymaga elementu ETag na potrzeby wykrywania współbieżności.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-150">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0c4a0-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0c4a0-151">Response success and error codes</span></span>

<span data-ttu-id="0c4a0-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0c4a0-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0c4a0-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0c4a0-154">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0c4a0-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0c4a0-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0c4a0-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1210
Content-Type: application/json
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
Date: Mon, 23 Nov 2015 18:20:43 GMT

{
    "id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "companyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "One Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
