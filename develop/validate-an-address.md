---
title: Weryfikowanie adresu
description: Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14d45977f3af6e8bba1b7cb7f969aa7c5bb671da
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529889"
---
# <a name="validate-an-address"></a><span data-ttu-id="2f7dd-103">Weryfikowanie adresu</span><span class="sxs-lookup"><span data-stu-id="2f7dd-103">Validate an address</span></span>

<span data-ttu-id="2f7dd-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2f7dd-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f7dd-105">Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="2f7dd-106">Interfejs API weryfikacji adresu powinien być używany tylko do wstępnej weryfikacji aktualizacji profilu klienta.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="2f7dd-107">Użyj go ze zrozumieniem, że jeśli kraj jest regionem Stany Zjednoczone, Kanadzie, Chinach lub Meksyku, pole stanu jest weryfikowane względem listy prawidłowych stanów dla odpowiedniego kraju.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="2f7dd-108">We wszystkich innych krajach ten test nie jest przeprowadzane, a interfejs API sprawdza tylko, czy stan jest prawidłowym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f7dd-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f7dd-109">Prerequisites</span></span>

<span data-ttu-id="2f7dd-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2f7dd-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f7dd-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2f7dd-112">C\#</span><span class="sxs-lookup"><span data-stu-id="2f7dd-112">C\#</span></span>

<span data-ttu-id="2f7dd-113">Aby zweryfikować adres, najpierw należy utworzyć nowe wystąpienia obiektu **Address** i wypełnić go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="2f7dd-114">Następnie pobierz interfejs operacji **Validations** z właściwości **IAggregatePartner.Validations** i wywołaj metodę **IsAddressValid** przy użyciu obiektu adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="java"></a><span data-ttu-id="2f7dd-115">Java</span><span class="sxs-lookup"><span data-stu-id="2f7dd-115">Java</span></span>

<span data-ttu-id="2f7dd-116">Aby zweryfikować adres, najpierw należy utworzyć nowe wystąpienia obiektu **Address** i wypełnić go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-116">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="2f7dd-117">Następnie pobierz interfejs do operacji **walidacji** z funkcji **IAggregatePartner.getValidations** i wywołaj metodę **isAddressValid** za pomocą obiektu adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-117">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="2f7dd-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f7dd-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2f7dd-119">Aby zweryfikować adres, wykonaj [**polecenie Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) z wypełnionymi parametrami adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-119">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="2f7dd-120">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2f7dd-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f7dd-121">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2f7dd-121">Request syntax</span></span>

| <span data-ttu-id="2f7dd-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="2f7dd-122">Method</span></span>   | <span data-ttu-id="2f7dd-123">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2f7dd-123">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="2f7dd-124">**Post**</span><span class="sxs-lookup"><span data-stu-id="2f7dd-124">**POST**</span></span> | <span data-ttu-id="2f7dd-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2f7dd-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2f7dd-126">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2f7dd-126">Request headers</span></span>

<span data-ttu-id="2f7dd-127">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2f7dd-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f7dd-128">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2f7dd-128">Request body</span></span>

