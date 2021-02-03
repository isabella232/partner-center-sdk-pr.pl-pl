---
title: Dodawanie zweryfikowanej domeny dla klienta
description: Dowiedz się, jak dodać zweryfikowaną domenę do listy zatwierdzonych domen dla klienta w centrum partnerskim. Należy to zrobić przy użyciu interfejsów API Centrum partnerskiego i interfejsów API REST.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d0ea9998324e99c7986645dc90fdfba0a2a71571
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768518"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Dodawanie zweryfikowanej domeny do listy zatwierdzonych domen dla istniejącego klienta 

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak dodać zweryfikowaną domenę do listy zatwierdzonych domen dla istniejącego klienta.

## <a name="prerequisites"></a>Wymagania wstępne

- Musisz być partnerem, który jest rejestratorem domeny.

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Identyfikator klienta ( `customer-tenant-id` ). Jeśli nie znasz identyfikatora klienta, możesz go wyszukać na [pulpicie nawigacyjnym](https://partner.microsoft.com/dashboard)Centrum partnerskiego. Wybierz pozycję **dostawca CSP** z menu Centrum partnerskiego, po którym znajdują się **klienci**. Wybierz klienta z listy klient, a następnie wybierz pozycję **konto**. Na stronie konto klienta Znajdź **Identyfikator Microsoft** w sekcji **Informacje o koncie klienta** . Identyfikator Microsoft jest taki sam jak identyfikator klienta ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Dodawanie zweryfikowanej domeny

Jeśli jesteś partnerem, który jest rejestratorem domeny, możesz użyć `verifieddomain` interfejsu API do opublikowania nowego zasobu [domeny](#domain) na liście domen dla istniejącego klienta. W tym celu Zidentyfikuj klienta przy użyciu ich CustomerTenantId. Określ wartość właściwości VerifiedDomainName. Przekaż zasób [domeny](#domain) w żądaniu z uwzględnieniem wymaganej nazwy, możliwości, uwierzytelnianiatype, stanu i właściwości VerificationMethod. Aby określić, że nowa [domena](#domain) jest domeną federacyjną, ustaw właściwość AuthenticationType w polu zasób [domeny](#domain) na `Federated` i Dołącz do żądania zasób [DomainFederationSettings](#domain-federation-settings) . Jeśli metoda zakończy się pomyślnie, odpowiedź będzie zawierać zasób [domeny](#domain) dla nowej zweryfikowanej domeny.

### <a name="custom-verified-domains"></a>Niestandardowe zweryfikowane domeny

Podczas dodawania niestandardowej zweryfikowanej domeny domena, która nie jest zarejestrowana w usłudze **onmicrosoft.com**, należy ustawić właściwość [CustomerUser. immutableId](user-resources.md#customeruser) na unikatową wartość identyfikatora dla klienta, dla którego dodawana jest domena. Ten unikatowy identyfikator jest wymagany podczas procesu walidacji, gdy domena jest weryfikowana. Aby uzyskać więcej informacji o kontach użytkowników klienta, zobacz [Tworzenie kont użytkowników dla klienta](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda | Identyfikator URI żądania                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/V1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby określić klienta, dla którego chcesz dodać zweryfikowaną domenę.

| Nazwa                   | Typ     | Wymagane | Opis                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Wartość jest identyfikatorem GUID w formacie **CustomerTenantId** , który umożliwia określenie klienta. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                                                  | Typ   | Wymagane                                      | Opis                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | ciąg | Tak                                           | Nazwa zweryfikowanej domeny. |
| [Domeny](#domain)                                     | object | Tak                                           | Zawiera informacje o domenie. |
| [DomainFederationSettings](#domain-federation-settings) | object | Tak (Jeśli AuthenticationType = `Federated` )     | Ustawienia Federacji domeny, które mają być używane, jeśli domena jest `Federated` domeną, a nie `Managed` domeną. |

### <a name="domain"></a>Domena

W tej tabeli opisano wymagane i opcjonalne właściwości **domeny** w treści żądania.

| Nazwa               | Typ                                     | Wymagane | Opis                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | ciąg           | Tak      | Określa, czy domena jest domeną, `Managed` czy `Federated` domeną. Obsługiwane wartości: `Managed` , `Federated` .|
| Możliwość                                            | ciąg           | Tak      | Określa możliwość domeny. Na przykład `Email`.                  |
| IsDefault                                             | wartość logiczna null | Nie       | Wskazuje, czy domena jest domeną domyślną dzierżawcy. Obsługiwane wartości: `True` , `False` , `Null` .        |
| Isinitial                                             | wartość logiczna null | Nie       | Wskazuje, czy domena jest początkową domeną. Obsługiwane wartości: `True` , `False` , `Null` .                       |
| Nazwa                                                  | ciąg           | Tak      | Nazwa domeny.                                                          |
| RootDomain                                            | ciąg           | Nie       | Nazwa domeny katalogu głównego.                                              |
| Stan                                                | ciąg           | Tak      | Stan domeny. Na przykład `Verified`. Obsługiwane wartości:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | ciąg           | Tak      | Typ metody weryfikacji domeny. Obsługiwane wartości: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Ustawienia Federacji domeny

W tej tabeli opisano wymagane i opcjonalne właściwości **DomainFederationSettings** w treści żądania.

| Nazwa   | Typ   | Wymagane | Opis                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | ciąg           | Nie      | Identyfikator URI logowania używany przez bogatych klientów. Ta właściwość jest adresem URL uwierzytelniania usługi STS partnera. |
| DefaultInteractiveAuthenticationMethod | ciąg           | Nie      | Wskazuje domyślną metodę uwierzytelniania, która ma być używana, gdy aplikacja wymaga, aby użytkownik mógł korzystać z interakcyjnego logowania. |
| FederationBrandName                    | ciąg           | Nie      | Nazwa marki federacyjnej.        |
| IssuerUri                              | ciąg           | Tak     | Nazwa wystawcy certyfikatów.                        |
| LogOffUri                              | ciąg           | Tak     | Identyfikator URI wylogowania. Ta właściwość opisuje identyfikator URI wylogowania domeny federacyjnej.        |
| MetadataExchangeUri                    | ciąg           | Nie      | Adres URL, który określa punkt końcowy wymiany metadanych używany do uwierzytelniania z rozbudowanych aplikacji klienckich. |
| NextSigningCertificate                 | ciąg           | Nie      | Certyfikat używany w przyszłości dla usług AD FS w wersji 2 usługi STS do podpisywania oświadczeń. Ta właściwość jest reprezentacją certyfikatu zakodowaną algorytmem Base64. |
| OpenIdConnectDiscoveryEndpoint         | ciąg           | Nie      | Punkt końcowy wykrywania OpenID Connect Connect dla federacyjnego dostawcy tożsamości STS. |
| PassiveLogOnUri                        | ciąg           | Tak     | Identyfikator URI logowania używany przez starszych klientów pasywnych. Ta właściwość jest adresem do wysyłania żądań logowania federacyjnego. |
| PreferredAuthenticationProtocol        | ciąg           | Tak     | Format tokenu uwierzytelniania. Na przykład `WsFed`. Obsługiwane wartości: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | ciąg           | Tak     | Typ zachowania Monituj o logowanie.  Na przykład `TranslateToFreshPasswordAuth`. Obsługiwane wartości: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | ciąg           | Tak     | Certyfikat używany obecnie przez usługę AD FS w wersji 2 w celu podpisywania oświadczeń. Ta właściwość jest reprezentacją certyfikatu zakodowaną algorytmem Base64. |
| SigningCertificateUpdateStatus         | ciąg           | Nie      | Wskazuje stan aktualizacji certyfikatu podpisywania. |
| SigningCertificateUpdateStatus         | wartość logiczna null | Nie      | Wskazuje, czy usługa STS dostawcy tożsamości obsługuje uwierzytelnianie wieloskładnikowe. Obsługiwane wartości: `True` , `False` , `Null` .|

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

Jeśli to się powiedzie, ten interfejs API zwraca zasób [domeny](#domain) dla nowej zweryfikowanej domeny.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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
