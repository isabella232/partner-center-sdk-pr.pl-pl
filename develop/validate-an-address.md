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
# <a name="validate-an-address"></a>Weryfikowanie adresu

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Sprawdzanie poprawności adresu przy użyciu interfejsu API weryfikacji adresów.

Interfejs API weryfikacji adresu powinien być używany tylko do weryfikacji aktualizacji profilu klienta. Należy jej użyć, aby w przypadku Stany Zjednoczone, Kanady, Chin lub Meksyku, pole Stan zostało zweryfikowane względem listy prawidłowych stanów w danym kraju. W pozostałych krajach ten test nie występuje, a interfejs API sprawdza, czy stan jest prawidłowym ciągiem.

## <a name="prerequisites"></a>Wymagania wstępne

Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

## <a name="c"></a>C\#

Aby sprawdzić poprawność adresu, najpierw Utwórz wystąpienie nowego obiektu **adresu** i wypełnij go adresem do zweryfikowania. Następnie Pobierz interfejs do operacji **walidacji** z właściwości **IAggregatePartner. walidacje** i Wywołaj metodę **IsAddressValid** z obiektem Address.

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

## <a name="java"></a>Java

Aby sprawdzić poprawność adresu, najpierw Utwórz wystąpienie nowego obiektu **adresu** i wypełnij go adresem do zweryfikowania. Następnie Pobierz interfejs do operacji **walidacji** z funkcji **IAggregatePartner. getwalidacji** i Wywołaj metodę **isAddressValid** z obiektem Address.

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

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby sprawdzić poprawność adresu, wykonaj polecenie [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) z wypełnionymi parametrami adresu.

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                                 |
|----------|-----------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/validations/Address http/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa         | Typ   | Wymagane | Opis                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | ciąg | Y        | Pierwszy wiersz adresu.                             |
| addressline2 | ciąg | N        | Drugi wiersz adresu. Ta właściwość jest opcjonalna. |
| city         | ciąg | Y        | Miasto.                                                  |
| stan        | ciąg | Y        | Stan.                                                 |
| pocztowy   | ciąg | Y        | Kod pocztowy.                                           |
| country      | ciąg | Y        | Dwuznakowy ISO kod kraju Alpha-2.                |

### <a name="request-example"></a>Przykład żądania

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

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca kod stanu 200, jak pokazano w przykładzie odpowiedzi-Walidacja zakończyła się pomyślnie.

Jeśli żądanie nie powiedzie się, metoda zwraca kod stanu 400, jak pokazano w przykładzie niepowodzenia weryfikacji odpowiedzi poniżej. Treść odpowiedzi zawiera ładunek JSON z dodatkowymi informacjami o błędzie.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response---validation-succeeded-example"></a>Odpowiedź — sprawdzanie poprawności zakończyło się pomyślnie

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a>Przykład weryfikacji odpowiedzi nie powiodła się

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
