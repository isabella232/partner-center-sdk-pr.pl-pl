---
title: Pobieranie ról użytkowników dla klienta
description: Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika. Odmiany obejmują pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników klienta i pobieranie listy użytkowników, którzy mają danej roli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f58e8b7eae5bb47265bb1ac83fcdcd160f735d2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445922"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="13d00-104">Pobieranie ról użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="13d00-104">Get user roles for a customer</span></span>

<span data-ttu-id="13d00-105">Pobierz listę wszystkich ról/uprawnień dołączonych do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13d00-105">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="13d00-106">Odmiany obejmują pobieranie listy wszystkich uprawnień dla wszystkich kont użytkowników klienta i pobieranie listy użytkowników, którzy mają danej roli.</span><span class="sxs-lookup"><span data-stu-id="13d00-106">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13d00-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13d00-107">Prerequisites</span></span>

- <span data-ttu-id="13d00-108">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="13d00-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="13d00-109">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13d00-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="13d00-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13d00-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="13d00-111">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="13d00-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="13d00-112">Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="13d00-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="13d00-113">Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**.</span><span class="sxs-lookup"><span data-stu-id="13d00-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="13d00-114">Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="13d00-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="13d00-115">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="13d00-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="13d00-116">C\#</span><span class="sxs-lookup"><span data-stu-id="13d00-116">C\#</span></span>

<span data-ttu-id="13d00-117">Aby pobrać wszystkie role katalogu dla określonego klienta, najpierw pobierz określony identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="13d00-117">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="13d00-118">Następnie użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="13d00-118">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="13d00-119">Następnie wywołaj **właściwość DirectoryRoles,** a następnie metodę **Get()** **lub GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="13d00-119">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="13d00-120">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="13d00-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="13d00-121">**Project:** zestaw SDK Centrum partnerskiego Samples **Class**: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="13d00-121">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="13d00-122">Aby pobrać listę użytkowników klientów, którzy mają określoną rolę, najpierw pobierz określony identyfikator klienta i identyfikator roli katalogu.</span><span class="sxs-lookup"><span data-stu-id="13d00-122">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="13d00-123">Następnie użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="13d00-123">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="13d00-124">Następnie wywołaj właściwość **DirectoryRoles,** następnie metodę **ById(),** następnie właściwość **UserMembers,** a następnie metodę **Get()** lub **GetAsync().**</span><span class="sxs-lookup"><span data-stu-id="13d00-124">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="13d00-125">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="13d00-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="13d00-126">**Project:** Klasa PartnerSDK.FeatureSamples: GetCustomerDirectoryRoleUserMembers.cs </span><span class="sxs-lookup"><span data-stu-id="13d00-126">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="13d00-127">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="13d00-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="13d00-128">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="13d00-128">Request syntax</span></span>

| <span data-ttu-id="13d00-129">Metoda</span><span class="sxs-lookup"><span data-stu-id="13d00-129">Method</span></span>  | <span data-ttu-id="13d00-130">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="13d00-130">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="13d00-131">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="13d00-131">**GET**</span></span> | <span data-ttu-id="13d00-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="13d00-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="13d00-133">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="13d00-133">**GET**</span></span> | <span data-ttu-id="13d00-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="13d00-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="13d00-135">**Pobierz**</span><span class="sxs-lookup"><span data-stu-id="13d00-135">**GET**</span></span> | <span data-ttu-id="13d00-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{identyfikator-dzierżawy-klienta}/directoryroles/{identyfikator-roli}/usermembers</span><span class="sxs-lookup"><span data-stu-id="13d00-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="13d00-137">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="13d00-137">URI parameter</span></span>

<span data-ttu-id="13d00-138">Użyj następującego parametru zapytania, aby zidentyfikować prawidłowego klienta.</span><span class="sxs-lookup"><span data-stu-id="13d00-138">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="13d00-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="13d00-139">Name</span></span>                   | <span data-ttu-id="13d00-140">Typ</span><span class="sxs-lookup"><span data-stu-id="13d00-140">Type</span></span>     | <span data-ttu-id="13d00-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="13d00-141">Required</span></span> | <span data-ttu-id="13d00-142">Opis</span><span class="sxs-lookup"><span data-stu-id="13d00-142">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="13d00-143">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="13d00-143">**customer-tenant-id**</span></span> | <span data-ttu-id="13d00-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="13d00-144">**guid**</span></span> | <span data-ttu-id="13d00-145">Y</span><span class="sxs-lookup"><span data-stu-id="13d00-145">Y</span></span>        | <span data-ttu-id="13d00-146">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="13d00-146">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="13d00-147">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="13d00-147">**user-id**</span></span>            | <span data-ttu-id="13d00-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="13d00-148">**guid**</span></span> | <span data-ttu-id="13d00-149">N</span><span class="sxs-lookup"><span data-stu-id="13d00-149">N</span></span>        | <span data-ttu-id="13d00-150">Wartość to identyfikator GUID sformatowany **jako identyfikator użytkownika** należący do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13d00-150">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="13d00-151">**identyfikator roli**</span><span class="sxs-lookup"><span data-stu-id="13d00-151">**role-id**</span></span>            | <span data-ttu-id="13d00-152">**guid**</span><span class="sxs-lookup"><span data-stu-id="13d00-152">**guid**</span></span> | <span data-ttu-id="13d00-153">N</span><span class="sxs-lookup"><span data-stu-id="13d00-153">N</span></span>        | <span data-ttu-id="13d00-154">Wartość jest identyfikatorem roli sformatowanym **przez identyfikator** GUID, który należy do typu roli.</span><span class="sxs-lookup"><span data-stu-id="13d00-154">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="13d00-155">Te identyfikatory można uzyskać, odpytując wszystkie role katalogu dla klienta na wszystkich kontach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="13d00-155">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="13d00-156">(Drugi scenariusz powyżej).</span><span class="sxs-lookup"><span data-stu-id="13d00-156">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="13d00-157">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="13d00-157">Request headers</span></span>

<span data-ttu-id="13d00-158">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="13d00-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="13d00-159">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="13d00-159">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="13d00-160">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="13d00-160">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="13d00-161">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="13d00-161">REST response</span></span>

<span data-ttu-id="13d00-162">W przypadku powodzenia ta metoda zwraca listę ról skojarzonych z danym kontem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13d00-162">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="13d00-163">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="13d00-163">Response success and error codes</span></span>

<span data-ttu-id="13d00-164">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="13d00-164">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="13d00-165">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="13d00-165">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="13d00-166">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="13d00-166">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="13d00-167">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="13d00-167">Response example</span></span>

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
