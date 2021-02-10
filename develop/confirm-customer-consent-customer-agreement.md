---
title: Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft
description: Dowiedz się, w jaki sposób potwierdzić akceptację umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006066"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a>Potwierdzenie akceptacji przez klienta umowy klienta firmy Microsoft przy użyciu interfejsów API Centrum partnerskiego

**Dotyczy:**

- Centrum partnerskie

Centrum partnerskie obecnie obsługuje Potwierdzanie akceptacji przez klienta umowy klienta firmy Microsoft tylko w *chmurze publicznej firmy Microsoft*. Ta funkcja nie ma obecnie zastosowania do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

W tym artykule opisano sposób potwierdzania lub ponownego potwierdzania akceptacji przez klienta umowy klienta firmy Microsoft.

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,14 lub nowszej.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). *Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.*

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

- Data (**dateAgreed**), gdy klient zaakceptował umowę klienta firmy Microsoft.

- Informacje o użytkowniku z organizacji klienta, które zaakceptowali umowę klienta firmy Microsoft. Obejmuje to następujące działania:
  - Imię
  - Nazwisko
  - Adres e-mail
  - Numer telefonu (opcjonalnie)
- Jeśli następujące wartości są zmieniane dla klienta, centrum partnerskie umożliwi utworzenie innej umowy dla tego klienta: imię nazwisko nazwisko numer telefonu adres E-mail w przeciwnym razie partnerzy otrzymają następujący kod błędu ze względu na utworzenie duplikatu klienta


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

Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:

1. Pobierz metadane umowy dla umowy klienta firmy Microsoft. Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft. Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Utwórz nowy obiekt **umowy** zawierający szczegóły potwierdzenia.

3. Użyj kolekcji **IAgreggatePartner. Customers** i Wywołaj metodę **ById** z określonym **identyfikatorem dzierżawy klienta**.

4. Użyj właściwości **Agreements** , a następnie wywoływanie metody **Create** lub **Async**.

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

Pełny przykład można znaleźć w klasie [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Żądanie REST

Aby potwierdzić lub ponownie potwierdzić akceptację klienta umowy klienta firmy Microsoft:

1. Pobierz metadane umowy dla umowy klienta firmy Microsoft. Musisz uzyskać **TemplateID** umowy klienta firmy Microsoft. Aby uzyskać więcej informacji, zobacz [Pobieranie metadanych umów dla umowy klienta firmy Microsoft](get-customer-agreement-metadata.md).

2. Utwórz nowy zasób [ **umowy**](agreement-resources.md) , aby potwierdzić, że klient zaakceptował umowę klienta firmy Microsoft. Użyj następującej [składni żądania REST](#request-syntax).

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, który potwierdzasz.

| Nazwa               | Typ | Wymagane | Opis                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| Identyfikator dzierżawy klienta | GUID | Tak | Wartość jest identyfikatorem GUID, który jest sformatowanym identyfikatorem **dzierżawy**, który umożliwia określenie klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania REST.

| Nazwa      | Typ   | Opis                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| Umowa | object | Szczegóły dostarczone przez partnera w celu potwierdzenia akceptacji umowy klienta firmy Microsoft przez klienta. |

#### <a name="agreement"></a>Umowa

Ta tabela zawiera opis minimalnych wymaganych pól w celu utworzenia [zasobu **umowy**](agreement-resources.md).

| Właściwość       | Typ   | Opis                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informacje o użytkowniku z organizacji klienta, którzy zaakceptowali umowę klienta firmy Microsoft, w tym:  **FirstName**, **LastName**, **email** i numer **telefonu** (opcjonalnie) |
| dateAgreed     | ciąg w formacie daty i godziny czasu UTC |Data zaakceptowania umowy przez klienta. |
| templateId     | ciąg | Unikatowy identyfikator typu umowy akceptowany przez klienta. Możesz uzyskać **templateId** dla umowy klienta Microsoft, pobierając metadane umowy dla umowy klienta firmy Microsoft. Aby uzyskać szczegółowe informacje, zobacz artykuł [Pobierz metadane umowy dla umowy klienta firmy Microsoft](./get-customer-agreement-metadata.md) . |
| typ           | ciąg | Typ umowy akceptowany przez klienta. Jeśli klient zaakceptuje umowę klienta firmy Microsoft, należy użyć "MicrosoftCustomerAgreement". |

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

Jeśli to się powiedzie, metoda zwraca [zasób **umowy**](./agreement-resources.md).

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania.

Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
