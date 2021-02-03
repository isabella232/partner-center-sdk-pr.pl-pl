---
title: Sprawdzanie dostępności domeny
description: Jak ustalić, czy domena jest dostępna do użycia.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768278"
---
# <a name="verify-domain-availability"></a>Sprawdzanie dostępności domeny

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Jak ustalić, czy domena jest dostępna do użycia.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w temacie [uwierzytelnianie w centrum partnerskim](partner-center-authentication.md). Ten scenariusz obsługuje uwierzytelnianie zarówno w przypadku aplikacji autonomicznych, jak i aplikacji oraz poświadczeń użytkownika.

- Domena (na przykład `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Aby sprawdzić, czy domena jest dostępna, najpierw Wywołaj [**IAggregatePartner. domen**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) , aby uzyskać interfejs do operacji na domenie. Następnie Wywołaj metodę [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) z domeną, aby sprawdzić. Ta metoda pobiera interfejs do operacji dostępnych dla określonej domeny. Na koniec Wywołaj metodę [**EXISTS**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) , aby sprawdzić, czy domena już istnieje.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Przykład**: [aplikacja testowa konsoli](console-test-app.md). **Projekt**: **Klasa** przykładów zestawu SDK centrum partnerskiego: CheckDomainAvailability.cs

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                              |
|----------|--------------------------------------------------------------------------|
| **MTP** | [*{baseURL}*](partner-center-rest-urls.md)/V1/Domains/{Domain} http/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby sprawdzić dostępność domeny.

| Nazwa       | Typ       | Wymagane | Opis                                   |
|------------|------------|----------|-----------------------------------------------|
| **domeny** | **parametry** | Y        | Ciąg, który identyfikuje domenę do sprawdzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, zobacz [nagłówki REST Centrum partnerskiego](headers.md).

### <a name="request-body"></a>Treść żądania

Brak

### <a name="request-example"></a>Przykład żądania

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli domena istnieje, nie jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 200 OK. Jeśli domena nie zostanie znaleziona, jest ona dostępna do użycia i zwracany jest kod stanu odpowiedzi 404.

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów REST centrum partnera](error-codes.md).

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Przykład odpowiedzi dla sytuacji, gdy domena jest już używana

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Przykład odpowiedzi dla momentu dostępności domeny

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
