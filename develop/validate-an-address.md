---
title: Weryfikowanie adresu
description: Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2eeca91b0e5a507dac6df4ecf61a56aed2d2d921
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572084"
---
# <a name="validate-an-address"></a><span data-ttu-id="a9a96-103">Weryfikowanie adresu</span><span class="sxs-lookup"><span data-stu-id="a9a96-103">Validate an address</span></span>

<span data-ttu-id="a9a96-104">**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a9a96-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a9a96-105">Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.</span><span class="sxs-lookup"><span data-stu-id="a9a96-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="a9a96-106">Interfejs API weryfikacji adresu powinien być używany tylko do wstępnej weryfikacji aktualizacji profilu klienta.</span><span class="sxs-lookup"><span data-stu-id="a9a96-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="a9a96-107">Użyj go ze zrozumieniem, że jeśli kraj jest regionem Stany Zjednoczone, Kanadzie, Chinach lub Meksyku, pole stanu jest weryfikowane względem listy prawidłowych stanów dla odpowiedniego kraju.</span><span class="sxs-lookup"><span data-stu-id="a9a96-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="a9a96-108">We wszystkich innych krajach ten test nie jest przeprowadzane, a interfejs API sprawdza tylko, czy stan jest prawidłowym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="a9a96-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a96-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9a96-109">Prerequisites</span></span>

<span data-ttu-id="a9a96-110">Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a9a96-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a9a96-111">Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9a96-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a9a96-112">C\#</span><span class="sxs-lookup"><span data-stu-id="a9a96-112">C\#</span></span>

<span data-ttu-id="a9a96-113">Aby zweryfikować adres, najpierw należy utworzyć nowe wystąpienia obiektu **Address** i wypełnić go adresem do zweryfikowania.</span><span class="sxs-lookup"><span data-stu-id="a9a96-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="a9a96-114">Następnie pobierz interfejs operacji **Validations** z właściwości **IAggregatePartner.Validations** i wywołaj metodę **IsAddressValid** przy użyciu obiektu adresu.</span><span class="sxs-lookup"><span data-stu-id="a9a96-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="a9a96-115">Żądanie REST</span><span class="sxs-lookup"><span data-stu-id="a9a96-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a9a96-116">Składnia żądania</span><span class="sxs-lookup"><span data-stu-id="a9a96-116">Request syntax</span></span>

| <span data-ttu-id="a9a96-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="a9a96-117">Method</span></span>   | <span data-ttu-id="a9a96-118">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a9a96-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="a9a96-119">**Post**</span><span class="sxs-lookup"><span data-stu-id="a9a96-119">**POST**</span></span> | <span data-ttu-id="a9a96-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a9a96-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a9a96-121">Nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="a9a96-121">Request headers</span></span>

<span data-ttu-id="a9a96-122">Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a9a96-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a9a96-123">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a9a96-123">Request body</span></span>

<span data-ttu-id="a9a96-124">W tej tabeli opisano wymagane właściwości w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="a9a96-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="a9a96-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a9a96-125">Name</span></span>         | <span data-ttu-id="a9a96-126">Typ</span><span class="sxs-lookup"><span data-stu-id="a9a96-126">Type</span></span>   | <span data-ttu-id="a9a96-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a9a96-127">Required</span></span> | <span data-ttu-id="a9a96-128">Opis</span><span class="sxs-lookup"><span data-stu-id="a9a96-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="a9a96-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="a9a96-129">addressline1</span></span> | <span data-ttu-id="a9a96-130">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-130">string</span></span> | <span data-ttu-id="a9a96-131">Y</span><span class="sxs-lookup"><span data-stu-id="a9a96-131">Y</span></span>        | <span data-ttu-id="a9a96-132">Pierwszy wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="a9a96-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="a9a96-133">Addressline2</span><span class="sxs-lookup"><span data-stu-id="a9a96-133">addressline2</span></span> | <span data-ttu-id="a9a96-134">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-134">string</span></span> | <span data-ttu-id="a9a96-135">N</span><span class="sxs-lookup"><span data-stu-id="a9a96-135">N</span></span>        | <span data-ttu-id="a9a96-136">Drugi wiersz adresu.</span><span class="sxs-lookup"><span data-stu-id="a9a96-136">The second line of the address.</span></span> <span data-ttu-id="a9a96-137">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="a9a96-137">This property is optional.</span></span> |
| <span data-ttu-id="a9a96-138">city</span><span class="sxs-lookup"><span data-stu-id="a9a96-138">city</span></span>         | <span data-ttu-id="a9a96-139">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-139">string</span></span> | <span data-ttu-id="a9a96-140">Y</span><span class="sxs-lookup"><span data-stu-id="a9a96-140">Y</span></span>        | <span data-ttu-id="a9a96-141">Miasto.</span><span class="sxs-lookup"><span data-stu-id="a9a96-141">The city.</span></span>                                                  |
| <span data-ttu-id="a9a96-142">stan</span><span class="sxs-lookup"><span data-stu-id="a9a96-142">state</span></span>        | <span data-ttu-id="a9a96-143">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-143">string</span></span> | <span data-ttu-id="a9a96-144">Y</span><span class="sxs-lookup"><span data-stu-id="a9a96-144">Y</span></span>        | <span data-ttu-id="a9a96-145">Stan.</span><span class="sxs-lookup"><span data-stu-id="a9a96-145">The state.</span></span>                                                 |
| <span data-ttu-id="a9a96-146">Postalcode</span><span class="sxs-lookup"><span data-stu-id="a9a96-146">postalcode</span></span>   | <span data-ttu-id="a9a96-147">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-147">string</span></span> | <span data-ttu-id="a9a96-148">Y</span><span class="sxs-lookup"><span data-stu-id="a9a96-148">Y</span></span>        | <span data-ttu-id="a9a96-149">Kod pocztowy.</span><span class="sxs-lookup"><span data-stu-id="a9a96-149">The postal code.</span></span>                                           |
| <span data-ttu-id="a9a96-150">country</span><span class="sxs-lookup"><span data-stu-id="a9a96-150">country</span></span>      | <span data-ttu-id="a9a96-151">ciąg</span><span class="sxs-lookup"><span data-stu-id="a9a96-151">string</span></span> | <span data-ttu-id="a9a96-152">Y</span><span class="sxs-lookup"><span data-stu-id="a9a96-152">Y</span></span>        | <span data-ttu-id="a9a96-153">Dwue znakowy kod kraju ISO alpha-2.</span><span class="sxs-lookup"><span data-stu-id="a9a96-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="a9a96-154">Szczegóły odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a9a96-154">Response details</span></span>

