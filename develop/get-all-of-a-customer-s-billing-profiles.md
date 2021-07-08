---
title: Pobieranie profilu rozliczeniowego klienta
description: Pobiera profil rozliczeniowy klienta. Na Partner Center nawigacyjnym tę operację można wykonać, wybierając najpierw klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760593"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="1ea5d-104">Pobieranie profilu rozliczeniowego klienta</span><span class="sxs-lookup"><span data-stu-id="1ea5d-104">Get a customer's billing profile</span></span>

<span data-ttu-id="1ea5d-105">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="1ea5d-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1ea5d-106">Pobiera profil rozliczeniowy klienta.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-106">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="1ea5d-107">Na Partner Center nawigacyjnym tę operację można wykonać, wybierając [najpierw klienta](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="1ea5d-108">Następnie pod nazwą klienta na lewym pasku bocznym wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-108">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="1ea5d-109">Profil rozliczeniowy można znaleźć pod nagłówkiem **Informacje dotyczące rozliczeń.**</span><span class="sxs-lookup"><span data-stu-id="1ea5d-109">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ea5d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ea5d-110">Prerequisites</span></span>

- <span data-ttu-id="1ea5d-111">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ea5d-112">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1ea5d-113">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1ea5d-114">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1ea5d-115">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="1ea5d-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1ea5d-116">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1ea5d-117">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1ea5d-118">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1ea5d-119">C\#</span><span class="sxs-lookup"><span data-stu-id="1ea5d-119">C\#</span></span>

<span data-ttu-id="1ea5d-120">Aby uzyskać profil rozliczeniowy klienta, użyj kolekcji [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) i wywołaj [**metodę ById().**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-120">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="1ea5d-121">Następnie wywołaj [**właściwość Profiles,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) a następnie właściwość [**Rozliczenia.**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-121">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="1ea5d-122">Na koniec wywołaj [**metody Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**lub GetAsync().**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-122">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="1ea5d-123">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1ea5d-124">**Project:** Klasa PartnerSDK.FeatureSamples: GetCustomerBillingProfile.cs </span><span class="sxs-lookup"><span data-stu-id="1ea5d-124">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1ea5d-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="1ea5d-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ea5d-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="1ea5d-126">Request syntax</span></span>

| <span data-ttu-id="1ea5d-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="1ea5d-127">Method</span></span>  | <span data-ttu-id="1ea5d-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="1ea5d-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ea5d-129">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="1ea5d-129">**GET**</span></span> | <span data-ttu-id="1ea5d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1ea5d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1ea5d-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="1ea5d-131">URI parameter</span></span>

<span data-ttu-id="1ea5d-132">Użyj następującego parametru zapytania, aby uzyskać profil rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-132">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="1ea5d-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1ea5d-133">Name</span></span>                   | <span data-ttu-id="1ea5d-134">Typ</span><span class="sxs-lookup"><span data-stu-id="1ea5d-134">Type</span></span>     | <span data-ttu-id="1ea5d-135">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1ea5d-135">Required</span></span> | <span data-ttu-id="1ea5d-136">Opis</span><span class="sxs-lookup"><span data-stu-id="1ea5d-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ea5d-137">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="1ea5d-137">**customer-tenant-id**</span></span> | <span data-ttu-id="1ea5d-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="1ea5d-138">**guid**</span></span> | <span data-ttu-id="1ea5d-139">Y</span><span class="sxs-lookup"><span data-stu-id="1ea5d-139">Y</span></span>        | <span data-ttu-id="1ea5d-140">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1ea5d-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1ea5d-141">Request headers</span></span>

<span data-ttu-id="1ea5d-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1ea5d-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="1ea5d-143">Request body</span></span>

<span data-ttu-id="1ea5d-144">Brak</span><span class="sxs-lookup"><span data-stu-id="1ea5d-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1ea5d-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="1ea5d-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="1ea5d-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="1ea5d-146">REST response</span></span>

<span data-ttu-id="1ea5d-147">W przypadku powodzenia ta metoda zwraca kolekcję zasobów [profilu](profile-resources.md) w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-147">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ea5d-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ea5d-148">Response success and error codes</span></span>

<span data-ttu-id="1ea5d-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ea5d-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ea5d-151">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ea5d-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1ea5d-152">Response example</span></span>

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
