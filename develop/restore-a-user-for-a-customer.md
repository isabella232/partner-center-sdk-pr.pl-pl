---
title: Przywracanie usuniętego użytkownika dla klienta
description: Jak przywrócić usuniętego użytkownika według identyfikatora klienta i identyfikatora użytkownika.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445718"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="63e21-103">Przywracanie usuniętego użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="63e21-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="63e21-104">Jak przywrócić usuniętego **użytkownika według** identyfikatora klienta i identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-104">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63e21-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="63e21-105">Prerequisites</span></span>

- <span data-ttu-id="63e21-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="63e21-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="63e21-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="63e21-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63e21-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="63e21-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="63e21-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="63e21-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="63e21-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="63e21-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="63e21-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="63e21-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="63e21-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="63e21-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63e21-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="63e21-114">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-114">The user ID.</span></span> <span data-ttu-id="63e21-115">Jeśli nie masz identyfikatora użytkownika, zobacz [Wyświetlanie usuniętych użytkowników dla klienta](view-a-deleted-user.md).</span><span class="sxs-lookup"><span data-stu-id="63e21-115">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="63e21-116">Kiedy można przywrócić usunięte konto użytkownika?</span><span class="sxs-lookup"><span data-stu-id="63e21-116">When can you restore a deleted user account?</span></span>

<span data-ttu-id="63e21-117">Stan użytkownika jest ustawiany na "nieaktywny" podczas usuwania konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-117">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="63e21-118">Pozostanie w ten sposób przez 30 dni, po czym konto użytkownika i skojarzone z nim dane są przeczyszczania i nie można ich uzyskać.</span><span class="sxs-lookup"><span data-stu-id="63e21-118">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="63e21-119">Usunięte konto użytkownika można przywrócić tylko w tym 30-dniowym oknie.</span><span class="sxs-lookup"><span data-stu-id="63e21-119">You can only restore a deleted user account during this 30-day window.</span></span> <span data-ttu-id="63e21-120">Gdy konto użytkownika zostanie usunięte i oznaczone jako "nieaktywne", nie będzie już zwracane jako członek kolekcji użytkowników (na przykład przy użyciu funkcji Pobierz listę wszystkich kont użytkowników [dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="63e21-120">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="63e21-121">C\#</span><span class="sxs-lookup"><span data-stu-id="63e21-121">C\#</span></span>

<span data-ttu-id="63e21-122">Aby przywrócić użytkownika, utwórz nowe wystąpienie klasy [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) i ustaw wartość właściwości [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) na [**UserState.Active.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)</span><span class="sxs-lookup"><span data-stu-id="63e21-122">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="63e21-123">Usunięty użytkownik można przywrócić, ustawiając jego stan na aktywny.</span><span class="sxs-lookup"><span data-stu-id="63e21-123">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="63e21-124">Nie trzeba ponownieopulacji pozostałych pól w zasobie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-124">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="63e21-125">Te wartości zostaną automatycznie przywrócone z usuniętego, nieaktywnego zasobu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-125">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="63e21-126">Następnie użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta w celu zidentyfikowania klienta, a metody [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) w celu zidentyfikowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-126">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="63e21-127">Na koniec wywołaj [**metodę Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) i przekaż wystąpienie **CustomerUser,** aby wysłać żądanie przywrócenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-127">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

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

<span data-ttu-id="63e21-128">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="63e21-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="63e21-129">**Project:** zestaw SDK Centrum partnerskiego Samples Class : CustomerUserRestore.cs **(Klasa przykładów** zestaw SDK Centrum partnerskiego: CustomerUserRestore.cs)</span><span class="sxs-lookup"><span data-stu-id="63e21-129">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="63e21-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="63e21-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="63e21-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="63e21-131">Request syntax</span></span>

| <span data-ttu-id="63e21-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="63e21-132">Method</span></span>    | <span data-ttu-id="63e21-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="63e21-133">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63e21-134">**Patch**</span><span class="sxs-lookup"><span data-stu-id="63e21-134">**PATCH**</span></span> | <span data-ttu-id="63e21-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="63e21-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="63e21-136">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="63e21-136">URI parameter</span></span>

