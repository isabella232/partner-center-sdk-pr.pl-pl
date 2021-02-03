---
title: Resetowanie hasła użytkownika dla klienta
description: Resetowanie hasła jest bardzo podobne do aktualizowania innych szczegółów w istniejącym koncie użytkownika dla klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0df93c2db55ec0fe49fc0e3089b7e11928f32bb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767790"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="2c370-103">Resetowanie hasła użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="2c370-103">Reset user password for a customer</span></span>

<span data-ttu-id="2c370-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="2c370-104">**Applies To**</span></span>

- <span data-ttu-id="2c370-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="2c370-105">Partner Center</span></span>

<span data-ttu-id="2c370-106">Resetowanie hasła jest bardzo podobne do aktualizowania innych szczegółów w istniejącym koncie użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="2c370-106">Resetting a password is very similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c370-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c370-107">Prerequisites</span></span>

- <span data-ttu-id="2c370-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2c370-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2c370-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c370-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2c370-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c370-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2c370-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="2c370-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2c370-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="2c370-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2c370-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="2c370-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2c370-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="2c370-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2c370-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c370-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2c370-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2c370-116">C\#</span></span>

<span data-ttu-id="2c370-117">Aby zresetować hasło dla określonego użytkownika klienta, najpierw Pobierz określony identyfikator klienta i wskazanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c370-117">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="2c370-118">Następnie utwórz nowy obiekt **CustomerUser** , który zawiera informacje dla istniejącego klienta, ale z nowym obiektem **PasswordProfile** .</span><span class="sxs-lookup"><span data-stu-id="2c370-118">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="2c370-119">Następnie użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="2c370-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="2c370-120">Następnie Wywołaj Właściwość **users** , metodę **ById ()** , a następnie metodę **patch** .</span><span class="sxs-lookup"><span data-stu-id="2c370-120">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="2c370-121">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2c370-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2c370-122">**Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="2c370-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2c370-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2c370-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2c370-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2c370-124">Request syntax</span></span>

| <span data-ttu-id="2c370-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="2c370-125">Method</span></span>    | <span data-ttu-id="2c370-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2c370-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c370-127">**WYSŁANA**</span><span class="sxs-lookup"><span data-stu-id="2c370-127">**PATCH**</span></span> | <span data-ttu-id="2c370-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users http/1.1</span><span class="sxs-lookup"><span data-stu-id="2c370-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2c370-129">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="2c370-129">URI parameter</span></span>

<span data-ttu-id="2c370-130">Użyj następującego parametru zapytania, aby zidentyfikować odpowiedniego klienta.</span><span class="sxs-lookup"><span data-stu-id="2c370-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="2c370-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2c370-131">Name</span></span>                   | <span data-ttu-id="2c370-132">Typ</span><span class="sxs-lookup"><span data-stu-id="2c370-132">Type</span></span>     | <span data-ttu-id="2c370-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2c370-133">Required</span></span> | <span data-ttu-id="2c370-134">Opis</span><span class="sxs-lookup"><span data-stu-id="2c370-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c370-135">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="2c370-135">**customer-tenant-id**</span></span> | <span data-ttu-id="2c370-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="2c370-136">**guid**</span></span> | <span data-ttu-id="2c370-137">Y</span><span class="sxs-lookup"><span data-stu-id="2c370-137">Y</span></span>        | <span data-ttu-id="2c370-138">Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="2c370-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2c370-139">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="2c370-139">**user-id**</span></span>            | <span data-ttu-id="2c370-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="2c370-140">**guid**</span></span> | <span data-ttu-id="2c370-141">Y</span><span class="sxs-lookup"><span data-stu-id="2c370-141">Y</span></span>        | <span data-ttu-id="2c370-142">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c370-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="2c370-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2c370-143">Request headers</span></span>

<span data-ttu-id="2c370-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2c370-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2c370-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2c370-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="2c370-146">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2c370-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="2c370-147">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2c370-147">REST response</span></span>

<span data-ttu-id="2c370-148">Jeśli to się powiedzie, ta metoda zwraca informacje o użytkowniku wraz z zaktualizowanymi informacjami o haśle.</span><span class="sxs-lookup"><span data-stu-id="2c370-148">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2c370-149">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2c370-149">Response success and error codes</span></span>

<span data-ttu-id="2c370-150">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="2c370-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2c370-151">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2c370-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2c370-152">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2c370-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2c370-153">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2c370-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
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
