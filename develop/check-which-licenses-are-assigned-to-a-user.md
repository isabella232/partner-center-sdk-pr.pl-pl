---
title: Pobieranie licencji przypisanych do użytkownika
description: Dowiedz się, jak używać interfejsów API Centrum partnerskiego, aby uzyskać listę licencji przypisanych do użytkownika w ramach konta klienta.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b754ba4ecba7067f78c6868b387bac0190bfd230
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768605"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="bc9be-103">Uzyskaj licencje przypisane do użytkownika w ramach konta klienta</span><span class="sxs-lookup"><span data-stu-id="bc9be-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="bc9be-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="bc9be-104">**Applies to:**</span></span>

- <span data-ttu-id="bc9be-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="bc9be-105">Partner Center</span></span>

<span data-ttu-id="bc9be-106">Jak uzyskać listę licencji przypisanych do użytkownika w ramach konta klienta.</span><span class="sxs-lookup"><span data-stu-id="bc9be-106">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="bc9be-107">Przykłady przedstawione w tym miejscu zwracają licencje przypisane do grupy licencji, która reprezentuje licencje zarządzane przez Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc9be-107">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="bc9be-108">Aby uzyskać licencje przypisane z określonych grup licencji, zobacz sekcję [pobieranie licencji przypisanych do użytkownika według grupy licencji](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="bc9be-108">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc9be-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc9be-109">Prerequisites</span></span>

- <span data-ttu-id="bc9be-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bc9be-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bc9be-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="bc9be-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bc9be-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bc9be-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bc9be-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bc9be-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="bc9be-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bc9be-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="bc9be-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bc9be-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="bc9be-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bc9be-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bc9be-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="bc9be-118">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-118">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="bc9be-119">C\#</span><span class="sxs-lookup"><span data-stu-id="bc9be-119">C\#</span></span>

<span data-ttu-id="bc9be-120">Aby sprawdzić, które licencje są przypisane do użytkownika z domyślnej grupy licencji grupa1, najpierw Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="bc9be-120">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="bc9be-121">Następnie Wywołaj metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika, aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-121">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="bc9be-122">Następnie uzyskaj interfejs do operacji licencji użytkownika klienta na podstawie właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) .</span><span class="sxs-lookup"><span data-stu-id="bc9be-122">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="bc9be-123">Na koniec Wywołaj metodę [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) , aby pobrać kolekcję licencji przypisanych do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="bc9be-124">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc9be-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bc9be-125">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="bc9be-125">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bc9be-126">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bc9be-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bc9be-127">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="bc9be-127">Request syntax</span></span>

| <span data-ttu-id="bc9be-128">Metoda</span><span class="sxs-lookup"><span data-stu-id="bc9be-128">Method</span></span>  | <span data-ttu-id="bc9be-129">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="bc9be-129">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bc9be-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="bc9be-130">**GET**</span></span> | <span data-ttu-id="bc9be-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses http/1.1</span><span class="sxs-lookup"><span data-stu-id="bc9be-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bc9be-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bc9be-132">URI parameter</span></span>

<span data-ttu-id="bc9be-133">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-133">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="bc9be-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bc9be-134">Name</span></span>        | <span data-ttu-id="bc9be-135">Typ</span><span class="sxs-lookup"><span data-stu-id="bc9be-135">Type</span></span>   | <span data-ttu-id="bc9be-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bc9be-136">Required</span></span> | <span data-ttu-id="bc9be-137">Opis</span><span class="sxs-lookup"><span data-stu-id="bc9be-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="bc9be-138">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="bc9be-138">customer-id</span></span> | <span data-ttu-id="bc9be-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="bc9be-139">string</span></span> | <span data-ttu-id="bc9be-140">Tak</span><span class="sxs-lookup"><span data-stu-id="bc9be-140">Yes</span></span>      | <span data-ttu-id="bc9be-141">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="bc9be-141">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="bc9be-142">user-id</span><span class="sxs-lookup"><span data-stu-id="bc9be-142">user-id</span></span>     | <span data-ttu-id="bc9be-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="bc9be-143">string</span></span> | <span data-ttu-id="bc9be-144">Tak</span><span class="sxs-lookup"><span data-stu-id="bc9be-144">Yes</span></span>      | <span data-ttu-id="bc9be-145">Ciąg w formacie GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bc9be-145">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="bc9be-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="bc9be-146">Request headers</span></span>

<span data-ttu-id="bc9be-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bc9be-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bc9be-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="bc9be-148">Request body</span></span>

<span data-ttu-id="bc9be-149">Brak.</span><span class="sxs-lookup"><span data-stu-id="bc9be-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bc9be-150">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="bc9be-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="bc9be-151">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bc9be-151">REST response</span></span>

<span data-ttu-id="bc9be-152">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [licencji](license-resources.md#license) .</span><span class="sxs-lookup"><span data-stu-id="bc9be-152">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bc9be-153">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bc9be-153">Response success and error codes</span></span>

<span data-ttu-id="bc9be-154">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="bc9be-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bc9be-155">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="bc9be-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bc9be-156">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bc9be-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bc9be-157">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bc9be-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```