---
title: Aktualizowanie kwalifikacji klienta
description: Asynchronicznie aktualizuje kwalifikacje klienta, w tym adres skojarzony z profilem.
ms.date: 03/23/2021
ms.service: partner-dashboard
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: d7dd3593894ce91ddc7b96d604b80153d41d3a67
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2021
ms.locfileid: "113572101"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Asynchroniczne aktualizowanie kwalifikacji klienta

Aktualizuje kwalifikacje klienta asynchronicznie.

Partner może asynchronicznie zaktualizować kwalifikacje klienta tak, aby zawierały "Edukacja" lub "GovernmentCo w chmurze". Innych wartości, "Brak" i "Nonprofit", nie można ustawić.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby utworzyć kwalifikację klienta do "Edukacja", najpierw utwórz obiekt reprezentujący typ kwalifikacji. Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta. Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Na koniec wywołaj element lub z `CreateQualifications()` `CreateQualificationsAsync()` obiektem typu kwalifikacji jako parametrem wejściowym.

``` csharp
var qualificationToCreate = "education";    // can also be "StateOwnedEntity" or "GovernmentCommunityCloud". See GCC example below.
var qualificationType = { Qualification = qualificationToCreate };
var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType);
```

**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples, **klasa**: CreateCustomerQualification.cs

Aby zaktualizować kwalifikację klienta do chmury **GovernmentCo w** przypadku istniejącego klienta bez kwalifikacji, partner musi również uwzględnić kod [**weryfikacji klienta**](utility-resources.md#validationcode). Najpierw utwórz obiekt reprezentujący typ kwalifikacji. Następnie wywołaj metodę [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) przy użyciu identyfikatora klienta. Następnie użyj właściwości [**Kwalifikacja,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) aby pobrać [**interfejs ICustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) Na koniec wywołaj `CreateQualifications()` parametr lub `CreateQualificationsAsync()` z obiektem typu kwalifikacji i kodem walidacji jako parametrami wejściowymi.

``` csharp
// GCC validation is type ValidationCode
var qualificationType = { Qualification = "GovernmentCommunityCloud" };
var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.CreateQualifications(qualificationType, gccValidation);
```

**Przykład:** [Przykładowa aplikacja konsoli](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples, **klasa**: CreateCustomerQualificationWithGCC.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualifications?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zaktualizować kwalifikację.

| Nazwa                   | Typ | Wymagane | Opis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | GUID | Tak      | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy. |
| **validationCode**     | int  | Nie       | Wymagane tylko w przypadku Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano obiekt kwalifikacji w treści żądania.

Właściwość | Typ | Wymagane | Opis
-------- | ---- | -------- | -----------
Kwalifikacja | ciąg | Tak | Wartość ciągu z [**wyli roku CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

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

W przypadku powodzenia ta metoda zwraca obiekt kwalifikacji w treści odpowiedzi. Poniżej znajduje się przykład rozmowy **POST** dotyczącej klienta (z wcześniejszą kwalifikacją **Brak)** z **kwalifikacją edukacja.**

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

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

- [Uzyskiwanie kwalifikacji klienta](./get-customer-qualification-asynchronous.md)
- [Pobieranie kodów weryfikacyjnych partnera](get-a-partner-s-validation-codes.md)
