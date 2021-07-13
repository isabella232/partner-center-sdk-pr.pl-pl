---
title: Weryfikowanie adresu
description: Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30f5cd526ab038dce400e79822d89b8086ba3799
ms.sourcegitcommit: 41bf9dca55f4c96d382b327a75b2d2418edfc9bc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/13/2021
ms.locfileid: "113655610"
---
# <a name="validate-an-address"></a><span data-ttu-id="2a712-103">Weryfikowanie adresu</span><span class="sxs-lookup"><span data-stu-id="2a712-103">Validate an address</span></span>

<span data-ttu-id="2a712-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="2a712-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2a712-105">Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.</span><span class="sxs-lookup"><span data-stu-id="2a712-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="2a712-106">Interfejs API weryfikacji adresu powinien być używany tylko do wstępnej weryfikacji aktualizacji profilu klienta.</span><span class="sxs-lookup"><span data-stu-id="2a712-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="2a712-107">Użyj go ze zrozumieniem, że jeśli kraj jest regionem Stany Zjednoczone, Kanadzie, Chinach lub Meksyku, pole stanu jest weryfikowane względem listy prawidłowych stanów dla odpowiedniego kraju.</span><span class="sxs-lookup"><span data-stu-id="2a712-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="2a712-108">We wszystkich innych krajach ten test nie jest przeprowadzane, a interfejs API sprawdza tylko, czy stan jest prawidłowym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="2a712-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a712-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2a712-109">Prerequisites</span></span>

<span data-ttu-id="2a712-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2a712-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2a712-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a712-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2a712-112">C\#</span><span class="sxs-lookup"><span data-stu-id="2a712-112">C\#</span></span>

<span data-ttu-id="2a712-113">Aby zweryfikować adres, najpierw należy utworzyć nowe wystąpienia obiektu **Address** i wypełnić go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="2a712-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="2a712-114">Następnie pobierz interfejs operacji **Validations** z właściwości **IAggregatePartner.Validations** i wywołaj metodę **IsAddressValid** przy użyciu obiektu adresu.</span><span class="sxs-lookup"><span data-stu-id="2a712-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
IAggregatePartner partnerOperations;

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
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a><span data-ttu-id="2a712-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="2a712-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2a712-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="2a712-116">Request syntax</span></span>

| <span data-ttu-id="2a712-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="2a712-117">Method</span></span>   | <span data-ttu-id="2a712-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="2a712-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="2a712-119">**Post**</span><span class="sxs-lookup"><span data-stu-id="2a712-119">**POST**</span></span> | <span data-ttu-id="2a712-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2a712-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2a712-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="2a712-121">Request headers</span></span>

<span data-ttu-id="2a712-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2a712-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2a712-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2a712-123">Request body</span></span>

<span data-ttu-id="2a712-124">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="2a712-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="2a712-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="2a712-125">Name</span></span>         | <span data-ttu-id="2a712-126">Typ</span><span class="sxs-lookup"><span data-stu-id="2a712-126">Type</span></span>   | <span data-ttu-id="2a712-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2a712-127">Required</span></span> | <span data-ttu-id="2a712-128">Opis</span><span class="sxs-lookup"><span data-stu-id="2a712-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="2a712-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="2a712-129">addressline1</span></span> | <span data-ttu-id="2a712-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-130">string</span></span> | <span data-ttu-id="2a712-131">Y</span><span class="sxs-lookup"><span data-stu-id="2a712-131">Y</span></span>        | <span data-ttu-id="2a712-132">Pierwszy wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="2a712-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="2a712-133">Addressline2</span><span class="sxs-lookup"><span data-stu-id="2a712-133">addressline2</span></span> | <span data-ttu-id="2a712-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-134">string</span></span> | <span data-ttu-id="2a712-135">N</span><span class="sxs-lookup"><span data-stu-id="2a712-135">N</span></span>        | <span data-ttu-id="2a712-136">Drugi wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="2a712-136">The second line of the address.</span></span> <span data-ttu-id="2a712-137">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="2a712-137">This property is optional.</span></span> |
| <span data-ttu-id="2a712-138">city</span><span class="sxs-lookup"><span data-stu-id="2a712-138">city</span></span>         | <span data-ttu-id="2a712-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-139">string</span></span> | <span data-ttu-id="2a712-140">Y</span><span class="sxs-lookup"><span data-stu-id="2a712-140">Y</span></span>        | <span data-ttu-id="2a712-141">Miasto.</span><span class="sxs-lookup"><span data-stu-id="2a712-141">The city.</span></span>                                                  |
| <span data-ttu-id="2a712-142">stan</span><span class="sxs-lookup"><span data-stu-id="2a712-142">state</span></span>        | <span data-ttu-id="2a712-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-143">string</span></span> | <span data-ttu-id="2a712-144">Y</span><span class="sxs-lookup"><span data-stu-id="2a712-144">Y</span></span>        | <span data-ttu-id="2a712-145">Stan.</span><span class="sxs-lookup"><span data-stu-id="2a712-145">The state.</span></span>                                                 |
| <span data-ttu-id="2a712-146">Postalcode</span><span class="sxs-lookup"><span data-stu-id="2a712-146">postalcode</span></span>   | <span data-ttu-id="2a712-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-147">string</span></span> | <span data-ttu-id="2a712-148">Y</span><span class="sxs-lookup"><span data-stu-id="2a712-148">Y</span></span>        | <span data-ttu-id="2a712-149">Kod pocztowy.</span><span class="sxs-lookup"><span data-stu-id="2a712-149">The postal code.</span></span>                                           |
| <span data-ttu-id="2a712-150">country</span><span class="sxs-lookup"><span data-stu-id="2a712-150">country</span></span>      | <span data-ttu-id="2a712-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="2a712-151">string</span></span> | <span data-ttu-id="2a712-152">Y</span><span class="sxs-lookup"><span data-stu-id="2a712-152">Y</span></span>        | <span data-ttu-id="2a712-153">Dwue znakowy kod kraju ISO alpha-2.</span><span class="sxs-lookup"><span data-stu-id="2a712-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="2a712-154">Szczegóły odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2a712-154">Response details</span></span>

