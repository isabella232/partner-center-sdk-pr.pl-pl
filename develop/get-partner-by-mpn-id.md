---
title: Weryfikowanie identyfikatora MPN partnera
description: Dowiedz się, jak zweryfikować identyfikator Microsoft Partner Network partnera (identyfikator MPN), żądając profilu MPN partnera za pośrednictwem usługi C \# lub interfejsu API REST Centrum partnerskiego.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768501"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Weryfikowanie identyfikatora MPN partnera za pośrednictwem języka C \# lub interfejsu API REST Centrum partnerskiego

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Weryfikowanie identyfikatora Microsoft Partner Network partnera (identyfikator MPN).

Pokazana tutaj technika sprawdza identyfikator Microsoft Partner Network partnera, żądając profilu MPN partnera od centrum partnerskiego. Identyfikator jest uznawany za ważny, jeśli żądanie zakończy się pomyślnie.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje tylko uwierzytelnianie przy użyciu aplikacji i poświadczeń użytkownika.

- IDENTYFIKATOR MPN partnera do zweryfikowania. W przypadku pominięcia tej wartości żądanie pobiera profil MPN zalogowanego partnera.

## <a name="c"></a>C\#

Aby sprawdzić identyfikator MPN partnera, najpierw Pobierz interfejs na potrzeby operacji zbierania profilów partnera z właściwości [**IAggregatePartner. profile**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) . Następnie uzyskaj interfejs do MPN operacji profilu z właściwości [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) . Na koniec wywołaj metody [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) lub [**GETasync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) z identyfikatorem MPN, aby pobrać profil MPN. W przypadku pominięcia identyfikatora MPN z wywołania get lub GetAsync żądanie próbuje pobrać profil MPN partnera zalogowanego.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: VerifyPartnerMpnId.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Pobierz** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Profiles/MPN? mpnId = {MPN-ID} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Podaj następujący parametr zapytania, aby zidentyfikować partnera. Jeśli pominięto ten parametr zapytania, żądanie zwróci profil MPN zalogowanego partnera.

| Nazwa   | Typ | Wymagane | Opis                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN — identyfikator | int  | Nie       | Identyfikator Microsoft Partner Network, który identyfikuje partnera. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

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

Jeśli to się powiedzie, treść odpowiedzi zawiera zasób [MpnProfile](profile-resources.md#mpnprofile) dla partnera.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

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

### <a name="response-example-failure"></a>Przykład odpowiedzi (niepowodzenie)

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
