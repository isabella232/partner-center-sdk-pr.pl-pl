---
title: Aktualizowanie profilu rozliczeniowego klienta
description: Aktualizuje profil rozliczeniowy klienta, w tym adres skojarzony z profilem.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 1605c3e8cb050717209cb482d2299e2a42b9b186
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530042"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="6767d-103">Aktualizowanie profilu rozliczeniowego klienta</span><span class="sxs-lookup"><span data-stu-id="6767d-103">Update a customer's billing profile</span></span>

<span data-ttu-id="6767d-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6767d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6767d-105">Aktualizuje profil rozliczeniowy klienta, w tym adres skojarzony z profilem.</span><span class="sxs-lookup"><span data-stu-id="6767d-105">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6767d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6767d-106">Prerequisites</span></span>

- <span data-ttu-id="6767d-107">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6767d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6767d-108">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6767d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6767d-109">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6767d-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6767d-110">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6767d-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6767d-111">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="6767d-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6767d-112">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="6767d-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6767d-113">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="6767d-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6767d-114">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6767d-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6767d-115">C\#</span><span class="sxs-lookup"><span data-stu-id="6767d-115">C\#</span></span>

<span data-ttu-id="6767d-116">Aby zaktualizować profil rozliczeniowy klienta, pobierz profil rozliczeniowy i zaktualizuj właściwości zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="6767d-116">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="6767d-117">Następnie pobierz kolekcję [**IPartner.Customers,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) a następnie wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="6767d-117">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="6767d-118">Następnie wywołaj [**właściwość Profiles,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) a następnie właściwość [**Rozliczenia.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing)</span><span class="sxs-lookup"><span data-stu-id="6767d-118">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="6767d-119">Następnie zakończ, wywołując metody [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) lub [**UpdateAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync)</span><span class="sxs-lookup"><span data-stu-id="6767d-119">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="6767d-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6767d-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6767d-121">**Project:** Klasa PartnerSDK.FeatureSamples: UpdateCustomerBillingProfile.cs </span><span class="sxs-lookup"><span data-stu-id="6767d-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6767d-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="6767d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6767d-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="6767d-123">Request syntax</span></span>

| <span data-ttu-id="6767d-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="6767d-124">Method</span></span>  | <span data-ttu-id="6767d-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="6767d-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6767d-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="6767d-126">**PUT**</span></span> | <span data-ttu-id="6767d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6767d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6767d-128">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="6767d-128">URI parameter</span></span>

<span data-ttu-id="6767d-129">Użyj następującego parametru zapytania, aby zaktualizować profil rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="6767d-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="6767d-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6767d-130">Name</span></span>                   | <span data-ttu-id="6767d-131">Typ</span><span class="sxs-lookup"><span data-stu-id="6767d-131">Type</span></span>     | <span data-ttu-id="6767d-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6767d-132">Required</span></span> | <span data-ttu-id="6767d-133">Opis</span><span class="sxs-lookup"><span data-stu-id="6767d-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6767d-134">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="6767d-134">**customer-tenant-id**</span></span> | <span data-ttu-id="6767d-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="6767d-135">**guid**</span></span> | <span data-ttu-id="6767d-136">Y</span><span class="sxs-lookup"><span data-stu-id="6767d-136">Y</span></span>        | <span data-ttu-id="6767d-137">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="6767d-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6767d-138">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="6767d-138">Request headers</span></span>

- <span data-ttu-id="6767d-139">**If-Match**: " &lt; ETag &gt; " jest wymagany do wykrywania współbieżności.</span><span class="sxs-lookup"><span data-stu-id="6767d-139">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="6767d-140">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6767d-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6767d-141">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="6767d-141">Request body</span></span>

<span data-ttu-id="6767d-142">Pełny zasób.</span><span class="sxs-lookup"><span data-stu-id="6767d-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="6767d-143">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="6767d-143">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6767d-144">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="6767d-144">REST response</span></span>

<span data-ttu-id="6767d-145">W przypadku powodzenia ta metoda zwraca [zaktualizowane](profile-resources.md) właściwości zasobu profilu w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6767d-145">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="6767d-146">To wywołanie wymaga tagu ETag do wykrywania współbieżności.</span><span class="sxs-lookup"><span data-stu-id="6767d-146">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6767d-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6767d-147">Response success and error codes</span></span>

<span data-ttu-id="6767d-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="6767d-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6767d-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6767d-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6767d-150">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6767d-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6767d-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6767d-151">Response example</span></span>

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