<span data-ttu-id="63e21-137">Użyj następujących parametrów zapytania, aby określić identyfikator klienta i identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-137">Use the following query parameters to specify the customer ID and user ID.</span></span>

| <span data-ttu-id="63e21-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="63e21-138">Name</span></span>                   | <span data-ttu-id="63e21-139">Typ</span><span class="sxs-lookup"><span data-stu-id="63e21-139">Type</span></span>     | <span data-ttu-id="63e21-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="63e21-140">Required</span></span> | <span data-ttu-id="63e21-141">Opis</span><span class="sxs-lookup"><span data-stu-id="63e21-141">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63e21-142">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="63e21-142">**customer-tenant-id**</span></span> | <span data-ttu-id="63e21-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="63e21-143">**guid**</span></span> | <span data-ttu-id="63e21-144">Y</span><span class="sxs-lookup"><span data-stu-id="63e21-144">Y</span></span>        | <span data-ttu-id="63e21-145">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników do danego klienta.</span><span class="sxs-lookup"><span data-stu-id="63e21-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="63e21-146">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="63e21-146">**user-id**</span></span>            | <span data-ttu-id="63e21-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="63e21-147">**guid**</span></span> | <span data-ttu-id="63e21-148">Y</span><span class="sxs-lookup"><span data-stu-id="63e21-148">Y</span></span>        | <span data-ttu-id="63e21-149">Wartość jest identyfikatorem użytkownika sformatowanym w **formacie** GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-149">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="63e21-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="63e21-150">Request headers</span></span>

<span data-ttu-id="63e21-151">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="63e21-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="63e21-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="63e21-152">Request body</span></span>

<span data-ttu-id="63e21-153">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="63e21-153">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="63e21-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="63e21-154">Name</span></span>       | <span data-ttu-id="63e21-155">Typ</span><span class="sxs-lookup"><span data-stu-id="63e21-155">Type</span></span>   | <span data-ttu-id="63e21-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="63e21-156">Required</span></span> | <span data-ttu-id="63e21-157">Opis</span><span class="sxs-lookup"><span data-stu-id="63e21-157">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="63e21-158">Stan</span><span class="sxs-lookup"><span data-stu-id="63e21-158">State</span></span>      | <span data-ttu-id="63e21-159">ciąg</span><span class="sxs-lookup"><span data-stu-id="63e21-159">string</span></span> | <span data-ttu-id="63e21-160">Y</span><span class="sxs-lookup"><span data-stu-id="63e21-160">Y</span></span>        | <span data-ttu-id="63e21-161">Stan użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63e21-161">The user state.</span></span> <span data-ttu-id="63e21-162">Aby przywrócić usuniętego użytkownika, ten ciąg musi zawierać wartość "active".</span><span class="sxs-lookup"><span data-stu-id="63e21-162">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="63e21-163">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="63e21-163">Attributes</span></span> | <span data-ttu-id="63e21-164">object</span><span class="sxs-lookup"><span data-stu-id="63e21-164">object</span></span> | <span data-ttu-id="63e21-165">N</span><span class="sxs-lookup"><span data-stu-id="63e21-165">N</span></span>        | <span data-ttu-id="63e21-166">Zawiera "ObjectType": "CustomerUser".</span><span class="sxs-lookup"><span data-stu-id="63e21-166">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="63e21-167">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="63e21-167">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="63e21-168">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="63e21-168">REST response</span></span>

<span data-ttu-id="63e21-169">Jeśli to się powiedzie, odpowiedź zwróci przywrócone informacje o użytkowniku w treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="63e21-169">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="63e21-170">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="63e21-170">Response success and error codes</span></span>

<span data-ttu-id="63e21-171">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="63e21-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="63e21-172">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="63e21-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="63e21-173">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="63e21-173">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="63e21-174">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="63e21-174">Response example</span></span>

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
