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
# <a name="validate-an-address"></a>Weryfikowanie adresu

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak zweryfikować adres przy użyciu interfejsu API weryfikacji adresu.

Interfejs API weryfikacji adresu powinien być używany tylko do wstępnej weryfikacji aktualizacji profilu klienta. Użyj go ze zrozumieniem, że jeśli kraj jest regionem Stany Zjednoczone, Kanadzie, Chinach lub Meksyku, pole stanu jest weryfikowane względem listy prawidłowych stanów dla odpowiedniego kraju. We wszystkich innych krajach ten test nie jest przeprowadzane, a interfejs API sprawdza tylko, czy stan jest prawidłowym ciągiem.

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

## <a name="c"></a>C\#

Aby zweryfikować adres, najpierw należy utworzyć nowe wystąpienia obiektu **Address** i wypełnić go adresem do zweryfikowania. Następnie pobierz interfejs operacji **Validations** z właściwości **IAggregatePartner.Validations** i wywołaj metodę **IsAddressValid** przy użyciu obiektu adresu.

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

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa         | Typ   | Wymagane | Opis                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | ciąg | Y        | Pierwszy wiersz adresu.                             |
| Addressline2 | ciąg | N        | Drugi wiersz adresu. Ta właściwość jest opcjonalna. |
| city         | ciąg | Y        | Miasto.                                                  |
| stan        | ciąg | Y        | Stan.                                                 |
| Postalcode   | ciąg | Y        | Kod pocztowy.                                           |
| country      | ciąg | Y        | Dwue znakowy kod kraju ISO alpha-2.                |

### <a name="response-details"></a>Szczegóły odpowiedzi

Odpowiedź zwróci jeden z następujących komunikatów o stanie:

| Stan     | Opis |    Liczba zwróconych sugerowanych adresów |
|-------|---------------|-------------------|
|Zweryfikowana wysyłka | Adres jest weryfikowany i można go wysłać. | Pojedynczy |
|Sprawdzonych | Adres jest weryfikowany. | Pojedynczy |
|Wymagana interakcja | Sugerowany adres został znacząco zmieniony i wymaga potwierdzenia przez użytkownika. | Pojedynczy |
|Część częściowa ulicy | Podana ulica w adresie jest częściowa i wymaga więcej informacji. | Wiele — maksymalnie trzy |
|Część lokalna | Dane lokalne (numer budynku, numer pakietu i inne) są częściowe i wymagają więcej informacji. | Wiele — maksymalnie trzy |
|Wiele | Adres zawiera wiele pól, które są częściowe (potencjalnie również częściowe ulice i część lokalna). | Wiele — maksymalnie trzy |
|Brak | Adres jest nieprawidłowy. | Brak |
|Nie sprawdzono | Nie można wysłać adresu w procesie weryfikacji. | Brak |

### <a name="request-example"></a>Przykład żądania

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

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia metoda zwraca obiekt **AddressValidationResponse** w treści odpowiedzi z kodem **stanu HTTP 200.** Przykład przedstawiono poniżej.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

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
