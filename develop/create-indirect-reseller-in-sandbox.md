---
title: Tworzenie odsprzedawcy pośredniego w piaskownicy
description: Zawiera informacje dla dostawców pośrednich piaskownicy na temat włączania testowania end-to-end przy użyciu interfejsów API.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973438"
---
# <a name="create-indirect-reseller-in-sandbox"></a>Tworzenie odsprzedawcy pośredniego w piaskownicy

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany

W tym dokumencie przedstawiono sposób tworzenia dostawców pośrednich piaskownicy i włączania testowania end-to-end przy użyciu interfejsów API.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center Authentication (Uwierzytelnianie).](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="csp-indirect-provider"></a>CSP Indirect Provider

| Możliwości produkcyjne             | Możliwości piaskownicy                            |
|-------------------------------------|-------------------------------------------------|
| Sprzedaż odsprzedawcy pośredniego klientowi końcowego | Obsługiwane |
| Właścicielem całej sprzedaży, rozliczeń, aprowiwizowania i zarządzania/pomocy technicznej | Obsługiwane |
| Żądanie partnerstwa z odsprzedawcami | Obsługiwane |
| Wyświetlanie klientów według odsprzedawcy | Obsługiwane |
| Dodawanie nowych klientów według odsprzedawców | Obsługiwane |
| Zapraszanie klientów | Żądanie relacji z klientem nie jest obsługiwane w piaskownicy |
| Dostawca pośredni piaskownicy może wybrać środowisko IR piaskownicy (identyfikator MPN) jako dostawcę tożsamości podczas umieszczania transakcji | Obsługiwane |
| Nie jest obsługiwane w środowisku produkcyjnym | Dostawca pośredni piaskownicy może utworzyć odsprzedawcę pośredniego piaskownicy |
| Należy wprowadzić identyfikator MPN piaskownicy. Identyfikator MPN produktu nie będzie działać | Nie jest obsługiwane w środowisku produkcyjnym |
| Nie jest obsługiwane w środowisku produkcyjnym | Dostawca pośredni piaskownicy może usunąć odsprzedawcę pośredniego piaskownicy |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a>Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy

Ta funkcja jest dostępna tylko w piaskownicy i umożliwia dostawcom pośrednim piaskownicy tworzenie odsprzedawców pośrednich piaskownicy.

1. Limit pięciu pośrednich odsprzedawców piaskownicy dozwolonych na dostawcę pośredniego piaskownicy
2. Dostawcy pośredni piaskownicy mogą tworzyć klientów u `associatedPartnerId` odsprzedawcy pośredniego piaskownicy
3. Wprowadź identyfikator [MPN](/partner-center/mpn-create-a-partner-center-account) określonego regionu podczas tworzenia odsprzedawcy pośredniego piaskownicy. Wielu pośrednich odsprzedawców piaskownicy można utworzyć przy użyciu tego samego identyfikatora MPN piaskownicy.
4. Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy

## <a name="sandbox-indirect-resellers--view-customers"></a>Odsprzedawcy pośredni piaskownicy — wyświetlanie klientów

1. Odsprzedawcy pośredni piaskownicy mogą wyświetlać listę klientów piaskownicy według dostawców pośrednich piaskownicy.
2. Odsprzedawcy pośredni piaskownicy mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.

## <a name="create-sandbox-indirect-reseller-through-api"></a>Tworzenie odsprzedawcy pośredniego piaskownicy za pomocą interfejsu API

### <a name="rest-request"></a>Żądanie REST

#### <a name="request-syntax"></a>Składnia żądania

| **Metoda** | **Identyfikator URI żądania**                                                        |
|------------|------------------------------------------------------------------------|
| **Post**   | [*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller |

#### <a name="request-headers"></a>Nagłówki żądań

- Ten interfejs API jest idempotentny (nie da innego wyniku, jeśli wywołasz go wielokrotnie).
- Wymagany jest identyfikator żądania i identyfikator korelacji.
- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

#### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Właściwość             | Typ           | Opis                                      |
|----------------------|----------------|--------------------------------------------------|
| mpnId                | ciąg         | Identyfikator MPN dla ir w określonym regionie         |
| Dzierżawy               | Ciąg &lt; słownika, ciąg&gt; | Zbieranie podstawowych informacji definiującej konto do utworzenia |
| legalBusinessProfile | Ciąg &lt; słownika, ciąg&gt; | Zbieranie informacji, które reprezentują prawne jednostki biznesowe, takie jak kontakt, adres i nazwa |
| organizationProfileLanguage | Ciąg &lt; słownika, ciąg&gt; | Identyfikator języka organizacji |

W tej tabeli opisano wymagane właściwości **atrybutu dzierżawy.**

| Właściwość           | Typ           | Opis                         |
|--------------------|----------------|-------------------------------------|
| domainPrefix       | Ciąg; Unikatowy | Domena dla konta dzierżawy       |
| name               | ciąg         | Przyjazna nazwa dzierżawy         |
| displayName        | ciąg         | Nazwa wyświetlana konta        |
| adminUserName      | ciąg         | Nazwa użytkownika konta do logowania |
| adminfirstname (nazwa administratora)     | ciąg         | Imię administratora       |
| adminlastname (nazwa administratora)      | ciąg         | Nazwisko administratora        |
| adminAlernateEmail | ciąg         | wiadomość e-mail dla administratora            |
| country            | ciąg         | Kraj konta              |
| kultura            | ciąg         | Preferencja języka dla konta     |

W tej tabeli opisano wymagane właściwości **atrybutu legalBusinessProfile.**

| Właściwość       | Typ                             | Opis                          |
|----------------|----------------------------------|--------------------------------------|
| Companyname    | ciąg                           | Nazwa firmy dla jednostki prawnej        |
| adres        | Ciąg &lt; słownika, ciąg&gt; | Adres lokalizacji jednostki prawnej |
| primaryContact | Ciąg &lt; słownika, ciąg&gt; | Dane kontaktowe firmy       |
| kultura        | ciąg                           | Język preferowany przez firmę    |

### <a name="request-example"></a>Przykład żądania

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a>Odpowiedź REST

W przypadku powodzenia ta metoda zwraca wypełniony zasób środowiska IR piaskownicy w treści odpowiedzi.

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
