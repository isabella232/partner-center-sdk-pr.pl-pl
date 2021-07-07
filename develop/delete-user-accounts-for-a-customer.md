---
title: Usuwanie konta użytkownika dla klienta
description: Jak usunąć istniejące konto użytkownika dla klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973064"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="af05c-103">Usuwanie konta użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="af05c-103">Delete a user account for a customer</span></span>

<span data-ttu-id="af05c-104">W tym artykule wyjaśniono, jak usunąć istniejące konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="af05c-104">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af05c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af05c-105">Prerequisites</span></span>

- <span data-ttu-id="af05c-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="af05c-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="af05c-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af05c-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="af05c-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="af05c-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="af05c-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="af05c-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="af05c-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="af05c-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="af05c-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="af05c-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="af05c-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="af05c-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="af05c-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="af05c-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="af05c-114">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af05c-114">A user ID.</span></span> <span data-ttu-id="af05c-115">Jeśli nie masz identyfikatora użytkownika, zobacz Get a list of all user accounts for a customer (Uzyskiwanie listy wszystkich kont [użytkowników dla klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="af05c-115">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="af05c-116">Usuwanie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="af05c-116">Deleting a user account</span></span>

<span data-ttu-id="af05c-117">Po usunięciu konta użytkownika stan użytkownika jest ustawiany na nieaktywny **przez** 30 dni.</span><span class="sxs-lookup"><span data-stu-id="af05c-117">When you delete a user account, the user state is set to **inactive** for 30 days.</span></span> <span data-ttu-id="af05c-118">Po upływie 30 dni konto użytkownika i skojarzone z nim dane są przeczyszczane i nienadajne do nieodwracalności.</span><span class="sxs-lookup"><span data-stu-id="af05c-118">After thirty 30 days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="af05c-119">Możesz [przywrócić usunięte konto użytkownika dla klienta,](restore-a-user-for-a-customer.md) jeśli nieaktywne konto znajduje się w 30-dniowym oknie.</span><span class="sxs-lookup"><span data-stu-id="af05c-119">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the 30-day window.</span></span> <span data-ttu-id="af05c-120">Jednak po przywróceniu konta, które zostało usunięte i oznaczone jako nieaktywne, konto nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład w przypadku uzyskania listy wszystkich kont użytkowników dla [klienta).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="af05c-120">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="af05c-121">C\#</span><span class="sxs-lookup"><span data-stu-id="af05c-121">C\#</span></span>

<span data-ttu-id="af05c-122">Aby usunąć istniejące konto użytkownika klienta:</span><span class="sxs-lookup"><span data-stu-id="af05c-122">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="af05c-123">Użyj metody [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="af05c-123">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="af05c-124">Wywołaj [**metodę Users.ById,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af05c-124">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="af05c-125">Wywołaj [**metodę Delete,**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) aby usunąć użytkownika i ustawić stan użytkownika na nieaktywny.</span><span class="sxs-lookup"><span data-stu-id="af05c-125">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="af05c-126">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="af05c-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="af05c-127">**Project:** zestaw SDK Centrum partnerskiego **Samples, klasa**: DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="af05c-127">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="af05c-128">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="af05c-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="af05c-129">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="af05c-129">Request syntax</span></span>

| <span data-ttu-id="af05c-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="af05c-130">Method</span></span>     | <span data-ttu-id="af05c-131">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="af05c-131">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="af05c-132">DELETE</span><span class="sxs-lookup"><span data-stu-id="af05c-132">DELETE</span></span>     | <span data-ttu-id="af05c-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="af05c-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="af05c-134">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="af05c-134">URI parameters</span></span>

<span data-ttu-id="af05c-135">Użyj następujących parametrów zapytania, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af05c-135">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="af05c-136">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af05c-136">Name</span></span>                   | <span data-ttu-id="af05c-137">Typ</span><span class="sxs-lookup"><span data-stu-id="af05c-137">Type</span></span>     | <span data-ttu-id="af05c-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af05c-138">Required</span></span> | <span data-ttu-id="af05c-139">Opis</span><span class="sxs-lookup"><span data-stu-id="af05c-139">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="af05c-140">identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="af05c-140">customer-tenant-id</span></span>     | <span data-ttu-id="af05c-141">GUID</span><span class="sxs-lookup"><span data-stu-id="af05c-141">GUID</span></span>     | <span data-ttu-id="af05c-142">Y</span><span class="sxs-lookup"><span data-stu-id="af05c-142">Y</span></span>        | <span data-ttu-id="af05c-143">Wartość jest identyfikatorem **customer-tenant-id** w formacie identyfikatora GUID, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="af05c-143">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="af05c-144">user-id</span><span class="sxs-lookup"><span data-stu-id="af05c-144">user-id</span></span>                | <span data-ttu-id="af05c-145">GUID</span><span class="sxs-lookup"><span data-stu-id="af05c-145">GUID</span></span>     | <span data-ttu-id="af05c-146">Y</span><span class="sxs-lookup"><span data-stu-id="af05c-146">Y</span></span>        | <span data-ttu-id="af05c-147">Wartość jest identyfikatorem użytkownika w formacie **GUID,** który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af05c-147">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="af05c-148">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="af05c-148">Request headers</span></span>

<span data-ttu-id="af05c-149">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="af05c-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="af05c-150">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="af05c-150">Request body</span></span>

<span data-ttu-id="af05c-151">Brak.</span><span class="sxs-lookup"><span data-stu-id="af05c-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="af05c-152">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="af05c-152">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="af05c-153">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="af05c-153">REST response</span></span>

<span data-ttu-id="af05c-154">W przypadku powodzenia ta metoda zwraca kod **stanu 204 Brak** zawartości.</span><span class="sxs-lookup"><span data-stu-id="af05c-154">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="af05c-155">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="af05c-155">Response success and error codes</span></span>

<span data-ttu-id="af05c-156">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="af05c-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="af05c-157">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="af05c-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="af05c-158">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="af05c-158">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="af05c-159">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="af05c-159">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
