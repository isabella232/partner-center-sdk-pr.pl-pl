---
title: Ustawianie ról użytkownika dla klienta
description: W ramach konta klienta istnieje zestaw ról w katalogu. Do tych ról można przypisywać konta użytkowników.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768269"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="bb44a-104">Ustawianie ról użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="bb44a-104">Set user roles for a customer</span></span>

<span data-ttu-id="bb44a-105">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="bb44a-105">**Applies To**</span></span>

- <span data-ttu-id="bb44a-106">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="bb44a-106">Partner Center</span></span>

<span data-ttu-id="bb44a-107">W ramach konta klienta istnieje zestaw ról w katalogu.</span><span class="sxs-lookup"><span data-stu-id="bb44a-107">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="bb44a-108">Do tych ról można przypisywać konta użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bb44a-108">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb44a-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb44a-109">Prerequisites</span></span>

- <span data-ttu-id="bb44a-110">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bb44a-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bb44a-111">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb44a-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="bb44a-112">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bb44a-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="bb44a-113">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="bb44a-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="bb44a-114">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="bb44a-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="bb44a-115">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="bb44a-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="bb44a-116">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="bb44a-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="bb44a-117">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="bb44a-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="bb44a-118">C\#</span><span class="sxs-lookup"><span data-stu-id="bb44a-118">C\#</span></span>

<span data-ttu-id="bb44a-119">Aby przypisać rolę katalogu do użytkownika klienta, Utwórz nowy [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) z odpowiednimi szczegółami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb44a-119">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="bb44a-120">Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z określonym identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="bb44a-120">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="bb44a-121">W tym miejscu Użyj metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu, aby określić rolę.</span><span class="sxs-lookup"><span data-stu-id="bb44a-121">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="bb44a-122">Następnie uzyskaj dostęp do kolekcji **UserMembers** i użyj metody [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) , aby dodać członka nowego użytkownika do kolekcji członków użytkownika przypisanych do tej roli.</span><span class="sxs-lookup"><span data-stu-id="bb44a-122">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

<span data-ttu-id="bb44a-123">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bb44a-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bb44a-124">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="bb44a-124">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bb44a-125">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="bb44a-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bb44a-126">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="bb44a-126">Request syntax</span></span>

| <span data-ttu-id="bb44a-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="bb44a-127">Method</span></span>   | <span data-ttu-id="bb44a-128">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="bb44a-128">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bb44a-129">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="bb44a-129">**POST**</span></span> | <span data-ttu-id="bb44a-130">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers http/1.1</span><span class="sxs-lookup"><span data-stu-id="bb44a-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="bb44a-131">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="bb44a-131">URI parameter</span></span>

<span data-ttu-id="bb44a-132">Użyj następujących parametrów identyfikatora URI, aby zidentyfikować prawidłowego klienta i rolę.</span><span class="sxs-lookup"><span data-stu-id="bb44a-132">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="bb44a-133">Aby zidentyfikować użytkownika, do którego ma zostać przypisana rola, podaj informacje identyfikacyjne w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="bb44a-133">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="bb44a-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bb44a-134">Name</span></span>                   | <span data-ttu-id="bb44a-135">Typ</span><span class="sxs-lookup"><span data-stu-id="bb44a-135">Type</span></span>     | <span data-ttu-id="bb44a-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bb44a-136">Required</span></span> | <span data-ttu-id="bb44a-137">Opis</span><span class="sxs-lookup"><span data-stu-id="bb44a-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bb44a-138">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="bb44a-138">**customer-tenant-id**</span></span> | <span data-ttu-id="bb44a-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="bb44a-139">**guid**</span></span> | <span data-ttu-id="bb44a-140">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-140">Y</span></span>        | <span data-ttu-id="bb44a-141">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="bb44a-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="bb44a-142">**Identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="bb44a-142">**role-id**</span></span>            | <span data-ttu-id="bb44a-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="bb44a-143">**guid**</span></span> | <span data-ttu-id="bb44a-144">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-144">Y</span></span>        | <span data-ttu-id="bb44a-145">Wartość jest **identyfikatorem** GUID z sformatowaną rolą identyfikującą rolę, która ma zostać przypisana do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb44a-145">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="bb44a-146">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="bb44a-146">Request headers</span></span>

