---
title: Pobieranie ról użytkowników dla klienta
description: Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Warianty obejmują Pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników dla klienta i pobieranie listy użytkowników, którzy mają daną rolę.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767813"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="75ad2-104">Pobieranie ról użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="75ad2-104">Get user roles for a customer</span></span>

<span data-ttu-id="75ad2-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="75ad2-105">**Applies To**</span></span>

- <span data-ttu-id="75ad2-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="75ad2-106">Partner Center</span></span>

<span data-ttu-id="75ad2-107">Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75ad2-107">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="75ad2-108">Warianty obejmują Pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników dla klienta i pobieranie listy użytkowników, którzy mają daną rolę.</span><span class="sxs-lookup"><span data-stu-id="75ad2-108">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75ad2-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75ad2-109">Prerequisites</span></span>

- <span data-ttu-id="75ad2-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="75ad2-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75ad2-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75ad2-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="75ad2-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75ad2-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="75ad2-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="75ad2-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="75ad2-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="75ad2-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="75ad2-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="75ad2-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="75ad2-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="75ad2-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="75ad2-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="75ad2-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="75ad2-118">C\#</span><span class="sxs-lookup"><span data-stu-id="75ad2-118">C\#</span></span>

<span data-ttu-id="75ad2-119">Aby pobrać wszystkie role katalogu dla określonego klienta, najpierw Pobierz określony identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="75ad2-119">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="75ad2-120">Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="75ad2-120">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="75ad2-121">Następnie Wywołaj Właściwość **DirectoryRoles** , a następnie metodę **Get ()** lub **GetAsync ()**.</span><span class="sxs-lookup"><span data-stu-id="75ad2-121">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="75ad2-122">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="75ad2-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="75ad2-123">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="75ad2-123">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="75ad2-124">Aby pobrać listę użytkowników klientów, którzy mają daną rolę, najpierw Pobierz określony identyfikator klienta i identyfikator roli katalogu.</span><span class="sxs-lookup"><span data-stu-id="75ad2-124">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="75ad2-125">Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="75ad2-125">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="75ad2-126">Następnie Wywołaj Właściwość **DirectoryRoles** , a następnie metodę **ById ()** , a następnie właściwość **UserMembers** , a następnie metodę **Get ()** lub **GetAsync ()** .</span><span class="sxs-lookup"><span data-stu-id="75ad2-126">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="75ad2-127">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="75ad2-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="75ad2-128">**Project**: PartnerSDK. FeatureSamples **Klasa**: GetCustomerDirectoryRoleUserMembers.cs</span><span class="sxs-lookup"><span data-stu-id="75ad2-128">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="75ad2-129">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="75ad2-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75ad2-130">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="75ad2-130">Request syntax</span></span>

| <span data-ttu-id="75ad2-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="75ad2-131">Method</span></span>  | <span data-ttu-id="75ad2-132">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="75ad2-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="75ad2-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="75ad2-133">**GET**</span></span> | <span data-ttu-id="75ad2-134">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="75ad2-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="75ad2-135">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="75ad2-135">**GET**</span></span> | <span data-ttu-id="75ad2-136">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="75ad2-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="75ad2-137">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="75ad2-137">**GET**</span></span> | <span data-ttu-id="75ad2-138">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="75ad2-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="75ad2-139">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="75ad2-139">URI parameter</span></span>

<span data-ttu-id="75ad2-140">Użyj następującego parametru zapytania, aby zidentyfikować odpowiedniego klienta.</span><span class="sxs-lookup"><span data-stu-id="75ad2-140">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="75ad2-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="75ad2-141">Name</span></span>                   | <span data-ttu-id="75ad2-142">Typ</span><span class="sxs-lookup"><span data-stu-id="75ad2-142">Type</span></span>     | <span data-ttu-id="75ad2-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="75ad2-143">Required</span></span> | <span data-ttu-id="75ad2-144">Opis</span><span class="sxs-lookup"><span data-stu-id="75ad2-144">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="75ad2-145">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="75ad2-145">**customer-tenant-id**</span></span> | <span data-ttu-id="75ad2-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="75ad2-146">**guid**</span></span> | <span data-ttu-id="75ad2-147">Y</span><span class="sxs-lookup"><span data-stu-id="75ad2-147">Y</span></span>        | <span data-ttu-id="75ad2-148">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="75ad2-148">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="75ad2-149">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="75ad2-149">**user-id**</span></span>            | <span data-ttu-id="75ad2-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="75ad2-150">**guid**</span></span> | <span data-ttu-id="75ad2-151">N</span><span class="sxs-lookup"><span data-stu-id="75ad2-151">N</span></span>        | <span data-ttu-id="75ad2-152">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75ad2-152">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="75ad2-153">**Identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="75ad2-153">**role-id**</span></span>            | <span data-ttu-id="75ad2-154">**guid**</span><span class="sxs-lookup"><span data-stu-id="75ad2-154">**guid**</span></span> | <span data-ttu-id="75ad2-155">N</span><span class="sxs-lookup"><span data-stu-id="75ad2-155">N</span></span>        | <span data-ttu-id="75ad2-156">Wartość jest **identyfikatorem** GUID o formacie ID, który należy do typu roli.</span><span class="sxs-lookup"><span data-stu-id="75ad2-156">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="75ad2-157">Identyfikatory te można uzyskać, badając wszystkie role katalogu dla klienta w ramach wszystkich kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="75ad2-157">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="75ad2-158">(Drugi scenariusz, powyżej).</span><span class="sxs-lookup"><span data-stu-id="75ad2-158">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="75ad2-159">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="75ad2-159">Request headers</span></span>

<span data-ttu-id="75ad2-160">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="75ad2-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75ad2-161">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="75ad2-161">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="75ad2-162">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="75ad2-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="75ad2-163">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="75ad2-163">REST response</span></span>

<span data-ttu-id="75ad2-164">Jeśli to się powiedzie, metoda zwraca listę ról skojarzonych z danym kontem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75ad2-164">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75ad2-165">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="75ad2-165">Response success and error codes</span></span>

<span data-ttu-id="75ad2-166">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="75ad2-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75ad2-167">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="75ad2-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75ad2-168">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="75ad2-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75ad2-169">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="75ad2-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
