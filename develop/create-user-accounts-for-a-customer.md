---
title: Tworzenie kont użytkowników dla klienta
description: Utwórz nowe konto użytkownika dla klienta.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767746"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="4b16c-103">Tworzenie kont użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="4b16c-103">Create user accounts for a customer</span></span>

<span data-ttu-id="4b16c-104">**Dotyczy:**</span><span class="sxs-lookup"><span data-stu-id="4b16c-104">**Applies to:**</span></span>

- <span data-ttu-id="4b16c-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="4b16c-105">Partner Center</span></span>

<span data-ttu-id="4b16c-106">Utwórz nowe konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="4b16c-106">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b16c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b16c-107">Prerequisites</span></span>

- <span data-ttu-id="4b16c-108">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4b16c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4b16c-109">Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b16c-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4b16c-110">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4b16c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4b16c-111">Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego.</span><span class="sxs-lookup"><span data-stu-id="4b16c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4b16c-112">Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**.</span><span class="sxs-lookup"><span data-stu-id="4b16c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4b16c-113">Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**.</span><span class="sxs-lookup"><span data-stu-id="4b16c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4b16c-114">Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** .</span><span class="sxs-lookup"><span data-stu-id="4b16c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4b16c-115">Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4b16c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="4b16c-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4b16c-116">C\#</span></span>

<span data-ttu-id="4b16c-117">Aby uzyskać nowe konto użytkownika dla klienta:</span><span class="sxs-lookup"><span data-stu-id="4b16c-117">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="4b16c-118">Utwórz nowy obiekt **CustomerUser** z odpowiednimi informacjami o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="4b16c-118">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="4b16c-119">Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById ()** .</span><span class="sxs-lookup"><span data-stu-id="4b16c-119">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="4b16c-120">Wywołaj Właściwość **users** , a następnie metodę **Create** .</span><span class="sxs-lookup"><span data-stu-id="4b16c-120">Call the **Users** property, followed by the **Create** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

<span data-ttu-id="4b16c-121">**Przykład**: [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4b16c-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4b16c-122">**Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="4b16c-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4b16c-123">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="4b16c-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4b16c-124">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="4b16c-124">Request syntax</span></span>

| <span data-ttu-id="4b16c-125">Metoda</span><span class="sxs-lookup"><span data-stu-id="4b16c-125">Method</span></span>   | <span data-ttu-id="4b16c-126">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="4b16c-126">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="4b16c-127">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="4b16c-127">**POST**</span></span> | <span data-ttu-id="4b16c-128">[*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/users http/1.1</span><span class="sxs-lookup"><span data-stu-id="4b16c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4b16c-129">Parametry identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="4b16c-129">URI parameters</span></span>

<span data-ttu-id="4b16c-130">Użyj następujących parametrów zapytania, aby zidentyfikować odpowiedniego klienta.</span><span class="sxs-lookup"><span data-stu-id="4b16c-130">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="4b16c-131">Nazwa</span><span class="sxs-lookup"><span data-stu-id="4b16c-131">Name</span></span> | <span data-ttu-id="4b16c-132">Typ</span><span class="sxs-lookup"><span data-stu-id="4b16c-132">Type</span></span> | <span data-ttu-id="4b16c-133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4b16c-133">Required</span></span> | <span data-ttu-id="4b16c-134">Opis</span><span class="sxs-lookup"><span data-stu-id="4b16c-134">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="4b16c-135">**Identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="4b16c-135">**customer-tenant-id**</span></span> | <span data-ttu-id="4b16c-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="4b16c-136">**guid**</span></span> | <span data-ttu-id="4b16c-137">Y</span><span class="sxs-lookup"><span data-stu-id="4b16c-137">Y</span></span> | <span data-ttu-id="4b16c-138">Wartość jest identyfikatorem GUID z sformatowanym **identyfikatorem dzierżawy**. Umożliwia odsprzedawcy odfiltrować wyniki dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="4b16c-138">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="4b16c-139">**Identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="4b16c-139">**user-id**</span></span> | <span data-ttu-id="4b16c-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="4b16c-140">**guid**</span></span> | <span data-ttu-id="4b16c-141">N</span><span class="sxs-lookup"><span data-stu-id="4b16c-141">N</span></span> | <span data-ttu-id="4b16c-142">Wartość jest **identyfikatorem użytkownika** w formacie GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b16c-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4b16c-143">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="4b16c-143">Request headers</span></span>

<span data-ttu-id="4b16c-144">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4b16c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4b16c-145">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="4b16c-145">Request body</span></span>

<span data-ttu-id="4b16c-146">Brak.</span><span class="sxs-lookup"><span data-stu-id="4b16c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4b16c-147">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="4b16c-147">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="4b16c-148">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="4b16c-148">REST response</span></span>

<span data-ttu-id="4b16c-149">Jeśli to się powiedzie, metoda zwraca konto użytkownika, w tym identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="4b16c-149">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4b16c-150">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4b16c-150">Response success and error codes</span></span>

<span data-ttu-id="4b16c-151">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="4b16c-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4b16c-152">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="4b16c-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4b16c-153">Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4b16c-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4b16c-154">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4b16c-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```