<span data-ttu-id="2f7dd-129">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-129">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="2f7dd-130">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2f7dd-130">Name</span></span>         | <span data-ttu-id="2f7dd-131">Typ</span><span class="sxs-lookup"><span data-stu-id="2f7dd-131">Type</span></span>   | <span data-ttu-id="2f7dd-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f7dd-132">Required</span></span> | <span data-ttu-id="2f7dd-133">Opis</span><span class="sxs-lookup"><span data-stu-id="2f7dd-133">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="2f7dd-134">addressline1</span><span class="sxs-lookup"><span data-stu-id="2f7dd-134">addressline1</span></span> | <span data-ttu-id="2f7dd-135">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-135">string</span></span> | <span data-ttu-id="2f7dd-136">Y</span><span class="sxs-lookup"><span data-stu-id="2f7dd-136">Y</span></span>        | <span data-ttu-id="2f7dd-137">Pierwszy wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-137">The first line of the address.</span></span>                             |
| <span data-ttu-id="2f7dd-138">Addressline2</span><span class="sxs-lookup"><span data-stu-id="2f7dd-138">addressline2</span></span> | <span data-ttu-id="2f7dd-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-139">string</span></span> | <span data-ttu-id="2f7dd-140">N</span><span class="sxs-lookup"><span data-stu-id="2f7dd-140">N</span></span>        | <span data-ttu-id="2f7dd-141">Drugi wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-141">The second line of the address.</span></span> <span data-ttu-id="2f7dd-142">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-142">This property is optional.</span></span> |
| <span data-ttu-id="2f7dd-143">city</span><span class="sxs-lookup"><span data-stu-id="2f7dd-143">city</span></span>         | <span data-ttu-id="2f7dd-144">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-144">string</span></span> | <span data-ttu-id="2f7dd-145">Y</span><span class="sxs-lookup"><span data-stu-id="2f7dd-145">Y</span></span>        | <span data-ttu-id="2f7dd-146">Miasto.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-146">The city.</span></span>                                                  |
| <span data-ttu-id="2f7dd-147">stan</span><span class="sxs-lookup"><span data-stu-id="2f7dd-147">state</span></span>        | <span data-ttu-id="2f7dd-148">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-148">string</span></span> | <span data-ttu-id="2f7dd-149">Y</span><span class="sxs-lookup"><span data-stu-id="2f7dd-149">Y</span></span>        | <span data-ttu-id="2f7dd-150">Stan.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-150">The state.</span></span>                                                 |
| <span data-ttu-id="2f7dd-151">Postalcode</span><span class="sxs-lookup"><span data-stu-id="2f7dd-151">postalcode</span></span>   | <span data-ttu-id="2f7dd-152">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-152">string</span></span> | <span data-ttu-id="2f7dd-153">Y</span><span class="sxs-lookup"><span data-stu-id="2f7dd-153">Y</span></span>        | <span data-ttu-id="2f7dd-154">Kod pocztowy.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-154">The postal code.</span></span>                                           |
| <span data-ttu-id="2f7dd-155">country</span><span class="sxs-lookup"><span data-stu-id="2f7dd-155">country</span></span>      | <span data-ttu-id="2f7dd-156">ciąg</span><span class="sxs-lookup"><span data-stu-id="2f7dd-156">string</span></span> | <span data-ttu-id="2f7dd-157">Y</span><span class="sxs-lookup"><span data-stu-id="2f7dd-157">Y</span></span>        | <span data-ttu-id="2f7dd-158">Dwue znakowy kod kraju ISO alpha-2.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-158">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="2f7dd-159">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2f7dd-159">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2f7dd-160">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2f7dd-160">REST response</span></span>

<span data-ttu-id="2f7dd-161">Jeśli to się powiedzie, metoda zwróci kod stanu 200, jak pokazano w poniższym przykładzie Odpowiedź — walidacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-161">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="2f7dd-162">Jeśli żądanie zakończy się niepowodzeniem, metoda zwróci kod stanu 400, jak pokazano w przykładzie Odpowiedź — weryfikacja nie powiodła się, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-162">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="2f7dd-163">Treść odpowiedzi zawiera ładunek JSON z dodatkowymi informacjami o błędzie.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-163">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f7dd-164">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2f7dd-164">Response success and error codes</span></span>

<span data-ttu-id="2f7dd-165">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f7dd-166">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2f7dd-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f7dd-167">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2f7dd-167">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="2f7dd-168">Odpowiedź — przykład powodzenia walidacji</span><span class="sxs-lookup"><span data-stu-id="2f7dd-168">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="2f7dd-169">Odpowiedź — przykład błędu walidacji</span><span class="sxs-lookup"><span data-stu-id="2f7dd-169">Response - validation failed example</span></span>

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
