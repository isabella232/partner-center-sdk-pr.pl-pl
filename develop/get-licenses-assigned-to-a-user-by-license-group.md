---
title: Pobieranie licencji przypisanych do użytkownika według grupy licencji
description: Jak uzyskać listę licencji przypisanych do użytkowników dla określonych grup licencji.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768321"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="10a37-103">Pobieranie licencji przypisanych do użytkownika według grupy licencji</span><span class="sxs-lookup"><span data-stu-id="10a37-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="10a37-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="10a37-104">**Applies To**</span></span>

- <span data-ttu-id="10a37-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="10a37-105">Partner Center</span></span>

<span data-ttu-id="10a37-106">Jak uzyskać listę licencji przypisanych do użytkowników dla określonych grup licencji.</span><span class="sxs-lookup"><span data-stu-id="10a37-106">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10a37-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="10a37-107">Prerequisites</span></span>

- <span data-ttu-id="10a37-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="10a37-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="10a37-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10a37-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="10a37-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="10a37-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="10a37-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="10a37-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="10a37-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="10a37-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="10a37-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="10a37-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="10a37-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="10a37-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="10a37-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="10a37-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="10a37-116">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10a37-116">A user identifier.</span></span>

- <span data-ttu-id="10a37-117">Lista co najmniej jednego z identyfikatorów grup licencji.</span><span class="sxs-lookup"><span data-stu-id="10a37-117">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="10a37-118">C\#</span><span class="sxs-lookup"><span data-stu-id="10a37-118">C\#</span></span>

<span data-ttu-id="10a37-119">Aby sprawdzić, które licencje są przypisane do użytkownika z określonych grup licencji, Zacznij od utworzenia wystąpienia [list/dotnet/API/System. Collections. Generic. list -1) typu [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), a następnie Dodaj do listy grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="10a37-119">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="10a37-120">Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="10a37-120">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="10a37-121">Następnie Wywołaj metodę user [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika, aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10a37-121">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="10a37-122">Następnie uzyskaj interfejs do operacji licencji użytkownika klienta na podstawie właściwości [**licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) .</span><span class="sxs-lookup"><span data-stu-id="10a37-122">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="10a37-123">Na koniec Przekaż listę grup licencji do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) , aby pobrać kolekcję licencji przypisanych do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10a37-123">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="10a37-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="10a37-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="10a37-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="10a37-125">Request syntax</span></span>

| <span data-ttu-id="10a37-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="10a37-126">Method</span></span>  | <span data-ttu-id="10a37-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="10a37-127">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="10a37-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="10a37-128">**GET**</span></span> | <span data-ttu-id="10a37-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = grupa1 http/1.1</span><span class="sxs-lookup"><span data-stu-id="10a37-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="10a37-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="10a37-130">**GET**</span></span> | <span data-ttu-id="10a37-131">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="10a37-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="10a37-132">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="10a37-132">**GET**</span></span> | <span data-ttu-id="10a37-133">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-ID}/users/{User-ID}/licenses? LicenseGroupIds = grupa1&LicenseGroupIds = group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="10a37-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="10a37-134">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="10a37-134">URI parameter</span></span>

<span data-ttu-id="10a37-135">Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klientów, użytkowników i grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="10a37-135">Use the following path and query parameters to identify the customer, user and license groups.</span></span>

| <span data-ttu-id="10a37-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="10a37-136">Name</span></span>            | <span data-ttu-id="10a37-137">Typ</span><span class="sxs-lookup"><span data-stu-id="10a37-137">Type</span></span>   | <span data-ttu-id="10a37-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="10a37-138">Required</span></span> | <span data-ttu-id="10a37-139">Opis</span><span class="sxs-lookup"><span data-stu-id="10a37-139">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="10a37-140">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="10a37-140">customer-id</span></span>     | <span data-ttu-id="10a37-141">ciąg</span><span class="sxs-lookup"><span data-stu-id="10a37-141">string</span></span> | <span data-ttu-id="10a37-142">Tak</span><span class="sxs-lookup"><span data-stu-id="10a37-142">Yes</span></span>      | <span data-ttu-id="10a37-143">Ciąg w formacie GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="10a37-143">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="10a37-144">user-id</span><span class="sxs-lookup"><span data-stu-id="10a37-144">user-id</span></span>         | <span data-ttu-id="10a37-145">ciąg</span><span class="sxs-lookup"><span data-stu-id="10a37-145">string</span></span> | <span data-ttu-id="10a37-146">Tak</span><span class="sxs-lookup"><span data-stu-id="10a37-146">Yes</span></span>      | <span data-ttu-id="10a37-147">Ciąg w formacie GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10a37-147">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="10a37-148">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="10a37-148">licenseGroupIds</span></span> | <span data-ttu-id="10a37-149">ciąg</span><span class="sxs-lookup"><span data-stu-id="10a37-149">string</span></span> | <span data-ttu-id="10a37-150">Nie</span><span class="sxs-lookup"><span data-stu-id="10a37-150">No</span></span>       | <span data-ttu-id="10a37-151">Wartość wyliczenia wskazująca grupę licencji przypisanych licencji.</span><span class="sxs-lookup"><span data-stu-id="10a37-151">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="10a37-152">Prawidłowe wartości: grupa1, group2 grupa1 — ta grupa zawiera wszystkie produkty, których licencja może być zarządzana w Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="10a37-152">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="10a37-153">Group2 — ta grupa ma tylko Minecraft licencje na produkty.</span><span class="sxs-lookup"><span data-stu-id="10a37-153">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="10a37-154">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="10a37-154">Request headers</span></span>

<span data-ttu-id="10a37-155">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="10a37-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="10a37-156">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="10a37-156">Request body</span></span>

<span data-ttu-id="10a37-157">Brak.</span><span class="sxs-lookup"><span data-stu-id="10a37-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="10a37-158">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="10a37-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="10a37-159">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="10a37-159">REST response</span></span>

<span data-ttu-id="10a37-160">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [licencji](license-resources.md#license) .</span><span class="sxs-lookup"><span data-stu-id="10a37-160">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="10a37-161">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="10a37-161">Response success and error codes</span></span>

<span data-ttu-id="10a37-162">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="10a37-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="10a37-163">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="10a37-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="10a37-164">Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="10a37-164">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="10a37-165">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="10a37-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="10a37-166">Przykład odpowiedzi (nie znaleziono pasujących licencji)</span><span class="sxs-lookup"><span data-stu-id="10a37-166">Response example (no matching licenses found)</span></span>

<span data-ttu-id="10a37-167">Jeśli nie można znaleźć pasujących licencji dla określonych grup licencji, odpowiedź zawiera pustą kolekcję z elementem totalCount, którego wartość wynosi 0.</span><span class="sxs-lookup"><span data-stu-id="10a37-167">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
