---
title: Resetowanie hasła użytkownika dla klienta
description: Zresetowanie hasła jest podobne do aktualizowania innych szczegółów na istniejącym koncie użytkownika dla klienta.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: f3661a588f566485cbd58035c63ae9f8e5d383af
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445684"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="44d02-103">Resetowanie hasła użytkownika dla klienta</span><span class="sxs-lookup"><span data-stu-id="44d02-103">Reset user password for a customer</span></span>

<span data-ttu-id="44d02-104">Zresetowanie hasła jest podobne do aktualizowania innych szczegółów na istniejącym koncie użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="44d02-104">Resetting a password is similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44d02-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44d02-105">Prerequisites</span></span>

- <span data-ttu-id="44d02-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="44d02-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44d02-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44d02-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="44d02-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44d02-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="44d02-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="44d02-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="44d02-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="44d02-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="44d02-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="44d02-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="44d02-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="44d02-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="44d02-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44d02-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="44d02-114">C\#</span><span class="sxs-lookup"><span data-stu-id="44d02-114">C\#</span></span>

<span data-ttu-id="44d02-115">Aby zresetować hasło dla określonego użytkownika klienta, najpierw pobierz określony identyfikator klienta i docelowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44d02-115">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="44d02-116">Następnie utwórz nowy obiekt **CustomerUser** zawierający informacje dotyczące istniejącego klienta, ale z nowym **obiektem PasswordProfile.**</span><span class="sxs-lookup"><span data-stu-id="44d02-116">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="44d02-117">Następnie użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="44d02-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="44d02-118">Następnie **wywołaj właściwość Users,** **metodę ById(),** a następnie metodę **Patch.**</span><span class="sxs-lookup"><span data-stu-id="44d02-118">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

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

<span data-ttu-id="44d02-119">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="44d02-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="44d02-120">**Project:** PartnerSDK.FeatureSamples, **klasa**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="44d02-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="44d02-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="44d02-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44d02-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="44d02-122">Request syntax</span></span>

| <span data-ttu-id="44d02-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="44d02-123">Method</span></span>    | <span data-ttu-id="44d02-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="44d02-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="44d02-125">**Patch**</span><span class="sxs-lookup"><span data-stu-id="44d02-125">**PATCH**</span></span> | <span data-ttu-id="44d02-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="44d02-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="44d02-127">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="44d02-127">URI parameter</span></span>

<span data-ttu-id="44d02-128">Użyj następującego parametru zapytania, aby zidentyfikować prawidłowego klienta.</span><span class="sxs-lookup"><span data-stu-id="44d02-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="44d02-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="44d02-129">Name</span></span>                   | <span data-ttu-id="44d02-130">Typ</span><span class="sxs-lookup"><span data-stu-id="44d02-130">Type</span></span>     | <span data-ttu-id="44d02-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="44d02-131">Required</span></span> | <span data-ttu-id="44d02-132">Opis</span><span class="sxs-lookup"><span data-stu-id="44d02-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44d02-133">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="44d02-133">**customer-tenant-id**</span></span> | <span data-ttu-id="44d02-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="44d02-134">**guid**</span></span> | <span data-ttu-id="44d02-135">Y</span><span class="sxs-lookup"><span data-stu-id="44d02-135">Y</span></span>        | <span data-ttu-id="44d02-136">Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="44d02-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="44d02-137">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="44d02-137">**user-id**</span></span>            | <span data-ttu-id="44d02-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="44d02-138">**guid**</span></span> | <span data-ttu-id="44d02-139">Y</span><span class="sxs-lookup"><span data-stu-id="44d02-139">Y</span></span>        | <span data-ttu-id="44d02-140">Wartość jest identyfikatorem użytkownika sformatowanym w **formacie** GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44d02-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="44d02-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="44d02-141">Request headers</span></span>

<span data-ttu-id="44d02-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="44d02-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44d02-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="44d02-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="44d02-144">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="44d02-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="44d02-145">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="44d02-145">REST response</span></span>

<span data-ttu-id="44d02-146">W przypadku powodzenia ta metoda zwraca informacje o użytkowniku wraz ze zaktualizowanymi informacjami o hasłach.</span><span class="sxs-lookup"><span data-stu-id="44d02-146">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44d02-147">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44d02-147">Response success and error codes</span></span>

<span data-ttu-id="44d02-148">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="44d02-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44d02-149">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="44d02-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44d02-150">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44d02-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44d02-151">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="44d02-151">Response example</span></span>

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
