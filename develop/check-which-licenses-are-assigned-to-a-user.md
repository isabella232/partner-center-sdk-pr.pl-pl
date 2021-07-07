---
title: Pobieranie licencji przypisanych do użytkownika
description: Dowiedz się, jak za Partner Center API uzyskać listę licencji przypisanych do użytkownika w ramach konta klienta.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a51fc4493e2476107206b03be66004d030e2aa47
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974067"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="0dd8b-103">Uzyskiwanie licencji przypisanych do użytkownika w ramach konta klienta</span><span class="sxs-lookup"><span data-stu-id="0dd8b-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="0dd8b-104">Jak uzyskać listę licencji przypisanych do użytkownika w ramach konta klienta.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-104">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="0dd8b-105">Przedstawione tutaj przykłady zwracają licencje przypisane z grupy group1, czyli domyślnej grupy licencji reprezentującej licencje zarządzane przez Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-105">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="0dd8b-106">Aby uzyskać licencje przypisane z określonych grup licencji, zobacz [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md)(Uzyskiwanie licencji przypisanych do użytkownika według grupy licencji).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-106">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd8b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0dd8b-107">Prerequisites</span></span>

- <span data-ttu-id="0dd8b-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0dd8b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0dd8b-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0dd8b-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0dd8b-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0dd8b-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="0dd8b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0dd8b-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0dd8b-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0dd8b-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0dd8b-116">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-116">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="0dd8b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0dd8b-117">C\#</span></span>

<span data-ttu-id="0dd8b-118">Aby sprawdzić, które licencje są przypisane do użytkownika z domyślnej grupy licencji grupa1, najpierw użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-118">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="0dd8b-119">Następnie wywołaj [**metodę Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika, aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-119">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="0dd8b-120">Następnie pobierz interfejs do operacji licencji użytkownika klienta z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses)</span><span class="sxs-lookup"><span data-stu-id="0dd8b-120">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="0dd8b-121">Na koniec wywołaj [**metodę Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) aby pobrać kolekcję licencji przypisanych do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="0dd8b-122">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0dd8b-123">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="0dd8b-123">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0dd8b-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="0dd8b-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0dd8b-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="0dd8b-125">Request syntax</span></span>

| <span data-ttu-id="0dd8b-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="0dd8b-126">Method</span></span>  | <span data-ttu-id="0dd8b-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="0dd8b-127">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0dd8b-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="0dd8b-128">**GET**</span></span> | <span data-ttu-id="0dd8b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/users/{user-id}/licenses HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0dd8b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0dd8b-130">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="0dd8b-130">URI parameter</span></span>

<span data-ttu-id="0dd8b-131">Użyj następujących parametrów ścieżki, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-131">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="0dd8b-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0dd8b-132">Name</span></span>        | <span data-ttu-id="0dd8b-133">Typ</span><span class="sxs-lookup"><span data-stu-id="0dd8b-133">Type</span></span>   | <span data-ttu-id="0dd8b-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0dd8b-134">Required</span></span> | <span data-ttu-id="0dd8b-135">Opis</span><span class="sxs-lookup"><span data-stu-id="0dd8b-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="0dd8b-136">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="0dd8b-136">customer-id</span></span> | <span data-ttu-id="0dd8b-137">ciąg</span><span class="sxs-lookup"><span data-stu-id="0dd8b-137">string</span></span> | <span data-ttu-id="0dd8b-138">Tak</span><span class="sxs-lookup"><span data-stu-id="0dd8b-138">Yes</span></span>      | <span data-ttu-id="0dd8b-139">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-139">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="0dd8b-140">user-id</span><span class="sxs-lookup"><span data-stu-id="0dd8b-140">user-id</span></span>     | <span data-ttu-id="0dd8b-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="0dd8b-141">string</span></span> | <span data-ttu-id="0dd8b-142">Tak</span><span class="sxs-lookup"><span data-stu-id="0dd8b-142">Yes</span></span>      | <span data-ttu-id="0dd8b-143">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-143">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="0dd8b-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="0dd8b-144">Request headers</span></span>

<span data-ttu-id="0dd8b-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0dd8b-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0dd8b-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="0dd8b-146">Request body</span></span>

<span data-ttu-id="0dd8b-147">Brak.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0dd8b-148">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="0dd8b-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0dd8b-149">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="0dd8b-149">REST response</span></span>

<span data-ttu-id="0dd8b-150">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [licencji.](license-resources.md#license)</span><span class="sxs-lookup"><span data-stu-id="0dd8b-150">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0dd8b-151">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0dd8b-151">Response success and error codes</span></span>

<span data-ttu-id="0dd8b-152">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0dd8b-153">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="0dd8b-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0dd8b-154">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0dd8b-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0dd8b-155">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0dd8b-155">Response example</span></span>

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