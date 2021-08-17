---
title: Weryfikowanie identyfikatora MPN partnera
description: Dowiedz się, jak zweryfikować identyfikator Microsoft Partner Network partnera (identyfikator MPN), żądając profilu MPN partnera za pośrednictwem języka C lub interfejsu \# API REST Partner Center.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 471a94153ab4baffe45d43bee473bf68230106ad
ms.sourcegitcommit: b0534995c36d644cc5f7bdf31b2afd5355cf7149
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/16/2021
ms.locfileid: "122208062"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Weryfikowanie identyfikatora MPN partnera za pośrednictwem języka C \# lub interfejsu API REST Partner Center

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak zweryfikować identyfikator Microsoft Partner Network partnera (IDENTYFIKATOR MPN).

Technika pokazana w tym miejscu weryfikuje identyfikator Microsoft Partner Network partnera, żądając profilu MPN partnera z Partner Center. Identyfikator jest uznawany za prawidłowy, jeśli żądanie zakończy się pomyślnie.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie tylko przy użyciu poświadczeń aplikacji i użytkownika.

- Identyfikator MPN partnera do zweryfikowania. Jeśli pominiesz tę wartość, żądanie pobierze profil MPN partnera, który się zalogował.

## <a name="c"></a>C\#

Aby zweryfikować identyfikator MPN partnera, najpierw pobierz interfejs do operacji zbierania profilów partnerów z właściwości [**IAggregatePartner.Profiles.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) Następnie pobierz interfejs do operacji profilu MPN z właściwości [**MpnProfile.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) Na koniec wywołaj metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) lub [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) z identyfikatorem MPN, aby pobrać profil MPN. Jeśli pominiesz identyfikator MPN z wywołania Get lub GetAsync, żądanie podejmie próbę pobrania profilu MPN partnera, który się zalogował.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : VerifyPartnerMpnId.cs **(Klasa przykładów** zestaw SDK Centrum partnerskiego: VerifyPartnerMpnId.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podaj następujący parametr zapytania, aby zidentyfikować partnera. Jeśli ten parametr zapytania zostanie pominięty, żądanie zwróci profil MPN partnera, który się zalogował.

| Nazwa   | Typ | Wymagane | Opis                                                 |
|--------|------|----------|-------------------------------------------------------------|
| identyfikator mpn | int  | Nie       | Identyfikator Microsoft Partner Network, który identyfikuje partnera. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, treść odpowiedzi zawiera [zasób MpnProfile](profile-resources.md#mpnprofile) partnera.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example-success"></a>Przykład odpowiedzi (powodzenie)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>Przykład odpowiedzi (błąd)

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
