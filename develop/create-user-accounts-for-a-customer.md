---
title: Tworzenie kont użytkowników dla klienta
description: Utwórz nowe konto użytkownika dla klienta.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d086d7ba72c9d9e42dc88684ddeafc9a597bfd7c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973387"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="f2292-103">Tworzenie kont użytkowników dla klienta</span><span class="sxs-lookup"><span data-stu-id="f2292-103">Create user accounts for a customer</span></span>

<span data-ttu-id="f2292-104">Utwórz nowe konto użytkownika dla klienta.</span><span class="sxs-lookup"><span data-stu-id="f2292-104">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2292-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2292-105">Prerequisites</span></span>

- <span data-ttu-id="f2292-106">Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f2292-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2292-107">Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2292-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f2292-108">Identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f2292-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f2292-109">Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f2292-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f2292-110">Wybierz **pozycję CSP** z menu Partner Center, a następnie pozycję **Klienci.**</span><span class="sxs-lookup"><span data-stu-id="f2292-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f2292-111">Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**.</span><span class="sxs-lookup"><span data-stu-id="f2292-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f2292-112">Na stronie Konto klienta poszukaj identyfikatora **Microsoft w** sekcji Informacje o **koncie** klienta.</span><span class="sxs-lookup"><span data-stu-id="f2292-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f2292-113">Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f2292-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f2292-114">C\#</span><span class="sxs-lookup"><span data-stu-id="f2292-114">C\#</span></span>

<span data-ttu-id="f2292-115">Aby uzyskać nowe konto użytkownika dla klienta:</span><span class="sxs-lookup"><span data-stu-id="f2292-115">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="f2292-116">Utwórz nowy obiekt **CustomerUser** z odpowiednimi informacjami o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="f2292-116">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="f2292-117">Użyj **kolekcji IAggregatePartner.Customers** i wywołaj **metodę ById().**</span><span class="sxs-lookup"><span data-stu-id="f2292-117">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="f2292-118">Wywołaj **właściwość Users,** a następnie metodę **Create.**</span><span class="sxs-lookup"><span data-stu-id="f2292-118">Call the **Users** property, followed by the **Create** method.</span></span>

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

<span data-ttu-id="f2292-119">**Przykład:** [aplikacja testowa konsoli](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f2292-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f2292-120">**Project:** PartnerSDK.FeatureSamples, **klasa:** CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="f2292-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f2292-121">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="f2292-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f2292-122">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="f2292-122">Request syntax</span></span>

| <span data-ttu-id="f2292-123">Metoda</span><span class="sxs-lookup"><span data-stu-id="f2292-123">Method</span></span>   | <span data-ttu-id="f2292-124">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="f2292-124">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2292-125">**Post**</span><span class="sxs-lookup"><span data-stu-id="f2292-125">**POST**</span></span> | <span data-ttu-id="f2292-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f2292-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f2292-127">Parametry URI</span><span class="sxs-lookup"><span data-stu-id="f2292-127">URI parameters</span></span>

<span data-ttu-id="f2292-128">Użyj następujących parametrów zapytania, aby zidentyfikować właściwego klienta.</span><span class="sxs-lookup"><span data-stu-id="f2292-128">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="f2292-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f2292-129">Name</span></span> | <span data-ttu-id="f2292-130">Typ</span><span class="sxs-lookup"><span data-stu-id="f2292-130">Type</span></span> | <span data-ttu-id="f2292-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f2292-131">Required</span></span> | <span data-ttu-id="f2292-132">Opis</span><span class="sxs-lookup"><span data-stu-id="f2292-132">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="f2292-133">**identyfikator dzierżawy klienta**</span><span class="sxs-lookup"><span data-stu-id="f2292-133">**customer-tenant-id**</span></span> | <span data-ttu-id="f2292-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="f2292-134">**guid**</span></span> | <span data-ttu-id="f2292-135">Y</span><span class="sxs-lookup"><span data-stu-id="f2292-135">Y</span></span> | <span data-ttu-id="f2292-136">Wartość to identyfikator GUID w **formacie customer-tenant-id.** Dzięki temu odsprzedawca może filtrować wyniki dla danego klienta, który należy do odsprzedawcy.</span><span class="sxs-lookup"><span data-stu-id="f2292-136">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="f2292-137">**identyfikator użytkownika**</span><span class="sxs-lookup"><span data-stu-id="f2292-137">**user-id**</span></span> | <span data-ttu-id="f2292-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="f2292-138">**guid**</span></span> | <span data-ttu-id="f2292-139">N</span><span class="sxs-lookup"><span data-stu-id="f2292-139">N</span></span> | <span data-ttu-id="f2292-140">Wartość jest identyfikatorem użytkownika sformatowanym w **formacie** GUID, który należy do jednego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2292-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f2292-141">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="f2292-141">Request headers</span></span>

<span data-ttu-id="f2292-142">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f2292-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f2292-143">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f2292-143">Request body</span></span>

<span data-ttu-id="f2292-144">Brak.</span><span class="sxs-lookup"><span data-stu-id="f2292-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f2292-145">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="f2292-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f2292-146">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="f2292-146">REST response</span></span>

<span data-ttu-id="f2292-147">W przypadku powodzenia ta metoda zwraca konto użytkownika, w tym identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="f2292-147">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f2292-148">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f2292-148">Response success and error codes</span></span>

<span data-ttu-id="f2292-149">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="f2292-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f2292-150">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="f2292-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f2292-151">Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f2292-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f2292-152">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f2292-152">Response example</span></span>

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