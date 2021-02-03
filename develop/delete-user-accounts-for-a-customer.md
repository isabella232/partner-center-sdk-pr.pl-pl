---
title: Usuwanie konta użytkownika dla klienta
description: Jak usunąć istniejące konto użytkownika dla klienta.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768129"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="918a5-103">Usuwanie konta użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="918a5-103">Delete a user account for a customer</span></span>

<span data-ttu-id="918a5-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="918a5-104">**Applies to:**</span></span>

- <span data-ttu-id="918a5-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="918a5-105">Partner Center</span></span>

<span data-ttu-id="918a5-106">W tym artykule wyjaśniono, jak usunąć istniejące konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="918a5-106">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="918a5-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="918a5-107">Prerequisites</span></span>

- <span data-ttu-id="918a5-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="918a5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="918a5-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="918a5-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="918a5-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="918a5-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="918a5-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="918a5-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="918a5-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="918a5-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="918a5-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="918a5-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="918a5-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="918a5-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="918a5-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="918a5-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="918a5-116">Identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="918a5-116">A user ID.</span></span> <span data-ttu-id="918a5-117">Jeśli nie masz identyfikatora użytkownika, zobacz temat [Pobieranie listy wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="918a5-117">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="918a5-118">Usuwanie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="918a5-118">Deleting a user account</span></span>

<span data-ttu-id="918a5-119">Po usunięciu konta użytkownika stan użytkownika jest ustawiony jako **nieaktywny** przez 30 dni.</span><span class="sxs-lookup"><span data-stu-id="918a5-119">When you delete a user account, the user state is set to **inactive** for thirty days.</span></span> <span data-ttu-id="918a5-120">Po upływie 30 dni konto użytkownika i powiązane z nim dane są przeczyszczane i niemożliwym do odzyskania.</span><span class="sxs-lookup"><span data-stu-id="918a5-120">After thirty days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="918a5-121">Można [przywrócić usunięte konto użytkownika dla klienta](restore-a-user-for-a-customer.md) , jeśli konto nieaktywne znajduje się w oknie trzydziestu dni.</span><span class="sxs-lookup"><span data-stu-id="918a5-121">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the thirty day window.</span></span> <span data-ttu-id="918a5-122">Jednak podczas przywracania konta, które zostało usunięte i oznaczone jako nieaktywne, konto nie jest już zwracane jako element członkowski kolekcji użytkowników (na przykład po wyświetleniu [listy wszystkich kont użytkowników dla klienta](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="918a5-122">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="918a5-123">C\#</span><span class="sxs-lookup"><span data-stu-id="918a5-123">C\#</span></span>

<span data-ttu-id="918a5-124">Aby usunąć istniejące konto użytkownika klienta:</span><span class="sxs-lookup"><span data-stu-id="918a5-124">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="918a5-125">Użyj metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta, aby zidentyfikować klienta.</span><span class="sxs-lookup"><span data-stu-id="918a5-125">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="918a5-126">Wywołaj metodę [**users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) , aby zidentyfikować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="918a5-126">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="918a5-127">Wywołaj metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) , aby usunąć użytkownika i ustawić stan użytkownika jako nieaktywny.</span><span class="sxs-lookup"><span data-stu-id="918a5-127">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="918a5-128">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="918a5-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="918a5-129">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="918a5-129">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="918a5-130">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="918a5-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="918a5-131">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="918a5-131">Request syntax</span></span>

| <span data-ttu-id="918a5-132">Metoda</span><span class="sxs-lookup"><span data-stu-id="918a5-132">Method</span></span>     | <span data-ttu-id="918a5-133">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="918a5-133">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="918a5-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="918a5-134">DELETE</span></span>     | <span data-ttu-id="918a5-135">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="918a5-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="918a5-136">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="918a5-136">URI parameters</span></span>

<span data-ttu-id="918a5-137">Użyj następujących parametrów zapytania, aby zidentyfikować klienta i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="918a5-137">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="918a5-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="918a5-138">Name</span></span>                   | <span data-ttu-id="918a5-139">Typ</span><span class="sxs-lookup"><span data-stu-id="918a5-139">Type</span></span>     | <span data-ttu-id="918a5-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="918a5-140">Required</span></span> | <span data-ttu-id="918a5-141">Opis</span><span class="sxs-lookup"><span data-stu-id="918a5-141">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="918a5-142">Identyfikator dzierżawy klienta</span><span class="sxs-lookup"><span data-stu-id="918a5-142">customer-tenant-id</span></span>     | <span data-ttu-id="918a5-143">GUID</span><span class="sxs-lookup"><span data-stu-id="918a5-143">GUID</span></span>     | <span data-ttu-id="918a5-144">Y</span><span class="sxs-lookup"><span data-stu-id="918a5-144">Y</span></span>        | <span data-ttu-id="918a5-145">Wartość jest formatem **identyfikatora dzierżawy klienta** w formacie GUID, który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="918a5-145">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="918a5-146">user-id</span><span class="sxs-lookup"><span data-stu-id="918a5-146">user-id</span></span>                | <span data-ttu-id="918a5-147">GUID</span><span class="sxs-lookup"><span data-stu-id="918a5-147">GUID</span></span>     | <span data-ttu-id="918a5-148">Y</span><span class="sxs-lookup"><span data-stu-id="918a5-148">Y</span></span>        | <span data-ttu-id="918a5-149">Wartość jest **identyfikatorem użytkownika** sformatowanym przez identyfikator GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="918a5-149">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="918a5-150">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="918a5-150">Request headers</span></span>

<span data-ttu-id="918a5-151">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="918a5-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="918a5-152">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="918a5-152">Request body</span></span>

<span data-ttu-id="918a5-153">Brak.</span><span class="sxs-lookup"><span data-stu-id="918a5-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="918a5-154">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="918a5-154">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="918a5-155">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="918a5-155">REST response</span></span>

<span data-ttu-id="918a5-156">Jeśli to się powiedzie, ta metoda zwraca 204 kod stanu **zawartości** .</span><span class="sxs-lookup"><span data-stu-id="918a5-156">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="918a5-157">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="918a5-157">Response success and error codes</span></span>

<span data-ttu-id="918a5-158">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="918a5-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="918a5-159">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="918a5-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="918a5-160">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="918a5-160">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="918a5-161">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="918a5-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
