---
title: Aktualizowanie kwalifikacji klienta
description: Program aktualizuje kwalifikacje klienta asynchronicznie, w tym adres skojarzony z profilem.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 7606eeaac4df158ec0fad6ffd4e565bb250f448e
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030610"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Aktualizowanie kwalifikacji klienta asynchronicznie

Aktualizuje kwalifikacje klienta asynchronicznie.

Partner może zaktualizować kwalifikacje klienta asynchronicznie do "Education" lub "GovernmentCommunityCloud". Nie można ustawić innych wartości, "none" i "non profit".

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby utworzyć kwalifikację klienta dla "edukacji", najpierw Utwórz obiekt reprezentujący typ kwalifikacji. Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) . Na koniec Wywołaj `CreateQualifications()` lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji jako parametr wejściowy.

``` csharp
var qualificationType = { Qualification = "education" };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples **Class**: CreateCustomerQualification. cs

Aby zaktualizować kwalifikację klienta do **GovernmentCommunityCloud** na istniejącym kliencie bez kwalifikacji, partner jest również zobowiązany do uwzględnienia [**ValidationCode**](utility-resources.md#validationcode)klienta. Najpierw Utwórz obiekt reprezentujący typ kwalifikacji. Następnie Wywołaj metodę [**IAggregatePartner. Customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) z identyfikatorem klienta. Następnie użyj właściwości [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) do pobrania interfejsu [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) . Na koniec Wywołaj `CreateQualifications()` lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji i kodem sprawdzania poprawności jako parametry wejściowe.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Przykład**: [Przykładowa aplikacja konsolowa](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Projekt**: SdkSamples **Class**: CreateCustomerQualificationWithGCC. cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **POUBOJOWEGO** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer_ID}/Qualifications? Code = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zaktualizować kwalifikacje.

| Nazwa                   | Typ | Wymagane | Opis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | GUID | Tak      | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |
| **validationCode**     | int  | Nie       | Wymagany tylko w przypadku chmury społecznościowej dla instytucji rządowych.                                                                                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano obiekt kwalifikacji w treści żądania.

Właściwość | Typ | Wymagane | Opis
-------- | ---- | -------- | -----------
Kwalifikacja | ciąg | Tak | Wartość ciągu z wyliczenia [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

{
    "Qualification": "Education"
}

```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, metoda zwraca obiekt kwalifikacji w treści odpowiedzi. Poniżej znajduje się przykład wywołania **post** na kliencie (z wcześniejszą kwalifikacją dla **braku**) z kwalifikacją **edukacyjną** .

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Pokrewne artykuły:

- [Pobierz kwalifikacje klienta](./get-customer-qualification-asynchronous.md)
- [Pobieranie kodów weryfikacyjnych partnera](get-a-partner-s-validation-codes.md)
