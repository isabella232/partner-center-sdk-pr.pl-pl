---
title: Pobieranie profilu rozliczeniowego klienta
description: Pobiera profil rozliczeń dla klienta. Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6c837c1c220e334df82e75eb680b6012862c9686
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768362"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="88107-103">Pobieranie profilu rozliczeniowego klienta</span><span class="sxs-lookup"><span data-stu-id="88107-103">Get a customer's billing profile</span></span>

<span data-ttu-id="88107-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="88107-104">**Applies To**</span></span>

- <span data-ttu-id="88107-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="88107-105">Partner Center</span></span>
- <span data-ttu-id="88107-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="88107-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="88107-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="88107-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="88107-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="88107-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="88107-109">Pobiera profil rozliczeń dla klienta.</span><span class="sxs-lookup"><span data-stu-id="88107-109">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="88107-110">Na pulpicie nawigacyjnym Centrum partnerskiego można wykonać tę operację, [wybierając najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="88107-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="88107-111">Następnie w polu Nazwa klienta na lewym pasku bocznym wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="88107-111">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="88107-112">Profil rozliczeń można znaleźć w nagłówku **informacji dotyczących rachunku** .</span><span class="sxs-lookup"><span data-stu-id="88107-112">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88107-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88107-113">Prerequisites</span></span>

- <span data-ttu-id="88107-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="88107-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="88107-115">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88107-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="88107-116">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88107-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="88107-117">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="88107-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="88107-118">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="88107-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="88107-119">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="88107-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="88107-120">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="88107-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="88107-121">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88107-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="88107-122">C\#</span><span class="sxs-lookup"><span data-stu-id="88107-122">C\#</span></span>

<span data-ttu-id="88107-123">Aby uzyskać profil rozliczeń klienta, Użyj kolekcji [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i Wywołaj metodę [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) .</span><span class="sxs-lookup"><span data-stu-id="88107-123">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="88107-124">Następnie Wywołaj Właściwość [**Profile**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) , a następnie właściwość [**rozliczenia**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) .</span><span class="sxs-lookup"><span data-stu-id="88107-124">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="88107-125">Na koniec wywołaj metody [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) lub [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) .</span><span class="sxs-lookup"><span data-stu-id="88107-125">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="88107-126">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="88107-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="88107-127">**Project**: PartnerSDK. FeatureSamples **Klasa**: GetCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="88107-127">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="88107-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="88107-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="88107-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="88107-129">Request syntax</span></span>

| <span data-ttu-id="88107-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="88107-130">Method</span></span>  | <span data-ttu-id="88107-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="88107-131">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="88107-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="88107-132">**GET**</span></span> | <span data-ttu-id="88107-133">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="88107-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="88107-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="88107-134">URI parameter</span></span>

<span data-ttu-id="88107-135">Użyj następującego parametru zapytania, aby uzyskać profil rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="88107-135">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="88107-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="88107-136">Name</span></span>                   | <span data-ttu-id="88107-137">Typ</span><span class="sxs-lookup"><span data-stu-id="88107-137">Type</span></span>     | <span data-ttu-id="88107-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="88107-138">Required</span></span> | <span data-ttu-id="88107-139">Opis</span><span class="sxs-lookup"><span data-stu-id="88107-139">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="88107-140">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="88107-140">**customer-tenant-id**</span></span> | <span data-ttu-id="88107-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="88107-141">**guid**</span></span> | <span data-ttu-id="88107-142">Y</span><span class="sxs-lookup"><span data-stu-id="88107-142">Y</span></span>        | <span data-ttu-id="88107-143">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="88107-143">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="88107-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="88107-144">Request headers</span></span>

<span data-ttu-id="88107-145">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="88107-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="88107-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="88107-146">Request body</span></span>

<span data-ttu-id="88107-147">Brak</span><span class="sxs-lookup"><span data-stu-id="88107-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="88107-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="88107-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="88107-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="88107-149">REST response</span></span>

<span data-ttu-id="88107-150">Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów [profilu](profile-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="88107-150">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="88107-151">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88107-151">Response success and error codes</span></span>

<span data-ttu-id="88107-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="88107-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="88107-153">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="88107-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="88107-154">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="88107-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="88107-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="88107-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
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
