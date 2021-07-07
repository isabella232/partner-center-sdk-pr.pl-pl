---
title: Aktualizowanie kwalifikacji klienta
description: Dowiedz się, jak zaktualizować kwalifikacje klienta za pomocą synchronicznego badania lub weryfikacyjnego, w tym adresu skojarzonego z profilem.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 5047743afdef02033d9494e3d8c16c9ab96b3fe9
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446653"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Aktualizowanie kwalifikacji klienta za pomocą walidacji synchronicznej

Dowiedz się, jak synchronicznie aktualizować kwalifikacje klienta za pośrednictwem Partner Center API. Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz Aktualizowanie kwalifikacji klienta za pomocą [walidacji asynchronicznej.](update-customer-qualification-asynchronous.md)

Partner może zaktualizować kwalifikację klienta na "Edukacja" lub "GovernmentCo w chmurze". Innych wartości, "Brak" i "Nonprofit", nie można ustawić.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby zaktualizować kwalifikację klienta do "Edukacja", wywołaj **[Update/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** istniejącego [**klienta.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer)

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** PartnerSDK.FeatureSamples, **klasa:** CustomerQualificationOperations.cs

Aby zaktualizować kwalifikację klienta do chmury **GovernmentCo w** przypadku istniejącego klienta bez kwalifikacji, partner musi uwzględnić kod [**weryfikacji klienta**](utility-resources.md#validationcode).

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer_id}/qualification?code={validationCode} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zaktualizować kwalifikację.

| Nazwa                   | Typ | Wymagane | Opis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **identyfikator dzierżawy klienta** | GUID | Tak      | Wartość jest identyfikatorem GUID w formacie **customer-tenant-id,** który umożliwia odsprzedawcy filtrowanie wyników dla danego klienta, który należy do odsprzedawcy. |
| **validationCode**     | int  | Nie       | Wymagane tylko w przypadku Government Community Cloud.                                                                                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Wartość całkowita z [**wyliczenia CustomerQualification.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification)

### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca zaktualizowaną właściwość [**Kwalifikacja**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Kody błędów](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-articles"></a>Pokrewne artykuły:

- [Pobieranie kwalifikacji klienta](./get-customer-qualification-synchronous.md)
- [Pobieranie kodów weryfikacyjnych partnera](get-a-partner-s-validation-codes.md)
