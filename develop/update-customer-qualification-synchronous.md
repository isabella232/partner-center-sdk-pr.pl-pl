---
title: Aktualizowanie kwalifikacji klienta
description: Dowiedz się, jak aktualizować kwalifikacje klienta za pośrednictwem synchronicznych ekranów lub przed sprawdzeniem, w tym adres skojarzony z profilem.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 7faab68d20c698f5b040a76f4776dbdf14180640
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770204"
---
# <a name="update-a-customers-qualification-via-synchronous-validation"></a>Aktualizowanie kwalifikacji klienta poprzez weryfikację synchroniczną

**Dotyczy**

- Centrum partnerskie

Dowiedz się, jak aktualizować kwalifikacje klienta synchronicznie za pośrednictwem interfejsów API Centrum partnerskiego. Aby dowiedzieć się, jak to zrobić asynchronicznie, zobacz [Aktualizowanie kwalifikacji klienta za pośrednictwem walidacji asynchronicznej](update-customer-qualification-asynchronous.md).

Partner może zaktualizować kwalifikację klienta pod kątem "edukacji" lub "GovernmentCommunityCloud". Nie można ustawić innych wartości, "none" i "non profit".

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Aby zaktualizować kwalifikację klienta do "edukacji", wywołaj polecenie **[Update/dotnet/API/Microsoft. Store. partnercenter. kwalifikacja. icustomerqualification. Update)** na istniejącym  [**kliencie**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer).

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Project**: PartnerSDK. FeatureSamples **Klasa**: CustomerQualificationOperations.cs

Aby zaktualizować kwalifikację klienta do **GovernmentCommunityCloud** na istniejącym kliencie bez kwalifikacji.  Partner jest również zobowiązany do uwzględnienia [**ValidationCode**](utility-resources.md#validationcode)klienta.

``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{Customer_ID}/Qualification? Code = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zaktualizować kwalifikacje.

| Nazwa                   | Typ | Wymagane | Opis                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Identyfikator dzierżawy klienta** | GUID | Tak      | Wartość jest identyfikatorem GUID z sformatowaną **dzierżawą klienta** , która umożliwia odsprzedawcy filtrowanie wyników dla danego klienta należącego do odsprzedawcy. |
| **validationCode**     | int  | Nie       | Wymagany tylko w przypadku chmury społecznościowej dla instytucji rządowych.                                                                                                            |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Wartość całkowita z wyliczenia [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .

### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca zaktualizowaną Właściwość [**kwalifikacji**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów](error-codes.md).

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

- [Pobieranie kwalifikacji klienta](get-a-customer-s-qualification.md)
- [Pobieranie kodów weryfikacyjnych partnera](get-a-partner-s-validation-codes.md)