<span data-ttu-id="a9a96-155">Odpowiedź zwróci jeden z następujących komunikatów o stanie:</span><span class="sxs-lookup"><span data-stu-id="a9a96-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="a9a96-156">Stan</span><span class="sxs-lookup"><span data-stu-id="a9a96-156">Status</span></span>     | <span data-ttu-id="a9a96-157">Opis</span><span class="sxs-lookup"><span data-stu-id="a9a96-157">Description</span></span> |    <span data-ttu-id="a9a96-158">Liczba zwróconych sugerowanych adresów</span><span class="sxs-lookup"><span data-stu-id="a9a96-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="a9a96-159">Zweryfikowana wysyłka</span><span class="sxs-lookup"><span data-stu-id="a9a96-159">Verified shippable</span></span> | <span data-ttu-id="a9a96-160">Adres jest weryfikowany i można go wysłać.</span><span class="sxs-lookup"><span data-stu-id="a9a96-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="a9a96-161">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="a9a96-161">Single</span></span> |
|<span data-ttu-id="a9a96-162">Sprawdzonych</span><span class="sxs-lookup"><span data-stu-id="a9a96-162">Verified</span></span> | <span data-ttu-id="a9a96-163">Adres jest weryfikowany.</span><span class="sxs-lookup"><span data-stu-id="a9a96-163">Address is verified.</span></span> | <span data-ttu-id="a9a96-164">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="a9a96-164">Single</span></span> |
|<span data-ttu-id="a9a96-165">Wymagana interakcja</span><span class="sxs-lookup"><span data-stu-id="a9a96-165">Interaction required</span></span> | <span data-ttu-id="a9a96-166">Sugerowany adres został znacząco zmieniony i wymaga potwierdzenia przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a9a96-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="a9a96-167">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="a9a96-167">Single</span></span> |
|<span data-ttu-id="a9a96-168">Część częściowa ulicy</span><span class="sxs-lookup"><span data-stu-id="a9a96-168">Street partial</span></span> | <span data-ttu-id="a9a96-169">Podana ulica w adresie jest częściowa i wymaga więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a9a96-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="a9a96-170">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="a9a96-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="a9a96-171">Część lokalna</span><span class="sxs-lookup"><span data-stu-id="a9a96-171">Premises partial</span></span> | <span data-ttu-id="a9a96-172">Dane lokalne (numer budynku, numer pakietu i inne) są częściowe i wymagają więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a9a96-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="a9a96-173">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="a9a96-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="a9a96-174">Wiele</span><span class="sxs-lookup"><span data-stu-id="a9a96-174">Multiple</span></span> | <span data-ttu-id="a9a96-175">Adres zawiera wiele pól, które są częściowe (potencjalnie również częściowe ulice i część lokalna).</span><span class="sxs-lookup"><span data-stu-id="a9a96-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="a9a96-176">Wiele — maksymalnie trzy</span><span class="sxs-lookup"><span data-stu-id="a9a96-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="a9a96-177">Brak</span><span class="sxs-lookup"><span data-stu-id="a9a96-177">None</span></span> | <span data-ttu-id="a9a96-178">Adres jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="a9a96-178">Address is incorrect.</span></span> | <span data-ttu-id="a9a96-179">Brak</span><span class="sxs-lookup"><span data-stu-id="a9a96-179">None</span></span> |
|<span data-ttu-id="a9a96-180">Nie sprawdzono</span><span class="sxs-lookup"><span data-stu-id="a9a96-180">Not validated</span></span> | <span data-ttu-id="a9a96-181">Nie można wysłać adresu w procesie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="a9a96-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="a9a96-182">Brak</span><span class="sxs-lookup"><span data-stu-id="a9a96-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="a9a96-183">Przykład żądania</span><span class="sxs-lookup"><span data-stu-id="a9a96-183">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a9a96-184">Odpowiedź REST</span><span class="sxs-lookup"><span data-stu-id="a9a96-184">REST response</span></span>

<span data-ttu-id="a9a96-185">W przypadku powodzenia metoda zwraca obiekt **AddressValidationResponse** w treści odpowiedzi z kodem **stanu HTTP 200.**</span><span class="sxs-lookup"><span data-stu-id="a9a96-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="a9a96-186">Przykład przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="a9a96-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a9a96-187">Kody powodzenia i błędów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a9a96-187">Response success and error codes</span></span>

<span data-ttu-id="a9a96-188">Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.</span><span class="sxs-lookup"><span data-stu-id="a9a96-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a9a96-189">Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="a9a96-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a9a96-190">Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a9a96-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a9a96-191">Przykład odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a9a96-191">Response example</span></span>

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
