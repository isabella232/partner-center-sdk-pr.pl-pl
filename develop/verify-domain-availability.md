---
title: Sprawdzanie dostępności domeny
description: Jak określić, czy domena jest dostępna do użycia.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530280"
---
# <a name="verify-domain-availability"></a>Sprawdzanie dostępności domeny

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Jak określić, czy domena jest dostępna do użycia.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w [te Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu zarówno poświadczeń aplikacji autonomicznej, jak i aplikacji i użytkownika.

- Domena (na przykład `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Aby sprawdzić, czy domena jest dostępna, najpierw wywołaj [**element IAggregatePartner.Domains,**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) aby uzyskać interfejs operacji domeny. Następnie wywołaj [**metodę ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) z domeną, aby to sprawdzić. Ta metoda pobiera interfejs do operacji dostępnych dla określonej domeny. Na koniec wywołaj [**metodę Exists,**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) aby sprawdzić, czy domena już istnieje.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Przykład:** [aplikacja testowa konsoli](console-test-app.md). **Project:** zestaw SDK Centrum partnerskiego Samples Class : CheckDomainAvailability.cs **(Klasa** przykładów zestaw SDK Centrum partnerskiego: CheckDomainAvailability.cs)

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                              |
|----------|--------------------------------------------------------------------------|
| **Głowy** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domena} HTTP/1.1 |

### <a name="uri-parameter"></a>Parametr URI

Użyj następującego parametru zapytania, aby zweryfikować dostępność domeny.

| Nazwa       | Typ       | Wymagane | Opis                                   |
|------------|------------|----------|-----------------------------------------------|
| **Domeny** | **ciąg** | Y        | Ciąg, który identyfikuje domenę do sprawdzenia. |

### <a name="request-headers"></a>Nagłówki żądań

Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

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

Jeśli domena istnieje, nie jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 200 OK. Jeśli domena nie zostanie znaleziona, jest dostępna do użycia i zwracany jest kod stanu odpowiedzi 404 Nie znaleziono.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kody błędów REST.](error-codes.md)

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Przykład odpowiedzi dla sytuacji, gdy domena jest już w użyciu

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Przykład odpowiedzi dotyczącej tego, kiedy domena jest dostępna

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
