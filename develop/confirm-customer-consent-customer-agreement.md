---
title: Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft
description: Dowiedz się, jak potwierdzić akceptację przez klientów Umowa z Klientem Microsoft użyciu Partner Center API.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 374a9670f5d4c05209e5cec07afe766bcf57f255f9266138b7aaf0e85f90f0ed
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991926"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Potwierdzanie akceptacji przez klienta Umowa z Klientem Microsoft przy użyciu Partner Center API

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner Center obsługuje obecnie potwierdzenie akceptacji przez klienta Umowa z Klientem Microsoft tylko w chmurze publicznej firmy Microsoft.

W tym artykule opisano sposób potwierdzania lub ponownego potwierdzania akceptacji Umowa z Klientem Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli używasz zestawu SDK platformy Partner Center .NET, wymagana jest wersja 1.14 lub nowsza.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](./partner-center-authentication.md) *Ten scenariusz obsługuje tylko uwierzytelnianie app+user.*

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz **pozycję Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Data **(dateAgreed),** kiedy klient zaakceptował Umowa z Klientem Microsoft.

- Informacje o użytkowniku z organizacji klienta, który zaakceptował Umowa z Klientem Microsoft. Obejmuje to następujące działania:
  - Imię
  - Nazwisko
  - Adres e-mail
  - Telefon (opcjonalnie)
- Jeśli następujące wartości zmienią się dla klienta, program Partner Center zezwoli na Partner Center utworzenia innej umowy dla tego klienta: Imię Nazwisko Adres e-mail Telefon numer W przeciwnym razie partnerzy otrzymają następujący kod błędu z powodu utworzenia zduplikowanego klienta


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a>.NET

Aby potwierdzić lub ponownie potwierdzić akceptację przez klienta Umowa z Klientem Microsoft:

1. Pobierz metadane umowy dla Umowa z Klientem Microsoft. Musisz uzyskać **szablon templateId** Umowa z Klientem Microsoft. Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md)(Uzyskiwanie metadanych umowy dla Umowa z Klientem Microsoft ).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Utwórz nowy obiekt **Umowy** zawierający szczegóły potwierdzenia.

3. Użyj **kolekcji IAgreggatePartner.Customers** i wywołaj metodę **ById** z określonym **identyfikatorem customer-tenant-id**.

4. Użyj właściwości **Agreements,** a następnie wywołaj właściwość **Create** lub **CreateAsync.**

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

Kompletny przykład można znaleźć w klasie [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) w projekcie [aplikacji testowej konsoli.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="rest-request"></a>Żądanie REST

Aby potwierdzić lub ponownie potwierdzić akceptację przez klienta Umowa z Klientem Microsoft:

1. Pobierz metadane umowy dla Umowa z Klientem Microsoft. Musisz uzyskać **szablon templateId** Umowa z Klientem Microsoft. Aby uzyskać więcej informacji, zobacz [Get agreement metadata for Umowa z Klientem Microsoft](get-customer-agreement-metadata.md)(Uzyskiwanie metadanych umowy dla Umowa z Klientem Microsoft ).

2. Utwórz nowy [ **zasób umowy,**](agreement-resources.md) aby potwierdzić, że klient zaakceptował Umowa z Klientem Microsoft. Użyj następującej [składni żądania REST.](#request-syntax)

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, który potwierdzasz.

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| identyfikator dzierżawy klienta | GUID | Tak | Wartość jest identyfikatorem **customer-tenant-id** w formacie identyfikatora GUID, który jest identyfikatorem umożliwiającym określenie klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania REST.

| Nazwa      | Typ   | Opis                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Umowa | object | Szczegółowe informacje udostępniane przez partnera w celu potwierdzenia akceptacji Umowa z Klientem Microsoft. |

#### <a name="agreement"></a>Umowa

W tej tabeli opisano minimalne pola wymagane do utworzenia zasobu [ **umowy**](agreement-resources.md).

| Właściwość       | Typ   | Opis                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informacje o użytkowniku z organizacji klienta, który zaakceptował Umowa z Klientem Microsoft, w tym:  **firstName,** **lastName,** **email** i **phoneNumber** (opcjonalnie) |
| dateAgreed     | ciąg w formacie daty i czasu UTC |Data zaakceptowania umowy przez klienta. |
| templateId     | ciąg | Unikatowy identyfikator typu umowy zaakceptowany przez klienta. Możesz uzyskać szablon **templateId** dla Umowa z Klientem Microsoft, pobierania metadanych umowy dla Umowa z Klientem Microsoft. Aby [uzyskać szczegółowe informacje, zobacz Get agreement metadata for Umowa z Klientem Microsoft](./get-customer-agreement-metadata.md) (Uzyskiwanie metadanych umowy). |
| typ           | ciąg | Typ umowy zaakceptowany przez klienta. Użyj "MicrosoftCustomerAgreement", jeśli klient zaakceptował Umowa z Klientem Microsoft. |

#### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca [ **zasób umowy**](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu.

Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

#### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
