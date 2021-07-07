---
title: Aktualizowanie zasad samoobsługi
description: Jak zaktualizować zasady samoobsługi.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445259"
---
# <a name="update-a-selfservepolicy"></a>Aktualizowanie selfServePolicy

W tym artykule wyjaśniono, jak zaktualizować zasady samoobsługi.

## <a name="prerequisites"></a>Wymagania wstępne

- Poświadczenia zgodnie z opisem w te [Partner Center uwierzytelniania.](partner-center-authentication.md) Ten scenariusz obsługuje uwierzytelnianie przy użyciu poświadczeń aplikacji i użytkownika.

## <a name="c"></a>C\#

Aby usunąć zasady samoobsługi:

1. Wywołaj [**metodę IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) z identyfikatorem jednostki, aby pobrać interfejs do operacji na zasadach.

2. Wywołaj [**metodę Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) lub [**PutAsync,**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) aby zaktualizować zasady samoobsługi.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>Żądanie REST

### <a name="request-syntax"></a>Składnia żądania

| Metoda   | Identyfikator URI żądania                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1 |

### <a name="request-headers"></a>Nagłówki żądań

- Wymagany jest identyfikator żądania i identyfikator korelacji.
- Aby uzyskać więcej informacji, [zobacz Partner Center REST headers (Nagłówki REST).](headers.md)

### <a name="request-body"></a>Treść żądania

W tej tabeli opisano wymagane właściwości w treści żądania.

| Nazwa                              | Typ   | Opis                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | Informacje o zasadach samoobsługi. |

#### <a name="selfservepolicy"></a>SelfServePolicy

W tej tabeli opisano minimalne wymagane pola z zasobu [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) potrzebne do utworzenia nowych zasad samoobsługi.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.     |
| SelfServeEntity       | SelfServeEntity  | Jednostka samoobsługi, która ma przyznany dostęp.                                                     |
| Grantor               | Grantor          | Grantor, który udziela dostępu.                                                                    |
| Uprawnienia           | Tablica uprawnień| Tablica [zasobów](self-serve-policy-resources.md#permission) uprawnień.                                                      |
| Etag                  | ciąg           | Tag Etag.                                                                                               |


### <a name="request-example"></a>Przykład żądania

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```

## <a name="rest-response"></a>Odpowiedź REST

Jeśli to się powiedzie, ten interfejs API zwraca [zasób SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dla zaktualizowanych zasad samoobsługi.

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów REST.](error-codes.md)

Ta metoda zwraca następujące kody błędów:

| Kod stanu HTTP     | Kod błędu   | Opis                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Nie znaleziono zasad samoobsługi                                            |
| 404                  | 600040       | Identyfikator zasad samoobsługi jest nieprawidłowy                                  |


### <a name="response-example"></a>Przykład odpowiedzi

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