<span data-ttu-id="2a712-155">Odpowiedź zwróci jeden z następujących komunikatów o stanie:</span><span class="sxs-lookup"><span data-stu-id="2a712-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="2a712-156">Stan</span><span class="sxs-lookup"><span data-stu-id="2a712-156">Status</span></span>     | <span data-ttu-id="2a712-157">Opis</span><span class="sxs-lookup"><span data-stu-id="2a712-157">Description</span></span> |    <span data-ttu-id="2a712-158">Liczba zwróconych sugerowanych adresów</span><span class="sxs-lookup"><span data-stu-id="2a712-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="2a712-159">Zweryfikowana wysyłka</span><span class="sxs-lookup"><span data-stu-id="2a712-159">Verified shippable</span></span> | <span data-ttu-id="2a712-160">Adres jest weryfikowany i można go wysłać.</span><span class="sxs-lookup"><span data-stu-id="2a712-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="2a712-161">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2a712-161">Single</span></span> |
|<span data-ttu-id="2a712-162">Sprawdzonych</span><span class="sxs-lookup"><span data-stu-id="2a712-162">Verified</span></span> | <span data-ttu-id="2a712-163">Adres jest weryfikowany.</span><span class="sxs-lookup"><span data-stu-id="2a712-163">Address is verified.</span></span> | <span data-ttu-id="2a712-164">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2a712-164">Single</span></span> |
|<span data-ttu-id="2a712-165">Wymagana interakcja</span><span class="sxs-lookup"><span data-stu-id="2a712-165">Interaction required</span></span> | <span data-ttu-id="2a712-166">Sugerowany adres został znacząco zmieniony i wymaga potwierdzenia przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a712-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="2a712-167">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2a712-167">Single</span></span> |
|<span data-ttu-id="2a712-168">Część częściowa ulicy</span><span class="sxs-lookup"><span data-stu-id="2a712-168">Street partial</span></span> | <span data-ttu-id="2a712-169">Podana ulica w adresie jest częściowa i wymaga więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2a712-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="2a712-170">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="2a712-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="2a712-171">Część lokalna</span><span class="sxs-lookup"><span data-stu-id="2a712-171">Premises partial</span></span> | <span data-ttu-id="2a712-172">Dane lokalne (numer budynku, numer pakietu i inne) są częściowe i wymagają więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2a712-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="2a712-173">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="2a712-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="2a712-174">Wiele</span><span class="sxs-lookup"><span data-stu-id="2a712-174">Multiple</span></span> | <span data-ttu-id="2a712-175">Adres zawiera wiele pól, które są częściowe (potencjalnie również częściowe ulice i część lokalna).</span><span class="sxs-lookup"><span data-stu-id="2a712-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="2a712-176">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="2a712-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="2a712-177">Brak</span><span class="sxs-lookup"><span data-stu-id="2a712-177">None</span></span> | <span data-ttu-id="2a712-178">Adres jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="2a712-178">Address is incorrect.</span></span> | <span data-ttu-id="2a712-179">Brak</span><span class="sxs-lookup"><span data-stu-id="2a712-179">None</span></span> |
|<span data-ttu-id="2a712-180">Nie sprawdzono</span><span class="sxs-lookup"><span data-stu-id="2a712-180">Not validated</span></span> | <span data-ttu-id="2a712-181">Nie można wysłać adresu w procesie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="2a712-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="2a712-182">Brak</span><span class="sxs-lookup"><span data-stu-id="2a712-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="2a712-183">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="2a712-183">Request example</span></span>

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="2a712-184">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="2a712-184">REST response</span></span>

<span data-ttu-id="2a712-185">W przypadku powodzenia metoda zwraca obiekt **AddressValidationResponse** w treści odpowiedzi z kodem **stanu HTTP 200.**</span><span class="sxs-lookup"><span data-stu-id="2a712-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="2a712-186">Przykład przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="2a712-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2a712-187">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2a712-187">Response success and error codes</span></span>

<span data-ttu-id="2a712-188">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="2a712-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2a712-189">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="2a712-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2a712-190">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2a712-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2a712-191">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="2a712-191">Response example</span></span>

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
