---
title: Ustawianie ról użytkownika dla klienta
description: W ramach konta klienta istnieje zestaw ról katalogu. Do tych ról można przypisać konta użytkowników.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446704"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="40368-104">Ustawianie ról użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="40368-104">Set user roles for a customer</span></span>

<span data-ttu-id="40368-105">W ramach konta klienta istnieje zestaw ról katalogu.</span><span class="sxs-lookup"><span data-stu-id="40368-105">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="40368-106">Do tych ról można przypisać konta użytkowników.</span><span class="sxs-lookup"><span data-stu-id="40368-106">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40368-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40368-107">Prerequisites</span></span>

- <span data-ttu-id="40368-108">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="40368-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40368-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40368-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="40368-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40368-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="40368-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="40368-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="40368-112">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="40368-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="40368-113">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="40368-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="40368-114">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="40368-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="40368-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40368-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="40368-116">C\#</span><span class="sxs-lookup"><span data-stu-id="40368-116">C\#</span></span>

<span data-ttu-id="40368-117">Aby przypisać rolę katalogu do użytkownika klienta, utwórz nowego użytkownika [**UserMember z**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) odpowiednimi szczegółami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40368-117">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="40368-118">Następnie wywołaj metodę [**IAggregatePartner.Customers.ById z**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) określonym identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="40368-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="40368-119">W tym miejscu użyj [**metody DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu, aby określić rolę.</span><span class="sxs-lookup"><span data-stu-id="40368-119">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="40368-120">Następnie uzyskaj dostęp do **kolekcji UserMembers** i użyj metody [**Create,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) aby dodać nowego członka użytkownika do kolekcji członków użytkowników przypisanych do tej roli.</span><span class="sxs-lookup"><span data-stu-id="40368-120">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

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

<span data-ttu-id="40368-121">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="40368-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="40368-122">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="40368-122">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="40368-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="40368-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40368-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="40368-124">Request syntax</span></span>

| <span data-ttu-id="40368-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="40368-125">Method</span></span>   | <span data-ttu-id="40368-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="40368-126">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40368-127">**Post**</span><span class="sxs-lookup"><span data-stu-id="40368-127">**POST**</span></span> | <span data-ttu-id="40368-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="40368-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="40368-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="40368-129">URI parameter</span></span>

<span data-ttu-id="40368-130">Użyj następujących parametrów URI, aby zidentyfikować prawidłowego klienta i rolę.</span><span class="sxs-lookup"><span data-stu-id="40368-130">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="40368-131">Aby zidentyfikować użytkownika, do którego ma zostać przypisana rola, należy podać informacje identyfikujące w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="40368-131">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="40368-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="40368-132">Name</span></span>                   | <span data-ttu-id="40368-133">Typ</span><span class="sxs-lookup"><span data-stu-id="40368-133">Type</span></span>     | <span data-ttu-id="40368-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="40368-134">Required</span></span> | <span data-ttu-id="40368-135">Opis</span><span class="sxs-lookup"><span data-stu-id="40368-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40368-136">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="40368-136">**customer-tenant-id**</span></span> | <span data-ttu-id="40368-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="40368-137">**guid**</span></span> | <span data-ttu-id="40368-138">Y</span><span class="sxs-lookup"><span data-stu-id="40368-138">Y</span></span>        | <span data-ttu-id="40368-139">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="40368-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="40368-140">**identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="40368-140">**role-id**</span></span>            | <span data-ttu-id="40368-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="40368-141">**guid**</span></span> | <span data-ttu-id="40368-142">Y</span><span class="sxs-lookup"><span data-stu-id="40368-142">Y</span></span>        | <span data-ttu-id="40368-143">Wartość jest identyfikatorem roli sformatowanym przez **identyfikator** GUID, który identyfikuje rolę, która ma zostać przypisana do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40368-143">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="40368-144">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="40368-144">Request headers</span></span>

<span data-ttu-id="40368-145">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="40368-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40368-146">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="40368-146">Request body</span></span>

<span data-ttu-id="40368-147">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="40368-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="40368-148">Nazwa</span><span class="sxs-lookup"><span data-stu-id="40368-148">Name</span></span>                  | <span data-ttu-id="40368-149">Typ</span><span class="sxs-lookup"><span data-stu-id="40368-149">Type</span></span>       | <span data-ttu-id="40368-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="40368-150">Required</span></span> | <span data-ttu-id="40368-151">Opis</span><span class="sxs-lookup"><span data-stu-id="40368-151">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="40368-152">**Identyfikator**</span><span class="sxs-lookup"><span data-stu-id="40368-152">**Id**</span></span>                | <span data-ttu-id="40368-153">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="40368-153">**string**</span></span> | <span data-ttu-id="40368-154">Y</span><span class="sxs-lookup"><span data-stu-id="40368-154">Y</span></span>        | <span data-ttu-id="40368-155">Identyfikator użytkownika, który ma dodać do roli.</span><span class="sxs-lookup"><span data-stu-id="40368-155">The ID of the user to add to the role.</span></span> |
| <span data-ttu-id="40368-156">**Nazwa wyświetlana**</span><span class="sxs-lookup"><span data-stu-id="40368-156">**DisplayName**</span></span>       | <span data-ttu-id="40368-157">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="40368-157">**string**</span></span> | <span data-ttu-id="40368-158">Y</span><span class="sxs-lookup"><span data-stu-id="40368-158">Y</span></span>        | <span data-ttu-id="40368-159">Przyjazna nazwa wyświetlana użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40368-159">The friendly display name of the user.</span></span> |
| <span data-ttu-id="40368-160">**Userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="40368-160">**UserPrincipalName**</span></span> | <span data-ttu-id="40368-161">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="40368-161">**string**</span></span> | <span data-ttu-id="40368-162">Y</span><span class="sxs-lookup"><span data-stu-id="40368-162">Y</span></span>        | <span data-ttu-id="40368-163">Nazwa podmiotu zabezpieczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="40368-163">The name of the user principal.</span></span>        |
| <span data-ttu-id="40368-164">**Atrybuty**</span><span class="sxs-lookup"><span data-stu-id="40368-164">**Attributes**</span></span>        | <span data-ttu-id="40368-165">**Obiektu**</span><span class="sxs-lookup"><span data-stu-id="40368-165">**object**</span></span> | <span data-ttu-id="40368-166">Y</span><span class="sxs-lookup"><span data-stu-id="40368-166">Y</span></span>        | <span data-ttu-id="40368-167">Zawiera "ObjectType":"UserMember"</span><span class="sxs-lookup"><span data-stu-id="40368-167">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="40368-168">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="40368-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="40368-169">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="40368-169">REST response</span></span>

<span data-ttu-id="40368-170">Ta metoda zwraca konto użytkownika z dołączonym identyfikatorem roli, gdy użytkownik zostanie pomyślnie przypisany do roli.</span><span class="sxs-lookup"><span data-stu-id="40368-170">This method returns the user account with the role ID attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40368-171">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40368-171">Response success and error codes</span></span>

<span data-ttu-id="40368-172">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="40368-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40368-173">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="40368-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40368-174">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="40368-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40368-175">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40368-175">Response example</span></span>

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
