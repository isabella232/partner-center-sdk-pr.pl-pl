---
title: Pobieranie licencji przypisanych do użytkownika według grupy licencji
description: Jak uzyskać listę licencji przypisanych przez użytkownika dla określonych grup licencji.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 54acf6f315e3062d03903a98d0c6c1946065f95e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446007"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="4696a-103">Pobieranie licencji przypisanych do użytkownika według grupy licencji</span><span class="sxs-lookup"><span data-stu-id="4696a-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="4696a-104">Jak uzyskać listę licencji przypisanych przez użytkownika dla określonych grup licencji.</span><span class="sxs-lookup"><span data-stu-id="4696a-104">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4696a-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4696a-105">Prerequisites</span></span>

- <span data-ttu-id="4696a-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4696a-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4696a-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4696a-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4696a-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4696a-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4696a-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="4696a-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4696a-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="4696a-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4696a-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="4696a-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4696a-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="4696a-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4696a-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4696a-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4696a-114">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4696a-114">A user identifier.</span></span>

- <span data-ttu-id="4696a-115">Lista co najmniej jednego identyfikatora grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="4696a-115">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="4696a-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4696a-116">C\#</span></span>

<span data-ttu-id="4696a-117">Aby sprawdzić, które licencje są przypisane do użytkownika z określonych grup licencji, rozpocznij od wystąpienia klasy [List/dotnet/api/system.collections.generic.list-1) typu [**LicenseGroupId,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)a następnie dodaj grupy licencji do listy.</span><span class="sxs-lookup"><span data-stu-id="4696a-117">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="4696a-118">Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="4696a-118">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4696a-119">Następnie wywołaj [**metodę Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) z identyfikatorem użytkownika, aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4696a-119">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="4696a-120">Następnie pobierz interfejs do operacji licencji użytkownika klienta z [**właściwości Licencje.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses)</span><span class="sxs-lookup"><span data-stu-id="4696a-120">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="4696a-121">Na koniec przekaż listę grup licencji do metody [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) lub [**GetAsync,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) aby pobrać kolekcję licencji przypisanych do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4696a-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="4696a-122">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4696a-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4696a-123">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4696a-123">Request syntax</span></span>

| <span data-ttu-id="4696a-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="4696a-124">Method</span></span>  | <span data-ttu-id="4696a-125">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4696a-125">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4696a-126">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="4696a-126">**GET**</span></span> | <span data-ttu-id="4696a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4696a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="4696a-128">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="4696a-128">**GET**</span></span> | <span data-ttu-id="4696a-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4696a-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="4696a-130">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="4696a-130">**GET**</span></span> | <span data-ttu-id="4696a-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-klienta}/users/{identyfikator-użytkownika}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4696a-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4696a-132">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4696a-132">URI parameter</span></span>

<span data-ttu-id="4696a-133">Użyj następującej ścieżki i parametrów zapytania, aby zidentyfikować klienta, użytkownika i grupy licencji.</span><span class="sxs-lookup"><span data-stu-id="4696a-133">Use the following path and query parameters to identify the customer, user, and license groups.</span></span>

| <span data-ttu-id="4696a-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4696a-134">Name</span></span>            | <span data-ttu-id="4696a-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4696a-135">Type</span></span>   | <span data-ttu-id="4696a-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4696a-136">Required</span></span> | <span data-ttu-id="4696a-137">Opis</span><span class="sxs-lookup"><span data-stu-id="4696a-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4696a-138">identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="4696a-138">customer-id</span></span>     | <span data-ttu-id="4696a-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="4696a-139">string</span></span> | <span data-ttu-id="4696a-140">Tak</span><span class="sxs-lookup"><span data-stu-id="4696a-140">Yes</span></span>      | <span data-ttu-id="4696a-141">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="4696a-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="4696a-142">user-id</span><span class="sxs-lookup"><span data-stu-id="4696a-142">user-id</span></span>         | <span data-ttu-id="4696a-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="4696a-143">string</span></span> | <span data-ttu-id="4696a-144">Tak</span><span class="sxs-lookup"><span data-stu-id="4696a-144">Yes</span></span>      | <span data-ttu-id="4696a-145">Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4696a-145">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="4696a-146">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="4696a-146">licenseGroupIds</span></span> | <span data-ttu-id="4696a-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="4696a-147">string</span></span> | <span data-ttu-id="4696a-148">Nie</span><span class="sxs-lookup"><span data-stu-id="4696a-148">No</span></span>       | <span data-ttu-id="4696a-149">Wartość wyliczania wskazująca grupę licencji przypisanych licencji.</span><span class="sxs-lookup"><span data-stu-id="4696a-149">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="4696a-150">Prawidłowe wartości: Grupa1, Grupa2 Grupa1 — ta grupa ma wszystkie produkty, których licencją można zarządzać w Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="4696a-150">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="4696a-151">Grupa2 — ta grupa ma tylko Minecraft licencji produktów.</span><span class="sxs-lookup"><span data-stu-id="4696a-151">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4696a-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4696a-152">Request headers</span></span>

<span data-ttu-id="4696a-153">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4696a-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4696a-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4696a-154">Request body</span></span>

<span data-ttu-id="4696a-155">Brak.</span><span class="sxs-lookup"><span data-stu-id="4696a-155">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4696a-156">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4696a-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4696a-157">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4696a-157">REST response</span></span>

<span data-ttu-id="4696a-158">Jeśli to się powiedzie, treść odpowiedzi zawiera kolekcję zasobów [licencji.](license-resources.md#license)</span><span class="sxs-lookup"><span data-stu-id="4696a-158">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4696a-159">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4696a-159">Response success and error codes</span></span>

<span data-ttu-id="4696a-160">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="4696a-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4696a-161">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4696a-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4696a-162">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4696a-162">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4696a-163">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4696a-163">Response example</span></span>

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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="4696a-164">Przykład odpowiedzi (nie znaleziono pasujących licencji)</span><span class="sxs-lookup"><span data-stu-id="4696a-164">Response example (no matching licenses found)</span></span>

<span data-ttu-id="4696a-165">Jeśli nie można znaleźć pasujących licencji dla określonych grup licencji, odpowiedź zawiera pustą kolekcję z elementem totalCount, którego wartość to 0.</span><span class="sxs-lookup"><span data-stu-id="4696a-165">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
