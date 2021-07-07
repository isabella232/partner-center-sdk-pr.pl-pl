---
title: Usuwanie zasad samoobsługi
description: Jak usunąć zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973098"
---
# <a name="delete-a-selfservepolicy"></a>Usuwanie samoobsługi (SelfServePolicy)

W tym artykule wyjaśniono, jak zaktualizować zasady samoobsługi.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="c"></a>C\#

Aby usunąć zasady samoobsługi:

1. Wywołaj [**metodę IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji na zasadach.

2. Wywołaj [**metodę Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) lub [**DeleteAsync,**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) aby usunąć zasady samoobsługi.

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Przykład można znaleźć w następujących tematach:

- Przykład: [aplikacja testowa konsoli](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Klasa: **DeleteSelfServePolicies.cs**

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda  | Identyfikator URI żądania                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Usunąć** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**Parametr URI**

Użyj następujących parametrów ścieżki, aby uzyskać określony produkt.

| Nazwa                       | Typ         | Wymagane | Opis                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **ciąg**   | Tak      | Ciąg, który identyfikuje zasady samoobsługi.                 |

### <a name="request-headers"></a>Nagłówki żądań

- Wymagany jest identyfikator żądania i identyfikator korelacji.
- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

Brak.

### <a name="request-example"></a>Przykład żądania

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>Odpowiedź REST

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
