---
title: Weryfikowanie adresu
description: Sprawdzanie poprawności adresu przy użyciu interfejsu API weryfikacji adresów.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 22d5faec2fdab4907067bb01cb74e110032dea9a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767829"
---
# <a name="validate-an-address"></a><span data-ttu-id="e38ae-103">Weryfikowanie adresu</span><span class="sxs-lookup"><span data-stu-id="e38ae-103">Validate an address</span></span>

<span data-ttu-id="e38ae-104">**Dotyczy**</span><span class="sxs-lookup"><span data-stu-id="e38ae-104">**Applies To**</span></span>

- <span data-ttu-id="e38ae-105">Centrum partnerskie</span><span class="sxs-lookup"><span data-stu-id="e38ae-105">Partner Center</span></span>
- <span data-ttu-id="e38ae-106">Centrum partnerskie obsługiwane przez firmę 21Vianet</span><span class="sxs-lookup"><span data-stu-id="e38ae-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e38ae-107">Centrum partnerskie dla Microsoft Cloud Niemcy</span><span class="sxs-lookup"><span data-stu-id="e38ae-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e38ae-108">Centrum partnerskie Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e38ae-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e38ae-109">Sprawdzanie poprawności adresu przy użyciu interfejsu API weryfikacji adresów.</span><span class="sxs-lookup"><span data-stu-id="e38ae-109">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="e38ae-110">Interfejs API weryfikacji adresu powinien być używany tylko do weryfikacji aktualizacji profilu klienta.</span><span class="sxs-lookup"><span data-stu-id="e38ae-110">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="e38ae-111">Należy jej użyć, aby w przypadku Stany Zjednoczone, Kanady, Chin lub Meksyku, pole Stan zostało zweryfikowane względem listy prawidłowych stanów w danym kraju.</span><span class="sxs-lookup"><span data-stu-id="e38ae-111">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="e38ae-112">W pozostałych krajach ten test nie występuje, a interfejs API sprawdza, czy stan jest prawidłowym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="e38ae-112">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e38ae-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e38ae-113">Prerequisites</span></span>

<span data-ttu-id="e38ae-114">Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e38ae-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e38ae-115">Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e38ae-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e38ae-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e38ae-116">C\#</span></span>

<span data-ttu-id="e38ae-117">Aby sprawdzić poprawność adresu, najpierw Utwórz wystąpienie nowego obiektu **adresu** i wypełnij go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="e38ae-117">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="e38ae-118">Następnie Pobierz interfejs do operacji **walidacji** z właściwości **IAggregatePartner. walidacje** i Wywołaj metodę **IsAddressValid** z obiektem Address.</span><span class="sxs-lookup"><span data-stu-id="e38ae-118">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";

    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);

    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

## <a name="java"></a><span data-ttu-id="e38ae-119">Java</span><span class="sxs-lookup"><span data-stu-id="e38ae-119">Java</span></span>

<span data-ttu-id="e38ae-120">Aby sprawdzić poprawność adresu, najpierw Utwórz wystąpienie nowego obiektu **adresu** i wypełnij go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="e38ae-120">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="e38ae-121">Następnie Pobierz interfejs do operacji **walidacji** z funkcji **IAggregatePartner. getwalidacji** i Wywołaj metodę **isAddressValid** z obiektem Address.</span><span class="sxs-lookup"><span data-stu-id="e38ae-121">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");

    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

## <a name="powershell"></a><span data-ttu-id="e38ae-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e38ae-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e38ae-123">Aby sprawdzić poprawność adresu, wykonaj polecenie [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) z wypełnionymi parametrami adresu.</span><span class="sxs-lookup"><span data-stu-id="e38ae-123">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="e38ae-124">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="e38ae-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e38ae-125">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="e38ae-125">Request syntax</span></span>

| <span data-ttu-id="e38ae-126">Metoda</span><span class="sxs-lookup"><span data-stu-id="e38ae-126">Method</span></span>   | <span data-ttu-id="e38ae-127">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="e38ae-127">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="e38ae-128">**POUBOJOWEGO**</span><span class="sxs-lookup"><span data-stu-id="e38ae-128">**POST**</span></span> | <span data-ttu-id="e38ae-129">[*{baseURL}*](partner-center-rest-urls.md)/V1/validations/Address http/1.1</span><span class="sxs-lookup"><span data-stu-id="e38ae-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e38ae-130">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="e38ae-130">Request headers</span></span>

<span data-ttu-id="e38ae-131">Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e38ae-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e38ae-132">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="e38ae-132">Request body</span></span>

