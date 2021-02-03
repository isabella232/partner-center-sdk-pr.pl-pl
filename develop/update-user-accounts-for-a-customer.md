---
title: Aktualizowanie kont użytkowników dla klienta
description: Zaktualizuj szczegóły w istniejącym koncie użytkownika dla klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 52a43341bf2c3ba64d8c232af01f3fbae6765d82
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767997"
---
# <a name="update-user-accounts-for-a-customer"></a><span data-ttu-id="04f43-103">Aktualizowanie kont użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="04f43-103">Update user accounts for a customer</span></span>

<span data-ttu-id="04f43-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="04f43-104">**Applies To**</span></span>

- <span data-ttu-id="04f43-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="04f43-105">Partner Center</span></span>

<span data-ttu-id="04f43-106">Zaktualizuj szczegóły w istniejącym koncie użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="04f43-106">Update details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04f43-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="04f43-107">Prerequisites</span></span>

- <span data-ttu-id="04f43-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="04f43-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="04f43-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="04f43-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="04f43-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="04f43-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="04f43-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="04f43-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="04f43-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="04f43-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="04f43-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="04f43-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="04f43-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="04f43-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="04f43-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="04f43-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="04f43-116">C\#</span><span class="sxs-lookup"><span data-stu-id="04f43-116">C\#</span></span>

<span data-ttu-id="04f43-117">Aby zaktualizować szczegóły określonego użytkownika klienta, należy najpierw pobrać określonego identyfikatora klienta i użytkownika w celu zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="04f43-117">To update the details for a specified customer user, first retrieve the specified customer ID and user to update.</span></span> <span data-ttu-id="04f43-118">Następnie utwórz zaktualizowaną wersję użytkownika w nowym obiekcie **CustomerUser** .</span><span class="sxs-lookup"><span data-stu-id="04f43-118">Then, create an updated version of the user in a new **CustomerUser** object.</span></span> <span data-ttu-id="04f43-119">Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="04f43-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="04f43-120">Następnie Wywołaj Właściwość **users** , metodę **ById ()** , a następnie metodę **patch ()** .</span><span class="sxs-lookup"><span data-stu-id="04f43-120">Then call the **Users** property, the **ById()** method, followed by the **Patch()** method.</span></span>

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="04f43-121">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="04f43-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="04f43-122">**Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="04f43-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="04f43-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="04f43-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="04f43-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="04f43-124">Request syntax</span></span>

| <span data-ttu-id="04f43-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="04f43-125">Method</span></span>    | <span data-ttu-id="04f43-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="04f43-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="04f43-127">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="04f43-127">**PATCH**</span></span> | <span data-ttu-id="04f43-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users http/1.1</span><span class="sxs-lookup"><span data-stu-id="04f43-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="04f43-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="04f43-129">URI parameter</span></span>

<span data-ttu-id="04f43-130">Użyj następującego parametru zapytania, aby zidentyfikować odpowiedniego klienta.</span><span class="sxs-lookup"><span data-stu-id="04f43-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="04f43-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="04f43-131">Name</span></span>                   | <span data-ttu-id="04f43-132">Typ</span><span class="sxs-lookup"><span data-stu-id="04f43-132">Type</span></span>     | <span data-ttu-id="04f43-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="04f43-133">Required</span></span> | <span data-ttu-id="04f43-134">Opis</span><span class="sxs-lookup"><span data-stu-id="04f43-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="04f43-135">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="04f43-135">**customer-tenant-id**</span></span> | <span data-ttu-id="04f43-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="04f43-136">**guid**</span></span> | <span data-ttu-id="04f43-137">Y</span><span class="sxs-lookup"><span data-stu-id="04f43-137">Y</span></span>        | <span data-ttu-id="04f43-138">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="04f43-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="04f43-139">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="04f43-139">**user-id**</span></span>            | <span data-ttu-id="04f43-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="04f43-140">**guid**</span></span> | <span data-ttu-id="04f43-141">Y</span><span class="sxs-lookup"><span data-stu-id="04f43-141">Y</span></span>        | <span data-ttu-id="04f43-142">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="04f43-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="04f43-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="04f43-143">Request headers</span></span>

<span data-ttu-id="04f43-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="04f43-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="04f43-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="04f43-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="04f43-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="04f43-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="04f43-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="04f43-147">REST response</span></span>

<span data-ttu-id="04f43-148">Jeśli to się powiedzie, ta metoda zwraca konto użytkownika ze zaktualizowanymi informacjami.</span><span class="sxs-lookup"><span data-stu-id="04f43-148">If successful, this method returns a user account with the updated information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="04f43-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="04f43-149">Response success and error codes</span></span>

<span data-ttu-id="04f43-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="04f43-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="04f43-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="04f43-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="04f43-152">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="04f43-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="04f43-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="04f43-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
