---
title: Przywracanie usuniętego użytkownika dla klienta
description: Jak przywrócić usuniętego użytkownika według identyfikatora klienta i identyfikatora użytkownika.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768406"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="54c26-103">Przywracanie usuniętego użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="54c26-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="54c26-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="54c26-104">**Applies To**</span></span>

- <span data-ttu-id="54c26-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="54c26-105">Partner Center</span></span>

<span data-ttu-id="54c26-106">Jak przywrócić usuniętego **użytkownika** według identyfikatora klienta i identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-106">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54c26-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54c26-107">Prerequisites</span></span>

- <span data-ttu-id="54c26-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="54c26-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="54c26-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="54c26-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54c26-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="54c26-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="54c26-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="54c26-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="54c26-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="54c26-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="54c26-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="54c26-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="54c26-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="54c26-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="54c26-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="54c26-116">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-116">The user ID.</span></span> <span data-ttu-id="54c26-117">Jeśli nie masz identyfikatora użytkownika, zobacz [Wyświetlanie usuniętych użytkowników dla klienta](view-a-deleted-user.md).</span><span class="sxs-lookup"><span data-stu-id="54c26-117">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="54c26-118">Kiedy można przywrócić usunięte konto użytkownika?</span><span class="sxs-lookup"><span data-stu-id="54c26-118">When can you restore a deleted user account?</span></span>

<span data-ttu-id="54c26-119">Po usunięciu konta użytkownika stan użytkownika ma wartość "nieaktywne".</span><span class="sxs-lookup"><span data-stu-id="54c26-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="54c26-120">Nie jest to możliwe przez 30 dni, po upływie których konto użytkownika i powiązane z nim dane zostaną usunięte i nie można ich odzyskać.</span><span class="sxs-lookup"><span data-stu-id="54c26-120">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="54c26-121">Usunięte konto użytkownika można przywrócić tylko w tym trzydzieści-dniowym oknie.</span><span class="sxs-lookup"><span data-stu-id="54c26-121">You can only restore a deleted user account during this thirty-day window.</span></span> <span data-ttu-id="54c26-122">Po usunięciu i oznaczeniu elementu "nieaktywne" konto użytkownika nie jest już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu polecenia [Pobierz listę wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="54c26-122">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="54c26-123">C\#</span><span class="sxs-lookup"><span data-stu-id="54c26-123">C\#</span></span>

<span data-ttu-id="54c26-124">Aby przywrócić użytkownika, Utwórz nowe wystąpienie klasy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) i ustaw wartość właściwości [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span><span class="sxs-lookup"><span data-stu-id="54c26-124">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="54c26-125">Użytkownik zostanie przywrócony przez ustawienie stanu użytkownika jako aktywny.</span><span class="sxs-lookup"><span data-stu-id="54c26-125">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="54c26-126">Nie trzeba ponownie wypełniać pozostałych pól w zasobie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-126">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="54c26-127">Te wartości zostaną automatycznie przywrócone z usuniętego zasobu nieaktywnego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-127">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="54c26-128">Następnie użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta i metodę user [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-128">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="54c26-129">Na koniec Wywołaj metodę [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) i przekaż wystąpienie **CustomerUser** w celu wysłania żądania przywrócenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-129">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

<span data-ttu-id="54c26-130">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="54c26-130">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="54c26-131">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="54c26-131">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="54c26-132">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="54c26-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="54c26-133">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="54c26-133">Request syntax</span></span>

| <span data-ttu-id="54c26-134">Metoda</span><span class="sxs-lookup"><span data-stu-id="54c26-134">Method</span></span>    | <span data-ttu-id="54c26-135">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="54c26-135">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54c26-136">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="54c26-136">**PATCH**</span></span> | <span data-ttu-id="54c26-137">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="54c26-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="54c26-138">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="54c26-138">URI parameter</span></span>

<span data-ttu-id="54c26-139">Użyj następujących parametrów zapytania, aby określić identyfikator klienta i identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-139">Use the following query parameters to specify the customer id and user id.</span></span>

| <span data-ttu-id="54c26-140">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54c26-140">Name</span></span>                   | <span data-ttu-id="54c26-141">Typ</span><span class="sxs-lookup"><span data-stu-id="54c26-141">Type</span></span>     | <span data-ttu-id="54c26-142">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54c26-142">Required</span></span> | <span data-ttu-id="54c26-143">Opis</span><span class="sxs-lookup"><span data-stu-id="54c26-143">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="54c26-144">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="54c26-144">**customer-tenant-id**</span></span> | <span data-ttu-id="54c26-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="54c26-145">**guid**</span></span> | <span data-ttu-id="54c26-146">Y</span><span class="sxs-lookup"><span data-stu-id="54c26-146">Y</span></span>        | <span data-ttu-id="54c26-147">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników do danego klienta.</span><span class="sxs-lookup"><span data-stu-id="54c26-147">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="54c26-148">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="54c26-148">**user-id**</span></span>            | <span data-ttu-id="54c26-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="54c26-149">**guid**</span></span> | <span data-ttu-id="54c26-150">Y</span><span class="sxs-lookup"><span data-stu-id="54c26-150">Y</span></span>        | <span data-ttu-id="54c26-151">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-151">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="54c26-152">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="54c26-152">Request headers</span></span>

<span data-ttu-id="54c26-153">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="54c26-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="54c26-154">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="54c26-154">Request body</span></span>

<span data-ttu-id="54c26-155">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="54c26-155">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="54c26-156">Nazwa</span><span class="sxs-lookup"><span data-stu-id="54c26-156">Name</span></span>       | <span data-ttu-id="54c26-157">Typ</span><span class="sxs-lookup"><span data-stu-id="54c26-157">Type</span></span>   | <span data-ttu-id="54c26-158">Wymagane</span><span class="sxs-lookup"><span data-stu-id="54c26-158">Required</span></span> | <span data-ttu-id="54c26-159">Opis</span><span class="sxs-lookup"><span data-stu-id="54c26-159">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="54c26-160">Stan</span><span class="sxs-lookup"><span data-stu-id="54c26-160">State</span></span>      | <span data-ttu-id="54c26-161">ciąg</span><span class="sxs-lookup"><span data-stu-id="54c26-161">string</span></span> | <span data-ttu-id="54c26-162">Y</span><span class="sxs-lookup"><span data-stu-id="54c26-162">Y</span></span>        | <span data-ttu-id="54c26-163">Stan użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54c26-163">The user state.</span></span> <span data-ttu-id="54c26-164">Aby przywrócić usuniętego użytkownika, ten ciąg musi zawierać wartość "Active".</span><span class="sxs-lookup"><span data-stu-id="54c26-164">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="54c26-165">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="54c26-165">Attributes</span></span> | <span data-ttu-id="54c26-166">object</span><span class="sxs-lookup"><span data-stu-id="54c26-166">object</span></span> | <span data-ttu-id="54c26-167">N</span><span class="sxs-lookup"><span data-stu-id="54c26-167">N</span></span>        | <span data-ttu-id="54c26-168">Zawiera "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="54c26-168">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="54c26-169">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="54c26-169">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="54c26-170">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="54c26-170">REST response</span></span>

<span data-ttu-id="54c26-171">Jeśli to się powiedzie, odpowiedź zwróci przywrócone informacje o użytkowniku w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="54c26-171">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="54c26-172">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="54c26-172">Response success and error codes</span></span>

<span data-ttu-id="54c26-173">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="54c26-173">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="54c26-174">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="54c26-174">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="54c26-175">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="54c26-175">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="54c26-176">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="54c26-176">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