<span data-ttu-id="bb44a-147">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bb44a-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bb44a-148">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="bb44a-148">Request body</span></span>

<span data-ttu-id="bb44a-149">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="bb44a-149">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="bb44a-150">Nazwa</span><span class="sxs-lookup"><span data-stu-id="bb44a-150">Name</span></span>                  | <span data-ttu-id="bb44a-151">Typ</span><span class="sxs-lookup"><span data-stu-id="bb44a-151">Type</span></span>       | <span data-ttu-id="bb44a-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="bb44a-152">Required</span></span> | <span data-ttu-id="bb44a-153">Opis</span><span class="sxs-lookup"><span data-stu-id="bb44a-153">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="bb44a-154">**#C1**</span><span class="sxs-lookup"><span data-stu-id="bb44a-154">**Id**</span></span>                | <span data-ttu-id="bb44a-155">**parametry**</span><span class="sxs-lookup"><span data-stu-id="bb44a-155">**string**</span></span> | <span data-ttu-id="bb44a-156">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-156">Y</span></span>        | <span data-ttu-id="bb44a-157">Identyfikator użytkownika, który ma zostać dodany do roli.</span><span class="sxs-lookup"><span data-stu-id="bb44a-157">The Id of the user to add to the role.</span></span> |
| <span data-ttu-id="bb44a-158">**Nazwa wyświetlana**</span><span class="sxs-lookup"><span data-stu-id="bb44a-158">**DisplayName**</span></span>       | <span data-ttu-id="bb44a-159">**parametry**</span><span class="sxs-lookup"><span data-stu-id="bb44a-159">**string**</span></span> | <span data-ttu-id="bb44a-160">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-160">Y</span></span>        | <span data-ttu-id="bb44a-161">Przyjazna nazwa wyświetlana użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb44a-161">The friendly display name of the user.</span></span> |
| <span data-ttu-id="bb44a-162">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="bb44a-162">**UserPrincipalName**</span></span> | <span data-ttu-id="bb44a-163">**parametry**</span><span class="sxs-lookup"><span data-stu-id="bb44a-163">**string**</span></span> | <span data-ttu-id="bb44a-164">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-164">Y</span></span>        | <span data-ttu-id="bb44a-165">Nazwa podmiotu zabezpieczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb44a-165">The name of the user principal.</span></span>        |
| <span data-ttu-id="bb44a-166">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="bb44a-166">**Attributes**</span></span>        | <span data-ttu-id="bb44a-167">**Stream**</span><span class="sxs-lookup"><span data-stu-id="bb44a-167">**object**</span></span> | <span data-ttu-id="bb44a-168">Y</span><span class="sxs-lookup"><span data-stu-id="bb44a-168">Y</span></span>        | <span data-ttu-id="bb44a-169">Zawiera "ObjectType": "UserMember"</span><span class="sxs-lookup"><span data-stu-id="bb44a-169">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="bb44a-170">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="bb44a-170">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="bb44a-171">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="bb44a-171">REST response</span></span>

<span data-ttu-id="bb44a-172">Ta metoda zwraca konto użytkownika z identyfikatorem roli dołączonym, gdy użytkownik pomyślnie przypisał rolę.</span><span class="sxs-lookup"><span data-stu-id="bb44a-172">This method returns the user account with the role id attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bb44a-173">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bb44a-173">Response success and error codes</span></span>

<span data-ttu-id="bb44a-174">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="bb44a-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bb44a-175">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="bb44a-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bb44a-176">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bb44a-176">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bb44a-177">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="bb44a-177">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
