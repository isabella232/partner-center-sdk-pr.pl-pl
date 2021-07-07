---
title: Usuwanie użytkownika klienta z roli
description: Jak usunąć użytkownika z roli katalogu w ramach konta klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 36dc742c4f713131b4996d7dc945b6dd008a3ef5
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445650"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="9337e-103">Usuwanie użytkownika klienta z roli</span><span class="sxs-lookup"><span data-stu-id="9337e-103">Remove a customer user from a role</span></span>

<span data-ttu-id="9337e-104">Jak usunąć użytkownika z roli katalogu w ramach konta klienta.</span><span class="sxs-lookup"><span data-stu-id="9337e-104">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9337e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9337e-105">Prerequisites</span></span>

- <span data-ttu-id="9337e-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9337e-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9337e-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9337e-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9337e-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9337e-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9337e-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9337e-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9337e-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="9337e-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9337e-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="9337e-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9337e-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="9337e-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9337e-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9337e-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9337e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="9337e-114">C\#</span></span>

<span data-ttu-id="9337e-115">Aby usunąć użytkownika z roli katalogu, wybierz klienta z użytkownikiem do zmodyfikowania za pomocą wywołania metody [**IAggregatePartner.Customers.ById.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) W tym miejscu określ rolę przy użyciu metody [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) z identyfikatorem roli katalogu.</span><span class="sxs-lookup"><span data-stu-id="9337e-115">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="9337e-116">Następnie uzyskaj dostęp do [**metody UserMembers.ById,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) aby zidentyfikować użytkownika do usunięcia, oraz metody [**Delete,**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) aby usunąć użytkownika z roli.</span><span class="sxs-lookup"><span data-stu-id="9337e-116">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="9337e-117">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9337e-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9337e-118">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="9337e-118">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9337e-119">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="9337e-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9337e-120">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="9337e-120">Request syntax</span></span>

| <span data-ttu-id="9337e-121">Metoda</span><span class="sxs-lookup"><span data-stu-id="9337e-121">Method</span></span>     | <span data-ttu-id="9337e-122">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9337e-122">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9337e-123">**Usunąć**</span><span class="sxs-lookup"><span data-stu-id="9337e-123">**DELETE**</span></span> | <span data-ttu-id="9337e-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers/{identyfikator użytkownika} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9337e-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9337e-125">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="9337e-125">URI parameter</span></span>

<span data-ttu-id="9337e-126">Użyj następujących parametrów identyfikatorów URI, aby zidentyfikować prawidłowego klienta, rolę i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9337e-126">Use the following URI parameters to identify the correct customer, role, and user.</span></span>

| <span data-ttu-id="9337e-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="9337e-127">Name</span></span>                   | <span data-ttu-id="9337e-128">Typ</span><span class="sxs-lookup"><span data-stu-id="9337e-128">Type</span></span>     | <span data-ttu-id="9337e-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9337e-129">Required</span></span> | <span data-ttu-id="9337e-130">Opis</span><span class="sxs-lookup"><span data-stu-id="9337e-130">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="9337e-131">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="9337e-131">**customer-tenant-id**</span></span> | <span data-ttu-id="9337e-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="9337e-132">**guid**</span></span> | <span data-ttu-id="9337e-133">Y</span><span class="sxs-lookup"><span data-stu-id="9337e-133">Y</span></span>        | <span data-ttu-id="9337e-134">Wartość to identyfikator GUID sformatowany **jako customer-tenant-id,** który identyfikuje klienta.</span><span class="sxs-lookup"><span data-stu-id="9337e-134">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="9337e-135">**identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="9337e-135">**role-id**</span></span>            | <span data-ttu-id="9337e-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="9337e-136">**guid**</span></span> | <span data-ttu-id="9337e-137">Y</span><span class="sxs-lookup"><span data-stu-id="9337e-137">Y</span></span>        | <span data-ttu-id="9337e-138">Wartość jest identyfikatorem roli sformatowanym przez **identyfikator** GUID, który identyfikuje rolę.</span><span class="sxs-lookup"><span data-stu-id="9337e-138">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="9337e-139">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="9337e-139">**user-id**</span></span>            | <span data-ttu-id="9337e-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="9337e-140">**guid**</span></span> | <span data-ttu-id="9337e-141">Y</span><span class="sxs-lookup"><span data-stu-id="9337e-141">Y</span></span>        | <span data-ttu-id="9337e-142">Wartość jest identyfikatorem użytkownika sformatowanym w **formacie** GUID, który identyfikuje jedno konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9337e-142">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="9337e-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="9337e-143">Request headers</span></span>

<span data-ttu-id="9337e-144">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9337e-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9337e-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9337e-145">Request body</span></span>

<span data-ttu-id="9337e-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="9337e-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9337e-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="9337e-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9337e-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="9337e-148">REST response</span></span>

<span data-ttu-id="9337e-149">Jeśli użytkownik zostanie pomyślnie usunięty z roli, treść odpowiedzi będzie pusta.</span><span class="sxs-lookup"><span data-stu-id="9337e-149">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9337e-150">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9337e-150">Response success and error codes</span></span>

<span data-ttu-id="9337e-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="9337e-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9337e-152">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="9337e-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9337e-153">Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9337e-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9337e-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9337e-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
