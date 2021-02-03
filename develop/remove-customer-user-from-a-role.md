---
title: Usuwanie użytkownika klienta z roli
description: Jak usunąć użytkownika z roli katalogu w ramach konta klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768306"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="09dd5-103">Usuwanie użytkownika klienta z roli</span><span class="sxs-lookup"><span data-stu-id="09dd5-103">Remove a customer user from a role</span></span>

<span data-ttu-id="09dd5-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="09dd5-104">**Applies To**</span></span>

- <span data-ttu-id="09dd5-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="09dd5-105">Partner Center</span></span>

<span data-ttu-id="09dd5-106">Jak usunąć użytkownika z roli katalogu w ramach konta klienta.</span><span class="sxs-lookup"><span data-stu-id="09dd5-106">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09dd5-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="09dd5-107">Prerequisites</span></span>

- <span data-ttu-id="09dd5-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="09dd5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="09dd5-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09dd5-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="09dd5-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="09dd5-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="09dd5-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="09dd5-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="09dd5-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="09dd5-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="09dd5-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="09dd5-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="09dd5-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="09dd5-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="09dd5-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="09dd5-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="09dd5-116">C\#</span><span class="sxs-lookup"><span data-stu-id="09dd5-116">C\#</span></span>

<span data-ttu-id="09dd5-117">Aby usunąć użytkownika z roli katalogu, wybierz klienta, który ma zostać zmodyfikowany za pomocą wywołania metody [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) , w tym miejscu określ rolę przy użyciu metody [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu.</span><span class="sxs-lookup"><span data-stu-id="09dd5-117">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="09dd5-118">Następnie uzyskaj dostęp do metody [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) , aby zidentyfikować użytkownika do usunięcia, i metodę [**delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) , aby usunąć użytkownika z roli.</span><span class="sxs-lookup"><span data-stu-id="09dd5-118">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="09dd5-119">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="09dd5-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="09dd5-120">**Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: RemoveCustomerUserMemberFromDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="09dd5-120">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="09dd5-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="09dd5-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="09dd5-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="09dd5-122">Request syntax</span></span>

| <span data-ttu-id="09dd5-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="09dd5-123">Method</span></span>     | <span data-ttu-id="09dd5-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="09dd5-124">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="09dd5-125">**USUNIĘTY**</span><span class="sxs-lookup"><span data-stu-id="09dd5-125">**DELETE**</span></span> | <span data-ttu-id="09dd5-126">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/directoryroles/{role-ID}/usermembers/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="09dd5-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="09dd5-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="09dd5-127">URI parameter</span></span>

<span data-ttu-id="09dd5-128">Użyj następujących parametrów identyfikatora URI, aby zidentyfikować prawidłowy klient, rolę i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09dd5-128">Use the following URI parameters to identify the correct customer, role and user.</span></span>

| <span data-ttu-id="09dd5-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="09dd5-129">Name</span></span>                   | <span data-ttu-id="09dd5-130">Typ</span><span class="sxs-lookup"><span data-stu-id="09dd5-130">Type</span></span>     | <span data-ttu-id="09dd5-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="09dd5-131">Required</span></span> | <span data-ttu-id="09dd5-132">Opis</span><span class="sxs-lookup"><span data-stu-id="09dd5-132">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="09dd5-133">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="09dd5-133">**customer-tenant-id**</span></span> | <span data-ttu-id="09dd5-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="09dd5-134">**guid**</span></span> | <span data-ttu-id="09dd5-135">Y</span><span class="sxs-lookup"><span data-stu-id="09dd5-135">Y</span></span>        | <span data-ttu-id="09dd5-136">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="09dd5-136">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="09dd5-137">**Identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="09dd5-137">**role-id**</span></span>            | <span data-ttu-id="09dd5-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="09dd5-138">**guid**</span></span> | <span data-ttu-id="09dd5-139">Y</span><span class="sxs-lookup"><span data-stu-id="09dd5-139">Y</span></span>        | <span data-ttu-id="09dd5-140">Wartość jest **identyfikatorem** GUID z sformatowaną rolą identyfikującą rolę.</span><span class="sxs-lookup"><span data-stu-id="09dd5-140">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="09dd5-141">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="09dd5-141">**user-id**</span></span>            | <span data-ttu-id="09dd5-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="09dd5-142">**guid**</span></span> | <span data-ttu-id="09dd5-143">Y</span><span class="sxs-lookup"><span data-stu-id="09dd5-143">Y</span></span>        | <span data-ttu-id="09dd5-144">Wartość jest **identyfikatorem użytkownika** w formacie identyfikatora GUID, który identyfikuje pojedyncze konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09dd5-144">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="09dd5-145">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="09dd5-145">Request headers</span></span>

<span data-ttu-id="09dd5-146">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="09dd5-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="09dd5-147">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="09dd5-147">Request body</span></span>

<span data-ttu-id="09dd5-148">Brak.</span><span class="sxs-lookup"><span data-stu-id="09dd5-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="09dd5-149">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="09dd5-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="09dd5-150">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="09dd5-150">REST response</span></span>

<span data-ttu-id="09dd5-151">Jeśli użytkownik zostanie pomyślnie usunięty z roli, treść odpowiedzi jest pusta.</span><span class="sxs-lookup"><span data-stu-id="09dd5-151">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="09dd5-152">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="09dd5-152">Response success and error codes</span></span>

<span data-ttu-id="09dd5-153">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="09dd5-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="09dd5-154">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="09dd5-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="09dd5-155">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="09dd5-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="09dd5-156">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="09dd5-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