<span data-ttu-id="e38ae-133">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="e38ae-133">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e38ae-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e38ae-134">Name</span></span>         | <span data-ttu-id="e38ae-135">Typ</span><span class="sxs-lookup"><span data-stu-id="e38ae-135">Type</span></span>   | <span data-ttu-id="e38ae-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e38ae-136">Required</span></span> | <span data-ttu-id="e38ae-137">Opis</span><span class="sxs-lookup"><span data-stu-id="e38ae-137">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="e38ae-138">addressline1</span><span class="sxs-lookup"><span data-stu-id="e38ae-138">addressline1</span></span> | <span data-ttu-id="e38ae-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-139">string</span></span> | <span data-ttu-id="e38ae-140">Y</span><span class="sxs-lookup"><span data-stu-id="e38ae-140">Y</span></span>        | <span data-ttu-id="e38ae-141">Pierwszy wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="e38ae-141">The first line of the address.</span></span>                             |
| <span data-ttu-id="e38ae-142">addressline2</span><span class="sxs-lookup"><span data-stu-id="e38ae-142">addressline2</span></span> | <span data-ttu-id="e38ae-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-143">string</span></span> | <span data-ttu-id="e38ae-144">N</span><span class="sxs-lookup"><span data-stu-id="e38ae-144">N</span></span>        | <span data-ttu-id="e38ae-145">Drugi wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="e38ae-145">The second line of the address.</span></span> <span data-ttu-id="e38ae-146">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="e38ae-146">This property is optional.</span></span> |
| <span data-ttu-id="e38ae-147">city</span><span class="sxs-lookup"><span data-stu-id="e38ae-147">city</span></span>         | <span data-ttu-id="e38ae-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-148">string</span></span> | <span data-ttu-id="e38ae-149">Y</span><span class="sxs-lookup"><span data-stu-id="e38ae-149">Y</span></span>        | <span data-ttu-id="e38ae-150">Miasto.</span><span class="sxs-lookup"><span data-stu-id="e38ae-150">The city.</span></span>                                                  |
| <span data-ttu-id="e38ae-151">stan</span><span class="sxs-lookup"><span data-stu-id="e38ae-151">state</span></span>        | <span data-ttu-id="e38ae-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-152">string</span></span> | <span data-ttu-id="e38ae-153">Y</span><span class="sxs-lookup"><span data-stu-id="e38ae-153">Y</span></span>        | <span data-ttu-id="e38ae-154">Stan.</span><span class="sxs-lookup"><span data-stu-id="e38ae-154">The state.</span></span>                                                 |
| <span data-ttu-id="e38ae-155">pocztowy</span><span class="sxs-lookup"><span data-stu-id="e38ae-155">postalcode</span></span>   | <span data-ttu-id="e38ae-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-156">string</span></span> | <span data-ttu-id="e38ae-157">Y</span><span class="sxs-lookup"><span data-stu-id="e38ae-157">Y</span></span>        | <span data-ttu-id="e38ae-158">Kod pocztowy.</span><span class="sxs-lookup"><span data-stu-id="e38ae-158">The postal code.</span></span>                                           |
| <span data-ttu-id="e38ae-159">country</span><span class="sxs-lookup"><span data-stu-id="e38ae-159">country</span></span>      | <span data-ttu-id="e38ae-160">ciąg</span><span class="sxs-lookup"><span data-stu-id="e38ae-160">string</span></span> | <span data-ttu-id="e38ae-161">Y</span><span class="sxs-lookup"><span data-stu-id="e38ae-161">Y</span></span>        | <span data-ttu-id="e38ae-162">Dwuznakowy ISO kod kraju Alpha-2.</span><span class="sxs-lookup"><span data-stu-id="e38ae-162">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="e38ae-163">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="e38ae-163">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="e38ae-164">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="e38ae-164">REST response</span></span>

<span data-ttu-id="e38ae-165">Jeśli to się powiedzie, metoda zwraca kod stanu 200, jak pokazano w przykładzie odpowiedzi-Walidacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e38ae-165">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="e38ae-166">Jeśli żądanie nie powiedzie się, metoda zwraca kod stanu 400, jak pokazano w przykładzie niepowodzenia weryfikacji odpowiedzi poniżej.</span><span class="sxs-lookup"><span data-stu-id="e38ae-166">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="e38ae-167">Treść odpowiedzi zawiera ładunek JSON z dodatkowymi informacjami o błędzie.</span><span class="sxs-lookup"><span data-stu-id="e38ae-167">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e38ae-168">Kody sukcesu i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="e38ae-168">Response success and error codes</span></span>

<span data-ttu-id="e38ae-169">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.</span><span class="sxs-lookup"><span data-stu-id="e38ae-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e38ae-170">Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="e38ae-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e38ae-171">Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e38ae-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="e38ae-172">Odpowiedź — sprawdzanie poprawności zakończyło się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="e38ae-172">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="e38ae-173">Przykład weryfikacji odpowiedzi nie powiodła się</span><span class="sxs-lookup"><span data-stu-id="e38ae-173">Response - validation failed example</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```
