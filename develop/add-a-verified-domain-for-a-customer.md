---
title: Dodawanie zweryfikowanej domeny dla klienta
description: Dowiedz się, jak dodać zweryfikowaną domenę do listy zatwierdzonych domen dla klienta w Partner Center. Zrób to przy użyciu Partner Center API i interfejsów API REST.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fc24335aff6fe83b58ad2cb178d03db00614dd8ae24ee83d20b607b56a4bc51d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989138"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Dodawanie zweryfikowanych domen do listy zatwierdzonych domen dla istniejącego klienta 

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak dodać zweryfikowaną domenę do listy zatwierdzonych domen dla istniejącego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Musisz być partnerem, który jest rejestratorem domen.

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go znaleźć na pulpicie nawigacyjnym Partner Center [nawigacyjnym](https://partner.microsoft.com/dashboard). Wybierz **pozycję CSP** z Partner Center menu, a następnie pozycję **Klienci.** Wybierz klienta z listy klientów, a następnie wybierz pozycję **Konto**. Na stronie Konto klienta odszukaj identyfikator **Microsoft w** **sekcji Informacje o koncie** klienta. Identyfikator microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Dodawanie zweryfikowanego domeny

Jeśli jesteś partnerem, który jest rejestratorem domen, możesz użyć interfejsu API, aby opublikować nowy zasób domeny na liście domen `verifieddomain` dla istniejącego klienta. [](#domain) W tym celu zidentyfikuj klienta przy użyciu jego customerTenantId. Określ wartość właściwości VerifiedDomainName. Przekaż [zasób domeny](#domain) w żądaniu z wymaganymi właściwościami Name, Capability, AuthenticationType, Status i VerificationMethod. Aby określić, [](#domain) że nowa domena jest domeną federacyjną, ustaw właściwość AuthenticationType w zasobie Domena na wartość i uwzględnij zasób [](#domain) `Federated` [DomainFederationSettings](#domain-federation-settings) w żądaniu. Jeśli metoda powiedzie się, odpowiedź będzie zawierać zasób [Domena](#domain) dla nowej zweryfikowanych domen.

### <a name="custom-verified-domains"></a>Domeny zweryfikowane niestandardowo

Podczas dodawania domeny zweryfikowanej niestandardowo, domeny, która nie jest zarejestrowana w użytce **onmicrosoft.com,** należy ustawić właściwość [CustomerUser.immutableId](user-resources.md#customeruser) na wartość unikatowego identyfikatora dla klienta, dla którym dodajesz domenę. Ten unikatowy identyfikator jest wymagany podczas procesu weryfikacji domeny. Aby uzyskać więcej informacji na temat kont użytkowników klientów, zobacz [Tworzenie kont użytkowników dla klienta.](create-user-accounts-for-a-customer.md)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, dla który dodajesz zweryfikowaną domenę.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Wartość jest identyfikatorem GUID w **formacie CustomerTenantId,** który umożliwia określenie klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                                                  | Typ   | Wymagane                                      | Opis                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | ciąg | Tak                                           | Zweryfikowana nazwa domeny. |
| [Domeny](#domain)                                     | object | Tak                                           | Zawiera informacje o domenie. |
| [DomainFederationSettings](#domain-federation-settings) | object | Tak (Jeśli AuthenticationType = `Federated` )     | Ustawienia federacji domeny, które mają być używane, jeśli domena jest `Federated` domeną, a nie `Managed` domeną. |

### <a name="domain"></a>Domena

W tej tabeli opisano wymagane i opcjonalne **właściwości** domeny w treści żądania.

| Nazwa               | Typ                                     | Wymagane | Opis                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authenticationtype                                    | ciąg           | Tak      | Określa, czy domena jest `Managed` domeną, czy `Federated` domeną. Obsługiwane wartości: `Managed` , `Federated` .|
| Możliwość                                            | ciąg           | Tak      | Określa możliwość domeny. Na przykład `Email`.                  |
| Isdefault                                             | wartość logiczna dopuszczalna null | Nie       | Wskazuje, czy domena jest domeną domyślną dzierżawy. Obsługiwane wartości: `True` , `False` , `Null` .        |
| IsInitial                                             | wartość logiczna dopuszczalna null | Nie       | Wskazuje, czy domena jest domeną początkową. Obsługiwane wartości: `True` , `False` , `Null` .                       |
| Nazwa                                                  | ciąg           | Tak      | Nazwa domeny.                                                          |
| RootDomain (Domena główna)                                            | ciąg           | Nie       | Nazwa domeny głównej.                                              |
| Stan                                                | ciąg           | Tak      | Stan domeny. Na przykład `Verified`. Obsługiwane wartości:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | ciąg           | Tak      | Typ metody weryfikacji domeny. Obsługiwane wartości: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Ustawienia federacji domeny

W tej tabeli opisano wymagane i opcjonalne właściwości **DomainFederationSettings** w treści żądania.

| Nazwa   | Typ   | Wymagane | Opis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | ciąg           | Nie      | URI logowania używany przez rozbudowanych klientów. Ta właściwość jest adresem URL uwierzytelniania usługi STS partnera. |
| DefaultInteractiveAuthenticationMethod | ciąg           | Nie      | Wskazuje domyślną metodę uwierzytelniania, która powinna być używana, gdy aplikacja wymaga od użytkownika logowania interakcyjnego. |
| FederationBrandName                    | ciąg           | Nie      | Nazwa marki federacji.        |
| IssuerUri                              | ciąg           | Tak     | Nazwa wystawcy certyfikatów.                        |
| LogOffUri                              | ciąg           | Tak     | Wyloguj się URI. Ta właściwość opisuje federacyjną domenę wylogowywującą się z domeny URI.        |
| MetadataExchangeUri                    | ciąg           | Nie      | Adres URL określający punkt końcowy wymiany metadanych używany do uwierzytelniania z rozbudowanych aplikacji klienckich. |
| NextSigningCertificate                 | ciąg           | Nie      | Certyfikat używany na przyszłość przez usługę ADFS V2 STS do podpisywania oświadczeń. Ta właściwość jest zakodowaną w formacie base64 reprezentacją certyfikatu. |
| OpenIdConnectDiscoveryEndpoint         | ciąg           | Nie      | OpenID Połączenie punkt końcowy odnajdywania federowanych usług STS IDP. |
| PassiveLogOnUri                        | ciąg           | Tak     | Używany przez starszych pasywnych klientów URI logowania. Ta właściwość jest adresem do wysyłania federowanych żądań logowania. |
| PreferredAuthenticationProtocol        | ciąg           | Tak     | Format tokenu uwierzytelniania. Na przykład `WsFed`. Obsługiwane wartości: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | ciąg           | Tak     | Typ zachowania monitu logowania.  Na przykład `TranslateToFreshPasswordAuth`. Obsługiwane wartości: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | ciąg           | Tak     | Certyfikat używany obecnie przez usługę ADFS v2 STS do podpisywania oświadczeń. Ta właściwość jest zakodowaną w formacie base64 reprezentacją certyfikatu. |
| SigningCertificateUpdateStatus         | ciąg           | Nie      | Wskazuje stan aktualizacji certyfikatu podpisywania. |
| SigningCertificateUpdateStatus         | wartość logiczna dopuszczana wartość null | Nie      | Wskazuje, czy usługi STS dostawcy tożsamości obsługują uwierzytelniania wieloskładnikowego. Obsługiwane wartości: `True` , `False` , `Null` .|

### <a name="request-example"></a>Przykład żądania

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ten interfejs API zwraca [zasób domeny](#domain) dla nowej zweryfikowanych domen.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
