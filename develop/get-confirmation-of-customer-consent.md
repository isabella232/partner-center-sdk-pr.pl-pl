---
title: Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud
description: W tym artykule wyjaśniono, jak uzyskać potwierdzenie akceptacji przez klienta umowy Microsoft Cloud.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768446"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Pobieranie potwierdzenia akceptacji przez klienta umowy dotyczącej platformy Microsoft Cloud

**Dotyczy**

- Centrum partnerskie

> [!NOTE]
> Zasób z **umową** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft. Nie dotyczy:
>
> - Centrum partnerskie obsługiwane przez firmę 21Vianet
> - Centrum partnerskie dla Microsoft Cloud Niemcy
> - Centrum partnerskie Microsoft Cloud for US Government

## <a name="prerequisites"></a>Wymagania wstępne

- W przypadku korzystania z zestawu SDK platformy .NET w programie Partner Center wymagany jest program w wersji 1,9 lub nowszej.

- W przypadku korzystania z zestawu SDK języka Java Centrum partnerskiego wymagana jest wersja 1,8 lub nowsza.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](./partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie aplikacji i użytkowników.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="net-version-14-or-newer"></a>.NET (wersja 1,4 lub nowsza)

Aby pobrać potwierdzenia, które zostały wcześniej dostarczone przez klienta:

- Użyj metody **IAggregatePartner. Customers** i Wywołaj metodę **ById** z określonym identyfikatorem klienta.

- Pobierz Właściwość **Agreements** i przefiltruj wyniki do Microsoft Cloudej umowy przez wywołanie metody **ByAgreementType** .

- Wywoływanie metody **Get** lub **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) z projektu [aplikacji testowej konsoli](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="net-version-19---113"></a>.NET (wersja 1,9-1,13)

Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:

Użyj kolekcji **IAggregatePartner. Customers** i Wywołaj metodę **ById** przy użyciu identyfikatora określonego klienta. Następnie Pobierz Właściwość **Agreement** , a następnie wywołując metody **Get** lub **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:

Użyj funkcji **IAggregatePartner. GetCustomers** i wywołaj funkcję **byId** z identyfikatorem określonego klienta. Następnie Pobierz funkcję **Getagreements** , a następnie wywołując funkcję **Get** .

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Pełny przykład można znaleźć w klasie [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) z projektu [aplikacji testowej konsoli](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta:

Użyj polecenia [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) .

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a>Żądanie REST

Aby pobrać potwierdzenie podanej wcześniej akceptacji klienta, zapoznaj się z poniższymi instrukcjami.

Utwórz nowy zasób **umowy** z odpowiednimi informacjami o certyfikacji.

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/V1/Customers/{Customer-tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, który chcesz potwierdzić.

| Nazwa             | Typ | Wymagane | Opis                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| CustomerTenantId | GUID | Y        | Wartość jest identyfikatorem GUID w formacie **CustomerTenantId** , który umożliwia określenie klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ta metoda zwraca kolekcję zasobów **umowy** w treści odpowiedzi.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
